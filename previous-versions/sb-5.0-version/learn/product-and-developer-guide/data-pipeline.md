# Data Pipeline

Group of real-time stream processing jobs that processes the event stream of telemetry data generated from client apps and micro services. The telemetry data goes through a series of steps such as validation, de-duplication, transformation and denormalization of metadata. The transformed data is then stored in a consumable format that can be used for further analysis.

![Analytics Data Pipeline](<../../../../.gitbook/assets/DataPipeline\_Component (1).png>)

#### Key Features:

1. Lambda Architecture: A hybrid approach of using both batch-processing and stream-processing methods to process massive data sets.
2. Loose coupling: Data processing jobs are loosely coupled as they only communicate with a durable queue such as Apache Kafka.
3. Easy chaining: Data processing jobs can be chained easily by only configuring the input and output data sources they consume from. This allows easy introduction of new jobs required for processing custom workflows.
4. Data Sync points: The stream of data is synced to a configurable cloud storage which acts as a persistent data store with durability. The data sync points allow the capability to replay data from a specific stage in the pipeline.
5. Resiliency: The data pipeline guarantees AT LEAST ONCE processing semantics and ensures no data loss.
6. Monitoring: The data pipeline jobs has the capability to emit standard and custom metrics to monitor the health and also allows you to perform an audit of the system at various stages.
7. Auto-scaling: The data processing pipeline offers support for auto-scaling out of the box. This helps the pipeline to adapt to changes in the incoming data volume.
8. Real-time analytics: The data processing pipeline offers out of the box support with Apache Druid, an analytics data store design for fast slice-and-dice analytics.

#### Installation Configuration Reference:

| Property                   | Description                                                         | Default           |
| -------------------------- | ------------------------------------------------------------------- | ----------------- |
| kafka.consumer.broker.host | Host or IP addresses of Kafka brokers for consumption of data       | none              |
| kafka.producer.broker.host | Host or IP addresses of Kafka brokers for publishing data           | none              |
| enable.checkpointing       | A boolean variable to enable checkpointing on cloud storage         | false             |
| redis.host                 | Host or IP address of Redis cache used for metadata caching         | none              |
| consumer.parallelism       | Number of threads to consume data in parallel                       | 1                 |
| operator.parallelism       | Number of threads to process data in parallel                       | 1                 |
| telemetry.schema.path      | Directory path for JSON schema files to validate the telemetry data | schemas/telemetry |
| event.max.size             | Acceptable size of each event in bytes                              | 1 Mb              |
| redis.devicestore.id       | The index of the device data store in Redis cache                   | 2                 |
| redis.userstore.id         | The index of the user data store in Redis cache                     | 12                |
| redis.contentstore.id      | The index of the content data store in Redis cache                  | 5                 |
| redis.dialcodestore.id     | The index of the dialcode data store in Redis cache                 | 6                 |

####

{% embed url="https://github.com/project-sunbird/sunbird-data-pipeline" %}
Data Pipeline source code
{% endembed %}
