# MetricData Class

### Overview

The `MetricData` case class is a part of the `org.sunbird.obsrv.job.model.Models` package. It encapsulates metric information, including a map of metric names to their values and a list of labels associated with these metrics. This class is useful for representing and managing metrics data within the application.

### Class Definition

```scala
package org.sunbird.obsrv.job.model.Models

case class MetricData(
  metric: Map[String, Long],
  labels: List[Map[String, String]]
)
```

### Fields

#### `metric: Map[String, Long]`

* **Description**: A map where the keys are metric names and the values are the corresponding metric values.
* **Type**: `Map[String, Long]`

#### `labels: List[Map[String, String]]`

* **Description**: A list of maps, where each map represents a set of labels associated with the metrics.
* **Type**: `List[Map[String, String]]`

### Usage

The `MetricData` case class is used to encapsulate and manage metrics data, including the metric values and their associated labels. It provides a structured way to represent metrics in the application.

#### Example

```scala
import org.sunbird.obsrv.job.model.Models.MetricData

val metric = Map("metric1" -> 100L, "metric2" -> 200L)
val labels = List(
  Map("label1" -> "value1", "label2" -> "value2"),
  Map("label3" -> "value3", "label4" -> "value4")
)

val metricData = MetricData(metric, labels)

// Accessing metric data fields
println(s"Metrics: ${metricData.metric}")
println(s"Labels: ${metricData.labels}")
```

### JSON Representation

An instance of `MetricData` can be serialized to JSON as follows:

```json
{
  "metric": {
    "metric1": 100,
    "metric2": 200
  },
  "labels": [
    {
      "label1": "value1",
      "label2": "value2"
    },
    {
      "label3": "value3",
      "label4": "value4"
    }
  ]
}
```
