---
description: Functional capabilities that can be enabled using Sunbird Obsrv
---

# Functional Capabilities

The following are the key functional capabilities that one would turn to Sunbird Obsrv for:

**Flexible Data Model Specification to adapt to any domain:** The Telemetry data model is designed to instrument telemetry data (interactions, metrics and logs) for any domain.

The domain of an application determines to a vast extent the design of the data model for understanding various interactions and metrics from the application. Sunbird Obsrv is flexible to allows the application to decide on the data model for the Telemetry and it is designed intelligently to keep the data structure for the event data as flexible as possible while enforcing to capture some common characteristics to ascertain the component details of the source system that generates the Telemetry. The flexible data model also ensures that the downstream processing systems have to change very little to accommodate the changes in the data model and allows re-usability of the majority of the components in the analytics platform.

The data model works based on the telemetry specifications defined as per the domain of application, based on the [Sunbird Telemetry](https://telemetry.sunbird.org) building block.

**Data collection at scale:** Perform seamless telemetry data collection from client apps using horizontally scalable apis<mark style="color:green;">.</mark>

The ability to seamlessly scale the telemetry data collection is very important as it enables the client applications to sync the data without any data loss and also determines the rate at which . The data collection api in Sunbird Obsrv can be horizontally scaled by adding more instances of the collector both in containerized and virtual machine based environments. The data collector also provides options for configurable data sink such as Apache Kafka, Apache Cassandra or local hard disks. The data sinks, in turn, can be scaled horizontally which helps transferring telemetry data at very high transfer rates along with consistent and durable storage.

This is enabled by the [Telemetry Service](product-and-developer-guide/telemetry-service.md) component of the Obsrv building block

**Easy integration with Cloud providers:** The analytics platform is cloud agnostic and can be easily deployed onto any of the popular cloud platforms such as AWS, Azure or Google Cloud Platform.

The analytics platform has various plugable components and all of the components provide configurations to support deployments onto the popular cloud platforms. Furthermore, most of the components are deployed onto Kubernetes, the most popular tool for container orchestration.

**Streaming/Batch data processing:** The analytics platform provides an ability to process both real-time streaming data and batch data to derive insights.

The analytics platform is built using lambda architecture principles. Lambda architecture is designed to provide the capability to process both real-time streaming data and batch data. The analytics platform has both a batch layer and a stream layer storage which helps in fault-tolerant and scalable architecture for data processing. The stream layer ensures that insights are derived in near real time to take immediate actions on the data arriving and the batch layer ensures that reporting requirements over a specific time period are addressed. Fault tolerance is built into the pipeline which ensures that there will be no data loss. Lambda architecture also provides the capability to replay or reload data for data processing with idempotency.

The [Data Pipeline](product-and-developer-guide/data-pipeline.md) component of the building block is used to enable these capabilities

**Build fast, scalable data analytics:** The analytics platform is designed to build ad-hoc analytics or recurring reports in a fast, scalable manner.

Any analytics platform should allow ad-hoc user queries to be served with low latency response times and should provide an immutable data storage to obtain a snapshot of the historical data. Sunbird Obsrv's analytics platform uses different data stores to address the ability to query data with low latency. It uses the distributed cloud storage for batch processing of data to generate reports and it uses an Online Analytical Processing (OLAP) data store to address real-time adhoc user queries. Both these layers provide the ability to build fast and scalable analytics and reporting systems on top of large amounts (terabytes) of data with efficient infrastructure. The access of the data from the polyglot data stores is always using APIs which can horizontally scale according to the latency requirements.

**Readymade metrics & Downloadable data:** The analytics platform provides an ability to download both the raw data and aggregated data through the reporting api also with an ability to schedule recurring reporting requirements.

Apart from the ability to build a querying layer on top of the data, a data analytics platform should provide the ability to download the data from the system so that the client applications can build their own insights on top of the data. Sunbird Obsrv's analytics platform is designed with this capability in mind. Cloud data stores in general store objects that are private and only the object owner has permissions to access them. The analytics platform provides APIs with access control to download data. The APIs generate urls which are pre-signed with security credentials of the object owner to grant time-bound permissions to download the data. This capability opens up a lot of possibilities for the client applications to create a visualization without overloading the data platform.

The quick-analysis capabilities, along with the readymade metrics and downloadable datasets are made available using the [Data Service](product-and-developer-guide/data-service.md), [Report Service](product-and-developer-guide/report-service.md), [Report Configurator](product-and-developer-guide/report-configurator.md) and the [Summarisers](product-and-developer-guide/summarisers.md). These components come together to enable a boquet of reporting services for the Sunbird Obsrv building block.

Some additional possibiities that can be visualised using Sunbird Obsrv include:

* Allowing for `capture of telemetry` as per chosen specifications from an agricultural monitoring system, and `processing and analysis of the resulting data` to optimise output
* Aggregation of anonymised health data from across platforms, and its `analysis` to arrive at health indicators and patterns at population scale.
* Analysis of `streams of weather data` from satellites to better `predict` weather patterns.





_Obsrv_ allows for extensive configurability so as to enable creation of various custom workflows. Refer to the pages for different components listed in the Product & developer guide page to see details of what configurations are available for each.
