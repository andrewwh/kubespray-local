# Kubespray with Vagrant
[Kubespray](https://kubespray.io) with vagrant but not using the ansible local Vagrant file. Why not just use the vagrant that comes with Kubespray? I wanted to fully configure the kubespray and run as if it were remote hosts.

## Contents
- [Prerequisites](#pre-requisites)
- [Provision](#provision)
- [Kubernetes shortcuts](SHORTCUTS.md)
- [Network troubleshoot](NETWORK.md)
- [Setup a Local Docker Registry](REGISTRY.md)

## Pre-requisites
* Install ansible on your local machine
* Clone kubespray in the root of this directory

## Root ssh key
Copy your ssh key to each vagrant box root user. I created a vagrant public/private ssh key so that I can directly ssh as root to each machine. E.g.

```
ssh root@172.17.8.101
```

> TODO: Try to automate this

## Provision

### Stand up boxes
Run ``vagrant up`` to provision three vagrant boxes

_Run ansible against hosts:_
```
ansible-playbook -i ../inventory/local/hosts.ini --become --become-user=root cluster.yml
```

## Copy Cluster Configuration
Kubespray is configured with ``kubectl_localhost: true``, so the admin.conf is available in inventory/local/artifacts/

Copy this file to ~/.kube/config (on local machine, for current user)

## Kube Admin

_Create admin user and role_
```
kubectl apply -f k8s/kubeadm-user.yml
kubectl apply -f k8s/kubeadm-role.yml
```

_Get the admin user token_
```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```

_Proxy_
```
kubectl proxy
```

_Open Browser_
Open your browser to [Kube Admin](http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy)