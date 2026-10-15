# Changelog

## [1.4.0](https://github.com/Azure/osdu-spi-indexer/compare/v1.3.0...v1.4.0) (2026-10-14)


### ✨ Features

* Initial code ([65a1bd6](https://github.com/Azure/osdu-spi-indexer/commit/65a1bd6f34a87abc5e55123e82d6fa2a31e7a387))


### 🐛 Bug Fixes

* Aws build command ([48de2b9](https://github.com/Azure/osdu-spi-indexer/commit/48de2b9ead9bd0f80a0bdd1d76a98400ec7672c5))
* **azure:** Netty-bom before core-lib-azure (lettuce 7.5.2 NoClassDefFoundError) ([b99fc2b](https://github.com/Azure/osdu-spi-indexer/commit/b99fc2b9d8f5132d91c83fe10b6b18729f32f192))
* **azure:** Netty-bom before core-lib-azure (lettuce 7.5.2 NoClassDefFoundError) ([36ffdc5](https://github.com/Azure/osdu-spi-indexer/commit/36ffdc50ad0a0050209331e2adc9585814edd9ee))
* Bump netty to 4.2.18.Final ([f98e86d](https://github.com/Azure/osdu-spi-indexer/commit/f98e86df538f273236d0e725aeb173e5bb8617c2))
* Bump netty to 4.2.18.Final ([f3692dd](https://github.com/Azure/osdu-spi-indexer/commit/f3692dd5755d372f212f5089de0b93c318149f6f))
* Catch SchemaProcessingException directly to prevent poison message loop ([436ef2c](https://github.com/Azure/osdu-spi-indexer/commit/436ef2c39b241b7180c7957173371cbe8e613acc))
* Catch SchemaProcessingException directly to prevent poison message loop ([271e0ae](https://github.com/Azure/osdu-spi-indexer/commit/271e0ae7f5e2c843f4e7f3020c7d4849a6a5ac87))
* Cve and spring boot version bump ([0e5edca](https://github.com/Azure/osdu-spi-indexer/commit/0e5edcaec48feec5c47485eceb5baa5f02ddabdd))
* Cve and spring boot version bump ([ee20e10](https://github.com/Azure/osdu-spi-indexer/commit/ee20e102ac9464d67ef97f670436f11c1cfa4543))
* **cve:** Remediate HIGH/CRITICAL deps + pom cleanup ([45e63d2](https://github.com/Azure/osdu-spi-indexer/commit/45e63d2301d5ec3af0c56dd32b0dbce5631d4d09))
* **cve:** Remediate HIGH/CRITICAL deps + pom cleanup ([606e1ab](https://github.com/Azure/osdu-spi-indexer/commit/606e1ab223f22c27c2d9b5bcb1e09fb3976d20f1))
* Disable bagOfWords to complement mapBooleanToString for Azure in M25 ([03a02d4](https://github.com/Azure/osdu-spi-indexer/commit/03a02d48b91eb95706b65b598759ae030bced790))
* Disable bagOfWords to complement mapBooleanToString for Azure in M25 ([aed6f55](https://github.com/Azure/osdu-spi-indexer/commit/aed6f55ce54abf3ca5d4890ba89573cfa0417b94))
* Enabling mapping boolean to string fix for AWS ([0826dce](https://github.com/Azure/osdu-spi-indexer/commit/0826dce9f5cd7f487becbc2c12ef8dd1c045145a))
* Enabling mapping boolean to string fix for AWS ([0c37fc9](https://github.com/Azure/osdu-spi-indexer/commit/0c37fc9b5fb01fb808d2fc5cc17b0683c161f06e))
* Geospatial validation bug ([e7bd69d](https://github.com/Azure/osdu-spi-indexer/commit/e7bd69d4428f5042859b7e795bffe7ceae61d79d))
* Geospatial validation bug ([e110ce6](https://github.com/Azure/osdu-spi-indexer/commit/e110ce6b137e12b5b66aa4b7ffe53a2091d9f039))
* **indexer:** Recreate deleted index on wrapped mapping 404 ([b7d6d6b](https://github.com/Azure/osdu-spi-indexer/commit/b7d6d6bc69c5384c9a68ebf1d3e12fc5a8c2536a))
* **indexer:** Recreate stale index-exists cache on index_not_found ([a081e8b](https://github.com/Azure/osdu-spi-indexer/commit/a081e8b8afd59a2523eed17dcbe5e7b768e82a2a))
* **indexer:** Self-heal the index-exists cache when an index is deleted mid-flight ([3451db1](https://github.com/Azure/osdu-spi-indexer/commit/3451db1ab09d2e29e808580773b3c47bf6195dd5))
* **indexer:** Strip collaboration namespace from bulk item record ids ([7f0b14b](https://github.com/Azure/osdu-spi-indexer/commit/7f0b14b4b0c1bfc56008d3e4600f35743f28c2a4))
* Poll query result count in indexer step methods to eliminate single-shot flakiness ([e17032f](https://github.com/Azure/osdu-spi-indexer/commit/e17032f3810cbb1909464920114f5ba6acc20bc3))
* Poll query result count in indexer step methods to eliminate single-shot flakiness ([12b6b69](https://github.com/Azure/osdu-spi-indexer/commit/12b6b69ea1e632c8b13350ec6a6a883e456eb4dd))
* Removed unused comments per sonarqube ([c101014](https://github.com/Azure/osdu-spi-indexer/commit/c10101407863772db56a90f58aece0f4d0553cc9))
* Removed unused comments per sonarqube ([f3af12f](https://github.com/Azure/osdu-spi-indexer/commit/f3af12fc2643b99ab2a3542a21148623c88da7cc))
* Removing core profile from aws build command ([c9cd398](https://github.com/Azure/osdu-spi-indexer/commit/c9cd39897ec46bbe4a07057844458d1f4894b24c))
* Spring cves ([e711e2d](https://github.com/Azure/osdu-spi-indexer/commit/e711e2dd340df34a0c78de51e03a2c0c088a11e8))
* Spring cves ([62e5ef4](https://github.com/Azure/osdu-spi-indexer/commit/62e5ef46bb225b613ad2850772f19e7cfff583e0))
* **test:** Add junit-vintage-engine for JUnit 4 test discovery ([a8d26b0](https://github.com/Azure/osdu-spi-indexer/commit/a8d26b021dc5e57f0a4047dbe2ba95409da1668f))
* **test:** Add junit-vintage-engine for JUnit 4 test discovery ([f27b0c9](https://github.com/Azure/osdu-spi-indexer/commit/f27b0c90ff7799b7df27e09060d7b6143633e99f))
* Thread Exhaustion and ES Connection Errors by using request-scoped ElasticSearch client ([2864971](https://github.com/Azure/osdu-spi-indexer/commit/28649712497257875a3683e00449fbd823e71da3))
* Tomcat-core CVE ([682533a](https://github.com/Azure/osdu-spi-indexer/commit/682533a1c4825645ddc4a9fcfed893b66ae134e3))
* Tomcat-core CVE ([1dfd49b](https://github.com/Azure/osdu-spi-indexer/commit/1dfd49bd33d003024450cedbbc133e4a0ed8d2b6))
* Tomcat-core security-crypto json-smart netty-common ([220cb5f](https://github.com/Azure/osdu-spi-indexer/commit/220cb5f5787c751e7e5283376a2f109af4add0c1))
* Tomcat-core security-crypto json-smart netty-common ([9698e2b](https://github.com/Azure/osdu-spi-indexer/commit/9698e2bdd2a49eecb55abb11764c10c66bb020ca))
* Unique legal-tag names in parallel indexer tests ([bb34a83](https://github.com/Azure/osdu-spi-indexer/commit/bb34a8308f10c3759a166cf56bbb579a0e4c6756))
* Unique legal-tag names in parallel indexer tests ([1cae375](https://github.com/Azure/osdu-spi-indexer/commit/1cae3754ff1486098eca06006160b68d02102fc0))


### 📚 Documentation

* Fill in root README for Indexer and drop provider README ([ec1d050](https://github.com/Azure/osdu-spi-indexer/commit/ec1d050597a8ca7255f0caad02e38cca3f83a7bd))
* Root README in the standard SPI service format ([f93e5fb](https://github.com/Azure/osdu-spi-indexer/commit/f93e5fb57bc046a6ed2bcd32fed4cf6ee8c48fb1))


### 🔧 Miscellaneous

* **azure:** Add Apache 2.0 license header to RedisConfigTest ([5db75c1](https://github.com/Azure/osdu-spi-indexer/commit/5db75c18dadb948f06b8d1e3c61989d9b9aa13ef))
* **ci:** Remove IBM jobs from pipeline ([c85543d](https://github.com/Azure/osdu-spi-indexer/commit/c85543d43139b359f4c0d545d8b2798b5dcb29b4))
* **ci:** Remove IBM jobs from pipeline ([e47892e](https://github.com/Azure/osdu-spi-indexer/commit/e47892eefdf3155279d71dd6afd1d6979af6606a))
* Complete repository initialization ([8a36933](https://github.com/Azure/osdu-spi-indexer/commit/8a36933c73b73c72b7d5a6b57c9582a5311cdb84))
* Copy configuration and workflows from main branch ([c281f17](https://github.com/Azure/osdu-spi-indexer/commit/c281f17063e433d63648d19d50a9de2c02c0bd16))
* Defaulting collaboration ff to true to avoid compatibility issues ([e4703dc](https://github.com/Azure/osdu-spi-indexer/commit/e4703dc24c4d00eb31b4b45f8581b17c10b02c1b))
* Defaulting collaboration ff to true to avoid compatibility issues ([9ce4828](https://github.com/Azure/osdu-spi-indexer/commit/9ce48282321561fdd30a5a462e79e5cb21796d4b))
* Deleting aws helm chart ([359b741](https://github.com/Azure/osdu-spi-indexer/commit/359b741c71e88c541d8db53198ba1290056f2a65))
* Deleting aws helm chart ([f96a0e1](https://github.com/Azure/osdu-spi-indexer/commit/f96a0e1b62df629dc1ad4949c9780c79d84a863b))
* Fixing sonar issues ([3f6e169](https://github.com/Azure/osdu-spi-indexer/commit/3f6e16981bd7dc94135709848444c4ad0ea044ff))
* Fixing sonar issues ([03202b2](https://github.com/Azure/osdu-spi-indexer/commit/03202b21540d7289d0e781ee234b42b07a4e65d6))
* Generate filtered upstream tree ([3ec8dfc](https://github.com/Azure/osdu-spi-indexer/commit/3ec8dfcce52157b312bf469856663090ee84cf9d))
* License headers for the release review ([3c88def](https://github.com/Azure/osdu-spi-indexer/commit/3c88def798a0773b0ab312c369a8e71316d4071b))
* Remove AWS provider and AWS CI/CD ([916fedf](https://github.com/Azure/osdu-spi-indexer/commit/916fedf5424987e5a6008ad932993e14a6faca0d))
* Remove AWS provider and AWS CI/CD ([5b4f11e](https://github.com/Azure/osdu-spi-indexer/commit/5b4f11e2e3bfb021928f379059971d7ec2ef4b3a))
* Removing helm copy from aws buildspec ([c012554](https://github.com/Azure/osdu-spi-indexer/commit/c012554dcfb522ec2640d4f0cb89c8e27dbafb45))
* Seed fork-owned azure trees ([a5dc487](https://github.com/Azure/osdu-spi-indexer/commit/a5dc4872b0b6fa8beabdfbe541593811f9a1d871))
* **spi:** Add service descriptor for indexer ([90e050d](https://github.com/Azure/osdu-spi-indexer/commit/90e050d92d20d780048b855d22c96ed9bacaa0ed))
* **spi:** Add service descriptor for indexer ([1d89284](https://github.com/Azure/osdu-spi-indexer/commit/1d89284418f7706ceed0f2cd49ec93e57c3cc00e))
* Sync template updates ([0ad8105](https://github.com/Azure/osdu-spi-indexer/commit/0ad81057de029d7acda9bb797dc89c88f4475527))
* Sync template updates ([6524bef](https://github.com/Azure/osdu-spi-indexer/commit/6524bef22fc6d7c37c45381ec653fd948e9036f4))
* **template-sync:** Sync template updates 2026-10-13 ([40c2f2f](https://github.com/Azure/osdu-spi-indexer/commit/40c2f2ffc286004af201fcc6cdf3bab15c0696c1))
* **template-sync:** Sync template updates 2026-10-14 ([a24611f](https://github.com/Azure/osdu-spi-indexer/commit/a24611f903c87721fed85a57d39124503a66d4e9))


### ♻️ Code Refactoring

* **audit:** Encapsulate audit roles and request context in logging layer ([4a2bd12](https://github.com/Azure/osdu-spi-indexer/commit/4a2bd12e73f914460c93aade608287d16e42e2ce))
* **audit:** Encapsulate audit roles and request context in logging layer ([0354264](https://github.com/Azure/osdu-spi-indexer/commit/0354264e0e57237d9673aedf6854fd782d05a8a9))
* **indexer:** Extract index creation decision into helper methods ([beab206](https://github.com/Azure/osdu-spi-indexer/commit/beab2061f21556f4ef7b63d89140b8e1083072c3))


### 🔨 Build System

* **deps:** Bump netty, log4j, slf4j in indexer-test-azure ([413dde1](https://github.com/Azure/osdu-spi-indexer/commit/413dde153f479001600ecfea471955e18a210872))
* **deps:** Bump netty, log4j, slf4j in indexer-test-azure ([d4f0014](https://github.com/Azure/osdu-spi-indexer/commit/d4f0014b8b1cbef637a2bb38bb297c560ccbd06d))
