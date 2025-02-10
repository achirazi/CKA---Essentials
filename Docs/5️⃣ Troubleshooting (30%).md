

## **🔹 Understanding Kubernetes Troubleshooting**
Troubleshooting in Kubernetes involves diagnosing and resolving issues related to:
- **Pods & Containers** (Crashes, Pending, OOMKills)
- **Nodes & Networking** (Unavailable Nodes, DNS Issues, Service Failures)
- **Control Plane Issues** (API Server, Scheduler, Controller Manager)
- **Storage Failures** (PVCs not binding, Volume Errors)

---

## **🔹 Troubleshooting Pods & Containers**
### **1️⃣ Checking Pod Status**
```sh
kubectl get pods -o wide
kubectl describe pod my-pod
kubectl logs my-pod
kubectl exec -it my-pod -- /bin/sh
```
### **2️⃣ Common Pod Issues & Fixes**
| Issue | Solution |
|--------|-----------|
| **CrashLoopBackOff** | Check logs: `kubectl logs my-pod` |
| **ImagePullBackOff** | Verify image exists, check repo access |
| **OOMKilled** | Increase memory limits in Pod spec |
| **ContainerCreating** | Check node status, storage mounts |
| **Pod Stuck in Pending** | Check `kubectl describe pod` for scheduling errors |

---

## **🔹 Troubleshooting Nodes**
### **3️⃣ Checking Node Health**
```sh
kubectl get nodes
kubectl describe node my-node
kubectl get events
```
### **4️⃣ Common Node Issues & Fixes**
| Issue | Solution |
|--------|-----------|
| **Node Not Ready** | Check `kubectl describe node`, restart kubelet |
| **DiskPressure / MemoryPressure** | Free up disk/memory or increase node capacity |
| **Pods not scheduling on node** | Check taints with `kubectl describe node` |
| **Network Unreachable** | Verify CNI plugin, check `kubectl get pods -n kube-system` |

---

## **🔹 Troubleshooting Services & Networking**
### **5️⃣ Debugging Services**
```sh
kubectl get svc
kubectl describe svc my-service
kubectl get endpoints my-service
```
### **6️⃣ Testing Network Connectivity**
```sh
kubectl run busybox --image=busybox --restart=Never -it -- nslookup my-service
kubectl run curlpod --image=nginx --rm -it -- curl http://my-service:80
```
### **7️⃣ Common Service Issues & Fixes**
| Issue | Solution |
|--------|-----------|
| **Service has no endpoints** | Verify pod labels match service selector |
| **Pods cannot communicate** | Check `kubectl get networkpolicy` |
| **DNS resolution failure** | Restart CoreDNS, check logs `kubectl logs -n kube-system -l k8s-app=kube-dns` |

---

## **🔹 Troubleshooting Control Plane Issues**
### **8️⃣ Checking Control Plane Components**
```sh
kubectl get pods -n kube-system
kubectl describe pod kube-apiserver -n kube-system
journalctl -u kubelet -f
```
### **9️⃣ Common Control Plane Issues & Fixes**
| Issue | Solution |
|--------|-----------|
| **API Server Unreachable** | Restart `kube-apiserver`, check firewall rules |
| **Scheduler Not Assigning Pods** | Restart `kube-scheduler`, check logs |
| **Controller Manager Failing** | Check logs with `kubectl logs -n kube-system kube-controller-manager` |

---

## **🔹 Troubleshooting Storage Issues**
### 1️⃣0️⃣ Debugging PVC & Storage Issues**
```sh
kubectl get pvc
kubectl describe pvc my-pvc
kubectl get pv
kubectl describe pv my-pv
```
### **1️⃣1️⃣ Common Storage Issues & Fixes**
| Issue | Solution |
|--------|-----------|
| **PVC stuck in Pending** | Ensure StorageClass exists, check `kubectl get storageclass` |
| **Pod cannot mount volume** | Verify PV-PVC binding, restart pod |
| **Filesystem permission issues** | Use `fsGroup` in SecurityContext |

---

## **🔹 Backup & Restore etcd (Cluster State)**
### 1️⃣2️⃣ Backup etcd**
```sh
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-backup.db
```
### **1️⃣3️⃣ Restore etcd**
```sh
ETCDCTL_API=3 etcdctl snapshot restore /backup/etcd-backup.db
mv /backup/etcd-backup.db /var/lib/etcd
systemctl restart etcd
```

---

## **✅ Summary**
- **Pods:** Use `kubectl logs` and `kubectl describe pod` for debugging.
- **Nodes:** Check `kubectl describe node` and node events.
- **Services:** Verify selectors, endpoints, and CoreDNS.
- **Control Plane:** Restart API Server, Scheduler, Controller Manager.
- **Storage:** Verify PVC, PV, and StorageClasses.
- **etcd:** Regular backups and recovery planning.

---

[**🚀 Next Topic: Exam Tips & Best Practices**][obsidian://open?vault=Toyota&file=Personal%2FCKA%2F%F0%9F%93%8C%20Exam%20Tips%20%26%20Best%20Practices]

