# Prometheus on Minikube

This guide will help you set up a simple Prometheus environment using a Minikube cluster.

## Prerequisites

- 🛠️ Minikube installed
- 🛠️ kubectl installed

## Steps

1. **🚀 Start Minikube:**

    ```sh
    minikube start
    ```

2. **📂 Create a Namespace for Monitoring:**

    ```sh
    kubectl create namespace monitoring
    ```

3. **📦 Deploy Prometheus:**

    Create a file named `prometheus-deployment.yaml` with the following content:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: prometheus
      namespace: monitoring
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: prometheus
      template:
        metadata:
          labels:
            app: prometheus
        spec:
          containers:
          - name: prometheus
            image: prom/prometheus
            ports:
            - containerPort: 9090
    ```

    Apply the deployment:

    ```sh
    kubectl apply -f prometheus-deployment.yaml
    ```

4. **🌐 Expose Prometheus Service:**

    Create a file named `prometheus-service.yaml` with the following content:

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: prometheus
      namespace: monitoring
    spec:
      type: NodePort
      ports:
      - port: 9090
        targetPort: 9090
        nodePort: 30000
      selector:
        app: prometheus
    ```

    Apply the service:

    ```sh
    kubectl apply -f prometheus-service.yaml
    ```

5. **🔍 Access Prometheus:**

    Get the Minikube IP:

    ```sh
    minikube ip
    ```

    Access Prometheus at `http://<minikube-ip>:30000`.

## 🧹 Cleanup

To delete the Prometheus deployment and service, run:

```sh
kubectl delete -f prometheus-deployment.yaml
kubectl delete -f prometheus-service.yaml
kubectl delete namespace monitoring
```

