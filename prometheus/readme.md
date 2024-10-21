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

    Access Prometheus at `http://192.168.49.2:30000`.

    6. **🔄 Port Forward Prometheus Service:**

        Alternatively, you can port forward the Prometheus service to access it locally:

        ```sh
        kubectl port-forward -n monitoring svc/prometheus 9090:9090
        ```

        Access Prometheus at `http://localhost:9090`.
        ## 📊 Viewing Metrics

        To view the metrics collected by Prometheus, follow these steps:

        1. **Open Prometheus UI:**

            Access the Prometheus UI using the URL provided in the previous steps (`http://192.168.49.2:30000` or `http://localhost:9090` if using port forwarding).

        2. **Explore Metrics:**

            In the Prometheus UI, navigate to the "Graph" tab. Here, you can enter Prometheus query language (PromQL) expressions to explore the metrics.

            For example, to view the CPU usage of your nodes, you can use the following query:

            ```
            node_cpu_seconds_total
            ```

            Click on "Execute" to see the results and visualize the data.

        3. **Set Up Dashboards:**

            For a more user-friendly way to visualize metrics, consider setting up Grafana and connecting it to Prometheus. Grafana provides powerful dashboards and visualizations for your metrics.

            To deploy Grafana, you can follow similar steps as deploying Prometheus, creating a deployment and service for Grafana.

        By following these steps, you can effectively monitor and visualize the metrics collected by Prometheus.
## 🧹 Cleanup

To delete the Prometheus deployment and service, run:

```sh
kubectl delete -f prometheus-deployment.yaml
kubectl delete -f prometheus-service.yaml
kubectl delete namespace monitoring
```

