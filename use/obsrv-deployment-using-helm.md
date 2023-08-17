# Getting Started with Obsrv Deployment Using Helm
Sunbird Obsrv is a high-performance, cost-effective data stack with several components such as ingestion, querying, processing, backup, visualisation and monitoring. Obsrv 2.0 can be either installed using `Terraform` (Infrastructure as Code tool) or using `Helm` (Kubernets Package Manager).

## **Prerequisites**
Obsrv runs completely on a Kubernetes cluster. A completely functional Kubernetes cluster is expected for a seamless Obsrv installation.

### Hardware
Obsrv can support a volume of 5 million events per day with an average size of each event to be around 5 kb with the following specifications.

- Kubernetes version of 1.25 or greater
- Minimum of 16 cores of CPU
- Minimum of 64 GB of RAM
- PersistentVolume support in the Kubernetes cluster
- Support for LoadBalancer service to externally expose some of the Obsrv services. Popular implementations such as MetalLB or Traefik can be used to expose the services using external IPs.

### Software

#### Helm
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

#### Helm Dependencies
Run the following `helm repo add` command to download the required dependencies for running Obsrv.
    
```bash
# Example
helm repo add prometheus https://prometheus-community.github.io/helm-charts
```
    
- monitoring - `https://prometheus-community.github.io/helm-charts`
- redis - `https://charts.bitnami.com/bitnami`
- loki (version - 4.8.0 ) - `https://grafana.github.io/helm-charts`
- promtail (version - 6.9.3 ) - `https://grafana.github.io/helm-charts`
- velero (version - 3.1.6 ) -  `https://vmware-tanzu.github.io/helm-charts`

#### Source Code
Clone the [obsrv-automation](https://github.com/Sunbird-Obsrv/obsrv-automation) github repository. The required list of helm charts to deploy Obsrv will be under the `terraform/modules/helm` directory.

```bash
git clone https://github.com/Sunbird-Obsrv/obsrv-automation.git
cd obsrv-automation/terraform/modules/helm
```

#### Resources and Services

Please be advised that the list of resources will be completely different for different cloud service providers.

##### Common
The following list of buckets/containers need to be created for different services to store the data. This is applicable to Object Storage such as `MinIO/Ceph` as well.
- `flink-checkpoints`
- `velero-backup`
- `obsrv`

##### AWS
1. IAM role with `AmazonS3FullAccess` policy. Services such as Api, Druid, Flink, Secor need to read and write access to S3 buckets.

2. Velero is a service which provides backups of the entire Obsrv cluster state through snapshots. Velero backup service needs a restricted user access to upload the snapshot state onto S3. The following IAM role policy needs to be attached to user created for velero backup. The access keys needs to be generated for the velero backup user as well.
    ```json
    {
    "Statement": [
        {
        "Action": [
            "ec2:DescribeVolumes",
            "ec2:DescribeSnapshots",
            "ec2:CreateTags",
            "ec2:CreateVolume",
            "ec2:CreateSnapshot",
            "ec2:DeleteSnapshot"
        ],
        "Effect": "Allow",
        "Resource": "*"
        },
        {
        "Action": [
            "s3:GetObject",
            "s3:DeleteObject",
            "s3:PutObject",
            "s3:AbortMultipartUpload",
            "s3:ListMultipartUploadParts"
        ],
        "Effect": "Allow",
        "Resource": [
            "arn:aws:s3:::<velero-s3-container-name>/*"
        ]
        },
        {
        "Action": [
            "s3:ListBucket"
        ],
        "Effect": "Allow",
        "Resource": [
            "arn:aws:s3:::<velero-s3-container-name>"
        ]
        }
    ],
    "Version": "2012-10-17"
    }
    ```
3. Serive Accounts: Service accounts enable access of the S3 object storage without the need for the access keys. If you prefer to use keys instead, you can skip the creation of service accounts. The list of service accounts needed
- Dataset API with the name `dataset-api-sa`)
- Druid with the name `druid-raw-sa`
- Flink with the name `flink-sa`
- Secor with the name `secor-sa`


## **Deployment Instructions**

> Helm package manager provides an easy way to install specific components using a generic command. Configurations can be overriden by updating the `values.yaml` file in the respective Helm charts.
>
```bash
helm upgrade --install --atomic <release_name> <chart_name> -n <namespace> -f <path/values.yaml> --create-namespace --debug
```

### Prerequisites

#### Kubernetes Cluster Access
Helm package manager needs access to the Kubernetes cluster. The path to the KUBECONFIG file needs to be exported as an environment variable, either in the current shell or in environment configuration files such as `.bashrc`
```bash
export KUBECONFIG=<path_to_kubeconfig file>
```

