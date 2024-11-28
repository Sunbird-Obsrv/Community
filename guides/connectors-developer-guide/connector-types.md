# SDK Assumptions

## Package Strucuture

For the connector to work seamlessly with Obsrv, the connector package has to be in the following structure.

{% tabs %}
{% tab title="Java/Scala" %}
```
example-connector-0.1.0-distribution.tar.gz
├── libs
    └── sample-dependency.jar
├── example_connector.jar
├── alerts.yaml
├── metadata.json
├── metrics.yaml
├── ui-config.json
└── icon.svg
```
{% endtab %}

{% tab title="Python" %}
```
example-connector-0.1.0-distribution.tar.gz
├── libs # optional
    └── sample-dependency.jar
├── example_connector
    └── main.py
├── alerts.yaml
├── metadata.json
├── metrics.yaml
├── requirements.txt
├── ui-config.json
└── icon.svg
```

> NOTE: The `libs` in python distribution are only required, if PySpark has any dependent JARs.
{% endtab %}
{% endtabs %}

## Supported Event Types

### Stream Connectors

1. When emitting an event to the SDK, the SDK only supports JSON format. If the format is other than JSON, events will be skipped with an error of type `INVALID_DATA_FORMAT_ERROR`
2. In Stream Connectors, the ID has to be unique when registering a stream, if its a CONSTANT. If the ID is being referenced from the Configuration, no action has to be taken.

### Batch Connectors

The batch connector expects a [Spark DataFrame](https://spark.apache.org/docs/latest/sql-programming-guide.html#datasets-and-dataframes) when its returned to the SDK

