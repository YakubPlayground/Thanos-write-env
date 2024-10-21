```mermaid
graph TD
    B[1 - Prometheus] -->|Visulisation| C[2 -Grafana] --> |Storage| A[3 - Thanos]
    subgraph 0 - Minikube Cluster
        A
        B
        C
        E
    end
    E[Helm  Charts] --> D[Bitnami Repo]
```