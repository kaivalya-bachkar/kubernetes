# Pod in Kubernetes (K8s)
A **Pod** is the smallest and simplest unit that you can create or deploy. Pods represent a single instance of a running process in your cluster and can contain one or more tightly coupled containers.

### Key concepts about Pods in Kubernetes:

1. **Single or Multi-Container Pods**:
   - Pods usually have **one container** but can have multiple if the containers are closely related and need to share resources (e.g., sidecar containers).
   - Containers within a Pod share the same network namespace, IP address, and storage volumes.

2. **Lifecycle**:
   - Pods have a specific **lifecycle**. They are created, start running, and eventually die when their work is done or if they encounter a failure. When a Pod dies, it is not restarted by default; instead, a new Pod is created.
   - Pods are typically managed by higher-level controllers like **Deployments**, **DaemonSets**, **StatefulSets**, which handle the replication and scaling of Pods.

3. **Networking**:
   - Each Pod is assigned a **unique IP address** within the cluster. Containers inside a Pod can communicate with each other using `localhost` and shared ports.

4. **Volumes**:
   - Containers in a Pod share the same **storage volumes**. This allows them to persist data or share data between containers.

5. **Pod Status**:
   - Pods can be in different phases such as **Pending**, **Running**, **Succeeded**, **Failed**, and **Unknown**, depending on their current state.

6. **Pod Templates**:
   - When you define a **Deployment** or other Kubernetes object, you specify a **Pod template**. This template is used by the controller to create new Pods that match the configuration.

### Controllers Managing Pods:
- **Deployments** ensure that the desired number of Pods are running at all times and manage rolling updates to ensure zero downtime.
- **StatefulSets** are used for stateful applications, ensuring that Pod identity is preserved across restarts.
- **DaemonSets** run one Pod on each node in the cluster.

## Steps to Deploy Pod:

- Check or Enlist the pods:
  ```bash
   kubectl get pods/pod/po
  ```

- Check all the pods from system:
  ```bash
  kubectl get pods/pod/po -A
  ```

- Create a pod:
  ```bash
  kubectl run <pod_name> --image <image_name>
  ```

- Check the IP of pods:
  ```bash
  kubectl get pods -o wide
  ```
  
- Create a pod with Manifest.yml:
  ```bash
  kubectl apply -f <manifest.yml>
  ```  
  Manifest File:
  ```yml
   apiVersion: v1
   kind: Pod
   metadata:
     name: mypod
   spec:
     containers:
     - name: nginxcont
       image: nginx
       ports:
       - containerPort: 80
   ```
- In this example:
   - - A Pod named `my-app-pod` is defined.
   - - It runs a single container using the `nginx` image.
   - - The container listens on port 80.

- Execute or Run a pod:
  ```bash
   kubectl exec -it <pod_name> /bin/bash
  ```

- Check the logs of a pod:
  ```bash
   kubectl logs <pod_name>
  ```

- Delete a specific pod:
  ```bash
  kubectl delete <pod_name>
  ```
 
- Delete a multiple pods:
  ```bash
  kubectl delete <pod_name> --all
  ```
- Delete a pod forcefully:
  ```bash
  kubectl delete <pod_name> --all --force
  ```   
Pods are the foundation of all Kubernetes applications. They allow you to define how applications are deployed and interact with the environment in a controlled, scalable, and manageable way.
