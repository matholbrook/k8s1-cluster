# How To

## Documentation URL

### Control Plane Node


sudo apt install etcd-client

ETCDCTL_API=3 etcdctl \
--endpoints=https://127.0.0.1:2379 \
--cacert=<ca-file> \
--cert=<cert-file> \
--key=<key-file> \
snapshot save <backup-file-location>

ETCDCTL_API=3 etcdctl --write-out=table snapshot status <backup-file-location>

