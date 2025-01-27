# Daemonset in Kubernetes

### What is a daemonset?
- A DaemonSet in Kubernetes is a workload controller that ensures a pod runs on all or some nodes in a cluster
- Example: If you create a daemonset in a cluster of 3 nodes, then 3 pods will be created. No need to manage replicas.
- If you add another node to the cluster, a new pod will be automatically created on the new node.

### How it works
- A DaemonSet controller monitors for new and deleted nodes, and adds or removes pods as needed.

### What it's used for
- Logging collection
- Kube-proxy
- Weave-net
- Node monitoring

### Steps to deploy daemonset:

- You will see 1 manifest in the same directory (DaemonSet) with name daemonset.yml.
- Copy the content of the manifest and run the following command to deploy it.
  ```bash
  kubectl apply -f daemonset-deploy.yml
  ```

- Check or Enlist a DaemonSet:
  ```bash
  kubectl get ds
  ```

- Check details of a DaemonSet:
  ```bash
  kubectl describe ds/<daemonset-name>
  ```

- Check or Enlist of DaemonSet's pods with label :
  ```bash
  kubectl get pods --show-labels
  ```

- Check or Enlist of DaemonSet's pods with Specific label :
  ```bash
  kubectl get pods -l app=<label-name>
  ```

- Check or Enlist of DaemonSet's pods with Multiple label :
  ```bash
  kubectl get pods -l "app=<multiple_labels_name>"
  ```

 - Delete a DaemonSet:
   ```bash
   kubectl delete ds/<daemonset_name>
   ``` 
