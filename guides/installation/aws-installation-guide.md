---
description: Instructions to install in AWS infra
---

# AWS Installation Guide

### Infrastructure Requirements

1. **Minimal Installation:**
   * You need a system with a minimum of 16 CPUs. We recommend using 2 nodes with 8 cores each, totalling 64GB.
   * All machines must reside in the same availability zone to avoid data transfer charges across zones. Our Obsrv installer will automatically create the EKS cluster for you.
2. **Networking Environment:**
   * Ensure your environment has a CIDR of 23 (512 IP addresses).
   * For example, a VPC with CIDR `10.0.0.0/23` will have IP addresses ranging from `10.0.0.0` to `10.0.1.255`.
   * Subnets must be created in all availability zones within your region

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

*   Helm version 3.10.2 or later

    {% code overflow="wrap" %}
    ```bash
    curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/
    ```
    {% endcode %}
* Download from here - [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

#### AWS CLI

*   AWS CLI tool version 2.10 or later.

    {% code overflow="wrap" %}
    ```bash
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    # Fresh installation
    sudo ./aws/install
    # Update outdated aws cli with the following command
    sudo ./aws/install --update
    ```
    {% endcode %}
* Download from here - [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

#### Installation Steps:

1.  **Clone the `obsrv-automation` repository**:

    ```bash
    git clone https://github.com/Sanketika-Obsrv/obsrv-automation.git
    ```
2.  **Navigate to the setup directory**:

    ```bash
    cd ./obsrv-automation/automation-scripts/infra-setup
    ```
3.  **Update Configuration Files**: Update the configurations in both `setup.conf` and `cluster_overides.tf` files to match your environment settings. Example configuration in `cluster_overides.tf`

    ```jsx
    building_block                = "obsrv"
    env                           = "dev"
    region                        = "us-east-2"
    availability_zones            = ["us-east-2a", "us-east-2b", "us-east-2c"]
    timezone                      = "UTC"
    create_kong_ingress           = "true"
    create_vpc                    = "true"
    create_velero_user            = "true"
    vpc_id                        = ""
    eks_nodes_subnet_ids          = [""]
    eks_master_subnet_ids         = [""]
    velero_aws_access_key_id      = your_aws_access_key_id // Update the AWS Access Key
    velero_aws_secret_access_key  = your_aws_secret_access_key // Update the AWS Secret Key

    # cluster sizing

    eks_node_group_instance_type  = ["t2.2xlarge"]
    eks_node_group_capacity_type  = "ON_DEMAND"  
    eks_node_group_scaling_config = {
      desired_size = 4
      max_size = 4
      min_size = 1
    }

    # Disk node size in gb
    eks_node_disk_size            = 30

    # Image Tags
    command_service_image_tag    = "1.0.0-GA"
    web_console_image_tag        = "1.0.0-GA"
    dataset_api_image_tag        = "1.0.2-GA"
    flink_image_tag              = "1.0.1-GA"
    secor_image_tag              = "1.0.0-GA"
    superset_image_tag           = "3.0.2"
    ```
4.  **S3 Bucket**:

    Obsrv installation requires a S3 bucket to be created which will be subsequently used for storing the cluster state. The bucket name will then be referenced in the installation script mentioned below. For e.g, if the bucket created is **obsrv-tfstate**, please ensure it is updated in the `obsrv.conf` under the environment variable.

    Example configuration in `setup.conf`:

    ```bash
    AWS_ACCESS_KEY_ID=<your_access_key_id>
    AWS_SECRET_ACCESS_KEY=<your_secret_access_key>
    AWS_DEFAULT_REGION="us-east-2"
    KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config"
    AWS_TERRAFORM_BACKEND_BUCKET_NAME="obsrv-tfstate"
    AWS_TERRAFORM_BACKEND_BUCKET_REGION="us-east-2"
    ```

    The `AWS_DEFAULT_REGION` environment variable will control the AWS region in which the cluster will be created. Please make sure that the region is updated according to your installation needs. The `AWS_TERRAFORM_BACKEND_BUCKET_REGION` is used to store the terraform state
5.  **Run Installation Script**: Execute the following command to start the installation process:

    1. Before installing please provide executable permission to installation script `chmod +x ./obsrv.sh`

    ```bash
    ./obsrv.sh install --config ./obsrv.conf --install_dependencies false
    ```

    * Note: Setting `install_dependencies=true` will automatically download and install all required dependencies. If preferred, you can manually download the dependencies instead.
6. **Monitor Installation Progress**: The script will begin installing Obsrv within the AWS cluster. Monitor the progress and follow any on-screen prompts or instructions.
7. **Completion**: Once the installation process is complete, verify that Obsrv has been successfully installed and configured within your AWS cluster. One simple and quick way to check if you are able to communicate with the cluster is to run the command `kubectl get svc --all-namespaces`. This will list all the services running as a part of the Obsrv installation

### Upgrade Steps:

1.  Take latest code from **`obsrv-automation`** repository

    ```bash
    cd ./obsrv-automation
    git pull
    cd ./automation-scripts/infra-setup
    ```
2. Ensure all the configuration configured during the installation is properly updated in all places.
3.  Run the terraform to upgrade the cluster to the latest versions.

    ```bash
    ./obsrv.sh install --config ./obsrv.conf
    ```

