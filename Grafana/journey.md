# Setting Up Grafana with Prometheus 🚀

Follow these steps to set up Grafana using an existing Prometheus setup in Minikube:

## Prerequisites 📋
- Prometheus is already installed and running in Minikube.
- Grafana is installed. If not, [download and install Grafana](https://grafana.com/grafana/download).

## Step-by-Step Guide 🛠️

### 1. Start Grafana in Minikube
Create a Grafana deployment and service in Minikube:
```bash
kubectl create deployment grafana --image=grafana/grafana
kubectl expose deployment grafana --type=NodePort --port=3000
```
### 1.1. Port Forward Grafana
To access Grafana locally, set up port forwarding:
```bash
kubectl port-forward deployment/grafana 3000:3000
```
This command forwards port 3000 on your local machine to port 3000 on the Grafana deployment.

### 2. Access Grafana
Get the URL to access Grafana:
```bash
minikube service grafana --url
```
Open the URL in your web browser. Log in with the default credentials:
- **Username:** admin
- **Password:** admin

### 3. Add Prometheus as a Data Source 📊
1. Click on the **gear icon** ⚙️ in the sidebar.
2. Select **Data Sources**.
3. Click **Add data source**.
4. Select **Prometheus** from the list.
5. Configure the Prometheus data source:
    - **Name:** Prometheus
        - **URL:** `http://localhost:3000`
6. Click **Save & Test** to verify the connection.

### 4. Create a Dashboard 📈
1. Click on the **plus icon** ➕ in the sidebar.
2. Select **Dashboard**.
3. Click **Add new panel**.
4. Configure your panel with Prometheus queries.
5. Click **Apply** to save the panel.

### 5. Explore and Customize 🎨
- Use the **Explore** feature to run ad-hoc queries.
- Customize your dashboards with various panels and visualizations.

## Conclusion 🎉
You have successfully set up Grafana with Prometheus in Minikube! Enjoy monitoring your metrics.

For more information, visit the [prometheus documentation](https://grafana.com/docs/).

### 6. Describe the prometheus Service in the Monitoring Namespace
To get detailed information about the Grafana service in the `monitoring` namespace, use the following command:
```bash
kubectl describe service prometheus -n monitoring
```
This command provides information about the service, including endpoints, ports, and labels.