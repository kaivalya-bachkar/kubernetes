In Kubernetes (K8s), a **ReplicaSet** is a resource used to ensure that a specified number of pod replicas are running at any given time. It guarantees the availability of a certain number of identical pods in a cluster. If a pod crashes or is deleted, the ReplicaSet automatically creates a new pod to maintain the desired number of replicas.

### Key Features of ReplicaSet:
- **Self-healing**: Ensures that the specified number of pod replicas is always running.
- **Scaling**: Can scale the number of pods up or down by changing the `replicas` field.
- **Selection**: Uses a label selector to identify the pods it manages.

### ReplicaSet Example

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx
        ports:
        - containerPort: 80
```

### Breakdown:
1. **`replicas`**: Defines how many pods should be running (3 in this case).
2. **`selector`**: This identifies the pods that the ReplicaSet will manage using the label `app: my-app`.
3. **`template`**: Specifies the pod definition (containers, images, etc.). If no matching pods exist, the ReplicaSet creates new ones based on this template.

### Difference Between ReplicaSet and ReplicationController:
- A **ReplicationController** is the older form of ensuring pod replication. **ReplicaSet** is the newer, more efficient version with better label selection.

In modern Kubernetes applications, **Deployments** are typically used over ReplicaSets because they provide additional features like rolling updates and rollback.
