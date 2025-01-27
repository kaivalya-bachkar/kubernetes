# Replication Controller in Kubernetes
A **Replication Controller (RC)** in Kubernetes is a mechanism that ensures a specified number of pod replicas are running at all times. It is responsible for maintaining the desired state of replicas by creating or deleting pods as needed. If a pod goes down or is terminated, the Replication Controller ensures that a new one is started to replace it, maintaining the availability and reliability of your applications.

### Key Features:
- **Ensures availability**: Guarantees that the desired number of pod replicas are running.
- **Scaling**: Can be used to scale the number of replicas up or down.
- **Self-healing**: Automatically replaces failed or terminated pods.
  
### Components of a Replication Controller:
1. **Selector**: Defines which pods are managed by the Replication Controller. The selector matches labels assigned to pods.
2. **Replicas**: Specifies the desired number of pod replicas that should be running.
3. **Pod Template**: Defines the pod's configuration, such as the containers to run, volumes, etc., that will be replicated.

### Limitations:
- Replication Controllers have largely been replaced by **Deployments**, which offer more advanced features like rolling updates and rollbacks. While RCs are still supported, it's recommended to use Deployments for more robust replication and management.

## Steps to deploy Replication Controller:
- You will see 1 manifest in the same directory (Replication Controller) with name replicationcontroller.yml.
- Copy the content of the manifest and run the following command to deploy it.
  ```bash
  kubectl apply -f replicationcontroller.yml
  ```

- Check or Enlist a Replication Controller:
  ```bash
  kubectl get rc
  ```

- Check details of a Replication Controller:
  ```bash
  kubectl describe rc/<replicationcontroller-name>
  ```

- Scale-UP or Scale-Down a Replication Count:
  ```bash
  kubectl scale rc/<replicationcontroller-name> --replicas=<count>
  ```

 - Delete a Replication Controller:
   ```bash
   kubectl delete rc/<replicationcontroller-name>
   ``` 
