# Product Roadmap

Sunbird Obsrv 2.0 has been redesigned from ground up to allow ingestion, processing and querying of the telemetry data to be agnostic of the data specification of the telemetry data. The last stable release of Sunbird Obsrv 1.0, which is tightly coupled of the [Sunbird Telemetry](https://telemetry.sunbird.org/) Specification will be [Release 5.1.1](../use/release-notes/release-v-5.1.0.md). The product roadmap for Sunbird Obsrv 2.0 has been detailed out below with the features being logically grouped under specific functional features.

Sunbird Obsrv [ISSUE TRACKER](https://github.com/Sunbird-Lern/Community/issues) : This is the link to the set of issues/ submissions or requests that are being considered for development as part of the Sunbird Obsrv roadmap. You can upvote an issue if you find it relevant, or <mark style="color:blue;">add a new issue</mark> to the list

<mark style="color:orange;">**Obsrv 2.0.0 GA Release date - 31st Dec'23**</mark>

<mark style="color:orange;">**360 degree observability**</mark>

1. **Enhancements in datasets management** - These feature enhances data management capabilities and provides flexibility in dataset maintenance.
	- Users can now delete draft datasets using the API.
	- User can now retire live datasets using the API. 
	- Ability to configure the denorm on the master datasets
2. **Core pipeline enhancments** - Core pipeline changes to route all the failed events with detailed summary to failed topic.
3. **Detailed Debugging with Query Store** - Indexing all failed events into the query store for comprehensive and detailed debugging. This feature improves troubleshooting capabilities and accelerates issue resolution.
4. **Automated Backup Configuration** - Automated the configuration of the backup system during installation, allowing users to define their preferred timezone. This ensures a seamless and customized backup setup for enhanced data protection.
5. **Aggregated and Filtered Data Sources** - Introduced the option to create aggregated data sources and filtered data sources through the API. Also enhanced API to query on the rollup datasources. This feature provides users with more control over data sources, enabling customization based on specific requirements.
6. **Filtered Rollups** - Ability to create rollup on a filter using API
7. **Bug Fixes and Improvements**
	- Fixed the auto-conversion of the timestamp property to a string.
	- Automatically convert numeric field to Integer during ingestion into Query Store/Druid.
	- Improve the code coverage of obsrv core to 100%

<mark style="color:orange;">**Connector Ecosystem**</mark>

These connectors enable the data IN and OUT of the platform and expand the reach of our platform.

1. **JDBC connector** - This connector supports popular databases such as MySQL, PostgreSQL. 
2. **Data Stream Source Connector** - This connector supports real-time streaming data sources such as Apache Kafka.

<mark style="color:orange;">**Obsrv 2.2.0 Release date - 31st Oct'23**</mark>

<mark style="color:orange;">**360 degree observability**</mark>

1. Addressing major vulnerabilities, making Obsrv BB free from vulnerabilities.
2. Restarting Flink to pick up new datasets. The command service with the Flink restart command needs to be open-sourced.
3. Few Bug fixes with components & deployment.

<mark style="color:orange;">**Obsrv 2.1.0 Release date - 30th Sep'23**</mark>

<mark style="color:orange;">**360 degree observability**</mark>

1. Restarting Flink to pick up new datasets. The command service with the Flink restart command needs to be open-sourced.
2. Refactor of Sunbird Ed Cache Updater Jobs
3. Enhance the Device register/profile API to send transaction event to obsrv 2.0 system using data IN API or Kafka connector

<mark style="color:orange;">**Connector Ecosystem**</mark>

1. Object Storage Connectors - Cloud storages&#x20;
2. MinIO connector
3. Connector Marketplace/Framework
4. Postgresql Connector for data & denormalization

<mark style="color:orange;">**Obsrv 2.1.0 Release date - 31st Aug'23**</mark>

<mark style="color:orange;">**360 degree observability**</mark>

1. Data Exhaust API - Ability to download the raw data using the Data Exhaust APIs
2. Druid Query and Ingestion Submission Wrapper APIs - Ability to query and ingestion spec submission wrapper API 
3. APIs System to generate the Data IN/OUT Metrics Generation
4. Integrate the Obsrv superset with Query Wrapper APIs

<mark style="color:orange;">**Simplified Operations**</mark>

1. Configure the obsrv to run with MinIO object store
2. Support on multi channel alerts
3. Enabling the labels for all the services


<mark style="color:orange;">**[Obsrv 2.0.0 GA](<../../use/release-notes/release-v-5.3.0-GA.md>)(Planned release date - 2 May'23)**</mark>

<mark style="color:orange;">**360 degree observability**</mark>

1. Data Set Creation via APIs
2. Data Denormalization with API & Push to Kafka
3. Real time querying
4. Druid SQL & JSON query interface
5. Out-of-the-box visualizations with Superset

<mark style="color:orange;">**Simplified Operations**</mark>

1. One-click installation for AWS, Azure & GCP&#x20;
2. Standard Monitoring Capability&#x20;
3. Log Streaming with Grafana UI

<mark style="color:orange;">**Connector Ecosystem**</mark>

1. Kafka connector for data & denormalization

<mark style="color:orange;">**Unified Web Console**</mark>

1. General Cluster metrics

\
<mark style="color:orange;">**[Release-5.1.0](<../../use/release-notes/release-v-5.1.0.md>)**</mark> <mark style="color:orange;">**(Planned release date - 04 Nov'22) - Projects**</mark>



<mark style="color:orange;">**Project : Enabling ease of adoption**</mark>

<mark style="color:orange;">**Task : One click install enhancements**</mark>

a. Include the data products (work flow summary) as part of the one-click installer package. These allow for easy generation of common summaries once raw telemetry is generated by the adopter.&#x20;

b. Include a sample data set and some pre-configured charts as part of the one-click installer package so that an adopter trying it out can get a feel of the types of charts that can be generated, and the kind of data required to be generated for this purpose.

&#x20;

<mark style="color:orange;">**Project: Enabling ease of adoption**</mark>&#x20;

<mark style="color:orange;">**Task : Additional documentation**</mark>

Additional pending Sunbird Obsrv documentation work



<mark style="color:orange;">**Project: Enabling ease of adoption**</mark>

<mark style="color:orange;">**Task: Creation of a Learning module for Sunbird Obsrv**</mark>

Compile existing learning resources/ create new resources in order to put together a learning module/ course that will allow a developer to get familiar with the Obsrv building block, and potentially get "Obsrv certified" by earning a certificate after taking an assessment.&#x20;







<mark style="color:green;">**4.10.0 :**</mark> Planned for 06 Jun '22

| <p><strong>1. Functional Requirements: </strong><mark style="color:green;"><strong>4.10.0</strong></mark></p><p><strong>-</strong> API level accsess to data files that power the reports and charts on the portal</p>                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - Ability to configure Sunbird datasets as Public or Private at an instance level                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| - KT for indexing variables into Druid                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| <p><strong>2. Deployment and Release Processes: </strong><mark style="color:green;"><strong>4.10.0</strong></mark></p><p>Build, Deploy and provisioning scripts : refactoring of the provisioning and deployment scripts for the BB- Sunbird dev and staging environments will be repurposed for each BB. The deployment scripts need to be refactored to sandbox the environment on Kubernetes for Sunbird Obsrv BB. This will be done by deploying the services and components on Kubernetes onto a separate configurable namespace for Sunbird BB<br></p> |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| <mark style="color:green;">**5.0.0 :**</mark> Planned for 19 Aug'22                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| <p><strong>1. One click mini installation of data pipeline components on Kubernetes: </strong><mark style="color:green;"><strong>5.0.0</strong></mark></p><p><strong>-</strong> Currently not all components are deployed onto Kubernetes and it takes significant effort from the adopter to get all the components up and running. This capability will allow the adopter to quickly install required components on Kubernetes and have the entire analytics platform up and running.</p>                                                                  |
| <p><strong>2. Publish the minimum number of Kubernetes nodes required for one click installation: </strong><mark style="color:green;"><strong>5.0.0</strong></mark></p><p>- Analyse and publish minimum number of nodes required to get the analytics platform up and running on Kubernetes. Also, publish the mandatory components required to get the installation up and running.</p>                                                                                                                                                                     |
| <p><strong>3. Migration of API Swagger documentation to Sunbird Obsrv Building block pages: </strong><mark style="color:green;"><strong>5.0.0</strong></mark></p><p>- Migrate existing Sunbrid Swagger API for analytics API and data exhaust APIs documentation to Sunbird Obsrv Building block pages.</p>                                                                                                                                                                                                                                                  |
| <p><strong>4. Multi-cloud support for blob store:</strong> <mark style="color:green;"><strong>5.0.0</strong></mark></p><p>Update the framework, cloud-storage sdk, Secor and Flink checkpoints to work with GCP as well- Generalize the analytics framework, cloud-storage-sdk, Secor and Flink checkpoints to work with AWS S3, Azure Blob Storage and Google Cloud Storage- Add relevant configuration files required for the generalization<br></p>                                                                                                       |
| - Be able to deploy existing microservices into a different namespace (SB Ed)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| [**Sunbird Obsrv Backlog >**](https://project-sunbird.atlassian.net/issues/?filter=12538)                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| <p><strong>1. Documentation to configure data exhaust reports using the APIs:</strong> Detailed explanation of the different sections of the configuration schema.</p><p>- Add documentation to explain the configuration schema for the various data exhaust report API</p><p>- Add detailed documentation on the usage of the APIs</p>                                                                                                                                                                                                                     |
| <p><br></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