### Postgres
Postgres is a RDBMS database which is used as the metadata store
    
```powershell
helm upgrade --install --atomic postgresql postgresql/postgresql-helm-chart -n postgresql --create-namespace --debug
```
    
### Redis
Redis is an in-memory key-value store primarily used as a distributed cache
    
```powershell
helm upgrade --install --atomic obsrv-redis redis/redis -n redis -f redis/values.yaml --create-namespace --debug
```

### Prometheus
Prometheus is a monitoring system with a dimensional data model, flexible query language, efficient time series database and modern alerting approach.
    
```powershell
helm upgrade --install --atomic monitoring monitoring/kube-prometheus-stack -n monitoring -f monitoring/values.yaml --create-namespace --debug
```
    
### Kafka
Apache Kafka is a distributed event store and stream-processing platform.

```powershell
helm upgrade --install --atomic kafka kafka/kafka-helm-chart -n kafka --create-namespace --debug
```

The following list of kafka topics are created by default. If you would like to add more topics to the list, you can do so by adding it to `provisioning.topics` configuration in the [values.yaml](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/terraform/modules/helm/kafka/kafka-helm-chart/values.yaml) file.
- dev.ingest
- masterdata.ingest  
    
### Druid
Druid is a high performance, real-time analytics database that delivers sub-second queries on streaming and batch data at scale

#### Druid CRD   
```powershell
helm upgrade --install --atomic druid-operator druid_operator/druid-operator-helm-chart -n druid-raw --create-namespace --debug
```

#### Druid Cluster
Druid requires the following set of configurations to be provided for specific storage systems such as AWS S3, Azure Blob Storage, GCP Storage or MinIO/Ceph

##### AWS
```yaml
druid_deepstorage_type: s3
# S3 Access keys
s3_access_key: ""
s3_secret_key: ""
s3_bucket: "obsrv"
```

##### MinIO/Ceph
```yaml
druid_deepstorage_type: s3
# S3 Access keys
s3_access_key: ""
s3_secret_key: ""
# Use the ClusterIP of the MinIO service instead of the Kubernetes service name
# We have noticed that the service names don't resolve properly
druid_s3_endpoint_url: http://172.20.126.232:9000/
s3_bucket: "obsrv"
druid_s3_endpoint_signingRegion: "us-east-2"
```

##### Azure
```yaml
azure_storage_account_name: ""
azure_storage_account_key: ""
azure_storage_container: "obsrv"
```

##### GCP
```yaml
# Google cloud credentials json file where the access_token and credentials are stored.
google_application_credentials: 
gcs_bucket: "obsrv"
```
    
```powershell
helm upgrade --install --atomic druid-raw druid_raw_cluster/druid-raw-cluster-helm-chart -n druid-raw --create-namespace --debug
```
        
### API
This service provides metadata APIs related to various resources such as datasets/datasources in Obsrv. The following configurations need to be specified in the [values.yaml](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/terraform/modules/helm/dataset_api/dataset-api-helm-chart/values.yaml) file.

#### AWS
```yaml
exhaust_service.CONTAINER: obsrv
exhaust_service.CONTAINER_STORAGE_PROVIDER: aws
exhaust_service.CONTAINER_STORAGE_REGION: us-east-2
```

```powershell
helm upgrade --install --atomic dataset-api dataset_api/dataset-api-helm-chart -n dataset-api --create-namespace --debug 
```
    
### Flink Streaming Jobs
Flink jobs are used to process and enrich the data ingested into Obsrv in near-realtime.

#### Configuration Overrides

##### AWS
```yaml
checkpoint_store_type: s3
# S3 Access keys
s3_access_key: ""
s3_secret_key: ""
# Under base_config in the values.yaml
base.url: s3://flink-checkpoints
```

##### MinIO/Ceph
```yaml
checkpoint_store_type: s3
# S3 Access keys
s3_access_key: ""
s3_secret_key: ""
# Use the ClusterIP of the MinIO service instead of the Kubernetes service name
# We have noticed that the service names don't resolve properly
s3_endpoint:  http://172.20.126.232:9000/
# Under base_config in the values.yaml
base.url: s3://flink-checkpoints
```

##### Azure
```yaml
checkpoint_store_type: azure
azure_account: ""
azure_secret: ""
# Under base_config in the values.yaml
base.url: blob://flink-bucket
```

