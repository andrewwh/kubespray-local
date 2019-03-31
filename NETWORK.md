# Network troubleshooting

## Enable route to API server
CoreDns uses the cluster ip address for kubernetes API. This does not appear to route. So you may need to add a manual route on each host:
```
ip route add 10.233.0.0/16 dev eth1 src 172.17.8.101
```

## Reset weave meta data
```
kubectl exec -n kube-system weave-net-ptkb8 -c weave -- /home/weave/weave --local status
kubectl exec -n kube-system weave-net-ptkb8 -c weave -- /home/weave/weave --local report
```

```
rm /var/lib/weave/weave-netdata.db
```

## Contrack for kube-proxy on Ubuntu
Kube proxy may need conntract (for Ubunut)
```
sudo apt install conntrack
```