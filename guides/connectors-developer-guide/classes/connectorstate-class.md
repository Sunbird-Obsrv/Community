# ConnectorState Class

### Overview

The `ConnectorState` class is a part of the `org.sunbird.obsrv.connector.model` package. It encapsulates the state information for a connector instance, allowing for the tracking and management of various state attributes associated with the connector's lifecycle.

### Class Definition

Ref: [https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorState.scala](https://github.com/Sunbird-Obsrv/connector-sdk-scala/blob/main/connector-sdk-core/src/main/scala/org/sunbird/obsrv/connector/model/ConnectorState.scala)

### Args

#### `connectorInstanceId: String`

* **Description**: The unique identifier for the specific instance of the connector.

#### `stateJson: Option[String]`

* **Description**: The JSON representation of the state for the connector instance.

#### `state: mutable.Map[String, AnyRef]`

* **Description**: A mutable map that holds the state attributes for the connector instance.

### Methods

#### `getState[T](attribute: String): Option[T]`

* **Description**: Retrieves the value of the specified state attribute.
* **Parameters**: `attribute` - The name of the state attribute to retrieve.
* **Returns**: An `Option` containing the value of the state attribute, if it exists.

#### `getState[T](attribute: String, defaultValue: T): T`

* **Description**: Retrieves the value of the specified state attribute, or returns a default value if the attribute does not exist.
* **Parameters**:
  * `attribute` - The name of the state attribute to retrieve.
  * `defaultValue` - The default value to return if the attribute does not exist.
* **Returns**: The value of the state attribute, or the default value.

#### `putState[T <: AnyRef](attrib: String, value: T): Unit`

* **Description**: Adds or updates the value of the specified state attribute.
* **Parameters**:
  * `attrib` - The name of the state attribute to add or update.
  * `value` - The value to set for the state attribute.

#### `removeState(attrib: String): Option[AnyRef]`

* **Description**: Removes the specified state attribute from the state.
* **Parameters**: `attrib` - The name of the state attribute to remove.
* **Returns**: An `Option` containing the removed value, if it existed.

#### `contains(attrib: String): Boolean`

* **Description**: Checks if the specified state attribute exists in the state.
* **Parameters**: `attrib` - The name of the state attribute to check.
* **Returns**: `true` if the attribute exists, `false` otherwise.

#### `toJson(): String`

* **Description**: Serializes the state to a JSON string.
* **Returns**: A JSON string representation of the state.

#### `saveState(): Unit`

* **Description**: Saves the current state to the database.
* **Throws**: `ObsrvException` if the state could not be saved.

### Usage

The `ConnectorState` class is used to manage and track the state attributes of a connector instance. It provides methods to access, update, and persist these attributes.

#### Example

```scala
import org.sunbird.obsrv.connector.model.ConnectorState
import org.sunbird.obsrv.job.util.PostgresConnectionConfig

implicit val postgresConfig: PostgresConnectionConfig = // initialize config

val state = new ConnectorState("connectorInstanceId", None)

// Accessing and updating state
state.putState("attribute1", "value1".asInstanceOf[AnyRef])
println(state.getState[String]("attribute1"))
state.saveState()
```
