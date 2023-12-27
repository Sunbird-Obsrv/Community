# <mark style="color:blue;">Obsrv 2.0.0 GA Release</mark>
Release Date - 31st Dec'23
## **Features**
----------
#### **Functional** 
* [Enhancement] **Enhancements in datasets management** [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	These feature enhances data management capabilities and provides flexibility in dataset maintenance.
	- Users can now delete draft datasets using the API.
	- User can now retire live datasets using the API. 
	- Ability to configure the denorm on the master datasets

* [Enhancement] **Core pipeline enhancments** [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	 Core pipeline changes to route all the failed events with detailed summary to failed topic.

* [Enhancement] **Detailed Debugging with Query Store** [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	Indexing all failed events into the query store for comprehensive and detailed debugging. This feature improves troubleshooting capabilities and accelerates issue resolution.

* [Enhancement] **Automated Backup Configuration** [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	Automated the configuration of the backup system during installation, allowing users to define their preferred timezone. This ensures a seamless and customized backup setup for enhanced data protection.

* [Enhancement] **Filtered Rollups** [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	 Ability to create rollup on a filter using API

* [Enhancement] **Bug Fixes and Improvements**  [#OB-556](https://project-sunbird.atlassian.net/browse/OB-556)
	- Fixed the auto-conversion of the timestamp property to a string.
	- Automatically convert numeric field to Integer during ingestion into Query Store/Druid.
	- Improve the code coverage of obsrv core to 100%

* [Feature] **Aggregated and Filtered Data Sources** [#OB-557](https://project-sunbird.atlassian.net/browse/OB-557)
	Introduced the option to create aggregated data sources and filtered data sources through the API. Also enhanced API to query on the rollup datasources. This feature provides users with more control over data sources, enabling customization based on specific requirements.

* [Feature] **Connector Ecosystem** [#OB-557](https://project-sunbird.atlassian.net/browse/OB-557)
	These connectors enable the data IN and OUT of the platform and expand the reach of our platform.
	- JDBC connector - This connector supports popular databases such as MySQL, PostgreSQL. 
	- Data Stream Source Connector - This connector supports real-time streaming data sources such as Apache Kafka.
