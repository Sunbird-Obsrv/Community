---
description: Instructions to install in GCP infra
icon: google
---

# GCP Installation Guide

### Infrastructure Requirements

1. **Minimal Installation:**
   * You need a system with a minimum of 16 CPUs. We recommend using 2 nodes with 8 cores each, totalling 32GB.
   * All machines must reside in the same zone to avoid data transfer charges across zones. Our Obsrv installer will automatically create the GKE cluster for you.
2. **Networking Environment:**
   * The networking requirements change w.r.t the type of cluster we are creating. Follow this [link](https://cloud.google.com/kubernetes-engine/docs/concepts/types-of-clusters#availability) to find out different types of clusters supported by Google Cloud in the region you are installation.
   * By default our setup script creates a Single Zonal Public Cluster and the required VPC’s for it.

### Software Prerequisites

Installation of Obsrv requires the following CLI tools as prerequisites. Please note that the following instructions for installing the prerequisites are provided only for **Linux based operating systems**. Please follow the instructions for the specific tools depending upon your operating system.

#### Terraform

*   Terraform CLI version 1.5.x or older. Versions above 1.5.x are not MPL licensed.

    {% code overflow="wrap" %}
    ```bash
    curl "<https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip>" -o "terraform.zip" && unzip terraform.zip && sudo mv terraform /usr/local/bin/ && rm terraform.zip
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

*   Helm version 3.10.2 or later

    {% code overflow="wrap" %}
    ```bash
    curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/
    ```
    {% endcode %}
* Download from here - [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

#### Setup Google Cloud SDK

*   Install Google Cloud SDK by following the instructions [here](https://cloud.google.com/sdk/docs/install)

    {% code overflow="wrap" %}
    ```bash
    gcloud init
    gcloud auth application-default login
    ```
    {% endcode %}
*   Install additional dependencies to authenticate with GKE. Please see [Installing the gke-gcloud-auth-plugin](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl) for reference.

    ```bash
    gcloud components install gke-gcloud-auth-plugin
    ```

#### Create a GCP Project

*   Create a project on google cloud and export it as a variable. Please see [Creating and Managing Projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects) for reference.

    ```bash
    export GOOGLE_PROJECT_ID=<myproject>
    ```
* Enable the Kubernetes Engine API for the created project. Please see [Enabling the Kubernetes Engine API](https://cloud.google.com/kubernetes-engine/docs/how-to/creating-a-zonal-cluster#enable-api) for reference.

### Installation Steps:

1.  **Clone the `obsrv-automation` repository**:

    ```bash
    git clone https://github.com/Sanketika-Obsrv/obsrv-automation.git
    ```
2.  **Navigate to the setup directory**:

    ```bash
    cd ./obsrv-automation/terraform/gcp
    ```
3.  **Update Configuration Files**:

    Update the `vars/cluster_overrides.tfvars` file to match your environment and requirement settings. Example configuration in `cluster_overides.tf`

    ```bash
    project                       = "<myproject>"
    building_block                = "obsrv"
    env                           = "dev"
    region                        = "us-central-1"
    gke_cluster_location          = "us-central-1"
    zone                          = "us-central-1-a"
    timezone                      = "UTC"
    service_type                  = "LoadBalancer"

    # cluster sizing

    gke_node_pool_instance_type   = "c2d-standard-8"
    gke_node_pool_scaling_config = {
      desired_size = 2
      max_size = 2
      min_size = 1
    }

    # Image Tags
    command_service_image_tag    = "1.0.0-GA"
    web_console_image_tag        = "1.0.0-GA"
    dataset_api_image_tag        = "1.0.2-GA"
    flink_image_tag              = "1.0.1-GA"
    secor_image_tag              = "1.0.0-GA"
    superset_image_tag           = "3.0.2"
    ```

    Note: if you are changing the region, also check if the instance type is supported in that region. If not please change the instance type from the supported list which can be found in this [link](https://cloud.google.com/compute/docs/regions-zones#available)
4.  **GCS Bucket:**

    Obsrv installation requires a GCS bucket to be created which will be subsequently used for storing the cluster state. The bucket name will then be referenced in the installation script mentioned below. For e.g, if the bucket created is **obsrv-cluster-state**, please export it as a environment variable as show below, which will be referenced in the `terragrunt.hcl` under the environment variable **GOOGLE\_TERRAFORM\_BACKEND\_BUCKET**. The bucket will be created automatically if it doesn’t exist. The region can be updated by passing it in an environment variable **GOOGLE\_TERRAFORM\_BACKEND\_BUCKET\_REGION**

    ```bash
    export GOOGLE_TERRAFORM_BACKEND_BUCKET=obsrv-cluster-tfstate
    export GOOGLE_TERRAFORM_BACKEND_BUCKET_REGION=us-central1
    ```
5.  **Run Installation Script**: Execute the following command to start the installation process:

    ```bash
    terragrunt init
    terragrunt plan --var-file=vars/cluster_overrides.tfvars # to verify if everything is in order
    terragrunt apply --var-file=vars/cluster_overrides.tfvars
    ```
6. **Monitor Installation Progress**: The script will begin installing Obsrv within the GKE cluster. Monitor the progress and follow any on-screen prompts or instructions.
7. **Completion**: Once the installation process is complete, verify that Obsrv has been successfully installed and configured within your GKE cluster.

### Upgrade Steps:

1.  Take latest code from **`obsrv-automation`** repository

    ```bash
    cd ./obsrv-automation
    git pull
    cd ./terraform/gcp
    ```
2. Ensure all the configuration configured during the installation is properly updated in all places.
3.  Run the terraform to upgrade the cluster to the latest versions.

    ```bash
    terragrunt apply --var-file=vars/cluster_overrides.tfvars
    ```
