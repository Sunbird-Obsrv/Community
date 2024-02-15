# Installation Guide

All components in Sunbird Obsrv can be installed through automation scripts. The automation scripts require [Ansible](https://docs.ansible.com/ansible/latest/index.html) as a prerequisite. Some of the components also require the de-facto package manager for Kubernetes, [helm](https://helm.sh/docs/) as a prerequisite to run the component on [Kubernetes](https://kubernetes.io).

#### Telemetry Service

The Sunbird Obsrv Telemetry service can be deployed onto Kubernetes using the helm chart. The deployment is handled using Ansible to manage the configuration and the commands that are necessary. The deployments can also be integrated into Jenkins, a popular CI/CD tool. The Telemetry Service deployment also has the capability of configurable horizontal scaling using the Horizontal Pod Scaling (HPA) concept of Kubernetes. A sample command to deploy the telemetry service on Kubernetes is provided below.

```
helm install telemetry-service sunbird-devops/kubernetes/helm_charts/telemetry 
-n <namespace> --create-namespace
```

{% embed url="https://github.com/project-sunbird/sunbird-devops/tree/release-4.8.0/kubernetes/helm_charts/core/telemetry" %}
Telemetry Service helm chart
{% endembed %}

#### Data Pipeline

Sunbird Obsrv Data Pipeline consists of a series of real-time streaming jobs chained together to unzip, transform and enrich the telemetry data. We use ansible and helm charts to deploy the series of jobs. The list of jobs that need to be deployed and their configurations can be controlled by the [ansible defaults configuration](https://github.com/project-sunbird/sunbird-data-pipeline/blob/release-4.8.0/kubernetes/ansible/roles/flink-jobs-deploy/defaults/main.yml#L168-L339).

```
ansible-playbook $currentWs/kubernetes/ansible/deploy_jobs.yml 
--extra-vars "chart_path=${currentWs}/kubernetes/helm_charts/datapipeline_jobs 
job_names_to_deploy=<comma-separate-list-of-job-names>"
```

{% embed url="https://github.com/project-sunbird/sunbird-data-pipeline/tree/release-4.8.0/kubernetes/ansible/roles/flink-jobs-deploy" %}
Ansible role for Data Pipeline
{% endembed %}

Sunbird Obsrv uses the following list of fields to de-normalize the user metadata. These fields are obtained by calling the user-read api belonging to [Sunbird Lern](https://lern.sunbird.org) building block. The de-normalization job can be modified to read the user metadata from a service/api of the adopter's choice.

```
firstName, lastName, encEmail, encPhone, language, rootOrgId, profileUserType (usertype, subusertype), 
userLocations(state, district, block, cluster, school), rootOrg (orgName), userId, 
framework, profileUserTypes (usertype, subusertype)
```

#### Data Service

The Data Service is a collection of data exhaust and report apis. The Data Service can be installed on Kubernetes using Ansible and Helm. A sample command to install the service is provided below. All the required configuration is managed using the [ansible configuration](https://github.com/project-sunbird/sunbird-devops/blob/release-4.8.0/ansible/roles/stack-sunbird/defaults/main.yml#L987-L1015).

```
helm install telemetry-service sunbird-devops/kubernetes/helm_charts/analytics 
-n <namespace> --create-namespace
```

{% embed url="https://github.com/project-sunbird/sunbird-devops/tree/release-4.8.0/kubernetes/helm_charts/core/analytics" %}
Data Service helm chart
{% endembed %}

#### Report Service

{% embed url="https://github.com/project-sunbird/sunbird-devops/tree/release-4.8.0/kubernetes/helm_charts/core/report" %}
Report Service helm chart
{% endembed %}

#### Summarisers

{% embed url="https://github.com/project-sunbird/sunbird-data-pipeline/tree/release-4.8.0/ansible/roles/data-products-deploy" %}
Ansbile role for Summarizer data products
{% endembed %}
