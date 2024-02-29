# <mark style="color:blue;">Obsrv 2.0.1 GA Release</mark>
Release Date - 29th Feb'24
## **Features**
----------
#### **Functional** 
* [Enhancement] **Core pipeline enhancments** [#OB-559](https://project-sunbird.atlassian.net/browse/OB-559)
	- To handle denormalization logic for empty keys, both text & numeric keys.
	- Moved failed events sinking into a common base class
	- Updated framework to created dynamicKafkaSink object
	- Master dataset processor can now do denormalization with another master dataset as well
	- Added timezone handling to store the data in druid in the TZ specified by the dataset

* [Enhancement] **Tech software upgrades** [#OB-559](https://project-sunbird.atlassian.net/browse/OB-559)
	 Postgres, Druid, Superset, NodeJS, Kubernetes are upgraded to latest versions.

* [Enhancement] **Enhancements in dataset API service** [#OB-560](https://project-sunbird.atlassian.net/browse/OB-560)
	- Update API endpoints
	- Bug fixes

* [Enhancement] **Infra reliability** [#OB-560](https://project-sunbird.atlassian.net/browse/OB-560)
	 - Verification of metrics for various services
	 - Metrics intrumentation for services

* [Enhancement] **Benchmarking** [#OB-560](https://project-sunbird.atlassian.net/browse/OB-560)
	Processing, Ingestion & Querying benchmarking.

* [Enhancement] **Bug Fixes and Improvements**  [#OB-559](https://project-sunbird.atlassian.net/browse/OB-559)
	- Fix automation scripts for latest changes
	- Fixed unit tests and improve coverage

* [Feature] **Connector Framework implementation**

* [Feature] **Hudi Data Ingestion**
