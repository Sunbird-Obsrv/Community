# ErrorData Class

### Overview

The `ErrorData` case class is a part of the `org.sunbird.obsrv.job.model.Models` package. It encapsulates error information, including an error code and an error message, which can be used to provide detailed error reporting and handling within the application.

### Class Definition

```scala
package org.sunbird.obsrv.job.model.Models

import com.fasterxml.jackson.annotation.JsonProperty

case class ErrorData(
  @JsonProperty("error_code") errorCode: String,
  @JsonProperty("error_msg") errorMsg: String
)
```

### Fields

#### `errorCode: String`

* **Description**: The unique code representing the specific error.
* **Annotations**: `@JsonProperty("error_code")`

#### `errorMsg: String`

* **Description**: A descriptive message providing details about the error.
* **Annotations**: `@JsonProperty("error_msg")`

### Usage

The `ErrorData` case class is used to encapsulate error information that can be serialized and deserialized to and from JSON. It provides a structured way to represent errors in the application.

#### Example

```scala
import org.sunbird.obsrv.job.model.Models.ErrorData

val error = ErrorData(
  errorCode = "404",
  errorMsg = "Resource not found"
)

// Accessing error fields
println(s"Error Code: ${error.errorCode}")
println(s"Error Message: ${error.errorMsg}")
```

### JSON Representation

An instance of `ErrorData` can be serialized to JSON as follows:

```json
{
  "error_code": "404",
  "error_msg": "Resource not found"
}
```



