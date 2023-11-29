### <mark style="color:blue;">5.1.0</mark>


#### **Release Details**



| Phases                                             | Start Date                                                                                                         | End Date                                                                                                  |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Planning Phases**                                  | 01-AUG-2022 | 12-AUG-2022 |
| **Design Discussion**                                  | 15-AUG-2022 | 26-AUG-2022 |
| **Sprint 1**                                  | 29-AUG-2022 | 16-SEP-2022 |
| **Sprint 2**                                    | 19-SEP-2022 | 07-OCT-2022 |
| **Regression Testing & Releases**                                    | 10-OCT-2022 | 04-NOV-2022 |
| **Production Release**                                    | 04-NOV-2022 | 04-NOV-2022 |
| **Bug fixes and Support**                                    | 07-NOV-2022 | 11-NOV-2022 |


#### **Features**
**Sprint 1**
* Obsrv Infra single click installation in the local mode [#OB-27](https://project-sunbird.atlassian.net/browse/OB-27)
* CSP Migration plan analysis [#OB-45](https://project-sunbird.atlassian.net/browse/OB-45)

**Sprint 2**
* Moving of all the repos into the obsrv community and deployment script changes. [#OB-39](https://project-sunbird.atlassian.net/browse/OB-39)
* Obsrv infra single click installation bug fixes in the Kubernets cluster to setup the druid. [#OB-51](https://project-sunbird.atlassian.net/browse/OB-51)
* Obsrv Query Engine Deployment Script. [#OB-82](https://project-sunbird.atlassian.net/browse/OB-82)
* Obsrv Query Engine API Implementation [#OB-88](https://project-sunbird.atlassian.net/browse/OB-88)
* Merging of the release branches to main branch [#OB-244](https://project-sunbird.atlassian.net/browse/OB-244)
* Obsrv HdInsight Cluster CSP Variable generalisation changes [#OB-232](https://project-sunbird.atlassian.net/browse/OB-232)
* Obsrv Druid CSP Variable generalisation [#OB-226](https://project-sunbird.atlassian.net/browse/OB-226)
* Obsrv Secor Service CSP Variable Generalisation [#OB-220](https://project-sunbird.atlassian.net/browse/OB-220)
* Obsrv Report APIs CSP Variable Generalisation [#OB-214](https://project-sunbird.atlassian.net/browse/OB-214)
* Obsrv Pipeline CSP Variable Generalisation [#OB-208](https://project-sunbird.atlassian.net/browse/OB-208)
* Report API enhancement to generate the signed URL for the relative paths [#OB-202](https://project-sunbird.atlassian.net/browse/OB-202)
* Obsrv stand alone spark machine provision script CSP variable generalisation [#OB-238](https://project-sunbird.atlassian.net/browse/OB-238)

#### **Github Tag Details**
| Component                                             | Build Tag                                                                                                        | Deploy Tag                                                                                                 |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Analytics Service**                                  | [**release-5.1.0\_RC2**](https://github.com/Sunbird-Obsrv/sunbird-analytics-service/releases/tag/release-5.1.0_RC2) | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Spark Provision**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Spark HD Insights Cluster Provision**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Secor**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Flink Jobs**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Druid**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |
| **Sunbird Analytics Core**                                  | NA | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC1) |


### **Configurations**

| Service                                             | Old Configurations                                                                                                         | New Configurations                                                                                                  |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Analytics Service**                                  | azure_private_account_name, azure_private_account_secret, azure_public_account_secret, azure_public_account_name | cloud_private_storage_accountname, cloud_private_storage_secret, cloud_public_storage_secret, cloud_public_storage_accountname |
| **Spark Provision**                                  | sunbird_private_storage_account_name, sunbird_private_storage_account_key, sunbird_public_storage_account_name, sunbird_public_storage_account_key, s3_storage_key, s3_storage_secret, sunbird_private_azure_report_container_name, sunbird_public_azure_report_container_name, azure_private_storage_account_name, azure_private_storage_account_key  | cloud_private_storage_accountname, cloud_private_storage_secret, cloud_public_storage_accountname, cloud_public_storage_secret, cloud_storage_privatereports_bucketname, cloud_storage_publicreports_bucketname, cloud_private_storage_accountname, cloud_private_storage_secret |
| **Spark HD Insight Provision**                                  | sunbird_private_storage_account_name, sunbird_private_storage_account_key, | cloud_private_storage_accountname, cloud_private_storage_secret |
| **Secor**                                  | secor_azure_container_name, sunbird_private_storage_account_key, sunbird_private_storage_account_name, azure_container_name,  | cloud_storage_telemetry_bucketname, cloud_private_storage_secret, cloud_private_storage_accountname, cloud_storage_telemetry_bucketname |
| **Flink**                                  | sunbird_private_storage_account_name, sunbird_private_storage_account_key, checkpoint_store_type, sunbird_private_storage_account_name, sunbird_private_storage_account_key,   s3_access_key, s3_secret_key, s3_endpoint, s3_path_style_access| cloud_private_storage_accountname, cloud_private_storage_secret, cloud_service_provider, cloud_private_storage_endpoint, cloud_storage_pathstyle_access, cloud_private_storage_project |
| **Druid**                                  | sunbird_private_storage_account_name, sunbird_private_storage_account_key,sunbird_druid_storage_account_name, sunbird_druid_storage_account_key, druid_azure_container_name, s3_storage_key, s3_storage_secret, s3_storage_container, s3_storage_endpoint,s3_path_style_access, s3_default_bucket_location,  | cloud_private_storage_accountname, cloud_private_storage_secret, cloud_storage_telemetry_bucketname,  cloud_storage_pathstyle_access, cloud_private_storage_project, cloud_private_storage_endpoint,cloud_private_storage_region, cloud_storage_telemetry_type |
| **Sunbird Analytics Core**                                  | sunbird_private_storage_account_name, sunbird_private_storage_account_key, sunbird_public_storage_account_name, sunbird_public_storage_account_key | cloud_private_storage_accountname, cloud_private_storage_secret,  cloud_public_storage_accountname, cloud_public_storage_secret, cloud_storage_telemetry_type|








