# Required Files

The SDK expects the following files to be as part of the source distribution:

* [**metadata.json**](metadata.json.md): This file is used mainly for registering a connector with the Obsrv system.
* [**ui-config.json**](ui-config.json.md): This JSON configuration schema is used to define the data that the user interface (UI) will collect from the user to configure the connector.
* [**metrics.yaml**](metrics.yaml.md): This YAML configuration is used to define metrics for monitoring and reporting purposes in the  system.
* [**alerts.yaml**](alerts.yaml.md): This file contains the alert configuration, which will be converted into a Prometheus expression used to create the alert.

