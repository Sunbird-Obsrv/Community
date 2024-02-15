---
description: >-
  Another key construct of Obsrv which allows it to connect to wide variety of
  data sources & formats
---

# Connectors

### Introduction

Connectors are one of the core construct of Obsrv in addition to datasets. While datasets provide a construct to manage your data processing , storage and querying layers, connectors provide a construct to manage your data ingress and outgress.

### What does connectors do?

While Obsrv automatically enables data "push" into the platform there are many use-cases where one has to pull the data from sources. Trying to write custom scripts/jobs to read from many sources and pushing into Obsrv is a complex problem and is prone to quality and reliability issues. "**Connectors**" as a concept is used to solve the problem of pulling data efficiently and reliably. **Connectors** solve quite a few design problems of new age data platforms:

1. **Decoupled:** Enables Obsrv to be decoupled with the data ingestion from source systems. One source system cannot effect the data flowing in from another source system
2. **Source Data Management:** Data quality, volume and lineage can be segregated by source and can be managed independently.
3. **Efficient Scalability:** Only the specific connector that processes large volume needs to be scaled independently rather than the entire data platform
4. **Pluggability:** Just swap out the out of the box connector with your own custom connector or a market-place connector without any impact to the data platform
5. **Extensability:** Future proof where extensibility is guaranteed by design. Your data has a unique source - build your own connector using the connector framework. Connectors not only pull data from sources but can also sync data to choice of your destination (reverse ETL)

Connectors fall into 4 broad categories:

1. **Database:** Any connector pulling data from a OLTP or NoSQL database.
2. **Stream/Event:** Any connector pulling data from streams or event driven systems (like Kafka, RabbitMQ etc). The connectors of this type can process data in real-time.
3. **File:** Any connector pulling data from file systems or object stores like S3, Azure Blob,  GCS, MinIO etc
4. **Application:** Custom application specific connector. For ex: A SAP connector to pull data from SAP system.

### Available Connectors

Following are the connectors available out of the box. Connector with <mark style="color:blue;">blue</mark> are available and <mark style="color:orange;">orange</mark> are under incubation and will be available in future releases

| Connector Type | Connector Source                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Database       | <p><mark style="color:blue;">Postgres</mark>, <mark style="color:blue;">MySQL</mark>, <mark style="color:blue;">DB2</mark>, <mark style="color:blue;">MariaDB</mark></p><p><mark style="color:orange;">Oracle</mark>, <mark style="color:orange;">SQL Server</mark>, <mark style="color:blue;">Amazon RDS</mark>, <mark style="color:blue;">Azure SQL</mark>, <mark style="color:blue;">Google Cloud SQL</mark></p><p><mark style="color:orange;">MongoDB</mark>, <mark style="color:orange;">Cassandra</mark>, <mark style="color:orange;">ElasticSearch</mark></p> |
| Stream         | <mark style="color:blue;">Kafka</mark>, <mark style="color:orange;">Postgresql Debezium</mark>, <mark style="color:orange;">MySQL Debezium</mark>, <mark style="color:blue;">Neo4j Transactions</mark>, <mark style="color:orange;">DB2 Debezium</mark>, <mark style="color:orange;">Oracle Debezium</mark>, <mark style="color:orange;">SQL Server Debezium</mark>, <mark style="color:orange;">MongoDB Debezium</mark>, <mark style="color:orange;">Cassandra Debezium</mark>                                                                                      |
| File           | <mark style="color:blue;">AWS S3</mark>, <mark style="color:orange;">Azure Blob Storage</mark>, <mark style="color:orange;">MinIO</mark>, <mark style="color:orange;">Google Cloud Storage</mark>                                                                                                                                                                                                                                                                                                                                                                    |
