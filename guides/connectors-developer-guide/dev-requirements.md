# Dev Requirements

{% tabs %}
{% tab title="Java / Scala" %}
## Prerequisites&#x20;

### Stream Connectors

* Java  11
* Scala 2.12.11
* Apache Flink 1.17.2
* Apache Kafka 2.8.1

### Batch Connectors

* Java 11
* Scala  2.12.11
* Apache Spark 3.5.1
* Apache Kafka 2.8.1

## Libraries

Make sure you have the necessary repositories for the development

```sh
git clone git@github.com:Sunbird-Obsrv/job-sdk-scala.git
git clone git@github.com:Sunbird-Obsrv/connector-sdk-scala.git
```

### Setup

1. `job-sdk-scala`

```
cd job-sdk-scala
mvn clean install
```

2. `connector-sdk-scala`

```
cd connector-sdk-scala
mvn clean install
```

## Adding Dependencies

### Stream Connectors

Add the following to your project's `pom.xml` file under dependencies

{% code title="pom.xml" %}
```xml
<dependencies>
    ...
        <dependency>
            <groupId>org.sunbird.obsrv.connector</groupId>
            <artifactId>connector-sdk-flink</artifactId>
            <version>1.0.0</version>
        </dependency>
    ...
</dependencies>
```
{% endcode %}

### Batch Connectors

Add the following to your project's `pom.xml` file under dependencies

{% code title="pom.xml" %}
```xml
<dependencies>
    ...
        <dependency>
            <groupId>org.sunbird.obsrv.connector</groupId>
            <artifactId>connector-sdk-spark</artifactId>
            <version>1.0.0</version>
        </dependency>
    ...
</dependencies>
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
## Prerequisites&#x20;

* Python 3.10 or higher
* Kafka 2.8.1
* Spark (PySpark) 3.5.1

## Required Packages

The `obsrv` python package is distributed through PyPI repository and can be installed using pip

```bash
pip install "obsrv[batch]"
```

### Using Poetry for Dependency Management

{% hint style="info" %}
`Poetry` is recommended for its ease of managing and packaging
{% endhint %}

[Poetry](https://python-poetry.org) is a popular tool for dependency management and packaging in Python projects. It streamlines the process of installing and updating project dependencies. To get started with Poetry, first install it using the following command

```bash
pip install poetry
```

Once installed, you can create a new Poetry project:

```bash
poetry new your_project_name
```

To add dependencies to your project, such as the `obsrv` package, use:

```bash
poetry add "obsrv[batch]"
```

Poetry automatically creates and manages a virtual environment for your project, ensuring isolated dependencies and compatibility management.
{% endtab %}
{% endtabs %}



