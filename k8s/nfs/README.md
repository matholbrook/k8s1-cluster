# How To

## Node Software

Any node that could run the nfs-provisioner pod needs to have an NFS client installed.
```bash
sudo apt install -y nfs-common
```

## Add the Helm NFS repo

```bash
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
```

## Create the NFS provisioner namespace

```bash
kubectl create ns nfs-provisioner
```

## Set NFS Server Env Vars

```bash
export NFS_SERVER=192.168.1.29
export NFS_EXPORT_PATH=/data/homelab/nfs/share
```

## Deploy Helm NFS Provisioner

```bash
$ helm -n  nfs-provisioner install nfs-provisioner-01 nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
    --set nfs.server=${NFS_SERVER} \
    --set nfs.path=${NFS_EXPORT_PATH} \
    --set storageClass.defaultClass=true \
    --set replicaCount=1 \
    --set storageClass.name=nfs-01 \
   --set storageClass.provisionerName=nfs-provisioner-01  
level=WARN msg="unable to find exact version; falling back to closest available version" chart=nfs-subdir-external-provisioner requested="" selected=4.0.18
NAME: nfs-provisioner-01
LAST DEPLOYED: Mon Nov 24 10:26:49 2025
NAMESPACE: nfs-provisioner
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
TEST SUITE: None
```
