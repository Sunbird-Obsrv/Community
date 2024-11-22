# Connector Types

Batch connectors are designed to handle data in chunks or sets, enabling efficient processing of large volumes of data that do not require immediate handling. These connectors are ideal for use cases where data can be accumulated and processed at scheduled intervals. In contrast, streaming connectors are built to process data in real-time, providing instant insights and immediate data handling as it flows into the system. Streaming connectors are essential for applications that demand continuous data updates and low-latency processing, such as real-time analytics and monitoring systems. Together, these connectors facilitate seamless data integration across varying use cases and workloads.

## Source Connectors

### Batch Connectors

Batch connectors are commonly used to pull data from various sources such as databases and file systems. These connectors operate over accumulated data over time and then processing it collectively at scheduled intervals. This approach is especially effective when working with data stored in database systems or file systems by using frameworks such as Apache Spark, which can handle large datasets efficiently. By executing these tasks on a scheduled basis, batch connectors optimize resource usage and ensure that large volumes of data are processed with minimal latency.

{% hint style="info" %}
Current versions of SDKs are available for Java, Scala, and Python.
{% endhint %}

### Streaming Connectors

Streaming connectors that run on Apache Flink are crucial for integrating and processing real-time data streams from platforms like Apache Kafka, Amazon Kinesis, and Debezium. These connectors facilitate the seamless ingestion and processing of data in a distributed, fault-tolerant manner, enabling applications to react to data as it arrives. By leveraging Flink's robust stateful processing capabilities, these connectors support complex event processing, real-time analytics, and continuous data transformations, making them ideal for scenarios requiring immediate insights and low-latency responses.

{% hint style="info" %}
Current versions of SDKs are available for Java and Scala.
{% endhint %}



## Sink Connectors

Sink connectors are used to export data from centralized data platforms, like Obsrv, to various external systems and storage solutions. These connectors ensure that processed data can be efficiently moved to destinations such as data warehouses, cloud storage services, and analytics platforms. By leveraging sink connectors, businesses can maintain updated datasets across multiple systems, enabling actionable insights and enhanced data-driven decision-making.

{% hint style="info" %}
Current versions of SDKs don’t support Sink Connectors and are under development and not available as of now.
{% endhint %}







