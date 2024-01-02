### <mark style="color:blue;">5.1.3 (Hot Fix)</mark>


#### **Release Details**

#### **Features**
**Sprint 1**
* CSP Refactor [#OB-525](https://project-sunbird.atlassian.net/browse/OB-525)

#### **Github Tag Details**
| Component                                             | Build Tag                                                                                                        | Deploy Tag                                                                                                 |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Analytics Service**                                  | [**release-5.1.3_RC1**](https://github.com/Sunbird-Obsrv/sunbird-analytics-service/releases/tag/release-5.1.3_RC1) | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |
| **Spark Provision**                                  | NA | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |
| **Analytics Core**                                  | [**release-5.1.3_RC2**](https://github.com/Sunbird-Obsrv/sunbird-analytics-core/releases/tag/release-5.1.3_RC2) | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |
| **Core Data Products**                                  | [**release-5.1.3_RC1**](https://github.com/Sunbird-Obsrv/sunbird-core-dataproducts/releases/tag/release-5.1.3_RC1) | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |
| **Secor**                                  | NA | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |
| **Flink Jobs**                                  | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) | [**release-5.2.0_RC3**](https://github.com/Sunbird-Obsrv/sunbird-data-pipeline/releases/tag/release-5.2.0_RC3) |

### **Build Changes**

1. **Analytics Core Build Command** 
> mvn clean install -DskipTests -DCLOUD_STORE_GROUP_ID=org.sunbird -DCLOUD_STORE_ARTIFACT_ID=cloud-store-sdk_2.12 -DCLOUD_STORE_VERSION=1.4.6

2. **Analytics Core Data Products Build Command** 
> mvn clean install -DskipTests -DCLOUD_STORE_GROUP_ID=org.sunbird -DCLOUD_STORE_ARTIFACT_ID=cloud-store-sdk_2.12 -DCLOUD_STORE_VERSION=1.4.6

3. **Analytics Service Build Command** 
> mvn clean install -DskipTests -DCLOUD_STORE_GROUP_ID=org.sunbird -DCLOUD_STORE_ARTIFACT_ID=cloud-store-sdk_2.12 -DCLOUD_STORE_VERSION=1.4.6










