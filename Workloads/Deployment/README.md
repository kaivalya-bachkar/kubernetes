# Deployment in Kubernetes

### What is a Deployment?
A Deployment in Kubernetes is a resource that manages the rollout, scaling, and updates of a set of Pods (containers). It ensures that the desired number of Pod replicas are running at all times.

### How it Works
- Controller: The Deployment controller monitors the Pods and ensures the desired state (replica count, image version, etc.) is met.
- Scaling & Updates: Automatically handles scaling (up/down) and rolling updates to ensure minimal downtime.
- Self-Healing: If a Pod fails, the Deployment creates a new one to maintain the desired state.

### What It's Used For
- Running stateless applications (e.g., web servers).
- Managing rolling updates, rollbacks, and scaling.
- Ensuring high availability by managing multiple replicas of Pods.
- Continuous Delivery/Continuous Deployment (CI/CD).

### Steps to Deploy a Deployment:
- You will see 1 manifest in the same directory (Deployment) with name deployment.yml.
- Copy the content of the manifest and run the following command to deploy it.
  ```bash
  kubectl apply -f deployment.yml
  ```
  
  - Check or Enlist a Deployment:
  ```bash
  kubectl get deployment/<deployment_name>
  ```

- Check details of a Deployment:
  ```bash
  kubectl describe deployment/<deployment_name>
  ```

- Check full details of a Deployment yaml file:
  ```bash
  kubectl get deployment/<deployment_name> -o yaml
  ```

- Change the Current Deployment Image with command:
  ```bash
  kubectl set image deployment/<deployment_name> <container_name>=<iamge_name>
  ```

- Check Revision or Rollout history of a Deployment:
  ```bash
  kubectl rollout history deployment/<deployment_name>
  ```
  
  - Check a status of a rollout Deployment:
  ```bash
  kubectl rollout status deployment/<deployment_name>
  ```

- Rollout to Previous version of Revision of Deployment:
  ```bash
  kubectl rollout undo deployment/<deployment_name>
  ```

- Rollout to Specific version of Revision of Deployment:
  ```bash
  kubectl rollout undo deployment/<deployment_name> --to-revision=<revision_number>
  ```

- Change or Rename the change-cause details from <none> to any specific Deployment:
  ```bash
  kubectl annotate deployment/<deployment_name> kubernetes.io/change-cause="<revision_number>"
  ```
  or
  ```bash
  kubectl annotate deployments.app/<deployment_name> kubernetes.io/change-cause="<revision_number>"
  ```

 - Delete a Deployment:
   ```bash
   kubectl delete deployment/<deployment_name>
   ``` 
