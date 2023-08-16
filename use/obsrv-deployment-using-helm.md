# Getting Started with Obsrv Deployment Using Helm

Sunbird Obsrv is a comprehensive system that includes several components such as ingestion, querying, processing, backup, visualisation and monitoring. Each component can be easily deployed into a Kubernetes cluster using Helm charts, allowing for a seamless setup process.

If you're looking to get started with Obsrv 2.0, there are a few prerequisites to keep in mind. Once you've fulfilled these requirements, you'll be ready to deploy and utilize all of the system's powerful features.

### **Prerequisites**

Before deploying Obsrv ensure you have a running Kubernetes cluster.

1. Hardware Specifications

For smooth operation of the obsrv system, a minimum of 16 CPU cores and 64 GB of RAM is required to handle the processing of 10 to 15 million events per day.

2. Install helm 

```powershell
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

3. Run the following `helm repo add` command to download the required dependencies for running Obsrv.
    
    ```powershell
    helm repo add <repo_name> <repo_url>
    ex :- helm repo add prometheus https://prometheus-community.github.io/helm-charts
    ```
    
    - monitoring - `https://prometheus-community.github.io/helm-charts`
    - redis - `https://charts.bitnami.com/bitnami`
    - loki (version - 4.8.0 ) - `https://grafana.github.io/helm-charts`
    - promtail (version - 6.9.3 ) - `https://grafana.github.io/helm-charts`
    - velero (version - 3.1.6 ) -  `https://vmware-tanzu.github.io/helm-charts`
