# Useful Kubernetes Commands

## Kill all Pods
Kubernetes will automatically restart pods if killed:
```
kubectl get pods -n kube-system -oname | grep coredns | xargs kubectl delete -n kube-system

```