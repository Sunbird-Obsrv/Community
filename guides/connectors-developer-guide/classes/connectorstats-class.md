# ConnectorStats Class

## ConnectorStats

### Overview

The `ConnectorStats` class is a part of the `org.sunbird.obsrv.connector.model` package. It encapsulates the statistics information for a connector instance, allowing for the tracking and management of various metrics associated with the connector's performance.

### Class Definition

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorStats.scala](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorStats.scala)

### Arguments

#### `connectorInstanceId: String`

* **Description**: The unique identifier for the specific instance of the connector.

#### `statsJson: Option[String]`

* **Description**: The JSON representation of the statistics for the connector instance.

#### `stats: mutable.Map[String, AnyRef]`

* **Description**: A mutable map that holds the statistics metrics for the connector instance.

### Methods

#### `getStat[T](metric: String): Option[T]`

* **Description**: Retrieves the value of the specified metric.
* **Parameters**: `metric` - The name of the metric to retrieve.
* **Returns**: An `Option` containing the value of the metric, if it exists.

#### `getStat[T](metric: String, defaultValue: T): T`

* **Description**: Retrieves the value of the specified metric, or returns a default value if the metric does not exist.
* **Parameters**:
  * `metric` - The name of the metric to retrieve.
  * `defaultValue` - The default value to return if the metric does not exist.
* **Returns**: The value of the metric, or the default value.

#### `putStat[T <: AnyRef](metric: String, value: T): Unit`

* **Description**: Adds or updates the value of the specified metric.
* **Parameters**:
  * `metric` - The name of the metric to add or update.
  * `value` - The value to set for the metric.

#### `removeStat(metric: String): Option[AnyRef]`

* **Description**: Removes the specified metric from the statistics.
* **Parameters**: `metric` - The name of the metric to remove.
* **Returns**: An `Option` containing the removed value, if it existed.

#### `toJson(): String`

* **Description**: Serializes the statistics to a JSON string.
* **Returns**: A JSON string representation of the statistics.

#### `saveStats(): Unit`

* **Description**: Saves the current statistics to the database.
* **Throws**: `ObsrvException` if the statistics could not be saved.

### Usage

The `ConnectorStats` class is used to manage and track the performance metrics of a connector instance. It provides methods to access, update, and persist these metrics.

#### Example

```scala
import org.sunbird.obsrv.connector.model.ConnectorStats
import org.sunbird.obsrv.job.util.PostgresConnectionConfig

implicit val postgresConfig: PostgresConnectionConfig = // initialize config

val stats = new ConnectorStats("connectorInstanceId", None)

// Accessing and updating stats
stats.putStat("metric1", 100.asInstanceOf[AnyRef])
println(stats.getStat[Int]("metric1"))
stats.saveStats()
```
