# AWS Installation Guide

## Infrastructure Requirements

### 1. Minimal Installation
   - **CPU Requirements**: Minimum of 16 CPUs. Recommended: 2 nodes with 8 cores each, totaling 64GB RAM.
   - **Availability Zone**: All machines should be in the same availability zone to avoid cross-zone data transfer charges. The Obsrv installer will automatically create the EKS cluster for you.

### 2. Networking Environment
   - **CIDR Range**: Ensure a /23 CIDR (512 IPs) for your environment.
     - Example: A VPC with `10.0.0.0/23` provides IPs from `10.0.0.0` to `10.0.1.255`.
   - **Subnets**: Create subnets in all availability zones within your region.

## Software Prerequisites

Obsrv installation requires several CLI tools. The installation instructions provided here are specific to **Linux-based operating systems**.

### Terraform
   - **Version**: CLI version 1.5.x or earlier.
   ```bash
   curl "https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip" -o "terraform.zip" && unzip terraform.zip && sudo mv terraform /usr/local/bin/ && rm terraform.zip
   ```
   - [Terraform Download](https://developer.hashicorp.com/terraform/install)

### Terragrunt
   - **Version**: CLI version 0.48 or later.
   ```bash
   curl -OL https://github.com/gruntwork-io/terragrunt/releases/download/v0.49.0/terragrunt_linux_amd64 && sudo mv terragrunt_linux_amd64 /usr/local/bin/terragrunt && sudo chmod +x /usr/local/bin/terragrunt
   ```
   - [Terragrunt Download](https://terragrunt.gruntwork.io/docs/getting-started/install/)

### Terrahelp
   - **Version**: CLI version 0.7.5 or later.
   ```bash
   curl -OL https://github.com/opencredo/terrahelp/releases/download/v0.7.5/terrahelp_0.7.5_linux_386.tar.gz && tar -xzf terrahelp_0.7.5_linux_386.tar.gz && sudo mv terrahelp /usr/local/bin/terrahelp && sudo chmod +x /usr/local/bin/terrahelp
   ```
   - [Terrahelp Download](https://github.com/opencredo/terrahelp?tab=readme-ov-file#installation)

### Helm
   - **Version**: CLI version 3.10.2 or later.
   ```bash
   curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/
   ```
   - [Helm Download](https://helm.sh/docs/intro/install/)

### AWS CLI
   - **Version**: CLI tool version 2.10 or later.
   ```bash
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip
   sudo ./aws/install
   # Update outdated AWS CLI:
   sudo ./aws/install --update
   ```
   - [AWS CLI Download](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Installation Steps

### 1. Clone the Obsrv Repository
   ```bash
   git clone https://github.com/Sanketika-Obsrv/obsrv-automation.git
   ```

### 2. Cluster Creation
   - **Navigate to Directory**:
     ```bash
     cd ./obsrv-automation/terraform/aws/vars
     ```

   - **Update Configuration Files**: Update `cluster_overides.tf` to match your environment settings.
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
     velero_aws_access_key_id      = "<your_aws_access_key_id>"
     velero_aws_secret_access_key  = "<your_aws_secret_access_key>"
     eks_node_group_instance_type  = ["t2.2xlarge"]
     eks_node_group_capacity_type  = "ON_DEMAND"  
     eks_node_group_scaling_config = { desired_size = 4, max_size = 4, min_size = 1 }
     eks_node_disk_size            = 100
     ```

   - **S3 Bucket Configuration**: Obsrv requires an S3 bucket for cluster state storage. Update the bucket name in `setup.conf` with your bucket name.
     ```bash
     AWS_ACCESS_KEY_ID=<your_access_key_id>
     AWS_SECRET_ACCESS_KEY=<your_secret_access_key>
     AWS_DEFAULT_REGION="us-east-2"
     KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config"
     AWS_TERRAFORM_BACKEND_BUCKET_NAME="obsrv-tfstate"
     AWS_TERRAFORM_BACKEND_BUCKET_REGION="us-east-2"
     ```

### 3. Run Installation Script
   - Make the installation script executable:
     ```bash
     chmod +x ./obsrv.sh
     ```
   - Run the installation:
     ```bash
     ./obsrv.sh install --config ./obsrv.conf --install_dependencies false
     ```
     - Setting `install_dependencies=true` will automatically install required dependencies.

### 4. Verify Cluster Setup
   - Use `kubectl get svc --all-namespaces` to check if all services are running.

## Obsrv Installation

1. **Navigate to Helm Chart Directory**
   ```bash
   cd ./obsrv-automation/helmcharts/
   ```

2. **Update AWS Cloud Values**
   - Edit `global-cloud-values-aws.yaml` with your environment settings.
     ```jsx
     global:
       cloud_storage_provider: &cloud_storage_provider "aws"
       cloud_store_provider: &cloud_store_provider "s3"
       cloud_storage_region: &cloud_storage_region "<region>"
       dataset_api_cloud_bucket: "<dataset_bucket_name>"
       config_api_cloud_bucket: "<config_bucket_name>"
       postgresql_backup_cloud_bucket: &backups_bucket "<backup_bucket_name>"
       redis_backup_cloud_bucket: &redis_backup_cloud_bucket "<redis_backup_bucket_name>"
       velero_backup_cloud_bucket: &velero_backup_cloud_bucket "<velero_backup_bucket_name>"
       cloud_storage_bucket: &cloud_storage_bucket "<storage_bucket_name>"
       hudi_metadata_bucket: &hudi_metadata_bucket "s3a://<hudi_bucket_name>/hudi"
     ```

3. **Install Obsrv**
   ```bash
   sh install.sh all
   ```

## Upgrade Steps

1. **Pull Latest Code**
   ```bash
   cd ./obsrv-automation
   git pull
   cd ./automation-scripts/infra-setup
   ```

2. **Update Configurations**: Ensure all configurations are updated as needed.

3. **Run Terraform for Upgrade**:
   ```bash
   ./obsrv.sh install --config ./obsrv.conf --install_dependencies false
   ```

4. **Update Cloud Values and Re-Install**:
   ```bash
   sh install.sh all
   ```