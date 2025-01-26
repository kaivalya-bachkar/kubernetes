# Namaspace in Kubernetes
In Kubernetes (k8s), **namespaces** are a way to divide cluster resources between multiple users or applications. They provide a mechanism to isolate and manage groups of resources within a single Kubernetes cluster, allowing for better organization and segregation of environments, such as development, testing, and production. Here's how namespaces work:

## Key Points about Kubernetes Namespaces:

1. Logical Partitioning: Namespaces allow the creation of isolated environments within a cluster. Resources (pods, services, config maps, secrets, etc.) created in one namespace are invisible to other namespaces unless explicitly shared.

2. Default Namespace: If you don’t specify a namespace when creating a resource, Kubernetes will assign it to the **default** namespace.

3. System Namespaces:
   - `kube-system`: Contains Kubernetes system components (e.g., controllers, schedulers).
   - `kube-public`: Typically used for publicly accessible resources.
   - `kube-node-lease`: Holds node lease objects, which improve the performance of the node heartbeats.

4. Namespace Resource Quotas: You can set resource quotas on namespaces to limit the amount of CPU, memory, or other resources consumed by resources in a specific namespace.

5. Service Discovery: Services in a namespace are only accessible to pods in the same namespace unless a fully qualified domain name (FQDN) is used, such as `service-name.namespace.svc.cluster.local`.

6. Isolation: While namespaces provide isolation at the resource level, they do not provide network isolation. For network isolation, you need to use network policies.

### Basic Commands for Managing Namespaces:

- List all namespaces:
  ```bash
  kubectl get namespaces
  ```

- Create a new namespace:
  ```bash
  kubectl create namespace <namespace-name>
  ```

- Create a new namespace with manifest.yaml
  ```bash
  apiVersion: v1
  kind: Namespace
  metadata:
    name: <namespace-name> 
  ```
  
- Delete a namespace:
  ```bash
  kubectl delete namespace <namespace-name>
  ```

- View resources in a specific namespace:
  ```bash
  kubectl get pods --namespace <namespace-name>
  ```

- Switch between namespaces (To set a current namespace as default):
  ```bash
  kubectl config set-context --current --namespace=<namespace-name>
  ```

- Apply resources to a specific namespace:
  ```bash
  kubectl apply -f <manifest.yaml> --namespace=<namespace-name>
  ```

- Apply resources to a specific namespace with manifest.yaml:
  ```bash
  apiVersion: v1
  kind: Pod
  metadata:
    name: pod_name
    namespace: <namespace-name>
  ```
  
- To delete all resources inside a namespace:
  ```bash
  kubectl delete all --all --namespace=<namespace-name>
  ```
Namespaces help streamline Kubernetes resource management, especially in multi-tenant or large-scale environments.
