# StatefulSet
In Kubernetes, a StatefulSet is used to manage stateful applications, providing stable, persistent storage, ordered deployment and scaling, and unique network identifiers. 

### Key Features of StatefulSet

- Stable pod identifiers: Each pod in the StatefulSet has a predictable name like `<statefulset-name>-0`, `<statefulset-name>-1`, etc.
- Stable storage: Each pod can have its own persistent volume that is not affected by scaling or restarts.
- Ordered deployment and scaling: Pods are created and deleted sequentially.
- Ordered, graceful termination: Pods are terminated in reverse order of creation.
- Pod startup and termination guarantee: Each pod in the StatefulSet will start in a particular order and be shut down in the reverse order.

## Steps to deploy StatefulSet:
- You will see 1 manifest in the same directory (StatefulSet) with name statefulset.yml.
- Copy the content of the manifest and run the following command to deploy it.
  ```bash
    kubectl apply -f statefulset.yml
  ```
  
- To list all StatefulSets:
  ```bash
    kubectl get statefulsets
  ```

- To get more details about a specific StatefulSet:
  ```bash
    kubectl describe statefulset <statefulset-name>
  ```

- Each pod created by a StatefulSet has a unique name based on its index (e.g., `mysql-0`, `mysql-1`, etc.). To list the pods:
  ```bash
    kubectl get pods -l app=mysql
  ```
  
- To scale up or down the number of replicas in the StatefulSet:
  ```bash
    kubectl scale statefulset <statefulset-name> --replicas=<number>
  ```

- To delete a StatefulSet without deleting its persistent volumes (PVCs):
  ```bash
    kubectl delete statefulset <statefulset-name> --cascade=false
  ```

- To delete the StatefulSet along with the persistent volumes, just run:
  ```bash
    kubectl delete statefulset <statefulset-name>
  ```

- Update the container image or another aspect of the StatefulSet configuration, Kubernetes will automatically perform a rolling update of the pods:
  ```bash
    kubectl set image statefulset <statefulset-name> <container-name>=<new-image>
  ```
  Example:

  ```bash
    kubectl set image statefulset mysql mysql=mysql:8.0
  ```

- If you delete a pod managed by a StatefulSet, Kubernetes will automatically recreate it:
  ```bash
    kubectl delete pod <pod-name>
  ```

 - Delete a Statefulset:
   ```bash
   kubectl delete statefulset/<statefulset-name>
   ``` 
- To see the events related to your StatefulSet:
  ```bash
    kubectl get events --sort-by=.metadata.creationTimestamp
  ```

#### Persistent Volume Claims (PVCs)
- StatefulSet pods often use persistent volumes for storage. The `volumeClaimTemplates` in the YAML manifest allows Kubernetes to automatically create PVCs for each pod in the StatefulSet. To check the PVCs:
  ```bash
    kubectl get pvc -l app=mysql
  ```

#### Accessing StatefulSet Pods
- Each pod in a StatefulSet has a stable network identity that persists across rescheduling, based on its index. You can access a specific pod:
  ```bash
    kubectl exec -it <pod-name> -- /bin/bash
  ```
