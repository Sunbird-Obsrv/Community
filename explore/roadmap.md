
---


**Description**: A comprehensive overview of the features released, in-progress, and upcoming in Obsrv.

## **Completed Features (1.2.0-RC)**

| **Feature**                    | **Description**                                                                                                                                                                                                                                             | **Status**         | **Release**  |
|---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------|--------------|
| 📦 **Connector Framework**         | - Add and manage connectors via APIs<br>- Create and drop streams (Flik) or batch jobs (Spark) via APIs<br>- Add and manage custom jobs via APIs<br>- **Enhanced stability** with rigorous testing and fixes for key issues<br>- Open-source connectors for **Kafka**, **JDBC**, and **Object Store** | ✅ **Completed**      | **1.2.0-RC** |
| 🔌 **Open-Source Connectors**      | - Supported connectors:<br>&nbsp;&nbsp;&nbsp;• **Kafka**<br>&nbsp;&nbsp;&nbsp;• **JDBC**<br>&nbsp;&nbsp;&nbsp;• **Object Store**                                                                                                                           | ✅ **Completed**      | **1.2.0-RC** |
| 🏞️ **Lakehouse**                   | - Transactional Data Lake Platform for scalable and reliable data processing and storage                                                                                                                                                                      | ✅ **Completed**      | **1.2.0-RC** |
| ⚙️ **Automation Refactor**         | - Stabilized scripts for **greater reliability** and ease of use<br>- Support for **AWS**, **GCP**, **Azure**, and on-premises environments<br>- Streamlined installation for seamless deployments across any setup                                          | ✅ **Completed**      | **1.2.0-RC** |
| 📊 **Dataset Management**          | - Comprehensive dataset management with advanced features:<br>&nbsp;&nbsp;&nbsp;• Automatic schema evolution at processing/storage layers<br>&nbsp;&nbsp;&nbsp;• Seamless import/export<br>&nbsp;&nbsp;&nbsp;• Auto schema generation and indexing<br>&nbsp;&nbsp;&nbsp;• Proactive alerts and monitoring<br>&nbsp;&nbsp;&nbsp;• Masking and encryption<br>&nbsp;&nbsp;&nbsp;• JSONata and SQL transformations<br>&nbsp;&nbsp;&nbsp;• Data exhausts<br>&nbsp;&nbsp;&nbsp;• Data aliases for simplified replay and migration without downtime | ✅ **Completed**      | **1.2.0-RC** |
| 🛡️ **RBAC**                        | - Manage users and roles via APIs for robust role-based access control                                                                                                                                                                                         | ✅ **Completed**      | **1.2.0-RC** |
| 📡 **Obsrv Exporter**              | - Export OpenTelemetry-compliant monitoring data for seamless integration with external monitoring systems                                                                                                                                                    | 🔄 **Partially Completed** | **1.2.0-RC** |
| 🖥️ **Obsrv Management Console**    | - Full-featured **Obsrv Management Console** for managing datasets and connectors<br>- Effortless **dataset lifecycle management** (Draft → Ready for Publish → Published → Retired)<br>- **Source Connector Configuration** for **Kafka**, **JDBC**, **Object Store**<br>- Seamless **Export/Import** functionality<br>- Automatic **Schema Generation & Indexing**<br>- Proactive **Alerts & Monitoring** for dataset health<br>- **Resource Monitoring** for system performance | ✅ **Completed**      | **1.2.0-RC** |
| 📝 **Query APIs**                  | - **Query from Data Sources**: Query from multiple data sources such as **Druid**, **Hudi**, **Lakehouse**, and others.<br>- **Exhaust API**: API for retrieving data exhausts from blob stores for reporting and analysis.<br>- **Template API**: API for creating and using query templates, enabling reusable and efficient queries across different datasets and environments. | ✅ **Completed**     | **1.2.0-RC** |

---

## **Upcoming Features**

| **Feature**                      | **Description**                                                                                     | **Status**        | **Release** |
|-----------------------------------|-----------------------------------------------------------------------------------------------------|-------------------|-------------|
| ⚙️ **Stabilization Enhancements**    | - Improve automation scripts for **greater reliability** and ease of use.                                                                                             | ⏳ **Planned**       | **Future**  |
| 🔒 **Security & Performance Upgrades** | - Software updates for critical components like **Druid**, **Flink**, and **Kubernetes**.                                                           | ⏳ **Planned**       | **Future**  |
| 🖥️ **User Experience Improvements**  | - Enhanced management console for a better user experience, simplifying workflows for dataset and connector management. | ⏳ **Planned**       | **Future**  |
| 🔗 **Connector Framework Stabilization** | - Optimization and stabilization of the connector framework and its supported connectors.                                                             | ⏳ **Planned**       | **Future**  |

---