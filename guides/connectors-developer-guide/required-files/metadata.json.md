# metadata.json

This file is used by Obsrv while registering and running your connector. Here are the details of the file

| Name           | Description                                                                                                                                                                                                                                                                                                           |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`         | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"connector"</code><br>Specifies the type of the configuration. Must always be <code>"connector"</code>.</p>                                                                                                                   |
| `metadata`     | <p><strong>Type</strong>: <code>object</code><br>Contains detailed metadata for the connector, including attributes such as <code>id</code>, <code>version</code>, <code>tenant</code>, and others.</p>                                                                                                               |
| `id`           | <p><strong>Type</strong>: <code>string</code><br>A unique identifier for the connector.</p>                                                                                                                                                                                                                           |
| `name`         | <p><strong>Type</strong>: <code>string</code><br>The name of the connector.</p>                                                                                                                                                                                                                                       |
| `version`      | <p><strong>Type</strong>: <code>string</code><br>The version of the connector.</p>                                                                                                                                                                                                                                    |
| `tenant`       | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"single"</code>, <code>"multiple"</code><br>Indicates whether the connector is for a single or multiple tenants.</p>                                                                                                          |
| `type`         | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"source"</code><br>Specifies the type of connector, currently restricted to <code>"source"</code>.</p>                                                                                                                        |
| `category`     | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"batch"</code>, <code>"stream"</code><br>The processing category of the connector.</p>                                                                                                                                        |
| `description`  | <p><strong>Type</strong>: <code>string</code><br>A textual description of the connector.</p>                                                                                                                                                                                                                          |
| `technology`   | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"java"</code>, <code>"scala"</code>, <code>"python"</code><br>The primary technology used by the connector.</p>                                                                                                               |
| `runtime`      | <p><strong>Type</strong>: <code>string</code><br><strong>Allowed Values</strong>: <code>"spark"</code>, <code>"flink"</code><br>The runtime environment for the connector.<br><br>If category is <code>batch</code>, runtime should be <code>spark</code>; if <code>stream</code> it should be <code>flink</code></p> |
| `licence`      | <p><strong>Type</strong>: <code>string</code><br>Specifies the licence type of the connector.</p>                                                                                                                                                                                                                     |
| `owner`        | <p><strong>Type</strong>: <code>string</code><br>The owner or maintainer of the connector.</p>                                                                                                                                                                                                                        |
| `main_class`   | <p><strong>Type</strong>: <code>string</code><br>Specifies the main class of the program. Required for <code>java</code> or <code>scala</code> technologies, optional for <code>python</code>.</p>                                                                                                                    |
| `main_program` | <p><strong>Type</strong>: <code>string</code><br>Path to the main program of the connector.</p>                                                                                                                                                                                                                       |
| `icon`         | <p><strong>Type</strong>: <code>string</code> or <code>null</code><br>Path or URL for the icon representing the connector. Can be <code>null</code> if no icon is provided.</p>                                                                                                                                       |
| `connectors`   | <p><strong>Type</strong>: <code>array</code><br>A list of connectors associated with the configuration. Each item includes attributes like <code>id</code>, <code>name</code>, <code>description</code>, and <code>icon</code>.</p>                                                                                   |

Here is a sample `metadata.json` file for your reference

```json
{
  "type": "connector",
  "metadata": {
    "id": "example-connector",
    "name": "Example Connector",
    "description": "Pull data from a Source",
    "type": "source",
    "tenant": "single",
    "version": "1.0.0",
    "category": "stream",
    "technology": "scala",
    "runtime": "flink",
    "licence": "MIT",
    "owner": "Sunbird",
    "main_class": "org.sunbird.obsrv.connector.ExampleConnector",
    "main_program": "example-connector-1.0.0.jar",
    "icon": "icon.svg"
  }
}
```

Here is the JSON Schema to validate your `metadata.json`

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "type": {
      "type": "string",
      "enum": ["connector"]
    },
    "metadata": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "name": {
          "type": "string"
        },
        "version": {
          "type": "string"
        },
        "tenant": {
          "type": "string",
          "enum": ["single", "multiple"]
        },
        "type": {
          "type": "string",
          "enum": ["source"]
        },
        "category": {
          "type": "string",
          "enum": ["batch", "stream"]
        },
        "description": {
          "type": "string"
        },
        "technology": {
          "type": "string",
          "enum": ["java", "scala", "python"]
        },
        "runtime": {
          "type": "string",
          "enum": ["spark", "flink"]
        },
        "licence": {
          "type": "string"
        },
        "owner": {
          "type": "string"
        },
        "main_class": {
          "type": "string"
        },
        "main_program": {
          "type": "string"
        }
      },
      "required": [
        "id",
        "version",
        "tenant",
        "type",
        "category",
        "technology",
        "runtime",
        "licence",
        "owner",
        "main_program"
      ]
    },
    "connectors": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "icon": {
            "type": ["null", "string"]
          }
        },
        "required": [
          "id",
          "name",
          "description",
          "icon"
        ]
      }
    }
  },
  "required": [
    "type",
    "metadata"
  ],
  "dependentSchemas": {
    "metadata": {
      "allOf": [
        {
          "anyOf": [
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "tenant": {
                      "enum": ["single"]
                    }
                  },
                  "required": [
                    "id",
                    "description",
                    "version",
                    "tenant",
                    "type",
                    "category",
                    "technology",
                    "runtime",
                    "licence",
                    "owner",
                    "icon",
                    "main_program"
                  ]
                }
              },
              "not": {
                "required": ["connectors"]
              }
            },
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "tenant": {
                      "enum": ["multiple"]
                    }
                  },
                  "required": [
                    "id",
                    "name",
                    "version",
                    "tenant",
                    "type",
                    "category",
                    "technology",
                    "runtime",
                    "licence",
                    "owner",
                    "main_program"
                  ],
                  "not": {
                    "required": ["description"]
                  }
                },
                "connectors": {
                  "type": "array"
                }
              },
              "required": ["connectors"]
            }    
          ]
        },
        {
          "anyOf": [
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "technology": {
                      "enum": ["python"]
                    }
                  },
                  "not": {
                     "required": ["main_class"]
                  }
                }
              }
            },
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "technology": {
                      "enum": ["java", "scala"]
                    }
                  },
                  "required": ["main_class"]
                }
              }
            }
          ]
        },
        {
          "oneOf": [
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "runtime": {
                      "enum": ["flink"]
                    },
                    "technology": {
                      "not": {
                        "enum": ["python"]
                      }
                    }
                  }
                }
              }
            },
            {
              "properties": {
                "metadata": {
                  "properties": {
                    "runtime": {
                      "enum": ["spark"]
                    },
                    "technology": {
                      "enum": ["python", "java", "scala"]
                    }
                  }
                }
              }
            }
          ]
        }
      ]
    }
  }
}
```
