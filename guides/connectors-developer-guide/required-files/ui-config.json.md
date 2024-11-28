---
description: >-
  This page provides a comprehensive guide for developers on how to create and
  structure ui-config.json files used for auto-generating UIs for connectors.
---

# ui-config.json

### General Overview

1. **JSON Schema Standard**:
   * The file follows the **JSON Schema** standard (`type`, `properties`, `required`, etc.).
   * Developers should ensure compatibility with standard JSON Schema parsers for validation purposes.
2. **Custom Fields**:
   * `helptext`: A custom field providing detailed guidance that appears when a user focuses on a field.
   * `uiIndex`: Specifies the display order of fields in the UI.
3. **Flat Structure**: Ensure all fields are at the top level. Nested objects are not allowed.
4. **Key Attributes**:
   * `description`: Provides subtext for the input field.
   * `helptext`: Provides detailed guidance when the user focuses on the field.
   * `format`: Extended to include:
     * `hidden`: For fields with non-editable default values.
     * `password`: For sensitive inputs to hide entered text.
5. **Field Ordering**: Use the `uiIndex` attribute to dictate the order of fields in the UI.

***

### Core Sections in the `ui-config.json`

#### **1. Metadata**

* `title`: Title displayed in the UI.
* `description`: Brief summary of the connector setup.
* `helptext`: General instructions for the user.

```json
{
  "title": "Kafka Connector Setup Instructions",
  "description": "Configure Kafka Connector",
  "helptext": "Follow the below instructions to populate the required inputs needed for the connector correctly."
}
```

#### **2. Properties**

Each property represents a field in the UI. Define its type, validation rules, and additional UI hints.

**Example Field: Kafka Brokers**

```json
{
  "title": "Kafka Brokers",
  "type": "string",
  "description": "Enter Kafka broker addresses in the format: broker1-hostname:port,broker2-hostname:port",
  "helptext": "<p><strong>Kafka Broker Address Format:</strong> Enter the broker addresses in the following format:<code>&lt;broker1-hostname&gt;:&lt;port&gt;,&lt;broker2-hostname&gt;:&lt;port&gt;</code></p><p><em>Example:</em> <code>broker1.example.com:9092,broker2.example.com:9092</code></p>",
  "uiIndex": 1
}
```

#### **Field Attributes**

* **`type`**: Data type (e.g., `string`, `enum`).
* **`description`**: Short subtext visible below the field.
* **`helptext`**: Rich-text or HTML for focus-specific guidance.
* **`pattern`**: Regex for input validation.
* **`default`**: Default value, if any.
* **`enum`**: Allowed values for dropdowns or similar fields.
* **`format`**: Used for `hidden` or `password` to modify input behavior.

***

### Example Fields

Below are sample configurations for common Kafka connector fields:

1. **Kafka Brokers** (Required)
   * User inputs Kafka broker addresses.
   * Validation ensures correct format.
2. **Kafka Topic** (Required)
   * Alphanumeric with dots, dashes, or underscores.
   * Clear helptext and example.
3. **Kafka Auto Offset Reset** (Optional)
   * Dropdown with predefined values.
4. **Kafka Consumer Group ID** (Required)
   * Alphanumeric name identifying the consumer group.
5. **Data Format** (Hidden Default)
   * Predefined formats like `json`, `csv`, `parquet`.

***

### Required Fields

Specify the list of fields mandatory for the configuration:

```json
"required": [
  "source_kafka_broker_servers",
  "source_kafka_topic",
  "source_kafka_consumer_id",
  "source_kafka_auto_offset_reset",
  "source_data_format"
]
```

***

### Best Practices

1. **Descriptive Text**:
   * Ensure `description` and `helptext` are clear and concise.
   * Use examples where appropriate.
2. **UI Experience**:
   * Use `uiIndex` for logical field order.
   * Leverage `hidden` for technical defaults and `password` for secure inputs.
3. **Validation**:
   * Use `pattern` for format enforcement.
   * Provide feedback for invalid inputs.

***

### Example JSON

Here’s a full example for a Kafka connector:

