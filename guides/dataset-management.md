---
description: List of APIs to manage datasets
---

# Dataset Management

### Dataset APIs

Dataset APIs allow you to manage the datasets, such as creating new datasets, updating and list existing datasets and retrieving specific dataset metadata.

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasets/v1/create" method="post" expanded="true" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasets/v1/update" method="patch" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasets/v1/get/{datasetId}" method="get" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasets/v1/list" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

### Datasource (Tables) APIs

Datsources APIs enable you to manage datasources, i.e. tables in the database. You can add new datasources, retrieve information about existing datasources, update and list all existing data sources.

{% hint style="info" %}
These APIs will be merged into the Dataset APIs in the coming releases. Post that change, there is no need to configure the data sources (tables) separately.
{% endhint %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasources/v1/create" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasources/v1/update" method="patch" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasources/v1/get/{datasourceId}" method="get" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/datasources/v1/list" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml" path="/data/v1/submit/ingestion" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi.yaml)
{% endswagger %}
