# gd-k8s-tutorial
Gnomon Digital K8S and IaC tutorial

# Kubernetes RBAC Configuration

This repository contains YAML configurations for managing roles and role bindings (RoleBindings and ClusterRoleBindings) in a Kubernetes cluster. These configurations define and assign specific permissions to different users and groups.

## Repository Contents

- `Role.yaml`: Defines several Kubernetes roles with specific permissions for different types of resources.
- `RoleBindings.yaml`: Defines role bindings (RoleBindings) to associate specific users with the defined roles.
- `ClusterRole.yaml`: Defines a ClusterRole with specific permissions for deployment resources.
- `ClusterRoleBinding.yaml`: Defines a cluster role binding (ClusterRoleBinding) to associate a specific user with the defined ClusterRole.

## File Details

### Role.yaml

This file defines several roles with specific permissions:

- `pod-reader`: Allows creating, getting, watching, and listing pods.
- `service-manager`: Allows managing services (getting, listing, watching, creating, updating, patching, deleting).
- `deployment-manager`: Allows managing deployments (getting, listing, watching, creating, updating, patching, deleting).
- `secret-manager`: Allows managing secrets (getting, listing, watching, creating, updating, patching, deleting).

### RoleBindings.yaml

This file defines role bindings to associate specific users with the defined roles:

- `pod-reader-binding`: Associates the user `nom@entreprise.com` with the `pod-reader` role.
- `secret-manager-binding`: Associates the user `ju****@**************.com` with the `secret-manager` role.
- `cluster-admin-binding-alice`: Associates the user `g*****@**************.com` with the `cluster-admin` ClusterRole.

### ClusterRole.yaml

This file defines a ClusterRole with specific permissions for deployment resources:

- `deployment-manager`: Allows managing deployments (getting, listing, watching, creating, updating, patching, deleting).

### ClusterRoleBinding.yaml

This file defines a cluster role binding to associate a specific user with the defined ClusterRole:

- `deployment-manager-binding`: Associates the user `admin` with the `deployment-manager` ClusterRole.

## Usage

To apply these configurations to your Kubernetes cluster, use the `kubectl apply` command:

```sh
kubectl apply -f Role.yaml
kubectl apply -f RoleBindings.yaml
kubectl apply -f ClusterRole.yaml
kubectl apply -f ClusterRoleBinding.yaml

## Testing

Testing the RBAC configurations is essential to ensure that the defined roles and bindings work as expected. This section outlines the steps to verify the RBAC settings using the kubectl auth can-i command and the --as flag for impersonation.


### Example Commands


#### Verify if the user nom@entreprise.com can list pods:
```sh
kubectl auth can-i list pods --as=nom@entreprise.com


#### Check if the user ju****@**************.com can create secrets:
```sh
kubectl auth can-i create secrets --as=ju****@**************.com


#### Confirm if the user admin can delete deployments:
```sh
kubectl auth can-i delete deployments --as=admin


#### Ensure the user g*****@**************.com has cluster-admin privileges:
```sh
kubectl auth can-i '*' '*' --as=g*****@**************.com
