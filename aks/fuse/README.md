### check all statfs calls on fuse file system on Linux node
 - run following command to collect statefs calls on fuse file systems for 10 minutes
```console
wget https://raw.githubusercontent.com/andyzhangx/demo/master/aks/fuse/statfs_count.bt
bpftrace statfs_count.bt
Counting vfs_statfs for cifs... Hit Ctrl-C to end.

Top 10 vfs_statfs process:
@counter[20748, telegraf]: 28
@counter[14652, node-exporter]: 35
```

the above testing result shows `telegraf` has made 28 statefs calls and node-exporter has made 35 statefs calls.

### workaround
 - if it's `node-exporter` issue, you could run following command to disable `node-exporter` service on every agent node
```console
kubectl apply -f https://raw.githubusercontent.com/andyzhangx/demo/master/aks/disable-node-exporter-service.yaml
```