# Component Diagram



<figure><img src="../../../../.gitbook/assets/Screenshot 2023-08-17 at 5.37.41 PM.png" alt=""><figcaption></figcaption></figure>

On Demand Druid Exhaust service will generate CSV reports based on user request. As this is a generic data-product user can request a CSV report for selected columns using filters. &#x20;

1. **Database Layer**:

* **PostgreSQL Database (job\_request)**: This is where job requests are stored. These requests include information about job configuration. This data appended to postgress by [Filter Format From UI](https://project-sunbird.atlassian.net/wiki/spaces/MC/pages/3339780108/PD+-+Form+Config+-+Release-6.0.0+User+Detail+Report).&#x20;
* **Druid:** This is where flattened data is stored with the help [ml-analytics](https://ed.sunbird.org/contribute/source-code/workflows/manage-learn/ml-analytics-service/ingestions) ingestion specs and can retrieve data using Druid queries for specific datasorces using [Model Config](https://github.com/Sunbird-Ed/ml-analytics-service/blob/release-5.1.0/druid\_data\_product\_query\_config.txt).\
  \
  **Data provider**

| Database   | Table/Datasouces                                                               |
| ---------- | ------------------------------------------------------------------------------ |
| PostgreSQL | job\_request                                                                   |
| Druid      | sl-project, sl-observation, sl-observation-status, sl-survey, ml-survey-status |

2. **Data Processing Layer**:\
   Apache Spark is used to perform transformations, sort columns, eliminate duplicates, and replace unknown values with null. This process enhances data quality, organizes data logically before storing to CSV.

## **User Interaction Diagram**

<figure><img src="../../../../.gitbook/assets/Screenshot 2023-08-17 at 5.39.59 PM.png" alt=""><figcaption></figcaption></figure>

This interaction diagram details the complete process of requesting and generating reports. The user can request a specific report through SunbirdEd from the program dashboard. Using exhaust APIs, this will map the request to SunbirdObsrv. OnDemondDruidExhaust data-product will be triggered by a scheduled cron task, which will query postgress and druid to get data and process it using Spark to transform data and generate the report. The user receives the same report once it has been created.
