---
icon: aws
---

# AWS

This guide provides detailed, step-by-step instructions for installing and configuring Obsrv on AWS, utilizing Terraform, Terragrunt, and Helm.

***

## Infrastructure Requirements

### 1. System Specifications

* **CPU Requirements**:
  * **Minimum**: 19 CPUs.
  * **Optimal Configuration**: 5 nodes with 4 cores each, totaling 80GB of RAM.

The installation package includes both lakehouse and real-time OLAP storage by default. If the lakehouse component is not required, only the real-time OLAP storage can be installed, reducing requirements to **16 CPUs** and **64GB of RAM**.

In this case, we recommend using **2 nodes with 8 cores each**, totaling **64GB of RAM**, by selecting the **`t2.2xlarge`** AWS instance type.

* **Availability Zones**: All instances should be within the same availability zone to minimize cross-zone data transfer costs. The Obsrv installer will automatically create the EKS (Elastic Kubernetes Service) cluster for you.

### 2. Networking Setup

* **CIDR Block**: Use a `/23` CIDR range (512 IPs) for your environment.
  * Example: A VPC with `10.0.0.0/23` provides IPs from `10.0.0.0` to `10.0.1.255`.
* **Subnets**: Ensure subnets are created in all availability zones within your AWS region.

***

## Prerequisites

Before beginning the installation, make sure the following tools are installed on your Linux-based system:

