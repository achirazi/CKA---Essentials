
## **🔹 Cluster Management**
### **Check Cluster & Contexts**
```sh
kubectl config get-contexts
kubectl config use-context <context-name>
kubectl cluster-info
kubectl get nodes -o wide
```

### **Manage Namespaces**
```sh
kubectl get namespaces
kubectl create namespace my-namespace
kubectl delete namespace my-namespace
```

---

## **🔹 Pods & Deployments**
### **Create & Manage Pods**
```sh
kubectl run nginx --image=nginx --restart=Never
kubectl get pods -o wide
kubectl delete pod nginx
```

### **Create & Manage Deployments**
```sh
kubectl create deployment my-app --image=nginx --replicas=3
kubectl scale deployment my-app --replicas=5
kubectl rollout restart deployment my-app
kubectl rollout undo deployment my-app
```

### **Check Logs & Execute Commands in Pods**
```sh
kubectl logs my-pod
kubectl exec -it my-pod -- /bin/sh
```

---

## **🔹 Services & Networking**
### **Expose a Deployment as a Service**
```sh
kubectl expose deployment my-app --type=ClusterIP --port=80
kubectl expose deployment my-app --type=NodePort --port=80 --target-port=8080
```

### **Check Service Details**
```sh
kubectl get svc
kubectl describe svc my-service
kubectl get endpoints my-service
```

### **Test Networking Inside Cluster**
```sh
kubectl run busybox --image=busybox -it -- nslookup my-service
kubectl run curlpod --image=nginx --rm -it -- curl http://my-service:80
```

---

## **🔹 Storage**
### **Create a Persistent Volume & PVC**
```sh
kubectl create pvc my-pvc --storage=10Gi --access-mode=ReadWriteOnce
```

### **Attach PVC to a Pod**
```yaml
volumes:
  - name: storage
    persistentVolumeClaim:
      claimName: my-pvc
```

### **Check Persistent Volumes & Claims**
```sh
kubectl get pv
kubectl get pvc
kubectl describe pvc my-pvc
```

---

## **🔹 Troubleshooting**
### **Check Pod & Node Issues**
```sh
kubectl describe pod my-pod
kubectl get events
kubectl describe node my-node
kubectl get pods --field-selector=status.phase!=Running
```

### **Check Logs & Debugging**
```sh
kubectl logs my-pod
kubectl exec -it my-pod -- /bin/sh
kubectl get pods -n kube-system
```

### **Networking & DNS Issues**
```sh
kubectl get svc
kubectl get endpoints my-service
kubectl logs -n kube-system -l k8s-app=kube-dns
```

---

## **🔹 Exam Tips**
### **Time-Saving Commands**
```sh
kubectl create deployment my-app --image=nginx --dry-run=client -o yaml > my-app.yaml
kubectl explain pod.spec
```

### **Backup & Restore etcd**
```sh
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd-backup.db
ETCDCTL_API=3 etcdctl snapshot restore /backup/etcd-backup.db
```

---

## **✅ Summary**
- **Master `kubectl` shortcuts** for speed.
- **Check logs & events** to troubleshoot issues.
- **Use `kubectl explain` for quick reference.**
- **Switch contexts carefully** in multi-cluster environments.
- **Memorize common YAML patterns for efficiency.**


