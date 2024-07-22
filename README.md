
# ELK Stack on Kubernetes
This repository contains Kubernetes YAMLs and Helm values files for setting up the ELK stack (Elasticsearch, Filebeat, Logstash, and Kibana) in a Kubernetes cluster.

### Prerequisites
Kubernetes cluster
Helm installed

## Installation
1. Clone the Repository

git clone https://github.com/Gatete-Bruno/Logging
cd elasticsearch-logstash-kibana-kubernetes

2. Add the Helm Repo

```bash
helm repo add elastic https://helm.elastic.co
helm repo update
```

3. Elasticsearch Setup
Create and Apply Persistent Volumes
```bash
kubectl apply -f elasticsearch/pv.yaml
```

Install Elasticsearch
```bash
cd elasticsearch
helm install elasticsearch elastic/elasticsearch --version="7.17.3" -f values.yaml
cd ..
```

4. Filebeat Setup
Create and Apply Persistent Volumes
```bash
kubectl apply -f filebeat/pv.yaml
cd ..
```
Install Filebeat
```bash
cd filebeat
helm install filebeat elastic/filebeat --version="7.17.3" -f values.yaml
cd ..
```

5. Kibana Setup
Install Kibana
```bash
cd kibana
helm install kibana elastic/kibana --version="7.17.3" -f values.yaml
cd ..
cd ..
```

Update Ingress Hostname
Modify the ingress.yaml file to match your hostname.
Apply Ingress
```bash
kubectl apply -f kibana/
cd ..
```

6. Logstash Setup
Apply Logstash YAMLs
```bash
cd logstash
kubectl apply -f .
cd ..
```
7. Verify Installation
Check the status of the pods to ensure they are all running:

```bash
kubectl get pods
```
If all pods are in the Running status, go to your Kibana host address to access the ELK stack.
