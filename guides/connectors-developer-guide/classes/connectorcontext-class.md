# ConnectorContext Class

## ConnectorContext

The [ConnectorContext](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/Models.scala) class is a part of the `org.sunbird.obsrv.connector.model` package. It encapsulates the context information for a connector instance, including its configuration, state, and statistics. This class is essential for managing the lifecycle and execution of connector instances within the Obsrv platform.

### Class Definition

```scala
package org.sunbird.obsrv.connector.model

import com.fasterxml.jackson.annotation.{JsonIgnore, JsonProperty}
import org.sunbird.obsrv.job.model.Models.ErrorData

object Models {

  case class ConnectorContext(
     @JsonProperty("connector_id") connectorId: String,
     @JsonProperty("dataset_id") datasetId: String,
     @JsonProperty("connector_instance_id") connectorInstanceId: String,
     @JsonProperty("connector_type") connectorType: String,
     @JsonIgnore entryTopic: String,
     @JsonIgnore state: ConnectorState,
     @JsonIgnore stats: ConnectorStats
   )
}
```

### Fields

#### `connectorId: String`

* **Description**: The unique identifier for the connector.
* **Annotations**: `@JsonProperty("connector_id")`

#### `datasetId: String`

* **Description**: The unique identifier for the dataset associated with the connector.
* **Annotations**: `@JsonProperty("dataset_id")`

#### `connectorInstanceId: String`

* **Description**: The unique identifier for the specific instance of the connector.
* **Annotations**: `@JsonProperty("connector_instance_id")`

#### `connectorType: String`

* **Description**: The type of the connector (e.g., source, sink).
* **Annotations**: `@JsonProperty("connector_type")`

#### `entryTopic: String`

* **Description**: The entry topic for the connector. This field is ignored during JSON serialization.
* **Annotations**: `@JsonIgnore`

#### [state: ConnectorState](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorState.scala)

* **Description**: The state of the connector instance, encapsulated in a [ConnectorState](https://vscode-file/vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) object. This field is ignored during JSON serialization.
* **Annotations**: `@JsonIgnore`

#### [stats: ConnectorStats](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorStats.scala)

* **Description**: The statistics of the connector instance, encapsulated in a [ConnectorStats](https://vscode-file/vscode-app/Applications/Visual%20Studio%20Code.app/Contents/Resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) object. This field is ignored during JSON serialization.
* **Annotations**: `@JsonIgnore`

### Usage

The ConnectorContext class is used to manage and track the state and statistics of a connector instance. It provides a structured way to access and manipulate the context information required for the execution of connectors.

#### Example

```scala
import org.sunbird.obsrv.connector.model.Models.ConnectorContext
import org.sunbird.obsrv.connector.model.{ConnectorState, ConnectorStats}
import org.sunbird.obsrv.job.util.PostgresConnectionConfig

implicit val postgresConfig: PostgresConnectionConfig = // initialize config

val state = new ConnectorState("connectorInstanceId", None)
val stats = new ConnectorStats("connectorInstanceId", None)

val context = ConnectorContext(
  connectorId = "connectorId",
  datasetId = "datasetId",
  connectorInstanceId = "connectorInstanceId",
  connectorType = "source",
  entryTopic = "entryTopic",
  state = state,
  stats = stats
)

// Accessing context fields
println(context.connectorId)
println(context.datasetId)
```

### See Also

* [ConnectorState](connectorstate-class.md)
* [ConnectorStats](connectorstats-class.md)
