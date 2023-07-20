# Getting Started with Obsrv Deployment Using Helm

Sunbird Obsrv is a comprehensive system that includes several components such as ingestion, querying, processing, backup, visualisation and monitoring. Each component can be easily deployed into a Kubernetes cluster using Helm charts, allowing for a seamless setup process.

If you're looking to get started with Obsrv 2.0, there are a few prerequisites to keep in mind. Once you've fulfilled these requirements, you'll be ready to deploy and utilize all of the system's powerful features.

### **Prerequisites**

Before deploying Obsrv ensure you have a running Kubernetes cluster.

1. Install helm 

```powershell
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

1. Run the following `helm repo add` command to download the required dependencies for running Obsrv.
    
    ```powershell
    helm repo add <repo_name> <repo_url>
    ex :- helm repo add prometheus https://prometheus-community.github.io/helm-charts
    ```
    
    - prometheus - `https://prometheus-community.github.io/helm-charts`
    - redis - `https://charts.bitnami.com/bitnami`
    - loki - `https://grafana.github.io/helm-charts`
    - promtail - `https://grafana.github.io/helm-charts`
    - velero -  `https://vmware-tanzu.github.io/helm-chart`
2. Clone the repo [https://github.com/Sunbird-Obsrv/obsrv-automation](https://github.com/Sunbird-Obsrv/obsrv-automation), navigate to `obsrv-automation/terraform/modules/helm`, `ls -lrt` to list all the available helm charts and configurations.

### **Deployment Instructions**

Follow these simple steps to deploy Observations 2.0 on your Kubernetes cluster. 

> To install any of the helm charts run this command `helm upgrade --install --atomic <release_name> <chart_name> -n <namespace> -f <path/values.yaml> --create-namespace --debug` If any additional configuration changes are required, please update the `values.yaml` file in the Helm chart.
> 

1. **Export Kubeconfig File**:
In one terminal tab, export the kubeconfig files for your Kubernetes cluster.
2. **Deploying Postgresql**
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic postgresql postgresql/postgresql-helm-chart -n postgresql --create-namespace --debug
    ```
    
3. **Redis:**  Redis is an in-memory data structure store, used as a distributed, in-memory key–value database
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic redis redis/redis -n redis -f redis/values.yaml --create-namespace --debug
    ```
    
4.  **Kafka**: Kafka is a distributed event store and stream-processing platform. Use the following commands to deploy Kafka:
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic kafka kafka/kafka-helm-chart -n kafka --create-namespace --debug
    ```
    
5. ****Druid:**** Druid is a high performance, real-time analytics database that delivers sub-second queries on streaming and batch data at scale and under load
    1. **Druid Operator**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-operator druid_operator/druid-operator-helm-chart -n druid-raw --create-namespace --debug
        ```
        
    2. **Druid Exporter**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-exporter druid_exporter/druid-exporter-helm-chart -n druid-raw --create-namespace --debug
        ```
        
6. **API:** This service enables CRUD operations on the dataset and data source levels.
    - Install command:
    
    ```powershell
    helm upgrade --install --atomic druid-exporter druid_exporter/druid-exporter-helm-chart -n druid-raw --create-namespace --debug 
    ```
    
7. **Flink Streaming Jobs:**  Flink Streaming job which ensures data quality and reliability. It performs various tasks, including data validation against predefined schemas, filtering out duplicates, and enriching data through joins with multiple data stores. This powerful job is designed to efficiently process data at scale.
    1. **Streaming Jobs**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic merged-pipeline flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-merged-pipeline --create-namespace --debug
        ```
        
    2. **Flink Master Data Processor:**
        - Install Command
        
        ```powershell
        helm upgrade --install --atomic master-data-processor flink/flink-helm-chart -n flink --set image.registry=sunbird --set image.repository=sb-obsrv-master-data-processor --create-namespace --debug
        ```
        
    
    c. **Service account**
    
    - Install Command:
    
    ```powershell
    helm upgrade --install --atomic flink-sa flink/flink-helm-chart-sa -n flink --create-namespace --debug
    ```
    
8. **Secor Backup Process:**
    1. **Service account**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic secor-sa secor/secor-helm-chart-sa -n secor --create-namespace --debug
        ```
        
    2. **Backup Process**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic ingest-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic extractor-duplicate-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic extractor-failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic raw-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic invalid-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic unique-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic duplicate-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic denorm-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic denorm-failed-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic transform-backup secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic system-stats secor/secor-helm-chart -n secor --create-namespace --debug && helm upgrade --install --atomic system-events secor/secor-helm-chart -n secor --create-namespace --debug
        ```
        

1. **Monitoring stack:**
    1. **Promethes**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic monitoring prometheus/kube-prometheus-stack -n monitoring -f monitoring/values.yaml --create-namespace --debug
        ```
        
    2. **Grafana Configs**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic grafana-configs grafana_configs/grafana-configs-helm-chart -n monitoring --create-namespace --debug
        ```
        
    3. **Alert Rules**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic alertrules alert_rules/alert-rules-helm-chart -n monitoring --create-namespace --debug
        ```
        
    4. **Druid Exporter**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic druid-exporter druid_exporter/druid-exporter-helm-chart -n druid-raw --create-namespace --debug
        ```
        
    5. **Kafka Exporter**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic kafka-exporter kafka_exporter/kafka-exporter-helm-chart -n druid-raw --create-namespace --debug
        ```
        
    6. **Postgres Exporter**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic kafka-exporter postgresql_exporter/kafka-exporter-helm-chart -n druid-raw --create-namespace --debug
        ```
        
    7. **Velero**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic velero velero/velero -n velero -f velero/values.yaml --create-namespace --debug
        ```
        
    8. **Loki**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic loki loki/loki -n monitoring -f loki/values.yaml --create-namespace --debug
        ```
        
    9. **Promtail**
        - Install Command:
        
        ```powershell
        helm upgrade --install --atomic promtail promtail/promtail -n monitoring -f promtail/values.yaml --create-namespace --debug
        ```
        

### **Conclusion**

By following these instructions, you can easily deploy Obsrv on your Kubernetes cluster using Helm charts. Once all components are up and running, you can take advantage of the system's comprehensive features for data processing, visualisation, and analysis on your datasets. For more details on each service's configuration, please visit the configuration [page](https://github.com/Sunbird-Obsrv/obsrv-automation/blob/main/INSTALLATION.md). Enjoy seamless data management and insights with Sunbird Obsrv!