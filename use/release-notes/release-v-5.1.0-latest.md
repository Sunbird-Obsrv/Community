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
* Obsrv Query Engine API Implementation [#OB-51](https://project-sunbird.atlassian.net/browse/OB-88)


#### **Github Tag Details**
| Component                                             | Build Tag                                                                                                        | Deploy Tag                                                                                                 |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Analytics Service**                                  | [**release-5.1.0\_RC1**](https://github.com/Sunbird-Obsrv/sunbird-analytics-service/releases/tag/release-5.1.0_RC1) | [**release-5.1.0\_RC1**](https://github.com/project-sunbird/sunbird-devops/releases/tag/release-5.1.0_RC3) |


### **Deprecated variables**
* azure_private_account_secret
* azure_private_account_name
* azure_public_account_secret
* azure_public_account_name

### **Configurations**

| Service                                             | Old Configurations                                                                                                         | New Configurations                                                                                                  |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |------------------------------------------------------------------------------------------------------------|
| **Analytics Service**                                  | azure_private_account_name, azure_private_account_secret, azure_public_account_secret, azure_public_account_name | cloud_private_account_secret, cloud_private_account_name, cloud_public_account_secret, cloud_public_account_name |




