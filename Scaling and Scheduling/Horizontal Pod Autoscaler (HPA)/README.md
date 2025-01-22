# Horizontal Pod Autoscaler (HPA) in Kubernetes
The Horizontal Pod Autoscaler (HPA) in Kubernetes automatically scales the number of pod replicas in a deployment, replication controller, or stateful set based on observed metrics such as CPU utilization, memory usage, or custom metrics. It adjusts the number of replicas to ensure the workload can handle varying loads, making it an essential tool for dynamically scaling applications.

## How Horizontal Pod Autoscaler Works:
- The HPA controller monitors the resource utilization of pods and compares it against the desired thresholds.
- If the utilization exceeds or falls below the set target, HPA adjusts the number of pods accordingly.

## Prerequisites:
The Metrics Server must be installed and configured in your cluster to provide metrics such as CPU and memory utilization. You can install it using:

### Ensure Metrics Server is Installed: 
To check if the metrics server is installed:

```
kubectl get apiservers | grep metrics
```

### To Install Metrics Server:
```
wget https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml | -o mertics-server-components.yml

```
### Open the Metrics-Server-Components.yml file:
- In the file add arg for tls
```
spec:
  containers:
    -args:
      - --kubelet-insecure-tls
```
- After Adding save the file

### Run the Metrics-Server:
```
kubectl apply -f mertics-server-components.yml
```

## Create the Horizontal Pod Autoscaler: Now, let's create the HPA to scale the deployment based on CPU utilization.
### Horizontal Pod Autoscaler
The hps.yml Create the HPA to scale the deployment based on CPU utilization.

- To Apply the hpa.yml
HPA configuration that scales based on CPU utilization:
```
kubectl apply -f hpa.yml
```

- To Check HPA Status: You can view the status of the Horizontal Pod Autoscaler using:
```
kubectl get hpa

```
## Pod Template:

### Ensure Resource Requests and Limits:
- In order for HPA to scale based on CPU or memory, you need to define resource requests in your pod template:
```
resources:
          requests:
            cpu: "100m"
            memory: "128Mi"
          limits:
            cpu: "200m"
            memory: "256Mi"
```

- To remove the HPA:
```
kubectl delete hpa <hpa-name>

```

- Ensure the metrics server is running properly. Check its logs with:
```
kubectl logs -n kube-system -l k8s-app=metrics-server

```
HPA needs valid resource requests/limits in your deployment. Make sure they are defined, and the metrics server is able to collect them.

Use the kubectl describe hpa command to see the detailed status and any potential errors.
