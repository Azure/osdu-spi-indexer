# OSDU Indexer Service for Azure

[![Release](https://img.shields.io/github/v/release/Azure/osdu-spi-indexer)](https://github.com/Azure/osdu-spi-indexer/releases)
[![Validate](https://github.com/Azure/osdu-spi-indexer/actions/workflows/validate.yml/badge.svg?branch=main)](https://github.com/Azure/osdu-spi-indexer/actions/workflows/validate.yml)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

> [!NOTE]
> Shared service code comes from the [OSDU community upstream](https://community.opengroup.org/osdu/platform/system/indexer-service); the [OSDU documentation](https://osdu.pages.opengroup.org/platform/system/indexer-service/) covers the API.

Indexer keeps the search index in step with Storage: it turns each record change into an Elasticsearch document shaped by the record's schema, and rebuilds the index for a kind on request.

## At a glance

| | |
|---|---|
| API base path | `/api/indexer/v2/` |
| Swagger UI | `/api/indexer/v2/swagger` |
| Health | `:8081/actuator/health` |
| Depends on | Partition, Entitlements, Schema, Storage, Indexer Queue |
| Azure resources | Service Bus (`recordstopic` topic), Key Vault (Redis and Elasticsearch credentials); Elasticsearch and Redis run inside the cluster |
| Deployed by | [OSDU SPI Stack](https://github.com/Azure/osdu-spi-stack) (`software/stacks/osdu/services/indexer.yaml`) |

## Repository layout

[CONTRIBUTING.md](CONTRIBUTING.md) explains where each kind of change belongs.

| Path | Owner | Contents |
|---|---|---|
| `indexer-core/` | OSDU upstream | Shared service code |
| `provider/indexer-azure/` | This repository | Azure provider |
| `indexer-acceptance-test/` | OSDU upstream | End-to-end suite run against a deployed environment |
| `testing/indexer-test-core/` | OSDU upstream | Shared code for the integration tests |
| `testing/indexer-test-azure/` | This repository | Legacy Azure integration tests |
| `.spi/service.yaml` | This repository | How CI deploys and tests the service on SPI Stack |

## Build

Requires Java 25 and Maven 3.6.3+. OSDU dependencies resolve from the public community registry through the settings file in `.mvn`:

```bash
mvn --settings .mvn/community-maven.settings.xml -P core,azure clean install
```

The runnable jar lands at `provider/indexer-azure/target/indexer-azure-*-spring-boot.jar`.

## Configuration

SPI Stack sets the service's environment from two places: the shared `osdu-config` ConfigMap and the service's own entry in [`services/indexer.yaml`](https://github.com/Azure/osdu-spi-stack/blob/main/software/stacks/osdu/services/indexer.yaml). Those files are the contract; the tables below list what Indexer actually reads from them.

**Shared, from `osdu-config`:**

| Variable | Purpose |
|---|---|
| `KEYVAULT_URI` | Central Key Vault |
| `AAD_CLIENT_ID` | Application ID that caller tokens are issued for |
| `APPINSIGHTS_KEY` | Telemetry |
| `SERVER_PORT` | HTTP port (`8080`) |
| `REDIS_PORT` | Redis port (`6379`); binds to `redis.port` ahead of the provider default of `6380` |

**Specific to Indexer**, from `services/indexer.yaml`:

| Variable and value on SPI Stack | Purpose |
|---|---|
| `SPRING_APPLICATION_NAME`<br>`indexer` | Application name, in place of the provider default `indexer-azure` |
| `SERVER_SERVLET_CONTEXTPATH`<br>`/api/indexer/v2/` | API base path |
| `AZURE_ISTIOAUTH_ENABLED`<br>`true` | Trust the mesh's token validation |
| `AZURE_PAAS_WORKLOADIDENTITY_ISENABLED`<br>`true` | Authenticate to Azure with workload identity |
| `SECURITY_HTTPS_CERTIFICATE_TRUST`<br>`true` | Trust the in-cluster Elasticsearch certificate and skip hostname verification |
| `PARTITION_SERVICE_ENDPOINT`<br>`http://partition/api/partition/v1` | Per-partition resource lookup |
| `ENTITLEMENTS_SERVICE_ENDPOINT`<br>`http://entitlements/api/entitlements/v2` | Caller authorization |
| `ENTITLEMENTS_SERVICE_API_KEY`<br>`OBSOLETE` | Legacy key passed to the Entitlements client; the property has no default, so the placeholder must stay set |
| `SCHEMA_SERVICE_URL`<br>`http://schema/api/schema-service/v1` | Schema lookups; the service appends `/schema` |
| `STORAGE_SERVICE_URL`<br>`http://storage/api/storage/v2` | Base for the Storage kinds query |
| `STORAGE_SCHEMA_HOST`<br>`http://storage/api/storage/v2/schemas` | Storage schema API |
| `STORAGE_QUERY_RECORD_HOST`<br>`http://storage/api/storage/v2/query/records` | Records by ID, and record IDs by kind for reindex |
| `STORAGE_QUERY_RECORD_FOR_CONVERSION_HOST`<br>`http://storage/api/storage/v2/query/records:batch` | Batch record fetch for indexing |
| `COSMOSDB_DATABASE`<br>`osdu-db` | Database inside each partition's Cosmos DB account |
| `SERVICEBUS_TOPIC_NAME`<br>`indexing-progress` | Indexing status topic; publishing to it is off in `application.properties` |
| `REINDEX_TOPIC_NAME`<br>`recordstopic` | Topic a reindex request publishes record batches to |
| `REDIS_DATABASE`<br>`4` | Redis database for the service's caches |

The service authenticates to Azure with workload identity, which injects `AZURE_CLIENT_ID` and a federated token; there are no client secrets. Per-partition resources are resolved at request time through the Partition service, including the Elasticsearch endpoint and credentials, which SPI Stack stores in Key Vault as `<partition>-elastic-endpoint`, `<partition>-elastic-username`, and `<partition>-elastic-password`. The Redis host and password come from the Key Vault secrets `redis-hostname` and `redis-password`. The stack's `elasticTls` and `redisTls` values import the Elasticsearch and Redis CA certificates into the JVM truststore.

## Test

| Suite | Where | Runs in CI | Run it yourself |
|---|---|---|---|
| Unit | `indexer-core`, `provider/indexer-azure` | Pull requests (Java Build) | `mvn ... install` from [Build](#build) |
| Acceptance | [`indexer-acceptance-test`](indexer-acceptance-test/docs/README.md) | Pull requests, against SPI Stack (Deploy and Test) | `spi test indexer` |
| Integration | `testing/indexer-test-core`, `testing/indexer-test-azure` | No | See below |

CI runs these on pull requests from this repository that change code. Documentation-only changes skip the build, and pull requests from forks build without deploying.

**Acceptance** proves a change on real infrastructure before it merges. It calls the deployed service through the gateway as a privileged test identity, and the bindings in `.spi/service.yaml` supply its inputs. It also connects to Elasticsearch directly to check what landed in the index, so it needs `ELASTIC_HOST`, `ELASTIC_PORT`, `ELASTIC_USER_NAME`, `ELASTIC_PASSWORD`, and `ELASTIC_SSL_ENABLED` alongside the gateway host and token. Against an environment you are connected to:

```bash
spi test indexer                   # the image and suite the environment is running
spi test indexer --source .        # this checkout's suite and descriptor
```

**Integration** is the older suite carried from upstream. It sits outside the root Maven build and CI does not run it. It accepts a bearer token in `INTEGRATION_TESTER_ACCESS_TOKEN`, so `spi token` can supply one, and like acceptance it reads the Elasticsearch connection settings directly. It has not been proven against SPI Stack.

To call the API by hand, `spi token` mints a bearer token:

```bash
curl -H "Authorization: Bearer $(spi token)" -H "data-partition-id: <partition>" \
  https://<gateway>/api/indexer/v2/info
```

## Deploy

For a pull request from this repository that changes code, CI publishes the service image and its test suite image, `osdu-spi-indexer-acceptance`, to GHCR, and the Deploy and Test lane borrows an SPI Stack environment, runs the new image there, proves it with the acceptance suite, and restores the environment's own image. When that lane runs and passes, the change is proven on real infrastructure before it merges; the Validation Summary on the pull request shows whether it ran. This repository does not own infrastructure; SPI Stack does.

To try a build by hand on an environment you are connected to, pin it by digest and release the pin when done:

```bash
spi service pin indexer --image ghcr.io/azure/osdu-spi-indexer@sha256:<digest>
spi service reset indexer
```

## Service notes

**Indexer Queue delivers the work.** Indexer does not subscribe to Service Bus. On SPI Stack the separate Indexer Queue service subscribes to `recordstopic` and `schemachangedtopic` and calls this service's task handlers, `/api/indexer/v2/_dps/task-handlers/index-worker` and `/api/indexer/v2/_dps/task-handlers/schema-worker`. A reindex request publishes its record batches back to `recordstopic`, so it travels the same path. If Indexer Queue is not running, record changes are not indexed.

## License

Copyright © Microsoft Corporation

Licensed under the [Apache License 2.0](LICENSE).
