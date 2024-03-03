# Overview
This repository contains Kubernetes configurations for deploying Elasticsearch and Kibana. The setup includes a StatefulSet for Elasticsearch and a Deployment for Kibana.

### Elasticsearch Configuration (elastic.yaml)
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: es-cluster
  namespace: qa-log-analyzer
spec:
  # ... (Elasticsearch configuration details)
---
apiVersion: v1
kind: Service
metadata:
  name: elasticsearch
  namespace: qa-log-analyzer
  labels:
    app: elasticsearch
  # ... (Service configuration details)
---
# ... (VolumeClaimTemplates for Elasticsearch)
```

### Kibana Configuration (kibana.yaml)
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: kibana-config
  namespace: qa-log-analyzer
data:
  kibana.yml: |-
    # ... (Kibana configuration details)
---
apiVersion: v1
kind: Service
metadata:
  name: kibana
  namespace: qa-log-analyzer
  labels:
    app: kibana
  # ... (Service configuration details)
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kibana
  namespace: qa-log-analyzer
  labels:
    app: kibana
spec:
  # ... (Kibana deployment details)
```

### Elasticsearch Configuration Details
* **StatefulSet**: Defines a single replica Elasticsearch cluster.
* **Service**: Exposes Elasticsearch with a LoadBalancer for external access.
* **VolumeClaimTemplates**: Specifies the storage configuration for Elasticsearch.

### Kibana Configuration Details
* **ConfigMap**: Provides Kibana configuration settings.
* **Service**: Exposes Kibana with a LoadBalancer for external access.
* **Deployment**: Configures a single replica deployment for Kibana.

## How to Use
1. Apply Elasticsearch configuration:
```bash
kubectl apply -f elastic.yaml
```
2. Apply Kibana configuration:
```bash
kubectl apply -f kibana.yaml
```
3. Monitor the deployment:
```bash
kubectl get pods -n qa-log-analyzer
```
4. Access Kibana via the LoadBalancer IP.

**Note**: Ensure Kubernetes cluster settings and network configurations align with the provided YAML files.

For more details, refer to the official Elasticsearch and Kibana documentation.

Feel free to contribute and open issues for any improvements or questions!
