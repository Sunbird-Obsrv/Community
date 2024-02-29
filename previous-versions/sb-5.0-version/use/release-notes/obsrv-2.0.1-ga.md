# <mark style="color:blue;">Obsrv 2.0.1 GA Release</mark>
Release Date - 31st Jan'24
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

* [Enhancement] **Improvments** [#OB-559](https://project-sunbird.atlassian.net/browse/OB-559)
	Fixed unit tests and improve coverage