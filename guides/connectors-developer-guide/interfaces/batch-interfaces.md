# Batch Interfaces

The SDK's exposes an interface which is to be extended inorder to build a connector

{% tabs %}
{% tab title="Java" %}
## Imports

```java
package org.sunbird.obsrv.connector;

import com.typesafe.config.Config;
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;
import org.sunbird.obsrv.connector.model.Models.ConnectorContext;
import org.sunbird.obsrv.connector.source.ISourceConnector;

import java.util.Collections;
import java.util.Map;
```

## ISourceConnector

```java
public class ExampleSourceConnector implements ISourceConnector {

    @Override
    public Map<String, String> getSparkConf(Config config) {
        // TODO: Return the SparkConf related to your connector
        return Collections.emptyMap();
    }

    @Override
    public Dataset<Row> process(SparkSession spark, ConnectorContext ctx, Config config, BiConsumer<String, Long> metricFn) {
        // TODO: Add logic to read the data and return a dataframe
        return spark.emptyDataFrame();
    }
}
```

## Reference

* [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-spark/src/main/scala/org/sunbird/obsrv/connector/source/ISourceConnector.scala)&#x20;
{% endtab %}

{% tab title="Scala" %}
## Imports

```scala
package org.sunbird.obsrv.connector

import com.typesafe.config.Config
import org.apache.spark.sql.functions.{col, max}
import org.apache.spark.sql.{DataFrame, Dataset, Row, SparkSession}
import org.sunbird.obsrv.connector.model.Models.ConnectorContext
import org.sunbird.obsrv.connector.source.{ISourceConnector, SourceConnector}
```

## ISourceConnector

```scala
class ExampleSourceConnector extends ISourceConnector {

  override def getSparkConf(config: Config): Map[String, String] = {
    // TODO: Return the SparkConf related to your connector
    Map[String, String]()
  }

  override def process(spark: SparkSession, ctx: ConnectorContext, config: Config, metricFn: (String, Long) => Unit): Dataset[Row] = {
    // TODO: Add logic to read the data and return a dataframe
    spark.emptyDataFrame
  }
```

## Reference

* [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-spark/src/main/scala/org/sunbird/obsrv/connector/source/ISourceConnector.scala)&#x20;


{% endtab %}

{% tab title="Python" %}
## Imports

```python
from obsrv.common import ObsrvException
from obsrv.connector import ConnectorContext, MetricsCollector
from obsrv.connector.batch import ISourceConnector
from obsrv.job.batch import get_base_conf
from obsrv.models import ErrorData, StatusCode
from obsrv.utils import LoggerController
from pyspark.conf import SparkConf
from pyspark.sql import DataFrame, SparkSession
from pyspark.sql.functions import lit
```

## ISourceConnector

```python
class ExampleSource(ISourceConnector):
    def process(
        self,
        sc: SparkSession,
        ctx: ConnectorContext,
        connector_config: Dict[Any, Any],
        metrics_collector: MetricsCollector,
    ) -> Iterator[DataFrame]:
        # TODO: return or yield dataframe
        # yield sc.createDataFrame([], schema=None)
        return sc.createDataFrame([], schema=None)
        
    def get_spark_conf(self, connector_config) -> SparkConf:
        conf = get_base_conf()
        # TODO: Extend or Add the SparkConf related to your connector
        return conf

```

## Reference

* [https://github.com/Sunbird-Obsrv/obsrv-python-sdk](https://github.com/Sunbird-Obsrv/obsrv-python-sdk/blob/main/obsrv/connector/batch/source.py)


{% endtab %}
{% endtabs %}





