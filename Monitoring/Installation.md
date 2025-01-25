# Prometheus and Grafana via HELM
## Install Helm Chart
 ```
 curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
 chmod 700 get_helm.sh
 ./get_helm.sh
```
- Add Helm Stable Charts for Your Local Client
 ```helm repo add stable https://charts.helm.sh/stable```

- Add Prometheus Helm Repository
 ```helm repo add prometheus-community https://prometheus-community.github.io/helm-charts```

- Create Prometheus Namespace
```
kubectl create namespace monitoring
kubectl get ns
```

- Install Prometheus using Helm
 ``` helm install kind-prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --set prometheus.service.nodePort=30000 --set prometheus.service.type=NodePort --set grafana.service.nodePort=31000 --set grafana.service.type=NodePort --set alertmanager.service.nodePort=32000 --set alertmanager.service.type=NodePort --set prometheus-node-exporter.service.nodePort=32001 --set prometheus-node-exporter.service.type=NodePort```

- Verify Prometheus installation
 ```kubectl get pods -n monitoring```

- Check the services file (svc) of the Prometheus
```kubectl get svc -n monitoring```

- To access the Prometheus and Grafana on browser we need to forward the port will using **Kind Cluster** & **Minikube** because the cluster running in docker
  ```
  kubectl port-forward svc/kind-prometheus-kube-prome-prometheus -n monitoring 9090:9090 --address=0.0.0.0 &
  kubectl port-forward svc/kind-prometheus-grafana -n monitoring 3000:80 --address=0.0.0.0 &

  ```
 - Retrieve Grafana Initial Admin Password
```
kubectl get secret prometheus-stack-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 -d && echo 
```
