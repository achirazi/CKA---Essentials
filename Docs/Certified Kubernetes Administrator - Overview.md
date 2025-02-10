
**📜 CKA Exam Overview**

• **Duration**: 2 hours

• **Format**: Performance-based, hands-on tasks

• **Passing Score**: ~66%

• **Environment**: You’ll get a terminal to interact with multiple clusters.

• **Topics Breakdown**:

• Cluster Architecture, Installation & Configuration (25%)

• Workloads & Scheduling (15%)

• Services & Networking (20%)

• Storage (10%)

• Troubleshooting (30%)



**⏳ Preparation Timeline (3-4 Months Plan)**

• **Month 1:** Learn core Kubernetes concepts and architecture.

• **Month 2:** Focus on Deployments, Services, Storage, and Security.

• **Month 3:** Practice troubleshooting and mock exams.

• **Final Weeks:** Optimize speed and master kubectl commands.

---

**📌 Core Topics You Need to Master for CKA**

  

**1️⃣ Cluster Architecture, Installation & Configuration (25%)**

• **Kubernetes Components**:

• API Server, Controller Manager, Scheduler, Etcd, Kubelet, Kube Proxy

• Difference between Control Plane & Worker Nodes

• **Installing Kubernetes**:

• Using kubeadm, k3s, and minikube

• Bootstrap a cluster (kubeadm init, kubeadm join)

• **Kubeconfig & Contexts**:

• Switching between clusters (kubectl config use-context)

• Understanding authentication & authorization (RBAC)

• **Certificates & Security**:

• TLS certificates and their locations (/etc/kubernetes/pki/)

• Managing Kubernetes users & API authentication

• **Cluster Upgrades**:

• Upgrading Kubernetes components (kubeadm upgrade)

  

**2️⃣ Workloads & Scheduling (15%)**

• **Pods, Deployments, ReplicaSets, and StatefulSets**

• kubectl run, kubectl create deployment, kubectl scale

• **Static Pods & DaemonSets**

• Creating static pods (/etc/kubernetes/manifests)

• **Jobs & CronJobs**

• Running temporary workloads (kubectl create job, kubectl create cronjob)

• **Taints, Tolerations, and Node Affinity**

• Prevent scheduling on certain nodes

• kubectl taint nodes, nodeSelector

• **PriorityClasses & Pod Disruption Budgets (PDBs)**

• Controlling eviction policies

  

**3️⃣ Services & Networking (20%)**

• **Cluster Networking Basics**

• How Pods communicate within the cluster

• Understanding Service types (ClusterIP, NodePort, LoadBalancer)

• **Network Policies**

• Restricting Pod-to-Pod communication (kubectl apply -f network-policy.yaml)

• **Ingress Controllers**

• Setting up an NGINX Ingress Controller

• Path-based and host-based routing

• **CoreDNS**

• Debugging DNS issues inside Pods (nslookup, dig)

• **CNI Plugins**

• Flannel, Calico, Weave – What they do

  

**4️⃣ Storage (10%)**

• **Persistent Volumes (PVs) & Persistent Volume Claims (PVCs)**

• kubectl get pv, kubectl get pvc

• **Storage Classes**

• Dynamically provisioning storage

• **ConfigMaps & Secrets**

• Mounting configs into Pods

• Encrypting Secrets at rest

• **Volume Types**

• emptyDir, hostPath, NFS, cloud provider volumes

  

**5️⃣ Troubleshooting (30%) (Very Important!)**

• **Debugging Pods & Nodes**

• kubectl logs, kubectl describe pod, kubectl exec

• Checking node status (kubectl get nodes, kubectl describe node)

• **Identifying CrashLoopBackOff & OOMKilled Issues**

• kubectl get events

• **Debugging Network Issues**

• kubectl get svc, kubectl describe service

• Testing connectivity (curl, netcat, ping)

• **Troubleshooting Worker Node Issues**

• Checking kubelet logs (journalctl -u kubelet)

• Restarting Kubernetes components (systemctl restart kubelet)

• **Troubleshooting Etcd Issues**

• Checking etcd logs and backups (etcdctl snapshot save)

• **Recovery Scenarios**

• Restoring from an etcd snapshot

---

**💡 Exam Strategies**

1. **🔥 Practice Speed & Efficiency**

• Learn kubectl shortcuts (e.g., kubectl get pods -o wide)

• Use kubectl explain for quick help

• Use vim, nano, or cat to edit YAML files faster

2. **💾 Bookmark the Kubernetes Documentation**

• Allowed during the exam → Use kubectl explain & search quickly

3. **📝 YAML Manifest Writing Practice**

• Be comfortable creating YAML files without using kubectl create

4. **⏳ Time Management**

• Spend **max 5 minutes per question**, flag difficult ones & return later

5. **🚀 Use Imperative Commands**

• Instead of writing YAML from scratch, use:

```
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml
```

• Then modify the file as needed.

---

**🛠 Hands-On Practice**

  

**🔹 Playgrounds & Labs**

• **Kubernetes Playground** – [https://katacoda.com](https://katacoda.com)

• **Play with Kubernetes** – [https://labs.play-with-k8s.com/](https://labs.play-with-k8s.com/)

• **Kubernetes the Hard Way (by Kelsey Hightower)** – [https://github.com/kelseyhightower/kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way)

  

**🔹 Mock Exam Platforms**

• **Killer.sh** (Best for realistic CKA simulations)

• **KodeKloud CKA Simulator**

• **Cloud Academy CKA Hands-on Labs**

  

**🔹 Minikube & Kind (Local Cluster Setup)**


---


**📚 Recommended Study Materials**

  

**🔹 Official Kubernetes Docs**

• [https://kubernetes.io/docs](https://kubernetes.io/docs)

• [https://kubernetes.io/docs/reference/kubectl/](https://kubernetes.io/docs/reference/kubectl/)

  

**🔹 CKA-Specific Courses**

• **KodeKloud CKA Course** (Best for hands-on labs)

• **Udemy: Certified Kubernetes Administrator by School of Devops®**

• **Linux Academy CKA Course** (Now part of A Cloud Guru)

---

**🚀 Final Tips for the CKA Exam**

  

✅ **Hands-on is key!** Do at least **30+ practice tasks** before the exam.

✅ **Time management** – Solve easy questions first, flag difficult ones.

✅ **Master kubectl commands** – Avoid writing YAML from scratch unless necessary.

✅ **Use kubectl explain & bookmarks** – Don’t memorize everything.

✅ **Know how to fix a broken cluster!** – Troubleshooting is 30% of the exam.