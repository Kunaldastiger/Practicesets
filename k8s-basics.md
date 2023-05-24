
# Kubernetes Overview

## Master
The master components in a Kubernetes cluster are responsible for managing and controlling the cluster. The key master components are:

### kube-apiserver
- Acts as the brain of the cluster.
- Front-end for the Kubernetes control plane.
- Exposes the API (REST) and consumes JSON via a manifest file to describe the desired state.

### Cluster Store (etcd)
- Persistently stores the cluster state and configuration.
- Uses etcd, an open-source distributed key-value store.
- Acts as the source of truth for the cluster.

### Kube-controller-manager
- Manages various controllers responsible for maintaining the desired state of the cluster.
- Includes the node controller, endpoints controller, namespace controller, etc.
- Watches for changes and takes actions to reconcile the state.

### Kube-scheduler
- Watches the API server for new pods.
- Assigns work (pods) to nodes based on factors like hardware, workloads, affinity, etc.
- Makes scheduling decisions to ensure optimal resource utilization.

### Kubelet
- The main Kubernetes agent running on each node.
- Registers the node with the cluster.
- Watches the API server for pod assignments.
- Instantiates and manages pods on the node.
- Reports back to the master.
- Exposes an endpoint on port 10255.

### Container Engine
- Responsible for container management in Kubernetes.
- Handles tasks like pulling container images, starting/stopping containers, etc.
- Most commonly uses Docker as the container runtime.
- Can also use other container runtimes like CoreOS Rocket (rkt).

### Kube-proxy (Kubernetes networking)
- Handles networking for Kubernetes services.
- Assigns IP addresses to pods.
- Provides load balancing across all pods in a service.

### Pods
- Containers always run inside pods.
- All containers in a pod share the pod environment (e.g., IPC, shared memory, network).

### Pod Lifecycle
- Failed pods are not automatically brought back to life.
- Kubernetes ensures the desired number of pods are running by creating or destroying them as necessary.

### Replication Controllers
- Scale pods and maintain the desired state.
- Ensure a specified number of replicas of a pod are always running.

### Deployments
- Manage rolling updates and rollbacks of application deployments.
- Provide declarative updates to pods and replica sets.

### Services
- Provide stable networking and load balancing for pods.
- Allow pods to be accessed by other pods or external clients.

## Kubernetes Installation

### Prerequisites
In this setup, we will install:
- 1 master node
- 2 worker nodes

### Step 1: Disable SELinux
```
setenforce 0
sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
```

### Step 2: Enable br_netfilter module
```
modprobe br_netfilter
echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```

### Step 3: Disable swap
```
swapoff -a
# Comment out the swap entry in /etc/fstab
```

### Step 4: Install Docker prerequisites
```
yum install -y yum-utils device-mapper-persistent-data lvm2
```

### Step 5: Add Docker repo and install Docker
```
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker-ce
```

### Step 6: Configure Docker Cgroup Driver to systemd (continued)
```
sed -i '/^ExecStart/ s/$/ --exec-opt native.cgroupdriver=systemd/' /usr/lib/systemd/system/docker.service
```

### Step 7: Start and enable Docker
```
systemctl start docker
systemctl enable docker
```

### Step 8: Add Kubernetes repo and install Kubernetes components
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF

yum install -y kubelet kubeadm kubectl
```

### Step 9: Configure kubelet
```
systemctl enable kubelet
systemctl start kubelet
```

### Step 10: Initialize the master node
```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

### Step 11: Configure kubectl for the current user
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Step 12: Install a Pod network add-on (e.g., Calico)
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### Step 13: Join worker nodes to the cluster
```
kubeadm join <master-node-ip>:<master-node-port> --token <token> --discovery-token-ca-cert-hash <discovery-token-ca-cert-hash>
```

Congratulations! You have successfully installed and configured Kubernetes on your master node and joined the worker nodes to the cluster. You can now start deploying and managing your applications using Kubernetes.