```json
{
  "title": "Kafka Connector Setup Instructions",
  "description": "Configure Kafka Connector",
  "helptext": "Follow the instructions to configure the Kafka connector.",
  "type": "object",
  "properties": {
    "source_kafka_broker_servers": {
      "title": "Kafka Brokers",
      "type": "string",
      "description": "Enter Kafka broker addresses.",
      "helptext": "<p>Format: <code>broker1:port,broker2:port</code></p>",
      "uiIndex": 1
    },
    "source_kafka_topic": {
      "title": "Kafka Topic",
      "type": "string",
      "pattern": "^[a-zA-Z0-9\\\\._\\\\-]+$",
      "description": "Kafka topic name.",
      "helptext": "<p>Allowed characters: A-Z, 0-9, ., -, _</p>",
      "uiIndex": 2
    },
    "source_kafka_auto_offset_reset": {
      "title": "Kafka Auto Offset Reset",
      "type": "string",
      "enum": ["earliest", "latest", "none"],
      "default": "earliest",
      "description": "Auto offset reset.",
      "helptext": "Start reading from earliest, latest, or none.",
      "uiIndex": 3
    },
    "source_data_format": {
      "title": "Data Format",
      "type": "string",
      "enum": ["json", "csv"],
      "default": "json",
      "format": "hidden",
      "description": "Default format is JSON.",
      "uiIndex": 4
    }
  },
  "required": ["source_kafka_broker_servers", "source_kafka_topic"]
}
```

***

### Structure for Multi-Tenant Configurations

A multi-tenant connector's `ui-config.json` organizes configurations under source-specific keys. Each key contains the UI configuration specific to that source, using the same schema as single-source connectors.

**Example Structure**

Using object store connectors ui-config.json file:&#x20;

```json
{
  "aws-s3": {
    "title": "AWS S3 Connector Setup",
    "description": "Configure AWS S3 for the connector",
    "helptext": "Enter details specific to AWS S3, such as bucket name and region.",
    "type": "object",
    "properties": {
      "s3_bucket": {
        "title": "S3 Bucket Name",
        "type": "string",
        "description": "Enter the name of the S3 bucket.",
        "helptext": "Specify the bucket name exactly as it appears in your AWS S3 console.",
        "uiIndex": 1
      },
      "s3_region": {
        "title": "S3 Region",
        "type": "string",
        "description": "Enter the AWS region of the S3 bucket.",
        "helptext": "Example: us-west-2",
        "uiIndex": 2
      },
      "s3_access_key": {
        "title": "Access Key",
        "type": "string",
        "description": "Enter your AWS Access Key ID.",
        "helptext": "This key is used to authenticate access to AWS S3.",
        "format": "password",
        "uiIndex": 3
      },
      "s3_secret_key": {
        "title": "Secret Key",
        "type": "string",
        "description": "Enter your AWS Secret Access Key.",
        "helptext": "This key is used to authenticate access to AWS S3.",
        "format": "password",
        "uiIndex": 4
      }
    },
    "required": ["s3_bucket", "s3_region", "s3_access_key", "s3_secret_key"]
  },
  "azure-blob": {
    "title": "Azure Blob Storage Setup",
    "description": "Configure Azure Blob Storage for the connector",
    "helptext": "Enter details specific to Azure Blob Storage, such as container name and connection string.",
    "type": "object",
    "properties": {
      "blob_container": {
        "title": "Container Name",
        "type": "string",
        "description": "Enter the Azure Blob container name.",
        "helptext": "Specify the container name exactly as it appears in your Azure Storage account.",
        "uiIndex": 1
      },
      "blob_connection_string": {
        "title": "Connection String",
        "type": "string",
        "description": "Enter your Azure Blob connection string.",
        "helptext": "Retrieve this from your Azure Portal under the storage account settings.",
        "format": "password",
        "uiIndex": 2
      }
    },
    "required": ["blob_container", "blob_connection_string"]
  }
}
```

***

### Guidelines for Multi-Tenant Connectors

1. **Source-Specific Keys**:
   * Use keys like to represent each source. For ex: an object store connector pulling data from multiple storage types can use the keys `aws-s3`, `azure-blob`, or `gcp-storage`
   * Each key encapsulates the configuration for that specific source type.
2. **Consistent Schema**:
   * The structure within each key follows the same JSON Schema standard as single-source connectors.
   * This ensures consistent validation and UI generation.
3. **UI Differentiation**:
   * Fields, help text, and validation can vary by source to accommodate source-specific requirements.
4. **Dynamic Selection**:
   * The UI can dynamically display the relevant configuration based on the source type selected by the user.

***

#### Best Practices for Multi-Tenant Configurations

1. **Clearly Defined Source Keys**:
   * Use meaningful and consistent source identifiers (e.g., `aws-s3`, `azure-blob`).
2. **Modular Design**:
   * Treat each source configuration as an independent module for easy updates and reusability.
3. **Dynamic UI**:
   * Leverage UI logic to dynamically display fields based on the selected `source_type`.
4. **Validation**:
   * Ensure each source configuration has clear validation rules and `required` fields.

