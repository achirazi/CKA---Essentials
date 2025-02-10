# CKA---Essentials

Certified Kubernetes Administrator - Essential learning path created by me with a bit of help from my AI companion.

## Table of Contents – Kubernetes Documentation

### [**1️⃣ Certified Kubernetes Administrator - Overview**](Docs/Certified%20Kubernetes%20Administrator%20-%20Overview.m)
- Introduction to the CKA Exam
- Exam Duration, Format, and Passing Score
- Core Topics Breakdown:
  - Cluster Architecture, Installation & Configuration (25%)
  - Workloads & Scheduling (15%)
  - Services & Networking (20%)
  - Storage (10%)
  - Troubleshooting (30%)
- Preparation Strategy & Timeline
- Exam Strategies & Tips
- Hands-on Practice Recommendations
- Study Materials & Resources

### [**2️⃣ Cluster Architecture, Installation & Configuration (25%)**](Docs/1️⃣%20Cluster%20Architecture,%20Installation%20&%20Configuration%20(25%)Untitled.md)
- Kubernetes Architecture Overview
- Control Plane Components:
  - API Server
  - Controller Manager
  - Scheduler
  - etcd
  - Cloud Controller Manager
- Worker Node Components:
  - Kubelet
  - Container Runtime
  - Kube Proxy
- Installing Kubernetes:
  - kubeadm Setup
  - Minikube Installation
  - k3s for Lightweight Kubernetes
- Managing Kubeconfig & Contexts
- TLS Certificates & Security
- Cluster Upgrades & Maintenance
- etcd Backup & Restore
- Key Kubernetes Commands

## [**3️⃣ Workloads & Scheduling (15%)**](Docs/2️⃣%20Workloads%20&%20Scheduling%20(15%).md)
- Kubernetes Workloads Overview
- Pods & Containers:
  - Creating and Managing Pods
- Deployments:
  - Scaling, Rolling Updates, and Rollbacks
- ReplicaSets & StatefulSets:
  - Differences and Use Cases
- DaemonSets:
  - Node-wide Pod Scheduling
- Jobs & CronJobs:
  - Running Batch & Scheduled Workloads
- Pod Scheduling & Node Selection:
  - Node Affinity, Taints, and Tolerations

### [**4️⃣ Services & Networking (20%)**](Docs/3️⃣%20Services%20&%20Networking%20(20%).md)
- Understanding Kubernetes Networking
- Service Types:
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName
- Ingress & Ingress Controllers
- Network Policies
- CoreDNS & Debugging DNS Issues

### [**5️⃣ Storage (10%)**](Docs/4️⃣%20Storage%20(10%).md)
- Storage Concepts in Kubernetes
- Ephemeral Storage:
  - emptyDir Usage
- Persistent Volumes (PV) & Persistent Volume Claims (PVC)
- Storage Classes & Dynamic Provisioning
- Volume Types (hostPath, NFS, Cloud Storage)
- PVC Backup & Restore

### [**6️⃣ Troubleshooting (30%)**](Docs/5️⃣%20Troubleshooting%20(30%).md)
- Debugging Pods & Containers:
  - Checking Logs & Events
  - Identifying CrashLoopBackOff & ImagePullBackOff Issues
- Node-Level Troubleshooting:
  - Checking Node Health & Disk Pressure
- Services & Networking Issues:
  - Debugging Endpoints & Connectivity
- Control Plane Debugging:
  - API Server, Scheduler, Controller Manager Issues
- Persistent Storage Troubleshooting
- etcd Backup & Recovery

### [**7️⃣ Exam Tips & Best Practices**](Docs/📌%20Exam%20Tips%20&%20Best%20Practices.md)
- Understanding the CKA Exam Environment
- Time Management Strategies
- YAML Generation & Management Tips
- Kubernetes Shortcuts for Efficiency
- Backup & Restore Strategies for Cluster Recovery
- Essential Troubleshooting Commands
- Final Exam Preparation Checklist

### [**8️⃣ Kubernetes Cheat Sheet**](Docs/📌%20Kubernetes%20Cheat%20Sheet.md)
- Cluster Management Quick Commands
- Pods & Deployments Cheat Sheet
- Services & Networking Commands
- Storage Management Quick References
- Troubleshooting & Debugging Commands
- Exam Day Command References

### [**9️⃣ Kubernetes Extra Details & Good-to-Know Concepts**](Docs/📌%20Kubernetes%20Extra%20Details%20&%20Good%20to%20Know%20Concepts.md)
- API Groups & Resource Versions
- Workload Best Practices:
  - Resource Limits & Probes
- Advanced Networking Details:
  - Service Discovery & Ingress TLS Setup
- Stateful Applications in Kubernetes:
  - StatefulSets & Persistent Storage
- Kubernetes Security Considerations:
  - RBAC & Pod Security Contexts
- Kubernetes Optimization Tips
