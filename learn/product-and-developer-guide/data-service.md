# Data Service

Data service comprises of a group of APIs that are used for configuring jobs and data exhausts - creation, updation, deletion etc. of jobs and exhausts are carried out via these APIs (CRUD for jobs)

#### Data Exhaust APIs:

Data exhaust apis provide the ability to create reports from pre-defined dataset configurations. The apis also provide the ability to create new datasets to generate reports.

![Data Exhaust/Report APIs](<../../.gitbook/assets/Data Service.png>)

#### Key Features:

1. Create Datasets: Create new reusuable, custom datasets to generate custom reports. For instance, a dataset with an ability to apply a filter on course batchIds to generate reports.
2. Submit Reports: Ability to submit report requests based on pre-existing datasets. Currently supported datasets are:
   * Course Progress Reports
   * Userinfo Reports
   * Assessment Response Reports
3. Standard Datasets: Standard datasets do not have an ability to apply filters other than the tenant information and data ranges. Currently support standard datasets are:
   * Raw data reports
   * Summary data reports
   * Aggregated Summary data reports
4. Public Datasets: The public dataset api can be used to expose a scheduled report to public without authentication.

{% hint style="info" %}
[Data Exhaust API Documentation](http://docs.sunbird.org/latest/apis/dataexhaustapi/index.html)
{% endhint %}

#### Report APIs:

The Report APIs provide the ability to generate and schedule custom reports from Druid data store. The APIs leverage the query infrastructure provided by the Druid data store to configure custom reports

![](<../../.gitbook/assets/Report APIs.png>)

#### Key Features:

1. Schedule reports: The Report APIs provides the capability to execute a configured report on a schedule. The reports are uploaded to a configurable cloud storage.
2. Update pre-configured reports: The Report APIs provides the capability to update the report configuration of an existing scheduled report.
3. Configurable report configuration: The Reports can be set up with configurable queries to generate custom report. The report queries can have dimensions, aggregations, filters etc.

{% hint style="info" %}
[Report APIs Documentation](http://docs.sunbird.org/latest/apis/druidreportapi/index.html)
{% endhint %}

**Additional Documentation:**

**Accessing Sunbird Data Exhaust APIs :**

{% file src="../../.gitbook/assets/Sunbird Data Exhaust APIs.pdf" %}

{% embed url="https://github.com/project-sunbird/sunbird-analytics-service" %}
Data Service source code
{% endembed %}

\\
