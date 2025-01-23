# Custom Resource Definitions (CRDs)
Custom Resource Definitions (CRDs) in Kubernetes extend the Kubernetes API by allowing users to define custom resource types that behave just like native Kubernetes resources (e.g., Pods, Deployments). CRDs enable you to create and manage resources specific to your application or use case, adding new APIs to Kubernetes without modifying the core source code.

## Key Concepts of Custom Resource Definitions (CRDs):
-	Custom Resource (CR): A new resource type defined by the CRD. Once a CRD is created, users can create instances of that resource, just like with built-in Kubernetes objects.
-	Custom Controller: A custom controller is often used to manage the lifecycle of custom resources. For example, if you create a custom resource called MyApp, a custom controller would handle the logic of how MyApp behaves when it's created, updated, or deleted.
-	Custom Operator: Operators are custom controllers that automate complex tasks. They extend the controller pattern and manage the application lifecycle based on the state of custom resources.

## Creating a Custom Resource Definition (CRD):

### 1. Define the CRD: The first step in creating a CRD is to define the new resource and its schema using a crd.yml manifest.

Breakdown For CRD file:
-	group: This is the API group for the custom resource (e.g., example.com).
-	versions: The versions of your custom resource (e.g., v1).
-	scope: Can be Namespaced (specific to namespaces) or Cluster (cluster-wide).
-	names: Defines the resource name (plural, singular, kind) and short names for easy CLI access.

### 2. Apply the CRD: Once the CRD is defined, apply it to the cluster:
```
kubectl apply -f crd.yaml
```
After applying the CRD, you can now create instances of the MyApp resource.

### 3. Create Custom Resource Instances: After the CRD is created, you can define instances of the custom resource (CR) using the cr.yml
You can create this custom resource with:
```
kubectl apply -f  cr.yml
```

### Interact with the Custom Resource: Once the resource is created, you can list, describe, and manage it like any other Kubernetes resource:
```
kubectl get myapps
kubectl describe myapp myapp-sample
```

## CRD Schema Validation:
CRDs support OpenAPI-based schema validation. This allows Kubernetes to validate the structure of the custom resource before creation or updates. You can define schema properties in the openAPIV3Schema field of the CRD. For example, you can enforce that replicas is an integer and image is a string.

### Custom Controllers and Operators:
To make CRDs functional, you often build a custom controller or operator to handle events related to the custom resource (e.g., create, update, delete). The controller runs as a pod in the cluster and watches for changes to the custom resources, then performs actions accordingly.

For example:
-	When a MyApp resource is created, the controller can launch a set of NGINX pods based on the spec (e.g., replicas and image).
-	When the resource is deleted, the controller cleans up the related pods.
