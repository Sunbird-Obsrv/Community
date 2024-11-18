# Obsrv AWS Installation Guide

This guide provides detailed, step-by-step instructions for installing and configuring Obsrv on AWS, utilizing Terraform, Terragrunt, and Helm.

---

## Infrastructure Requirements

### 1. System Specifications
- **CPU**: Minimum of 24 CPUs. For optimal performance, use 3 nodes with 8 cores each (total 96GB of RAM).
- **Availability Zones**: All instances should be within the same availability zone to minimize cross-zone data transfer costs. The Obsrv installer will automatically create the EKS (Elastic Kubernetes Service) cluster for you.

### 2. Networking Setup
- **CIDR Block**: Use a `/23` CIDR range (512 IPs) for your environment.
    - Example: A VPC with `10.0.0.0/23` provides IPs from `10.0.0.0` to `10.0.1.255`.
- **Subnets**: Ensure subnets are created in all availability zones within your AWS region.

---

## Prerequisites

Before beginning the installation, make sure the following tools are installed on your Linux-based system:

| **Tool**         | **Version**        | **Installation Command**                                                                                                                                                        | **Official Documentation**                                    |
|------------------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| **Terraform**     | 1.5.x or earlier   | `curl "https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip" -o terraform.zip && unzip terraform.zip && sudo mv terraform /usr/local/bin/ && rm terraform.zip` | [Terraform Install](https://developer.hashicorp.com/terraform/install) |
| **Terragrunt**    | 0.48 or later      | `curl -OL https://github.com/gruntwork-io/terragrunt/releases/download/v0.49.0/terragrunt_linux_amd64 && sudo mv terragrunt_linux_amd64 /usr/local/bin/terragrunt && sudo chmod +x /usr/local/bin/terragrunt` | [Terragrunt Install](https://terragrunt.gruntwork.io/docs/getting-started/install/) |
| **Helm**          | 3.10.2 or later    | `curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/` | [Helm Install](https://helm.sh/docs/intro/install/) |
| **AWS CLI**       | 2.10 or later      | `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip && sudo ./aws/install`                                                      | [AWS CLI Install](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |

---

---

## Installation Steps

### 1. Clone the Obsrv Repository
Start by cloning the Obsrv automation repository and checkout to either latest release tag or master.
```bash
git clone https://github.com/Sunbird-Obsrv/obsrv-automation.git
```

### 2. Configure the Kubernetes Cluster
By executing the following commands which will bring up the kubernetes cluster in the AWS environment of configured region.

1. **Navigate to the Configuration Directory**:
    ```bash
    cd ./obsrv-automation/terraform/aws/vars
    ```

2. **Update Configuration Files**:
    - Open `cluster_overides.tf` and modify the configuration values to match your environment.
    ```bash
    building_block = "obsrv"
    env = "dev"
    region = "us-east-2"
    availability_zones = ["us-east-2a", "us-east-2b", "us-east-2c"]
    timezone = "UTC"
    create_kong_ingress = "true"
    create_vpc = "true"
    create_velero_user = "true"
    eks_node_group_instance_type = ["t2.2xlarge"]
    eks_node_group_capacity_type = "ON_DEMAND"
    eks_node_group_scaling_config = { desired_size = 3, max_size = 3, min_size = 1 }
    eks_node_disk_size = 100
    ```

3. **Configure S3 for Cluster State**:
    - Open `obsrv.conf` and update your AWS credentials and bucket names.
    ```bash
    AWS_ACCESS_KEY_ID=<your_access_key_id>
    AWS_SECRET_ACCESS_KEY=<your_secret_access_key>
    AWS_DEFAULT_REGION="us-east-2"
    KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config.yaml"
    AWS_TERRAFORM_BACKEND_BUCKET_NAME="obsrv-tfstate"
    AWS_TERRAFORM_BACKEND_BUCKET_REGION="us-east-2"
    ```

### 3. Run the Installation Script

1. **Make the Script Executable**:
    ```bash
    chmod +x ./obsrv.sh
    ```

2. **Run the Installation**:
    - To start the installation, run the script:
    ```bash
    ./obsrv.sh install --config ./obsrv.conf --install_dependencies false
    ```
    - If you want the installer to automatically handle dependencies, set `install_dependencies=true`.

### 4. Verify the Cluster

Once the installation completes, verify that your Kubernetes cluster is up and running:
```bash
kubectl get nodes
```
This should show the nodes in your Kubernetes cluster.

---

## Helm Chart Configuration

### 1. Navigate to the Helm Chart Directory
```bash
cd ./obsrv-automation/helmcharts/
```

### 2. Update AWS Cloud Configuration
Modify `global-cloud-values-aws.yaml` with the appropriate values for your environment:
```yaml
global:
  cloud_storage_provider: "aws"
  cloud_store_provider: "s3"
  cloud_storage_region: "<region>"
  dataset_api_cloud_bucket: "<dataset_bucket_name>"
  config_api_cloud_bucket: "<config_bucket_name>"
  postgresql_backup_cloud_bucket: "<backup_bucket_name>"
  redis_backup_cloud_bucket: "<redis_backup_bucket_name>"
  velero_backup_cloud_bucket: "<velero_backup_bucket_name>"
  cloud_storage_bucket: "<storage_bucket_name>"
  hudi_metadata_bucket: "s3a://<hudi_bucket_name>/hudi"
  cloud_storage_config: |
    '{"identity":"<access-key>","credential":"<secret-key>","region":"<region-name>"}'

  storage_class_name: "gp2"
  checkpoint_bucket: "s3://<checkpoint-bucket-name>"
  s3_access_key: "<aws-access-key>"
  s3_secret_key: "<aws-secret-key>"

kong_annotations:
  service.beta.kubernetes.io/aws-load-balancer-type: nlb
  service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing
  service.beta.kubernetes.io/aws-load-balancer-eip-allocations: "<elastic-ip>"
  service.beta.kubernetes.io/aws-load-balancer-subnets: "<subnet-id>"

service_accounts:
  enabled: true
  secor: eks.amazonaws.com/role-arn: "<role-arn>"
  dataset_api: eks.amazonaws.com/role-arn: "<role-arn>"
  config_api: eks.amazonaws.com/role-arn: "<role-arn>"
  druid_raw: eks.amazonaws.com/role-arn: "<role-arn>" 
  flink: eks.amazonaws.com/role-arn: "<role-arn>" 
  postgresql_backup: eks.amazonaws.com/role-arn: "<role-arn>" 
  redis_backup: eks.amazonaws.com/role-arn: "<role-arn>" 
  s3_exporter: eks.amazonaws.com/role-arn: "<role-arn>" 
  spark: eks.amazonaws.com/role-arn: "<role-arn>" 

velero-backup:
  credentials:
    useSecret: true
    secretContents:
      cloud: |
        [default]
        aws_access_key_id="<aws-access-key>"
        aws_secret_access_key="<aws-secret-key>"

trino:
  additionalCatalogs:
    lakehouse: |-
      connector.name=hudi
      hive.metastore.uri=thrift://hudi-hms.hms.svc:9083
      hive.s3.aws-access-key=<aws-access-key>
      hive.s3.aws-secret-key=<aws-secret-key>
      hive.s3.ssl.enabled=false
```

### 3. Update Domain Configuration
In `global-values.yaml`, replace `<domain>` with your actual domain or Elastic IP:
```yaml
domain: "<domain>.sslip.io"
```

### 4. Update Private and Public Keys

Follow these steps to generate and configure the private and public keys for the web console and dataset API:

#### **Step 1: Generate a Private Key**
Run the following command to generate a private key for the web console:

```bash
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048
```

- Open the generated `private_key.pem` file.
- Copy its contents and update the `USER_TOKEN_PRIVATE_KEY` field in the following file:  
  `obsrv-automation/helmcharts/services/web-console/values.yaml`

Example:
```yaml
USER_TOKEN_PRIVATE_KEY: |-
    <paste-private-key-here>
```

---

#### **Step 2: Generate a Public Key**
Using the private key generated above, create a public key with the following command:

```bash
openssl rsa -pubout -in private_key.pem -out public_key.pem
```

- Open the generated `public_key.pem` file.
- Copy its contents and update the `user_token_public_key` field in the following file:  
  `obsrv-automation/helmcharts/services/dataset-api/values.yaml`

Example:
```yaml
user_token_public_key: <paste-public-key-here>
```



### 5. Install Obsrv
Make the script executable and set the environment variables and run the installation:
```bash
export cloud_env=aws
export AWS_ACCESS_KEY_ID=<aws-access-key>
export AWS_SECRET_ACCESS_KEY=<aws-secret-key>
export AWS_DEFAULT_REGION=<aws-region>
export KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config.yaml"
export KUBECONFIG="$HOME/.kube/obsrv-kube-config.yaml"
chmod +x ./kitchen/install.sh
./kitchen/install.sh all
```

---

## Post-Installation Verification

After completing the installation, follow these steps to verify that all components are running correctly:

### 1. Check Kubernetes Components

1. **Verify all pods are running**:
    ```bash
    kubectl get pods -A
    ```
    All pods should be in `Running` state. Common namespaces to check:
    - `flink`: Core Pipeline
    - `monitoring`: Monitoring stack
    - `dataset-api`: Dataset APIs
    - `web-console`: Dataset Management console

2. **Check Services**:
    ```bash
    kubectl get svc -A
    ```
    Verify that essential services have external IPs assigned, particularly the Kong service.

If any component fails these checks, refer to the component-specific logs:
```bash
kubectl logs -f <pod-name> -n <namespace>
```

---

## Upgrade Steps

1. **Pull the Latest Code**:
    ```bash
    cd ./obsrv-automation
    git pull
    cd ./automation-scripts/infra-setup
    ```

2. **Update Configurations**: Review and update configuration values as needed.

3. **Run Terraform for Upgrade**:
    ```bash
    ./obsrv.sh install --config ./obsrv.conf --install_dependencies false
    ```

4. **Upgrade with Updated Cloud Values**:
    ```bash
    export cloud_env=aws
   export AWS_ACCESS_KEY_ID=<aws-access-key>
   export AWS_SECRET_ACCESS_KEY=<aws-secret-key>
   export AWS_DEFAULT_REGION=<aws-region>
   export KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config.yaml"
   export KUBECONFIG="$HOME/.kube/obsrv-kube-config.yaml"
   chmod +x ./kitchen/install.sh
   ./kitchen/install.sh all
    ```

---

By following these steps, you will ensure a successful installation and configuration of Obsrv on AWS.