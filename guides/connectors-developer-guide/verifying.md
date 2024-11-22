# Verifying

## Environment Setup

1. Since connectors are configured at a dataset level, create a sample dataset. Here is a sample to create `new-york-taxi-data` dataset.

```sql
INSERT INTO public.datasets (id,dataset_id,"type","name",validation_config,extraction_config,dedup_config,data_schema,denorm_config,router_config,dataset_config,tags,data_version,status,created_by,updated_by,created_date,updated_date,published_date,api_version,"version",sample_data,entry_topic) VALUES
 ('new-york-taxi-data','new-york-taxi-data','event','new-york-taxi-data','{"validate": true, "mode": "Strict"}','{"is_batch_event": true, "batch_id": "id", "extraction_key": "events", "dedup_config": {"dedup_key": "id", "drop_duplicates": true, "dedup_period": 604800}}','{"dedup_key": "tripID", "drop_duplicates": true, "dedup_period": 604800}','{"$schema": "https://json-schema.org/draft/2020-12/schema", "type": "object", "properties": {"tripID": {"type": "string", "suggestions": [{"message": "The Property ''''tripID'''' appears to be ''''uuid'''' format type.", "advice": "Suggest to not to index the high cardinal columns", "resolutionType": "DEDUP", "severity": "LOW", "path": "properties.tripID"}], "arrival_format": "text", "data_type": "string"}, "VendorID": {"type": "string", "arrival_format": "text", "data_type": "string"}, "tpep_pickup_datetime": {"type": "string", "suggestions": [{"message": "The Property ''''tpep_pickup_datetime'''' appears to be ''''date-time'''' format type.", "advice": "The System can index all data on this column", "resolutionType": "INDEX", "severity": "LOW", "path": "properties.tpep_pickup_datetime"}], "arrival_format": "text", "data_type": "date-time"}, "tpep_dropoff_datetime": {"type": "string", "suggestions": [{"message": "The Property ''''tpep_dropoff_datetime'''' appears to be ''''date-time'''' format type.", "advice": "The System can index all data on this column", "resolutionType": "INDEX", "severity": "LOW", "path": "properties.tpep_dropoff_datetime"}], "arrival_format": "text", "data_type": "date-time"}, "passenger_count": {"type": "string", "arrival_format": "text", "data_type": "string"}, "trip_distance": {"type": "string", "arrival_format": "text", "data_type": "string"}, "RatecodeID": {"type": "string", "arrival_format": "text", "data_type": "string"}, "store_and_fwd_flag": {"type": "string", "arrival_format": "text", "data_type": "string"}, "PULocationID": {"type": "string", "arrival_format": "text", "data_type": "string"}, "DOLocationID": {"type": "string", "arrival_format": "text", "data_type": "string"}, "payment_type": {"type": "string", "arrival_format": "text", "data_type": "string"}, "primary_passenger": {"type": "object", "properties": {"email": {"type": "string", "arrival_format": "text", "data_type": "string"}, "mobile": {"type": "string", "arrival_format": "text", "data_type": "string"}}, "arrival_format": "object", "data_type": "object", "additionalProperties": false}, "fare_details": {"type": "object", "properties": {"fare_amount": {"type": "string", "arrival_format": "text", "data_type": "string"}, "extra": {"type": "string", "arrival_format": "text", "data_type": "string"}, "mta_tax": {"type": "string", "arrival_format": "text", "data_type": "string"}, "tip_amount": {"type": "string", "arrival_format": "text", "data_type": "string"}, "tolls_amount": {"type": "string", "arrival_format": "text", "data_type": "string"}, "improvement_surcharge": {"type": "string", "arrival_format": "text", "data_type": "string"}, "total_amount": {"type": "string", "arrival_format": "text", "data_type": "string"}, "congestion_surcharge": {"type": "string", "arrival_format": "text", "data_type": "string"}}, "arrival_format": "object", "data_type": "object", "additionalProperties": false}}, "additionalProperties": false}','{"denorm_fields": [], "redis_db_host": "localhost", "redis_db_port": 6379}','{"topic": "new-york-taxi-data"}','{"keys_config": {"timestamp_key": "obsrv_meta.syncts", "data_key": "", "partition_key": ""}, "indexing_config": {"olap_store_enabled": true, "lakehouse_enabled": false, "cache_enabled": false}, "cache_config": {"redis_db_host": "localhost", "redis_db_port": 6379, "redis_db": 0}, "file_upload_path": []}','{}',2,'Live','SYSTEM','SYSTEM','2024-09-12 13:13:15.400866','2024-09-17 11:26:00.774249','2024-09-17 11:26:00.774249','v2',1,'{"tripID": "0de066f6-e7e4-44e3-9d5a-af8be8cd360a", "VendorID": "2", "tpep_pickup_datetime": "2023-04-12 13:48:30", "tpep_dropoff_datetime": "2023-11-17 13:52:40", "passenger_count": "3", "trip_distance": ".00", "RatecodeID": "1", "store_and_fwd_flag": "N", "PULocationID": "236", "DOLocationID": "236", "payment_type": "1", "primary_passenger": {"email": "Felipe.Grant@hotmail.com", "mobile": "494-699-7052"}, "fare_details": {"fare_amount": "4.5", "extra": "0.5", "mta_tax": "0.5", "tip_amount": "0", "tolls_amount": "0", "improvement_surcharge": "0.3", "total_amount": "5.8", "congestion_surcharge": ""}, "suggestedPii": []}','local.ingest');
```

2. In order to run a connector, the connector must me registered in Obsrv. To do so, fill in the values and run the below query

