# Product & Developer Guide

**OVERVIEW**

Sunbird allows for generation and consumption of usage data in order to be able to carry out any required analysis. The data flow on the platform is as illustrated below.

The client apps and micro services within Sunbird are instrumented to generate Telemetry data to capture usage and various actions to derive insights. The data pipeline will process the Telemetry event stream data in near real-time by application of a series of validation, de-duplication, transformation and denormalization steps. The Telemetry data is synced at various points in the data pipeline to a configurable cloud storage which acts as the persistent data storage.

A generic summarized dataset is generated from the Telemetry data which will comprise of commonly used summaries such as session summary. The summarized dataset is an aggregated dataset which can be used to generate custom derived datasets required for custom workflows.

The telemetry event data is then synced to a configurable analytic data store to build a access layer to the data sets. The adopters are free to choose any analytics data store and/or visualisation tools (Sunbird supports Druid and Superset out-of-the-box) of their choice to build canned reports and dashboards to slice and dice the data.

Sunbird Obsrv is a combination of various tools which provide the capabilities such as streaming, processing and storage of telemetry data and deriving reporting insights from the data.

![L0 Sunbird Obsrv Component View](<../../.gitbook/assets/L0_View.png>)

![High Level Sunbird Obsrv Component Overview](<../../.gitbook/assets/Component_View.png>)

![Data analytics architecture](<../../.gitbook/assets/DataPipeline BB HighLevel Diagram.png>)	


