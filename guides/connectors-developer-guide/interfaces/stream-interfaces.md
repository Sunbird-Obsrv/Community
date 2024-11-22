# Stream Interfaces

The SDK's expose an interface that has to be extended inorder to build a connector. A sample is shown below



{% tabs %}
{% tab title="Java" %}
## Imports

```java
package org.sunbird.obsrv.connector;

import com.typesafe.config.Config;
import org.apache.flink.streaming.api.datastream.SingleOutputStreamOperator;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;

import org.sunbird.obsrv.connector.model.Models;
import org.sunbird.obsrv.connector.source.IConnectorSource;
import org.sunbird.obsrv.connector.source.SourceConnectorFunction;
import org.sunbird.obsrv.job.exception.UnsupportedDataFormatException;

import java.util.List;
```

## SourceConnectorFunction

```java
public class ExampleSourceFunction extends SourceConnectorFunction {
    public ExampleSourceFunction(List<Models.ConnectorContext> connectorContexts) {
        super(connectorContexts);
    }

    @Override
    public void processEvent(
        String event, 
        Function1<String, BoxedUnit> onSuccess, 
        Function2<String, org.sunbird.obsrv.job.model.Models.ErrorData, BoxedUnit> onFailure, 
        Function2<String, Object, BoxedUnit> incMetric
    ){
        // TODO: Implement this method to process the event
        // Call onSuccess.apply(event) if the event is processed successfully
        // Call onFailure.apply(event, errorData) if the event processing fails
        // Call incMetric.apply(event, metricData) to increment the metric
    }

    @Override
    public List<String> getMetrics() {
        // TODO: Return the list of metrics
        return List.empty();
    }
}
```

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-flink/src/main/scala/org/sunbird/obsrv/connector/source/SourceConnectorFunction.scala#L10)

## IConnectorSource Class

```java
public class ExampleSourceConnector extends IConnectorSource {
    @Override
    public SingleOutputStreamOperator<String> getSourceStream(
        StreamExecutionEnvironment env, Config config
    ) throws UnsupportedDataFormatException {
        // TODO: Implement this method to return the source stream
        // env.fromSource(...)
    }

    @Override
    public SourceConnectorFunction getSourceFunction(
        List<Models.ConnectorContext> contexts, Config config) 
    {
        return ExampleSourceFunction(contexts)
    }
}
```

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-flink/src/main/scala/org/sunbird/obsrv/connector/source/IConnectorSource.scala)


{% endtab %}

{% tab title="Scala" %}
## Imports

```scala
package org.sunbird.obsrv.connector

import com.typesafe.config.Config
import org.apache.flink.api.common.serialization.SimpleStringSchema
import org.apache.flink.streaming.api.datastream.SingleOutputStreamOperator
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment
import org.json.{JSONException, JSONObject}
import org.sunbird.obsrv.connector.model.Models
import org.sunbird.obsrv.connector.source.{IConnectorSource, SourceConnector, SourceConnectorFunction}
import org.sunbird.obsrv.job.exception.UnsupportedDataFormatException
import org.sunbird.obsrv.job.model.Models.ErrorData
```

## SourceConnectorFunction

```scala

class ExampleSourceConnectorFunction(connectorContexts: List[ConnectorContext]) extends SourceConnectorFunction(connectorContexts) {

  /**
   * This method processes the incoming event.
   *
   * @param event The event to be processed.
   * @param onSuccess Callback function to be called on successful processing of the event.
   * @param onFailure Callback function to be called on failure in processing the event.
   * @param incMetric Function to increment the metric counter.
   */
  override def processEvent(event: String, 
                            onSuccess: String => Unit, 
                            onFailure: (String, ErrorData) => Unit, 
                            incMetric: (String, Long) => Unit): Unit = {
    // Implement your event processing logic here.
  }
  
  // TODO: Returns a list of custom metrics if any
  override def getMetrics(): List[String] = List[String]()
}
```

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-flink/src/main/scala/org/sunbird/obsrv/connector/source/SourceConnectorFunction.scala#L10)

## IConnectorSource

```scala
class ExampleConnectorSource extends IConnectorSource {

  @throws[UnsupportedDataFormatException]
  override def getSourceStream(env: StreamExecutionEnvironment, config: Config): SingleOutputStreamOperator[String] = {
    // Implement the logic to create and return the source stream
    // Example:
    // env.fromElements("event1", "event2", "event3")
  }

  override def getSourceFunction(contexts: List[ConnectorContext], config: Config): SourceConnectorFunction = {
    new ExampleSourceConnectorFunction(contexts)
  }
}
```

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-flink/src/main/scala/org/sunbird/obsrv/connector/source/IConnectorSource.scala)


{% endtab %}
{% endtabs %}

















