---
description: Instructions to install in on-prem data centre
---

# Data Center Installation Guide

### Infrastructure Requirements

1. **Minimal Installation:**
   * You need a system with a minimum of 16 CPUs and 32GB RAM.
   * If running a multi-node cluster, ensure the network reachability between the nodes.

### Software Prerequisites

Installation of Obsrv requires the following CLI tools as prerequisites. Please note that the following instructions for installing the prerequisites are provided only for **Linux based operating systems**. Please follow the instructions for the specific tools depending upon your operating system.

#### MinIO

* Obsrv Installation requires an Object Store for backups, checkpointing and to store other configurations. We have tested our installations with MinIO, and is the recommended one for quick setup. Follow the instructions from [https://min.io/download](https://min.io/download) to install.

#### Helm

*   Helm version 3.10.2 or later

    {% code overflow="wrap" %}
    ```bash
    curl https://get.helm.sh/helm-v3.10.2-linux-amd64.tar.gz -o helm.tar.gz && tar -zxvf helm.tar.gz && sudo mv linux-amd64/helm /usr/local/bin/
    ```
    {% endcode %}
* Download from here - [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

#### Addons

*   Ensure LoadBalancer is available. For example on a a local setup add-ons such as `metallb` can be enabled and configured. Following is a sample for minikube

    ```bash
    minikube addons enable metallb
    minikube addons configure metallb
    ```
*   Ensure metrics is enabled. Following is a sample for minikube

    ```bash
    minikube addons enable metrics-server
    ```

#### Installation Steps:

1.  Clone the `obsrv-automation` repository:

    ```bash
    git clone https://github.com/Sanketika-Obsrv/obsrv-automation.git
    ```
2.  Navigate to the setup directory:

    ```bash
    cd ./obsrv-automation/terraform/modules/helm/unified-helm
    ```
3.  Export the KUBECONFIG environment variable with for your cluster. For example the below command is to set to its default path

    ```bash
    export KUBECONFIG=~/.kube/kubeconfig.yaml
    ```
4.  First create the CRD’s that are required to install Obsrv

    ```bash
    kubectl create -f ./crds/
    ```
5.  Run the below command to install the services. The following command may fail a couple of times due to timeouts while downloading the images. Run the same command for a couple of times incase of any errors for the installation to be successful

    {% code overflow="wrap" %}
    ```bash
    helm upgrade --install obsrv obsrv --namespace obsrv --create-namespace --atomic --debug --timeout 3600s
    ```
    {% endcode %}

### Upgrade Steps:

1.  Take latest code from **`obsrv-automation`** repository

    ```bash
    cd ./obsrv-automation
    git pull
    cd ./terraform/modules/helm/unified-helm
    ```
2. Ensure all the configuration configured during the installation is properly updated in all places.
3.  Run the helm upgrade the cluster to the latest versions.

    {% code overflow="wrap" %}
    ```bash
    helm upgrade --install obsrv obsrv --namespace obsrv --create-namespace --atomic --debug --timeout 3600s
    ```
    {% endcode %}
