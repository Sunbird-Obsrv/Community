---
description: List of APIs to write and read data
---

# Data In & Out APIs

### Data In (Write) API

The Data In APIs facilitate writing data into datasets, designed to simplify the ingestion of JSON data

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/data/in/{dataset_id}" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

### Data Out (Read) APIs

Use the Data Out APIs to fetch data from a dataset with support for SQL and Druid native query formats, suitable for analytics and visualization.

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/data/query/{dataset_id}" method="post"%}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}


### Template APIs

The Template APIs enable efficient management of templates, including creating new templates, updating existing ones, listing all available templates, and retrieving metadata for specific templates. These APIs are designed to facilitate data retrieval from various sources using predefined template formats. They are particularly recommended for production environments where queries remain relatively static and do not require frequent changes.

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/create/{template_id}" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/list" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/read/{template_id}" method="get" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/update/{template_id}" method="patch" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/query/{template_id}" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/template/delete/{template_id}" method="delete" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

