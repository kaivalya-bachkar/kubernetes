# Kubernetes RBAC Setup

This guide provides instructions for creating roles, cluster roles, role bindings, and cluster role bindings in a Kubernetes cluster. RBAC (Role-Based Access Control) allows you to control access to resources within the cluster based on user roles and permissions.

## Role
The role.yml file contains the configuration for creating a role named pod-reader. The role allows the user to perform actions like get, watch, and list on pods resources.


### To apply this role:

```
kubectl apply -f role.yaml
```

### To check the created role:
```
kubectl get role
```

## Role Binding
The rolebinding.yml file defines a role binding named read-pods that binds the pod-reader role to the user jack in the default namespace.


### To apply this role binding:

```
kubectl apply -f rolebinding.yaml
```

### To check the created role binding:

```
kubectl get rolebinding
```

### To check the permissions of the jack user:

```
kubectl auth can-i get pod --as jack
```

## Cluster Role
The clusterrole.yml file contains the configuration for creating a cluster role named secret-reader. This cluster role allows the user to perform actions like get, watch, and list on secrets resources.


### To apply this cluster role:

```
kubectl apply -f clusterrole.yaml
```

### To check the created cluster role:

```
kubectl get clusterrole
```

## Cluster Role Binding (Namespace-level)
The clusterrolebindingns.yml file defines a role binding named read-secrets that binds the secret-reader cluster role to the user dev in the development namespace.


### To apply this role binding:

```
kubectl apply -f clusterrolebindingns.yaml
```

### To check the created role binding:

```
kubectl get clusterrolebindingns
```

### To check the permissions of the dev user in the development namespace:

```
kubectl auth can-i get secret --as dev -n development
```

## Cluster Role Binding
The clusterrolebinding.yml file contains the configuration for creating a cluster role binding named read-secrets-global. This cluster role binding binds the secret-reader cluster role to the user riya globally.


### To apply this cluster role binding:

```
kubectl apply -f clusterrolebinding.yaml
```

### To check the created cluster role binding:

```
kubectl get clusterrolebinding
```

### To check the permissions of the riya user across all namespaces:

```
kubectl auth can-i get secret --as tom -A
```
