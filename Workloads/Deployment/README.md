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
  
