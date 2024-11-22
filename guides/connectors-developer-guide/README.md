# Connectors Developer Guide

Connectors, alongside datasets, are fundamental components of Obsrv. While datasets establish a framework for managing data processing, storage, and querying, connectors provide a framework for managing data ingress and egress.

This section will guide you through the process of developing, packaging, and deploying connectors using the provided SDKs and repositories. The connectors can be written in Scala, Java, or Python and can work with various data processing frameworks like Spark and Flink.

## Repositories

To begin developing a connector-based application, clone the corresponding repositories.

### Scala and Java Repositories

* [**job-sdk-scala**](https://github.com/Sunbird-Obsrv/job-sdk-scala): This repository houses the Software Development Kit (SDK) for crafting jobs in Scala and Java. It encompasses modules for fundamental functionalities, as well as specialized modules for Flink and Spark.
* [**connector-sdk-scala**](https://github.com/Sunbird-Obsrv/connector-sdk-scala): This repository furnishes the SDK for constructing connectors in Scala and Java. It includes core functionalities and specialized modules for Flink and Spark.

### Python Repositories

* [**obsrv-python-sdk**](https://github.com/Sunbird-Obsrv/obsrv-python-sdk): The repository offers a Python SDK for developing connectors. It includes the requisite modules and configurations to facilitate the creation of connectors.
