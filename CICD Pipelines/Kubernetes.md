**Kubernetes Pods** are the smallest deployable units in Kubernetes. They represent a single instance of a running process in your cluster.

### Key Concepts:

- **Single or Multiple Containers**: A pod can contain one or more containers that share the same network and storage.
    
- **Shared Resources**:
    
    - **IP Address**: All containers in a pod share the same IP.
        
    - **Volumes**: Storage is shared among containers in a pod.
        
- **Use Case**: Usually, one container per pod is common. Multiple containers are used when they need to work closely together (like a helper or sidecar container).
    
### Example (YAML):
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: nginx
    ports:
    - containerPort: 80
```
### ✅ **Create a Pod**

 From a YAML file

1. Save the YAML (like the one shown earlier) as `mypod.yaml`.
    
2. Run:
```
kubectl apply -f mypod.yaml
```

### 🔍 **Check Pod Status**
```
kubectl get pods
```

### 📄 **Get Detailed Info**
```
kubectl describe pod mypod
```

### 📦 **See Pod Logs**

```
kubectl logs mypod
```

### 🔁 **Execute a Command Inside Pod**

```
kubectl exec -it mypod -- /bin/bash
```

### ❌ **Delete a Pod**
```
kubectl delete pod mypod
```