4. Clone the repo [https://github.com/Sunbird-Obsrv/obsrv-automation](https://github.com/Sunbird-Obsrv/obsrv-automation), navigate to `obsrv-automation/terraform/modules/helm`, `ls -lrt` to list all the available helm charts and configurations.
5. Create the following resources
    - Service account for Api, Druid, Flink, Secor.
    - IAM role for Api, Druid, Flink, Secor with `AmazonS3FullAccess` policy.
    - User for velero and generate credentials
    - IAM role for velero user with the below policy
        ```{
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
        }```
    - Following three s3 buckets to be created 
        - Api,Druid,Secor
        - Flink
        - Velero

### **Deployment Instructions**

Follow these simple steps to deploy Observations 2.0 on your Kubernetes cluster. 

> To install any of the helm charts run this command `helm upgrade --install --atomic <release_name> <chart_name> -n <namespace> -f <path/values.yaml> --create-namespace --debug` If any additional configuration changes are required, please update the `values.yaml` file in the Helm chart.
> 

1. **Export Kubeconfig File:**
In one terminal tab, export the kubeconfig files for your Kubernetes cluster.
2. **Postgresql:**
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic postgresql postgresql/postgresql-helm-chart -n postgresql --create-namespace --debug
    ```
    
3. **Redis:**  Redis is an in-memory data structure store, used as a distributed, in-memory key–value database
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic obsrv-redis redis/redis -n redis -f redis/values.yaml --create-namespace --debug
    ```
4. **Prometheus**
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic monitoring monitoring/kube-prometheus-stack -n monitoring -f monitoring/values.yaml --create-namespace --debug
    ```
    
5. **Kafka:** Kafka is a distributed event store and stream-processing platform.
    - Variables to be passed before installing this chart:
        - Topic configuration like topic name, replication factor, no. of partitions etc. For ex: 
        ```powershell
        - name: "dev.ingest"
          partitions: 1
          replicationFactor: 1
        ```
    Here the topic name is `dev.ingest` with `1` `partition` and `1` `replication factor`.

    Use the following commands to deploy Kafka:
    - Install Command:
        
    ```powershell
    helm upgrade --install --atomic kafka kafka/kafka-helm-chart -n kafka --create-namespace --debug
    ```
    
6. ****Druid:**** Druid is a high performance, real-time analytics database that delivers sub-second queries on streaming and batch data at scale and under load 
    1. **Druid Operator**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-operator druid_operator/druid-operator-helm-chart -n druid-raw --create-namespace --debug
        ```
    - Variables to be passed before installing this chart:
        - If you are using a service account then the below list of variables needs to be passed:
            - s3 bucket name, service account role arn For ex: `s3_bucket: "druid-bucket"`, `eks.amazonaws.com/role-arn: "arn:aws:iam::012345678901:role/dev-obsrv-demo-druid-raw-sa-iam-role"`
            - Deepstorage configuration (provided below is the checklist for different type to deepstorages).
        - If you are not using a service account then the below list of variables needs to be passed:
             - s3 bucket name(for ex: `druid-bucket`), s3 access key, s3 secret key.
             - Deepstorage configuration (provided below is the checklist for different type to deepstorages).
    - Checklist for deepstorage configuration. [Multiple  Deepstorage Configuration for Druid,Flink,Secor](obsrv-deployment-deepstorage-csp.md)
    
    2. **Druid Cluster**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-raw druid_raw_cluster/druid-raw-cluster-helm-chart -n druid-raw --create-namespace --debug
        ```
        
7. **API:** This service enables CRUD operations on the dataset and data source levels.
    - Variables to be passed before installing this chart 
        - system-env (for ex: `dev`), container (for ex: `demo-bucket`), container-storage-provider (for ex: `aws`), container-storage-region (for ex: `us-east-2`), eks.amazonaws.com/role-arn (for ex: `arn:aws:iam::0123456789012:role/dev-obsrv-demo-dataset-api-sa-iam-role`)
    - Install command:
    
    ```powershell
    helm upgrade --install --atomic dataset-api dataset_api/dataset-api-helm-chart -n dataset-api --create-namespace --debug 
    ```
    
8. **Flink Streaming Jobs:**  Flink Streaming job which ensures data quality and reliability. It performs various tasks, including data validation against predefined schemas, filtering out duplicates, and enriching data through joins with multiple data stores. This powerful job is designed to efficiently process data at scale.
    1. **Service account**
    - Variables to be passed before installing this chart:
        - Service account role arn under annotations (for ex: `eks.amazonaws.com/role-arn:arn:aws:iam::012345678901:role/dev-obsrv-demo-flink-sa-iam-role`)

        - Install Command:
    
        ```powershell
        helm upgrade --install --atomic flink-sa flink/flink-helm-chart-sa -n flink --create-namespace --debug
        ```
    2. **Flink Merged Pipeline Job:** 
    - Variables to be passed before installing this chart:
        - env (for ex: `dev`)
        - Deepstorage configuration (provided below the checklist for different deepstorage types)    
        - Checklist for deepstorage configuration. [Multiple  Deepstorage Configuration for Druid,Flink,Secor](obsrv-deployment-deepstorage-csp.md)
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic merged-pipeline flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-merged-pipeline --create-namespace --debug
        ```
        
    3. **Flink Master Data Processor Job:**
    - Variables to be passed before installing this chart:
        - env (for ex: `dev`)
        - Deepstorage configuration (provided below the checklist for different deepstorage types)    
        - Checklist for deepstorage configuration. [Multiple  Deepstorage Configuration for Druid,Flink,Secor](obsrv-deployment-deepstorage-csp.md)
        - Install Command
        
        ```powershell
        helm upgrade --install --atomic master-data-processor flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-master-data-processor --create-namespace --debug
        ```
    
9. **Secor Backup Process:**
    1. **Service account**
    - Variables to be passed before installing this chart:
        - Service account role arn under annotations (for ex: `eks.amazonaws.com/role-arn:arn:aws:iam::012345678901:role/dev-obsrv-demo-secor-sa-iam-role`)
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic secor-sa secor/secor-helm-chart-sa -n secor --create-namespace --debug
        ```
    
    2. **Backup Process**
    - Variables to be passed before installing this chart:
        - Deepstorage configuration (provided below the checklist for different deepstorage types)    
        - Checklist for deepstorage configuration. [Multiple  Deepstorage Configuration for Druid,Flink,Secor](obsrv-deployment-deepstorage-csp.md)
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic ingest-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic extractor-duplicate-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic extractor-failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic raw-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic invalid-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic unique-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic duplicate-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic denorm-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic denorm-failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic transform-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic system-stats secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic system-events secor/secor-helm-chart -n secor --create-namespace --debug
        ```
        

10. **Monitoring Services:**
        
    1. **Grafana Configs**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic grafana-configs grafana_configs/grafana-configs-helm-chart -n monitoring --create-namespace --debug
        ```
        
    2. **Alert Rules**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic alertrules alert_rules/alert-rules-helm-chart -n monitoring --create-namespace --debug
        ```
        
    3. **Druid Exporter**
        - Variables to be passed before installing this chart:
            - druidURL (for ex: `http://druid-raw-routers.druid-raw.svc:8888`), namespace (for ex: `druid-raw`) 
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-exporter druid_exporter/druid-exporter-helm-chart -n druid-raw --create-namespace --debug
        ```
        
    4. **Kafka Exporter**
        - Variables to be passed before installing this chart:
            - kafka servers (for ex: `kafka-headless:9093`), zookeeper servers (for ex: `kafka-zookeeper-headless.svc.cluster.local:2181`), prometheus namespace (for ex: `kafka`)

        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic kafka-exporter kafka_exporter/kafka-exporter-helm-chart -n kafka --create-namespace --debug
        ```
        
    5. **Postgres Exporter**
        - Variables to be passed before installing this chart:
            - host (for ex: `postgresql-hl.postgresql.svc.cluster.local`), namespace (for ex: `postgresql`)
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic postgresql-exporter postgresql_exporter/postgresql-exporter-helm-chart -n postgresql --create-namespace --debug
        ```
        
    6. **Velero**
        - Variables to be passed before installing this chart:
            - aws_access_key_id, aws_secret_access_key, provider (for ex: `aws`), bucket (for ex: `velero-bucket`), region (for ex: `us-east-2`)
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic velero velero/velero -n velero -f velero/values.yaml --create-namespace --debug --version 3.1.6
        ```
        
    7. **Loki**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic loki loki/loki -n loki -f loki/values.yaml --create-namespace --debug --version 4.8.0
        ```
        
    8. **Promtail**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic promtail promtail/promtail -n loki -f promtail/values.yaml --create-namespace --debug --version 6.9.3
        ```
11. **Ingestion:** This service submits ingestion to druid.
    - Variables to be passed before installing this chart:
        - druid router host (for ex: `druid-raw-routers.druid-raw.svc.cluster.local:8888`), bootstrap servers (for ex: `kafka-headless.kafka.svc.cluster.local:9092`), topic (for ex: `dev.stats`,`dev.masterdata.stats`)
    - Install command:
    
    ```powershell
    helm upgrade --install --atomic submit-ingestion submit_ingestion/submit-ingestion-helm-chart -n submit-ingestion --create-namespace --debug 
    ```
12. **Visualization:** This service is used to visualize all the data
    1. **Superset**
        - Install command:

        ```powershell
        helm upgrade --install --atomic superset superset/superset-helm-chart -n superset --create-namespace --debug
        ```
    2. **Webconsole**
        - Variables to be passed before installing this chart:
            - namespace (for ex: `web-console`), prometheus url (for ex: ` http://localhost`), react app grafana url (for ex: ` http://localhost`), react app superset url (for ex: ` http://localhost`)
        - Install command:

        ```powershell
        helm upgrade --install --atomic web-console web_console/web-console-helm-chart -n web-console --create-namespace --debug
        ```
13. **Loadbalancers:** Below is the list of services  

    | Service       	| Loadbalancer (Required/Optional)  	| Description                                                                                                                                                                      	|
    |---------------	|---------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
    | Postgres      	| `Optional`      	| It is a database which need not be exposed.                                                                                                                                      	|
    | Redis         	| `Optional`      	| It is a cache service which need not be exposed.                                                                                                                                 	|
    | Prometheus    	| `Optional`      	| It is a monitoring service which need not be exposed.                                                                                                                            	|
    | Kafka         	| `Optional`      	| It is a queue service which need not be exposed.                                                                                                                                 	|
    | Druid         	| `Optional`      	| It is a analytical tool which need not be exposed.                                                                                                                               	|
    | API           	| **Required** 	| It is the entry point of the data in so it needs to be exposed as a loadbalancer.                                                                                                	|
    | Pipeline Jobs 	| `Optional`      	| It is a job which process data so it need not be exposed.                                                                                                                        	|
    | Backups       	| `Optional`      	| It is backup service which need not be exposed.                                                                                                                                  	|
    | Exporters     	| `Optional`      	| It is a exporter service which send metrics to prometheus from respective applications for ex: postgres-exporter,druid-exporter,kafka-exporter. This doesn't need to be exposed. 	|
    | Ingestion     	| `Optional`      	| It is a service which submits ingestion for analytical tool. This doesn't need to be exposed.                                                                                    	|
    | Superset      	| **Required** 	| It is one of the visualization tool which needs to be exposed.                                                                                                                   	|
    | Web console   	| **Required** 	| It is a visualization tool which need to be exposed.                                                                                                                             	|

### **Conclusion**

By following these instructions, you can easily deploy Obsrv on your Kubernetes cluster using Helm charts. Once all components are up and running, you can take advantage of the system's comprehensive features for data processing, visualisation, and analysis on your datasets. For more details on each service's configuration, please visit the configuration [page](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/INSTALLATION.md). Enjoy seamless data management and insights with Sunbird Obsrv!