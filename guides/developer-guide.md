---
description: Guide to setup and run in a developer machine
---

# Developer Guide

### Introduction: <a href="#id-5zntod7zxfl6" id="id-5zntod7zxfl6"></a>

In this document, we'll explore how to fork, clone, build, and install Obsrv from these GitHub repositories. Obsrv uses GitHub repositories as they are versatile tools for managing and sharing code, documentation, and other resources efficiently.

### Prerequisites: <a href="#lwdfmye9jg68" id="lwdfmye9jg68"></a>

Before we begin, ensure you have the following:

* A GitHub account
* Basic knowledge of Git and GitHub concepts.
  * Fork the Repository - [reference doc](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)
  * Clone the Repository - [reference doc](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
* IDE for development. Suggested - Intellij idea. Installation reference doc can be found under [IntelliJ](https://www.jetbrains.com/help/idea/installation-guide.html)
  * Open the Project - [reference doc](https://www.jetbrains.com/guide/java/tutorials/import-project/open-project/)
  * Build & Run
* Docker account & Docker desktop application - [reference doc](https://docs.docker.com/desktop/)
* Cloud provider account. Currently Obsrv supports - AWS, AZURE & GCP.
* Specific details about each repository are listed under the repository section.

### Obsrv GitHub repositories: <a href="#at5woe3fkmsh" id="at5woe3fkmsh"></a>

#### **obsrv-core:**

**Repository:** [https://github.com/Sunbird-Obsrv/obsrv-core](https://github.com/Sunbird-Obsrv/obsrv-core)

**Introduction:**

Obsrv-core is a framework consisting of Flink jobs designed to handle data extraction and processing tasks efficiently. It provides a flexible and customizable pipeline for various data-related operations. These jobs have been designed to process, enrich, and validate data from various sources, making them highly adaptable to a wide range of datasets. The data streaming jobs are built with a generic approach that makes them robust and able to handle diverse datasets without requiring significant changes to the underlying code. More details on Obsrv-core can be found here - [https://github.com/Sunbird-Obsrv/obsrv-core/blob/main/README.md](https://github.com/Sunbird-Obsrv/obsrv-core/blob/main/README.md)

**Prerequisite:**

To use the Obsrv core, make sure you have the following dependencies installed:

* Java 11
* Maven
* Docker

**Build Project:**

* Use the cd command to navigate to the root directory of obsrv-core project
* Run the following Maven command to build the project - ​​mvn clean install

**Build Artifact:**

* Run the following Docker command from the root directory of obsrv-core to build the artifact - ​​docker build .
* Tag the built image with name - docker tag \<digest-from-build-command> \<image-name>:\<version>

Sample command: docker tag sha256:6021feb600a9ec4139dadd06536f46e5201435f0837fd4f60581d41a6ae6cf63 sunbird/obsrv-core:1.0.0

* Push docker image to docker hub - docker push \<image-name>:\<version>

#### **obsrv-api-service:**

**Repository:** [https://github.com/Sunbird-Obsrv/obsrv-api-service](https://github.com/Sunbird-Obsrv/obsrv-api-service)

**Introduction:**

This repository mainly has 2 sets of APIs. Obsrv-api-service and Obsrv-command-service.

**Obsrv-api-service** is a set of APIs that provide access to a variety of data sources and datasets. These APIs can be used to query and analyze different types of events, as well as to manage data sources and datasets. More details on Obsrv-api-service can be found here - [https://github.com/Sunbird-Obsrv/obsrv-api-service/blob/main/README.md](https://github.com/Sunbird-Obsrv/obsrv-api-service/blob/main/README.md)

**Obsrv-command-service** is an API that provides access to restart the Obsrv pipeline to make a newly created dataset accessible on the Obsrv.

**Prerequisite:**

To use the Obsrv API service, make sure you have the following dependencies installed:

* Node.js: version 18
* TypeScript: version 4.8.4
* Express.js: version 4.18.2
* npm: version 9.6.4
* Docker

To use the Obsrv Command service, make sure you have the following dependencies installed:

* Python3
* pip3
* Docker

**Build Artifact:**

Obsrv API service:

* Use the following command to navigate to the api-service directory of obsrv-api-service project - cd obsrv-api-service/api-service
* Install the required dependencies by running the following command - npm install

Obsrv Command service:

* Use the following command to navigate to the command-service directory of obsrv-command-service project - cd obsrv-api-service/command-service
* Install the required dependencies by running the following command - pip install -r requirements.txt

Artifact build commands:

* Use the following command to navigate to the respective service directory of obsrv-api-service project - cd obsrv-api-service/api-service or cd obsrv-api-service/command-service
* Run the following Docker command from the respective services directory to build the artifact - ​​docker build .
* Tag the built image with name - docker tag \<digest-from-build-command> \<image-name>:\<version>

Sample command: docker tag sha256:8021feb600a9ec4139dadd06536f48e5201435f0837fd4f60581d41a6ae6cf83 sunbird/obsrv-api-service:1.0.0

* Push docker image to docker hub - docker push \<image-name>:\<version>

#### **obsrv-automation:**

**Repository:** [https://github.com/Sunbird-Obsrv/obsrv-automation](https://github.com/Sunbird-Obsrv/obsrv-automation)

**Introduction:**

Obsrv-automation repository provides support for installation of Obsrv across major cloud providers. More details of Obsrv installation on different cloud providers can be found here - [https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/README.md](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/README.md)

**Prerequisite:**

* Terragrunt: 0.45.6 - Please see [Install Terragrunt](https://terragrunt.gruntwork.io/docs/getting-started/install/) for reference.
* Terraform: 1.5.7
* Terrahelp: 0.7.5
* Kubectl
* Helm: 3.10.2
* Azure cli or AWS cli: 2.13.8

**Steps to install Obsrv:**

* Setup prerequisites depending on the choice of cloud provider from this [doc](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/README.md)
* Update the automation scripts to use the new docker images created if any from other repositories under terraform/\<cloud-provider>/variables.tf file.
* Below are the installation steps to setup complete Obsrv

```
cd terraform/<cloud-provider>
terragrunt init
terragrunt plan
terragrunt apply
```
