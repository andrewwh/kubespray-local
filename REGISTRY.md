# Docker Registry
Host a private docker registry in the cluster

## Create Registry and Proxy

```
kubectl apply -f k8s/registry/registry-pv.yml
kubectl apply -f k8s/registry/registry-pvc.yml
kubectl apply -f k8s/registry/registry-deployment.yml
kubectl apply -f k8s/registry/registry-svc.yml
kubectl apply -f k8s/registry/registry-proxy-ds.yml
```

## Proxy to Cluster Registry

```
POD=$(kubectl get pods --namespace kube-system -l k8s-app=registry \
            -o template --template '{{range .items}}{{.metadata.name}} {{.status.phase}}{{"\n"}}{{end}}' \
            | grep Running | head -1 | cut -f1 -d' ')

kubectl port-forward --namespace kube-system $POD 5000:5000

```

## Docker tag
Tag your local image and push to the cluster. Use a image name as follows:
```
image: localhost:5000/user/container
```