```sql
INSERT INTO public.connector_registry (id,connector_id,"name","type",category,"version",description,technology,runtime,licence,"owner",iconurl,status,ui_spec,source_url,"source",created_by,updated_by,created_date,updated_date,live_date) VALUES
	 ('example-connector',
	 'example-connector',
	 'Example Connector',
	 'source',
	 'stream',
	 '1.0.0',
	 'Pull data from a Source',
	 'scala',
	 'flink',
	 'MIT',
	 'Sunbird',
	 'data:image/svg+xml;base64,,',
	 'Live','{}','connector-1.0.0-distribution.tar.gz','{}',
	 'SYSTEM','SYSTEM',
	 now(), now(), now()
	);
```

3. The connector must have an active instance inorder where we specify the mapping of the dataset and the connector created above.

```sql
INSERT INTO public.connector_instances (id,dataset_id,connector_id,connector_config,operations_config,status,connector_state,connector_stats,created_by,updated_by,created_date,updated_date,published_date) VALUES
	 ('example-instance-1','new-york-taxi-data','example-connector-1.0.0',
	 '<aes-256-ecb encrypted string>',
	 '{}','Live','{}','{}','SYSTEM','SYSTEM', now(), now(), now()
	 );
```

{% hint style="info" %}
The `connector_config` in the instances uses AES ECB encryption with a key size of 256 bits.&#x20;
{% endhint %}

> To verify if the encryption is correct use an online tool like [this](https://encode-decode.com/aes-256-ecb-encrypt-online/) where algorithm is **AES**, mode is **ECB**, **No-Padding** and key size is **256 bits** (32 character).&#x20;
>
>
>
> For example the following JSON Config \
> `{"source_ip": "localhost", "source_port": 5432, "source_db": "obsrv", "table": "datasets"}` \
>
>
> with a secret `strong_encryption_key_to_encrypt` \
>
>
> should generate an encrypted string equal to&#x20;
>
> `mmT3tqwpq798ywgsdfEdhtp5VXcFzFjutmaEuFqAw9fl4G4OtK6vz89Nhd/deChFWzW3yJWB3Y//SpDzwc3RY31FGqwnAhhD3fpjXP+XYHthCWxBIKar5j8pdTBZ867J` \
>
>
> which can be verfied online, before you encrypt your config. Upon decrypting it should be a valid JSON

4. Make sure you have the configuration files based on the language you are writing the connector in

{% tabs %}
{% tab title="Java / Scala" %}
Here is a sample file to be used in Java / Scala

{% code title="obsrv-connector-config.conf" %}
```editorconfig
postgres {
  host = localhost
  port = 5432
  maxConnections = 2
  user = "postgres"
  password = "postgres"
  database = "obsrv"
}

kafka {
  producer = {
    broker-servers = "localhost:9092"
    compression = "snappy"
    max-request-size = 1000000 # 1MB
  }
  output = {
    connector = {
      failed.topic = "connector.failed"
      metric.topic = "obsrv-connectors-metrics"
    }
  }
}

obsrv.encryption.key = "strong_encryption_key_to_encrypt"

task {
  checkpointing.compressed = true
  checkpointing.interval = 60000
  checkpointing.pause.between.seconds = 30000
  restart-strategy.attempts = 3
  restart-strategy.delay = 30000 # in milli-seconds
  parallelism = 1
  consumer.parallelism = 1
  downstream.operators.parallelism = 1
}

env = local
building-block = obsrv
```
{% endcode %}

Please make sure you update the database and kafka connection values as per your setup
{% endtab %}

{% tab title="Python" %}
Here is a sample configuration file to be used in python

{% code title="obsrv-connector-config.yaml" %}
```yaml
postgres:
  dbname: obsrv
  user: postgres
  password: postgres
  host: localhost
  port: 5432

kafka:
  broker-servers: localhost:9092
  telemetry-topic: obsrv-connectors-telemetry
  connector-metrics-topic: obsrv-connectors-metrics
  producer:
    compression: snappy
    max-request-size: 1000000

obsrv_encryption_key: strong_encryption_key_to_encrypt

connector_instance_id: example-instance-1

building-block: obsrv
env: local
```
{% endcode %}

Please make sure you update the database and kafka connection values as per your setup
{% endtab %}
{% endtabs %}

## Running Stream Connectors

1. Make sure you have Apache Flink running and is ready to accept jobs for processing. Make sure you have atleast ONE task slot for submitting the job
2. Submit the JAR using flink submit.

{% code overflow="wrap" %}
```bash
$FLINK_HOME/bin/flink run <path_to_jar> --port <random_port> --config.file.path <path_to_obsrv-connector-config.conf> --metadata.id <id_from_connector_registry>
```
{% endcode %}

## Running Batch Connectors

1. Make sure you have spark installed
2. Submit the JAR to Spark using the following command

{% tabs %}
{% tab title="Java / Scala" %}
{% code overflow="wrap" %}
```bash
spark-submit --master=local[*] --jars <include_dependent_jars> --class <main_class> <path_to_jar> -f <path_to_obsrv-connector-config.conf> -c <id_from_connector_instances>
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code overflow="wrap" %}
```bash
spark-submit --master=local\[\*\] --conf "spark.pyspark.driver.python=<path_to_python_executable>" --conf "spark.pyspark.python=<path_to_python_executable>" --jars <include_dependent_jars> <path_to_main_python_file> -f <path_to_obsrv-connector-config.yaml> -c <id_from_connector_instances>
```
{% endcode %}

{% hint style="info" %}
If using an virtual environment for python development, then `path_to_python_executable` must be from the same environment&#x20;
{% endhint %}
{% endtab %}
{% endtabs %}



