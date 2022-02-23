# Manage Role Based Access Control (RBAC)
## Basics
- Role-based access control (RBAC) is a method of regulating access to computer or network resources 
based on the roles of individual users within an enterprise. In this context, access is the ability of 
an individual user to perform a specific task, such as view, create, or modify a file. 

- When specified RBAC (Role-Based Access Control) uses the rbac.authorization.k8s.io API group to drive 
authorization decisions, allowing admins to dynamically configure permission policies through the 
Kubernetes API.

- To enable RBAC, start the apiserver with `--authorization-mode=RBAC`

- The RBAC API declares four kinds of Kubernetes object: Role, ClusterRole, RoleBinding and 
ClusterRoleBinding. You can describe objects, or amend them, using tools such as kubectl, 
just like any other Kubernetes object.

## Role and ClusterRole
- An RBAC Role or ClusterRole contains rules that represent a set of permissions. Permissions are 
purely additive(there are no "deny" rules).

- A Role always sets permissions within a particular namespace; when you create a Role, you 
have to specify the namespace it belongs in.

- ClusterRole, by contrast, is a non-namespaced resource. The resources have different names 
(Role and ClusterRole) because a Kubernetes object always has to be either namespaced or not 
namespaced; it can't be both.

- ClusterRoles have several uses. You can use a ClusterRole to:

1. define permissions on namespaced resources and be granted within individual namespace(s)
2. define permissions on namespaced resources and be granted across all namespaces
3. define permissions on cluster-scoped resources

- If you want to define a role within a namespace, use a Role; if you want to define a role 
cluster-wide, use a ClusterRole.

## RoleBinding and ClusterRoleBinding





# Use kubeadm to install a basic cluster

- Initialize Control Plane Node. The Control Plane Node is where all of the control plane 
components run including etcd and api server. 

- Install kubeadm on your hosts
	 1. Verify MAC address and product_uuid are unique for every node
	 	-- `ip link` or `ifconfig -a` to check MAC address
	 	-- `sudo cat /sys/class/dmi/id/product_uuid` to check product_uuid 
	 2. Check network adapters
	 3. Let iptables see bridged traffic
	 	-- Make sure the br_netfilter module is loaded `lsmod | grep br_netfilter`
		-- To load it `sudo modprobe br_netfilter`
		-- Ensure iptables are set to '1' in sysctl config
			`cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
			br_netfilter
			EOF

			cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
			net.bridge.bridge-nf-call-ip6tables = 1
			net.bridge.bridge-nf-call-iptables = 1
			EOF
			
			sudo sysctl --system ` 

	4. Check required ports
		-- telnet 127.0.0.1 6443

	5. Install container runtime (docker/containerd)
	6. Install kubeadm, kubelet and kubectl
	7. 
# Manage a highly available Kubernetes cluster
- You can set up an HA cluster:

1. With stacked control plane nodes, where etcd nodes are colocated with control plane nodes
	- With this style of cluster, you will need to replicate the control plane node
	in order to get redundancy of etcd. If the control plane fails and is not replicated
	you lose data in the etcd instance and you cannot recover.
	Etcd is created in the control plane node when you create a cluster with kubeadm.

2. With external etcd nodes, where etcd runs on separate nodes from the control plane 
	- An HA cluster with external etcd is a topology where the distributed data 
	storage cluster provided by etcd is external to the cluster formed by the 
	nodes that run control plane components.
	
	- Like the stacked etcd topology, each control plane node in an external etcd topology 
	runs an instance of the kube-apiserver, kube-scheduler, and kube-controller-manager.
	 And the kube-apiserver is exposed to worker nodes using a load balancer. However, 
	etcd members run on separate hosts, and each etcd host communicates with the 
	kube-apiserver of each control plane node.This topology decouples the control plane 
	and etcd member. It therefore provides an HA setup where losing a control plane 
	instance or an etcd member has less impact and does not affect the cluster redundancy 
	as much as the stacked HA topology.However, this topology requires twice the number of 
	hosts as the stacked HA topology. A minimum of three hosts for control plane nodes and 
	three hosts for etcd nodes are required for an HA cluster with this topology.


# Upgrade a kudeadm cluster
	- At a high level, the steps you perform are:

	1. Upgrade the control plane
	2. Upgrade the nodes in your cluster
	3. Upgrade clients such as kubectl
	4. Adjust manifests and other resources based 
	on the API changes that accompany the new Kubernetes version


- Call kubeadm upgrade on the control plane node
- 