##### GCP
```yaml
checkpoint_store_type: gcp
# Google cloud credentials json file where the access_token and credentials are stored.
google_application_credentials: ""
base.url: blob://flink-bucket
```

#### Flink Merged Pipeline Job
```powershell
helm upgrade --install --atomic merged-pipeline flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-merged-pipeline --create-namespace --debug
```
        
#### Flink Master Data Processor Job
```powershell
helm upgrade --install --atomic master-data-processor flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-master-data-processor --create-namespace --debug
```
### Backup Processes

#### Secor

##### Configuration Overrides

###### AWS
```yaml
# S3 upload manager which is responsible to upload backup to deepstorage.
upload_manager: com.pinterest.secor.uploader.S3UploadManager
cloud_store_provider: S3
aws_access_key: ""
aws_secret_key: ""
aws_region: us-east-2
```

###### MinIO/Ceph
```yaml
# S3 upload manager which is responsible to upload backup to deepstorage.
upload_manager: com.pinterest.secor.uploader.S3UploadManager
cloud_store_provider: S3
aws_access_key: ""
aws_secret_key: ""
# Use the ClusterIP of the MinIO service instead of the Kubernetes service name
# We have noticed that the service names don't resolve properly
aws_endpoint: http://172.20.126.232:9000/
aws_region: us-east-2
```

###### Azure
```yaml
upload_manager: com.pinterest.secor.uploader.AzureUploadManager
cloud_store_provider: Azure
azure_account_name: ""
azure_account_key: ""
```

###### GCP
```yaml
upload_manager: com.pinterest.secor.uploader.GsUploadManager
# Credentials path where access token and secrets are stored.
gs_credentials_path: google_app_credentials.json
```

Secor backups are performed from various kafka topics which are part of the data processing pipeline. The following list of backup names need to be replaced in the below mentioned command. 

List of backup names
- ingest-backup
- extractor-duplicate-backup
- extractor-failed-backup
- raw-backup
- failed-backup
- invalid-backup
- unique-backup
- duplicate-backup
- denorm-backup
- denorm-failed-backup
- system-stats
- system-events

```powershell
helm upgrade --install --atomic <backup_name> secor/secor-helm-chart -n secor --create-namespace
```

#### Velero
```powershell
helm upgrade --install --atomic velero velero/velero -n velero -f velero/values.yaml --create-namespace --debug --version 3.1.6
```

### Monitoring Services

#### Monitoring Dashboards
```powershell
helm upgrade --install --atomic grafana-configs grafana_configs/grafana-configs-helm-chart -n monitoring --create-namespace --debug
```

#### Monitoring Alert Rules 
```powershell
helm upgrade --install --atomic alertrules alert_rules/alert-rules-helm-chart -n monitoring --create-namespace --debug
```

#### Druid Exporter
```powershell
helm upgrade --install --atomic druid-exporter druid_exporter/druid-exporter-helm-chart -n druid-raw --create-namespace --debug
```

#### Kafka Exporter
```powershell
helm upgrade --install --atomic kafka-exporter kafka_exporter/kafka-exporter-helm-chart -n kafka --create-namespace --debug
```
        
#### Postgres Exporter
```powershell
helm upgrade --install --atomic postgresql-exporter postgresql_exporter/postgresql-exporter-helm-chart -n postgresql --create-namespace --debug
```

#### Loki
```powershell
helm upgrade --install --atomic loki loki/loki -n loki -f loki/values.yaml --create-namespace --debug --version 4.8.0
```
        
#### Promtail 
```powershell
helm upgrade --install --atomic promtail promtail/promtail -n loki -f promtail/values.yaml --create-namespace --debug --version 6.9.3
```
        
### Ingestion
This helm chart is used to submit the default ingestion tasks required for the system statistics events 
    
```powershell
helm upgrade --install --atomic submit-ingestion submit_ingestion/submit-ingestion-helm-chart -n submit-ingestion --create-namespace --debug 
```

### Visualization

#### Superset
```powershell
helm upgrade --install --atomic superset superset/superset-helm-chart -n superset --create-namespace --debug
```

### Loadbalancers
Following is a list of services which are exposed as a LoadBalancer service.

| Component | Service Name | Description|
|---------------|---------------|---------------|
| Dataset API | service/dataset-api-service | Meta APIs |
| Superset | service/superset | Data Visualization Tool |

## Post Deployment
Please find documentation related to various application level functionalities in Obsrv below

- [Create Datasets](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/INSTALLATION.md#create-a-dataset)
- [Data Ingestion](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/INSTALLATION.md#data-ingestion)
- [Data Querying](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/INSTALLATION.md#data-query)