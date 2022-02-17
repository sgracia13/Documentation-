# Manage Role Based Access Control (RBAC)
## Basics
- Role-based access control (RBAC) is a method of regulating access to computer or network resources 
based on the roles of individual users within an enterprise. In this context, access is the ability of 
an individual user to perform a specific task, such as view, create, or modify a file. 

- When specified RBAC (Role-Based Access Control) uses the rbac.authorization.k8s.io API group to drive 
authorization decisions, allowing admins to dynamically configure permission policies through the Kubernetes API.
- To enable RBAC, start the apiserver with `--authorization-mode=RBAC`

- The RBAC API declares four kinds of Kubernetes object: Role, ClusterRole, RoleBinding and ClusterRoleBinding. 
You can describe objects, or amend them, using tools such as kubectl, just like any other Kubernetes object.

## Role and ClusterRole
- An RBAC Role or ClusterRole contains rules that represent a set of permissions. Permissions are purely additive
(there are no "deny" rules).

- A Role always sets permissions within a particular namespace; when you create a Role, you have to specify the 
namespace it belongs in.

- ClusterRole, by contrast, is a non-namespaced resource. The resources have different names 
(Role and ClusterRole) because a Kubernetes object always has to be either namespaced or not namespaced; it can't be both.

- ClusterRoles have several uses. You can use a ClusterRole to:

1. define permissions on namespaced resources and be granted within individual namespace(s)
2. define permissions on namespaced resources and be granted across all namespaces
3. define permissions on cluster-scoped resources

- If you want to define a role within a namespace, use a Role; if you want to define a role cluster-wide, use a ClusterRole.

## RoleBinding and ClusterRoleBinding





## Use kubeadm to install a basic cluster

- Initialize Control Plane Node. The Control Plane Node is where all of the control plane 
components run including etcd and api server. 

- 
