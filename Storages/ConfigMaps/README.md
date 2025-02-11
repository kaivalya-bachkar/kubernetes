In Kubernetes, **ConfigMaps** are used to store configuration data in key-value pairs. This configuration data can be consumed by Pods and used to configure applications without hardcoding values within the container images. ConfigMaps allow you to decouple configuration artifacts from application containers, making it easier to manage application configurations across environments.

### Use Cases:
- Store configuration files, environment variables, command-line arguments, or any other configuration data.
- Inject configuration values into Pods as environment variables or mount them as files.

### Ways to Use ConfigMaps:
1. **As Environment Variables** in a Pod.
2. **As Command-line Arguments**.
3. **As Configuration Files** by mounting them as volumes.

---

### Step 1: Create a ConfigMap

You can create a ConfigMap from a file, literal values, or directly from a manifest.

#### 1.1: Create a ConfigMap from Literal Values

You can create a ConfigMap using the `kubectl create configmap` command.

```bash
kubectl create configmap my-config --from-literal=APP_MODE=production --from-literal=LOG_LEVEL=info
```

This creates a ConfigMap named `my-config` with two key-value pairs:
- `APP_MODE=production`
- `LOG_LEVEL=info`

#### 1.2: Create a ConfigMap from a File

You can create a ConfigMap from a file, such as a configuration file.

```bash
kubectl create configmap my-config --from-file=app-config.yaml
```

If you have an `app-config.yaml` file, this command creates a ConfigMap where the contents of the file are stored under a key named `app-config.yaml`.

#### 1.3: Create a ConfigMap from a Manifest

Here’s an example of a ConfigMap defined in a YAML manifest:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_MODE: production
  LOG_LEVEL: info
  config.json: |
    {
      "setting1": "value1",
      "setting2": "value2"
    }
```

### Step 2: Using ConfigMaps in Pods

You can use a ConfigMap in your Pod in different ways, such as environment variables, volume mounts, or command-line arguments.

#### 2.1: Using ConfigMap as Environment Variables

You can inject the key-value pairs from a ConfigMap into a container as environment variables.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: busybox
    env:
    - name: APP_MODE
      valueFrom:
        configMapKeyRef:
          name: my-config
          key: APP_MODE
    - name: LOG_LEVEL
      valueFrom:
        configMapKeyRef:
          name: my-config
          key: LOG_LEVEL
    command: [ "printenv" ]
```

In this example:
- The ConfigMap `my-config` is used to inject the `APP_MODE` and `LOG_LEVEL` values as environment variables into the container.
- The `printenv` command will print the environment variables, which will include `APP_MODE=production` and `LOG_LEVEL=info`.

#### 2.2: Using ConfigMap as a Volume

You can also mount a ConfigMap as a volume, where each key in the ConfigMap becomes a file in the volume, and the corresponding value becomes the file's content.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: my-config
```

In this example:
- The ConfigMap `my-config` is mounted as a volume at `/etc/config` inside the container.
- Each key in the ConfigMap (e.g., `APP_MODE` and `LOG_LEVEL`) becomes a file in `/etc/config`, and the values become the contents of those files.

#### 2.3: Using ConfigMap as Command-line Arguments

You can pass values from a ConfigMap as command-line arguments to your container.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: busybox
    command: [ "echo" ]
    args:
      - "$(APP_MODE)"
    env:
    - name: APP_MODE
      valueFrom:
        configMapKeyRef:
          name: my-config
          key: APP_MODE
```

In this example:
- The value of `APP_MODE` from the ConfigMap is passed as a command-line argument to the container, and the container will echo `production`.

### Updating ConfigMaps

ConfigMaps can be updated dynamically, and Kubernetes will automatically make the updated values available to the Pods consuming the ConfigMap.

1. Update a ConfigMap using the `kubectl apply` command:

```bash
kubectl apply -f my-configmap.yaml
```

2. Rolling updates: When a ConfigMap is updated, the Pods using it will not be restarted automatically. However, if the ConfigMap is mounted as a volume, the changes will be reflected in the volume within a few minutes.

### Best Practices for Using ConfigMaps:

1. **Environment-Specific Configurations**: Use ConfigMaps to manage environment-specific configurations, keeping them separate from the application code.
2. **Avoid Sensitive Data**: ConfigMaps are not encrypted by default and should not be used to store sensitive information such as passwords or API keys. For sensitive data, use **Secrets**.
3. **Decouple Configurations**: Decouple configurations from your application’s container images to improve portability and make it easier to manage different configurations across different environments (e.g., development, testing, production).

### Summary:
- **ConfigMaps** in Kubernetes are used to store configuration data in key-value pairs and are consumed by Pods as environment variables, files, or command-line arguments.
- They allow decoupling configuration data from application containers.
- ConfigMaps are suitable for managing non-sensitive configurations, and for sensitive data, Kubernetes **Secrets** should be used.

