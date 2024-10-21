```mermaid
graph TD
    B[1 - Prometheus: 9000] -->|Visualization| C[2 - Grafana: 3000]
    A[3 - Thanos]
    subgraph 0 - Codespaces - LB
        E
        subgraph 1 - Minikube Cluster - IP
			n2["Remote Write Prometheus Endpoint"]
			n3(("Cluster Target Port 9090 This is for Data Source Prometheus"))
            B
            C
            E
            A
        end

    click C "https://musical-sniffle-wggjpgjg46xc9qpq-3000.app.github.dev/?orgId=1" "Click for Grafana"
    click B "https://musical-sniffle-wggjpgjg46xc9qpq-9090.app.github.dev/graph" "Click for Prometheus"
    end 
    F[Devops Workstation]
    D[Bitnami Repo] --> |Local Service| E[Helm Charts]
    B --> n2
    n2 --> A
	subGraph1
	
	subgraph n3["Cluster Target Port 9090 This is for Data Source Prometheus"]
	end
	n3
	n3
```
		
## Minikube IP Address
The Minikube IP address is `192.168.49.2`.

## Kubernetes Services
Here are the services running in the Kubernetes cluster:

| NAMESPACE   | NAME         | TYPE        | CLUSTER-IP       | EXTERNAL-IP | PORT(S)                  | AGE  |
|-------------|--------------|-------------|------------------|-------------|--------------------------|------|
| default     | kubernetes   | ClusterIP   | 10.96.0.1        | <none>      | 443/TCP                  | 9m6s |
| kube-system | kube-dns     | ClusterIP   | 10.96.0.10       | <none>      | 53/UDP,53/TCP,9153/TCP   | 9m5s |
| monitoring  | prometheus   | NodePort    | 10.101.225.175   | <none>      | 9090:30000/TCP           | 2m3s |


## Prometheus Service Details

```plaintext
Name:                     prometheus
Namespace:                monitoring
Labels:                   <none>
Annotations:              <none>
Selector:                 app=prometheus
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.101.225.175
IPs:                      10.101.225.175
Port:                     <unset>  9090/TCP
TargetPort:               9090/TCP
NodePort:                 <unset>  30000/TCP
Endpoints:                10.244.0.3:9090
Session Affinity:         None
External Traffic Policy:  Cluster
Internal Traffic Policy:  Cluster
Events:                   <none>
```