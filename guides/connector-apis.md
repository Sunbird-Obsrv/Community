---
description: List of APIs to manage data input connectors
---

# Connector APIs

### Connector Config APIs

Connectors are used to ingest data from external sources. It provides a set of APIs to register, list and read connectors configurations API 

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/connector/register" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/connectors/read/{connector_id}" method="get" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}

{% swagger src="https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml" path="/v2/connectors/list" method="post" %}
[https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml](https://raw.githubusercontent.com/Sanketika-Obsrv/obsrv-api-service/main/api-service/swagger-doc/openapi_v2.yml)
{% endswagger %}