| **Tool**       | **Version**      | **Installation Command**                                                                                                                                                                                      | **Official Documentation**                                                                       |
| -------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Terraform**  | 1.5.x or earlier | `curl "https://releases.hashicorp.com/terraform/1.5.2/terraform_1.5.2_linux_amd64.zip" -o terraform.zip && unzip terraform.zip && sudo mv terraform /usr/local/bin/ && rm terraform.zip`                      | [Terraform Install](https://developer.hashicorp.com/terraform/install)                           |
| **Terragrunt** | 0.48 or later    | `curl -OL https://github.com/gruntwork-io/terragrunt/releases/download/v0.49.0/terragrunt_linux_amd64 && sudo mv terragrunt_linux_amd64 /usr/local/bin/terragrunt && sudo chmod +x /usr/local/bin/terragrunt` | [Terragrunt Install](https://terragrunt.gruntwork.io/docs/getting-started/install/)              |
| **Helm**       | 3.10.2 or later  | `curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/`                                                                | [Helm Install](https://helm.sh/docs/intro/install/)                                              |
| **AWS CLI**    | 2.10 or later    | `curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && unzip awscliv2.zip && sudo ./aws/install`                                                                               | [AWS CLI Install](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) |

***

***

## Installation Steps

### 1. Clone the Obsrv Repository

Start by cloning the Obsrv automation repository and checkout to either the latest release tag or `main`.

```bash
git clone https://github.com/Sunbird-Obsrv/obsrv-automation.git
```

### 2. Configure the Kubernetes Cluster

By executing the following commands which will bring up the kubernetes cluster in the AWS environment of configured region.

1.  **Navigate to the Configuration Directory**:

    ```bash
    cd ./obsrv-automation/terraform/aws/vars
    ```
2.  **Update Configuration Files**:

    * Open `cluster_overides.tf` and modify the configuration values to match your environment.

    ```bash
    building_block = "obsrv"
    env = "dev"
    region = "us-east-2"
    availability_zones = ["us-east-2a", "us-east-2b", "us-east-2c"]
    timezone = "UTC"
    create_kong_ingress = "true"
    create_vpc = "true"
    create_velero_user = "true"
    eks_node_group_instance_type = ["t2.xlarge"] # Choose depending on your requirements by considering the CPU requirements
    eks_node_group_capacity_type = "ON_DEMAND"
    eks_node_group_scaling_config = { desired_size = 5, max_size = 5, min_size = 1 } # Choose depending on your requirements by considering the CPU requirements
    eks_node_disk_size = 100
    ```
3.  **Configure S3 for Cluster State**:

    * Open `obsrv.conf` and update your AWS credentials and bucket names.

    ```bash
    AWS_ACCESS_KEY_ID=<your_access_key_id>
    AWS_SECRET_ACCESS_KEY=<your_secret_access_key>
    AWS_DEFAULT_REGION="us-east-2"
    KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config.yaml"
    AWS_TERRAFORM_BACKEND_BUCKET_NAME="obsrv-tfstate"
    AWS_TERRAFORM_BACKEND_BUCKET_REGION="us-east-2"
    ```

### 3. Run the Installation Script

1.  **Navigate to the Infra Setup Directory**:

    ```bash
    cd obsrv-automation/infra-setup
    ```
2.  **Make the Script Executable**:

    ```bash
    chmod +x ./obsrv.sh
    ```
3.  **Run the Installation**:

    * To start the installation, run the script:

    ```bash
    ./obsrv.sh install --provider aws --config ./obsrv.conf --install_dependencies false
    ```

    * If you want the installer to automatically handle dependencies, set `install_dependencies=true`.

### 4. Verify the Cluster

Once the installation completes, verify that your Kubernetes cluster is up and running:

```bash
kubectl get nodes
```

This should show the nodes in your Kubernetes cluster.

***

## Helm Chart Configuration

### 1. Navigate to the Helm Chart Directory

```bash
cd ./obsrv-automation/helmcharts/
```

### 2. Update AWS Cloud Configuration

> **Note:** `global-cloud-values-aws.yaml` is auto-generated by Terraform (the `aws_cloud_values` module) during the `./obsrv.sh install` step in [Installation Steps](#installation-steps), using the values from `cluster_overrides.tfvars` and resources Terraform creates (S3 bucket names, region, IAM role ARNs, Elastic IP, etc). It gets overwritten every time you run `obsrv.sh install` — do not edit it manually. Shown below just so you know what Terraform fills in:

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

### 4. Install Obsrv

Make the script executable and set the environment variables and run the installation:

```bash
export cloud_env=aws
export AWS_ACCESS_KEY_ID=<aws-access-key>
export AWS_SECRET_ACCESS_KEY=<aws-secret-key>
export AWS_DEFAULT_REGION=<aws-region>
export KUBE_CONFIG_PATH="$HOME/.kube/obsrv-kube-config.yaml"
export KUBECONFIG="$HOME/.kube/obsrv-kube-config.yaml"
chmod +x ./kitchen/install.sh
./kitchen/install.sh core-setup
./kitchen/install.sh all
```

`core-setup` installs the bootstrap CRDs, prerequisites, core database, and Kafka — `all` (migrations, monitoring, oauth, coreinfra, obsrvapis, obsrvtools, additional) depends on these being in place first, so run them in this order.

***

## Post-Installation Verification

After completing the installation, follow these steps to verify that all components are running correctly:

### 1. Check Kubernetes Components

1.  **Verify all pods are running**:

    ```bash
    kubectl get pods -A
    ```

    All pods should be in `Running` state. Common namespaces to check:

    * `flink`: Core Pipeline
    * `monitoring`: Monitoring stack
    * `dataset-api`: Dataset APIs
    * `web-console`: Dataset Management console
2.  **Check Services**:

    ```bash
    kubectl get svc -A
    ```

    Verify that essential services have external IPs assigned, particularly the Kong service.

If any component fails these checks, refer to the component-specific logs:

```bash
kubectl logs -f <pod-name> -n <namespace>
```

***

## Troubleshooting

### "Unreadable module directory" / `lstat ../modules: no such file or directory` on `terragrunt init`

Terragrunt copies the source directory into `.terragrunt-cache` before running. If `terraform/aws/terragrunt.hcl` has no explicit `source` block, newer Terragrunt versions (`v1.x`) copy only the `aws` directory, breaking the `../modules` relative paths used by `main.tf`. Older Terragrunt versions (`~0.45`) didn't hit this because they ran in place.

**Fix**: ensure `terraform/aws/terragrunt.hcl` has a `terraform { source = ... }` block pointing at the repo root with the `//terraform/aws` working-dir suffix, so both `../modules` and `../../helmcharts` resolve correctly from the cache copy.

### `Failed to resolve provider packages: locked provider ... does not match configured version constraint`

`terraform/aws/.terraform.lock.hcl` can drift out of sync with the provider version constraints in `main.tf` (e.g. `main.tf` requiring `~> 6.0` while the lock file is still pinned to a `4.x` version). This happens when the constraint is bumped in a commit without regenerating the lock file.

**Fix**:

```bash
cd terraform/aws
tofu init -upgrade -backend=false
```

Commit the regenerated `.terraform.lock.hcl`.

### `S3 bucket does not exist` on `terragrunt init`

The remote state bucket configured in `obsrv.conf` (`AWS_TERRAFORM_BACKEND_BUCKET_NAME`) must exist before `terragrunt init` runs. Either create it manually with `aws s3api create-bucket`, or pass `--backend-bootstrap` to auto-provision it (requires Terragrunt with backend-bootstrap support, e.g. `v1.x`):

```bash
terragrunt init --backend-bootstrap
```

### Certificate shows valid in `cert-manager`, but browser still says "Not Secure"

`kubectl get certificate` reporting `Ready: True` only means cert-manager issued the cert into its Kubernetes Secret — it doesn't guarantee every service actually serving TLS on your domain can read that secret. If a service's Ingress lives in a namespace other than where the cert's Secret was created (commonly `web-console`), the `kubernetes-reflector` controller must be explicitly allowed to copy the secret into that namespace via the `reflector.v1.k8s.emberstack.com/reflection-allowed-namespaces` annotation on the Certificate (set in `helmcharts/services/letsencrypt-ssl/templates/issuer-and-certs.yaml`). A namespace missing from that list (e.g. `dataset-api`) causes the Kong ingress controller to fail fetching the secret for that Ingress, which can break Kong's config sync entirely and make it fall back to its default self-signed certificate for **every** host, not just the affected one.

**Diagnose** — check what cert is actually being served on the wire, independent of Kubernetes state:

```bash
echo | openssl s_client -connect <your-ip>:443 -servername <your-domain> 2>/dev/null | openssl x509 -noout -issuer -subject
```

If the issuer shows `O=Kong, CN=localhost` instead of Let's Encrypt, check the Kong ingress controller logs for `failed to fetch the secret` errors:

```bash
kubectl logs -n kong-ingress -l app.kubernetes.io/name=kong -c ingress-controller --tail=50 | grep -i error
```

**Fix**: add the missing namespace to the `reflection-allowed-namespaces` annotation, then re-run the `migrations` helm bundle and restart Kong:

```bash
cd helmcharts/kitchen
cloud_env=aws ./install.sh migrations
kubectl rollout restart deployment kong -n kong-ingress
```

***

## Upgrade Steps

1.  **Pull the Latest Code**:

    ```bash
    cd ./obsrv-automation
    git pull
    cd ./infra-setup
    ```
2. **Update Configurations**: Review and update configuration values as needed.
3.  **Run Terraform for Upgrade**:

    ```bash
    ./obsrv.sh install --provider aws --config ./obsrv.conf --install_dependencies false
    ```
4.  **Upgrade with Updated Cloud Values**:

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

***

By following these steps, you will ensure a successful installation and configuration of Obsrv on AWS.
