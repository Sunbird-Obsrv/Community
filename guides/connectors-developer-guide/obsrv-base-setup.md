# Obsrv Base Setup

To start developing connectors, here are the prerequisites

* Postgresql 16 or later
* Kafka 3.7.1 or later

## Postgresql

To set up a database for `obsrv` in PostgreSQL, follow these steps:

1. Start your PostgreSQL server.
2. Create a database named `obsrv` by executing the following command

```sql
CREATE DATABASE obsrv;
```

3. Proceed to create the required tables within the `obsrv` database as

```sql
CREATE TABLE public.datasets (
	id text NOT NULL,
	dataset_id text NULL,
	"type" text NOT NULL,
	"name" text NULL,
	validation_config json NULL,
	extraction_config json NULL,
	dedup_config json NULL,
	data_schema json NULL,
	denorm_config json NULL,
	router_config json NULL,
	dataset_config json NULL,
	tags _text NULL,
	data_version int4 NULL,
	status text NULL,
	created_by text NULL,
	updated_by text NULL,
	created_date timestamp DEFAULT now() NOT NULL,
	updated_date timestamp NOT NULL,
	published_date timestamp DEFAULT now() NOT NULL,
	api_version varchar(255) DEFAULT 'v1'::character varying NOT NULL,
	"version" int4 DEFAULT 1 NOT NULL,
	sample_data json DEFAULT '{}'::json NULL,
	entry_topic text DEFAULT 'dev.ingest'::text NOT NULL,
	CONSTRAINT datasets_pkey PRIMARY KEY (id)
);

CREATE TABLE public.connector_registry (
	id text NOT NULL,
	connector_id text NOT NULL,
	"name" text NOT NULL,
	"type" text NOT NULL,
	category text NOT NULL,
	"version" text NOT NULL,
	description text NULL,
	technology text NOT NULL,
	runtime text NOT NULL,
	licence text NOT NULL,
	"owner" text NOT NULL,
	iconurl text NULL,
	status text NOT NULL,
	ui_spec json DEFAULT '{}'::json NOT NULL,
	source_url text NOT NULL,
	"source" json NOT NULL,
	created_by text NOT NULL,
	updated_by text NOT NULL,
	created_date timestamp NOT NULL,
	updated_date timestamp NOT NULL,
	live_date timestamp NULL,
	CONSTRAINT connector_registry_connector_id_version_key UNIQUE (connector_id, version),
	CONSTRAINT connector_registry_pkey PRIMARY KEY (id)
);

CREATE TABLE public.connector_instances (
	id text NOT NULL,
	dataset_id text NOT NULL,
	connector_id text NOT NULL,
	connector_config text NOT NULL,
	operations_config json NOT NULL,
	status text NOT NULL,
	connector_state json DEFAULT '{}'::json NOT NULL,
	connector_stats json DEFAULT '{}'::json NOT NULL,
	created_by text NOT NULL,
	updated_by text NOT NULL,
	created_date timestamp NOT NULL,
	updated_date timestamp NOT NULL,
	published_date timestamp NOT NULL,
	"name" text NULL,
	CONSTRAINT connector_instances_pkey PRIMARY KEY (id),
	CONSTRAINT connector_instances_connector_id_fkey FOREIGN KEY (connector_id) REFERENCES public.connector_registry(id),
	CONSTRAINT connector_instances_dataset_id_fkey FOREIGN KEY (dataset_id) REFERENCES public.datasets(id)
);
```

{% hint style="info" %}
In case you already have a full version of Obsrv installed, the above steps can be skipped
{% endhint %}



## Kafka

The Obsrv pipeline utilizes Kafka to efficiently process data in real-time. Connector SDKs ensure data is pushed to Kafka upon confirmation of successful connection, facilitating smooth data integration and quick responsiveness.&#x20;

Ensure that you have Kafka up and running



