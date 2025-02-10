
## **🔹 Kubernetes Architecture & Components**
Kubernetes follows a **Master-Worker architecture** where:
- **Control Plane** manages the cluster.
- **Worker Nodes** run workloads.

### **🎮 Control Plane Components (Master Node)**
| Component                 | Purpose |
|---------------------------|---------|
| **API Server (`kube-apiserver`)** | The **entry point** for all commands (`kubectl` communicates with it). |
| **Controller Manager (`kube-controller-manager`)** | Manages controllers like **Deployments, ReplicaSets, Jobs, Endpoints, and Nodes**. |
| **Scheduler (`kube-scheduler`)** | Places pods onto worker nodes based on resource availability. |
| **etcd (Key-Value Store)** | Stores cluster state and configuration. **Critical for recovery**. |
| **Cloud Controller Manager** | Handles integration with cloud providers (AWS, GCP, Azure). |

### **⚙️ Worker Node Components**
| Component           | Purpose |
|---------------------|---------|
| **Kubelet**        | Ensures pods are running on the node and reports to the API server. |
| **Container Runtime** | Runs containers (Docker, containerd, CRI-O). |
| **Kube Proxy**     | Manages networking (service discovery, load balancing). |

### **🔹 Useful Commands**
```sh
kubectl get nodes -o wide
kubectl get pods -n kube-system
journalctl -u kubelet -f   # Check kubelet logs
```

---

## **🔹 Installing Kubernetes (kubeadm, minikube, k3s)**

### **1️⃣ kubeadm Installation (for production-like clusters)**
#### **Step 1: Install Dependencies**
```sh
apt update && apt install -y curl apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
apt update
apt install -y kubelet kubeadm kubectl
```

#### **Step 2: Initialize the Cluster (on the Master Node)**
```sh
kubeadm init --pod-network-cidr=192.168.0.0/16
```

#### **Step 3: Configure kubectl**
```sh
mkdir -p $HOME/.kube
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
chown $(id -u):$(id -g) $HOME/.kube/config
```

#### **Step 4: Deploy a Network Plugin (Flannel)**
```sh
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

#### **Step 5: Join Worker Nodes**
```sh
kubeadm join <MASTER_IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

#### **Verify Cluster Setup**
```sh
kubectl get nodes
```

---

### **2️⃣ Minikube Installation (for Local Development)**
```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start
kubectl get nodes
```

### **3️⃣ Lightweight Kubernetes with k3s**
```sh
curl -sfL https://get.k3s.io | sh -
kubectl get nodes
```

---

## **🔹 Managing Kubeconfig & Contexts**
### **Switching Between Kubernetes Clusters**
```sh
kubectl config get-contexts
kubectl config use-context my-cluster
```

### **Manually Setting Up Kubeconfig**
```sh
kubectl config set-cluster my-cluster --server=https://my-cluster.com
kubectl config set-credentials admin --username=admin --password=admin123
kubectl config set-context my-context --cluster=my-cluster --user=admin
kubectl config use-context my-context
```

---

## **🔹 TLS Certificates & Security**
### **Check Existing Certificates**
```sh
ls /etc/kubernetes/pki/
```

### **Manually Renew Kubernetes Certificates**
```sh
kubeadm certs renew all
```

### **Generate a New Admin Certificate**
```sh
openssl genrsa -out admin.key 2048
openssl req -new -key admin.key -out admin.csr -subj "/CN=admin/O=system:masters"
openssl x509 -req -in admin.csr -CA /etc/kubernetes/pki/ca.crt -CAkey /etc/kubernetes/pki/ca.key -CAcreateserial -out admin.crt -days 365
```

---

## **🔹 Backup & Restore etcd (Cluster State)**
### **Backup etcd**
```sh
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-backup.db
```

### **Restore etcd**
```sh
ETCDCTL_API=3 etcdctl snapshot restore /backup/etcd-backup.db
mv /backup/etcd-backup.db /var/lib/etcd
systemctl restart etcd
```

---

## **🔥 Key Commands to Memorize**
| Task | Command |
|------|---------|
| Get nodes | `kubectl get nodes -o wide` |
| Get control plane components | `kubectl get pods -n kube-system` |
| View logs of kubelet | `journalctl -u kubelet -f` |
| Restart kubelet | `systemctl restart kubelet` |
| Upgrade Kubernetes | `kubeadm upgrade apply v1.27.0` |
| Backup etcd | `ETCDCTL_API=3 etcdctl snapshot save /backup/etcd.db` |
| Restore etcd | `ETCDCTL_API=3 etcdctl snapshot restore /backup/etcd.db` |

---

## **✅ Summary**
- **Know Kubernetes architecture** (API Server, Controller, etcd, Kubelet, Proxy).
- **Set up clusters using kubeadm, minikube, or k3s**.
- **Manage `kubeconfig` and contexts**.
- **Understand TLS certificates** and how to **renew** them.
- **Upgrade Kubernetes** using `kubeadm upgrade`.
- **Back up & restore etcd** for disaster recovery.

---

[**🚀 Next Topic: Workloads & Scheduling**][obsidian://open?vault=Toyota&file=Personal%2FCKA%2F2%EF%B8%8F%E2%83%A3%20Workloads%20%26%20Scheduling%20(15%25)]

