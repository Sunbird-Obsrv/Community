---
description: Instructions to install in Azure infra
---

# Azure Installation Guide

### Infrastructure Requirements

1. **Minimal Installation:**
   * You need a system with a minimum of 16 CPUs. We recommend using 2 nodes with 8 cores each, totalling 64GB.
   * All machines must reside in the same availability zone to avoid data transfer charges across zones. Our Obsrv installer will automatically create the AKS cluster for you.
2. **Networking Environment:**
   * Ensure your environment has a CIDR of 16
     * For example, a Virtual Network with a CIDR of `10.0.0.0/23` will have IP addresses ranging from `10.0.0.0` to `10.0.1.255`.
   * Subnets must be created in all availability zones within your region.

### Software Prerequisites

Installation of Obsrv requires the following CLI tools as prerequisites. Please note that the following instructions for installing the prerequisites are provided only for **Linux based operating systems**. Please follow the instructions for the specific tools depending upon your operating system.

#### Terraform

*   Terraform CLI version 1.5.x or older. Versions above 1.5.x are not MPL licensed.

    {% code overflow="wrap" %}
    ```bash
    curl "https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip" -o "terraform.zip" && unzip terraform.zip && sudo mv terraform /usr/local/bin/ && rm terraform.zip
    ```
    {% endcode %}
* Download from here - [https://developer.hashicorp.com/terraform/install](https://developer.hashicorp.com/terraform/install)

#### Terragrunt

*   Terragrunt CLI version 0.48 or later.

    {% code overflow="wrap" %}
    ```bash
    curl -OL https://github.com/gruntwork-io/terragrunt/releases/download/v0.49.0/terragrunt_linux_amd64 && sudo mv terragrunt_linux_amd64 /usr/local/bin/terragrunt && sudo chmod +x /usr/local/bin/terragrunt
    ```
    {% endcode %}
* Download from here - [https://terragrunt.gruntwork.io/docs/getting-started/install/](https://terragrunt.gruntwork.io/docs/getting-started/install/)

#### Terrahelp

*   Terrahelp version 0.7.5 or later

    {% code overflow="wrap" %}
    ```bash
    curl -OL https://github.com/opencredo/terrahelp/releases/download/v0.7.5/terrahelp_0.7.5_linux_386.tar.gz && tar -xzf terrahelp_0.7.5_linux_386.tar.gz && sudo mv terrahelp /usr/local/bin/terrahelp && sudo chmod +x /usr/local/bin/terrahelp
    ```
    {% endcode %}
* Download from here - [https://github.com/opencredo/terrahelp?tab=readme-ov-file#installation](https://github.com/opencredo/terrahelp?tab=readme-ov-file#installation)

#### Helm

*   Helm version 3.10.2

    {% code overflow="wrap" %}
    ```bash
    curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/
    ```
    {% endcode %}
* Download from here - [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

#### Azure CLI

*   Azure CLI tool version 2.10 or later.

    ```bash
    curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
    ```
* Download from here - [https://learn.microsoft.com/en-us/cli/azure/install-azure-cli](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
*   Post installation, authenticate Azure CLI. Please refer to this [link](https://learn.microsoft.com/en-us/cli/azure/get-started-tutorial-1-prepare-environment?tabs=bash#sign-in-to-azure-using-the-azure-cli) for more details about Signing In to Azure CLI

    ```bash
    az login --allow-no-subscriptions
    ```

### Installation Steps:

1.  **Clone the `obsrv-automation` repository**:

    ```bash
    git clone https://github.com/Sanketika-Obsrv/obsrv-automation.git
    ```
2.  **Navigate to the setup directory**:

    ```bash
    cd ./obsrv-automation/terraform/azure
    ```
3.  **Export Azure Credentials**:

    Create a Resource Group, Storage Account and Storage Container through the Azure Portal. Once completed, export the below values as an environment variable.

    ```bash
    export AZURE_TERRAFORM_BACKEND_RG=<resource_group>
    export AZURE_TERRAFORM_BACKEND_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_TERRAFORM_BACKEND_CONTAINER=<storage_container_name>
    ```
4.  **Create the AKS cluster**

    The following commands will create an AKS Cluster

    ```bash
    terragrunt init
    terragrunt  apply -target module.aks -auto-approve
    terragrunt apply -auto-approve
    ```

    During creation of the cluster, you will be asked for prompts as and when required by the installation. Here is a sample of the inputs you have to provide while the above script executes.

    ```bash
    env: dev
    building_block: obsrv
    location: East US 2
    ```
5.  Make a note of **Resource Group** created during the cluster creation. Usually it is a combination of `<building_block>-<env>`. For the above example the resorce group will be `obsrv-dev`. You can look for the logs for the statement like below.

    {% code overflow="wrap" %}
    ```bash
    module.network.azurerm_resource_group.rg: Creation complete after 3s [id=/subscriptions/<uuid>/resourceGroups/<your-resource-group>]
    ```
    {% endcode %}

    Export the **Resource Group** name as an environment variable

    ```bash
    export AZ_RESOURCE_GROUP=<your-resource-group>
    ```

### Upgrade Steps:

1.  Take latest code from **`obsrv-automation`** repository

    ```bash
    cd ./obsrv-automation
    git pull
    cd ./terraform/azure
    ```
2. Ensure all the configuration configured during the installation is properly updated in all places.
3.  Run the terraform to upgrade the cluster to the latest versions.

    ```
    cd ./obsrv-automation
    git pull
    cd ./terraform/azure
    terragrunt apply -auto-approve
    ```
