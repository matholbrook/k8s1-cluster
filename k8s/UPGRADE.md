# How To

## Official Docs
https://v1-33.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/

## Upgrade Plan
Version upgrade from 1.32.10 to 1.33.1

## High Level Upgrade Plan
The upgrade workflow at high level is the following:

1. Upgrade a primary control plane node.
2. Upgrade additional control plane nodes.
3. Upgrade worker nodes.

## High Level Pre-Upgrade Plan

1. Read the Release Notes (https://git.k8s.io/kubernetes/CHANGELOG)
2. Take an etcd backup

## KUBEADM Upgrade

### First Control Plane Node

modify kubeadm apt sources list file
```bash
sudo sed -i 's/v1.32/v1.33/' /etc/apt/sources.list.d/kubernetes.list
```

check kubeadm upgrade versions
```bash
sudo apt update
sudo apt-cache madison kubeadm
```

upgrade kubeadm
```bash
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm=1.33.6-1.1 && \
sudo apt-mark hold kubeadm
dpkg -l | grep kube
```

confirm upgrade
```bash
kubeadm version
```

verify the upgrade plan
```bash
$ sudo kubeadm upgrade plan
[preflight] Running pre-flight checks.
[upgrade/config] Reading configuration from the "kubeadm-config" ConfigMap in namespace "kube-system"...
[upgrade/config] Use 'kubeadm init phase upload-config --config your-config-file' to re-upload it.
[upgrade] Running cluster health checks
[upgrade] Fetching available versions to upgrade to
[upgrade/versions] Cluster version: 1.32.10
[upgrade/versions] kubeadm version: v1.33.6
I1121 20:50:08.328824   85410 version.go:261] remote version is much newer: v1.34.2; falling back to: stable-1.33
[upgrade/versions] Target version: v1.33.6
[upgrade/versions] Latest version in the v1.32 series: v1.32.10

Components that must be upgraded manually after you have upgraded the control plane with 'kubeadm upgrade apply':
COMPONENT   NODE       CURRENT    TARGET
kubelet     k8s1-vm1   v1.32.10   v1.33.6
kubelet     k8s1-vm2   v1.32.10   v1.33.6
kubelet     k8s1-vm3   v1.32.10   v1.33.6

Upgrade to the latest stable version:

COMPONENT                 NODE       CURRENT    TARGET
kube-apiserver            k8s1-vm1   v1.32.10   v1.33.6
kube-controller-manager   k8s1-vm1   v1.32.10   v1.33.6
kube-scheduler            k8s1-vm1   v1.32.10   v1.33.6
kube-proxy                           1.32.10    v1.33.6
CoreDNS                              v1.11.3    v1.12.0
etcd                      k8s1-vm1   3.5.24-0   3.5.24-0

You can now apply the upgrade by executing the following command:

        kubeadm upgrade apply v1.33.6

_____________________________________________________________________


The table below shows the current state of component configs as understood by this version of kubeadm.
Configs that have a "yes" mark in the "MANUAL UPGRADE REQUIRED" column require manual config upgrade or
resetting to kubeadm defaults before a successful upgrade can be performed. The version to manually
upgrade to is denoted in the "PREFERRED VERSION" column.

API GROUP                 CURRENT VERSION   PREFERRED VERSION   MANUAL UPGRADE REQUIRED
kubeproxy.config.k8s.io   v1alpha1          v1alpha1            no
kubelet.config.k8s.io     v1beta1           v1beta1             no
_____________________________________________________________________


The table below shows the current state of component configs as understood by this version of kubeadm.
Configs that have a "yes" mark in the "MANUAL UPGRADE REQUIRED" column require manual config upgrade or
resetting to kubeadm defaults before a successful upgrade can be performed. The version to manually
upgrade to is denoted in the "PREFERRED VERSION" column.

API GROUP                 CURRENT VERSION   PREFERRED VERSION   MANUAL UPGRADE REQUIRED
kubeproxy.config.k8s.io   v1alpha1          v1alpha1            no
kubelet.config.k8s.io     v1beta1           v1beta1             no
_____________________________________________________________________

```

upgrade cluster
```bash
$ sudo kubeadm upgrade apply v1.33.6
[upgrade] Reading configuration from the "kubeadm-config" ConfigMap in namespace "kube-system"...
[upgrade] Use 'kubeadm init phase upload-config --config your-config-file' to re-upload it.
[upgrade/preflight] Running preflight checks
[upgrade] Running cluster health checks
[upgrade/preflight] You have chosen to upgrade the cluster version to "v1.33.6"
[upgrade/versions] Cluster version: v1.32.10
[upgrade/versions] kubeadm version: v1.33.6
[upgrade] Are you sure you want to proceed? [y/N]: y
[upgrade/preflight] Pulling images required for setting up a Kubernetes cluster
[upgrade/preflight] This might take a minute or two, depending on the speed of your internet connection
[upgrade/preflight] You can also perform this action beforehand using 'kubeadm config images pull'
[upgrade/control-plane] Upgrading your static Pod-hosted control plane to version "v1.33.6" (timeout: 5m0s)...
[upgrade/staticpods] Writing new Static Pod manifests to "/etc/kubernetes/tmp/kubeadm-upgraded-manifests3010876135"
[upgrade/staticpods] Preparing for "etcd" upgrade
[upgrade/staticpods] Renewing etcd-server certificate
[upgrade/staticpods] Renewing etcd-peer certificate
[upgrade/staticpods] Renewing etcd-healthcheck-client certificate
[upgrade/staticpods] Restarting the etcd static pod and backing up its manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2025-11-21-20-53-05/etcd.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=etcd
[upgrade/staticpods] Component "etcd" upgraded successfully!
[upgrade/etcd] Waiting for etcd to become available
[upgrade/staticpods] Preparing for "kube-apiserver" upgrade
[upgrade/staticpods] Renewing apiserver certificate
[upgrade/staticpods] Renewing apiserver-kubelet-client certificate
[upgrade/staticpods] Renewing front-proxy-client certificate
[upgrade/staticpods] Renewing apiserver-etcd-client certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-apiserver.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2025-11-21-20-53-05/kube-apiserver.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-apiserver
[upgrade/staticpods] Component "kube-apiserver" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-controller-manager" upgrade
[upgrade/staticpods] Renewing controller-manager.conf certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-controller-manager.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2025-11-21-20-53-05/kube-controller-manager.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-controller-manager
[upgrade/staticpods] Component "kube-controller-manager" upgraded successfully!
[upgrade/staticpods] Preparing for "kube-scheduler" upgrade
[upgrade/staticpods] Renewing scheduler.conf certificate
[upgrade/staticpods] Moving new manifest to "/etc/kubernetes/manifests/kube-scheduler.yaml" and backing up old manifest to "/etc/kubernetes/tmp/kubeadm-backup-manifests-2025-11-21-20-53-05/kube-scheduler.yaml"
[upgrade/staticpods] Waiting for the kubelet to restart the component
[upgrade/staticpods] This can take up to 5m0s
[apiclient] Found 1 Pods for label selector component=kube-scheduler
[upgrade/staticpods] Component "kube-scheduler" upgraded successfully!
[upgrade/control-plane] The control plane instance for this node was successfully upgraded!
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config" in namespace kube-system with the configuration for the kubelets in the cluster
[upgrade/kubeconfig] The kubeconfig files for this node were successfully upgraded!
W1121 20:54:45.521572   86066 postupgrade.go:117] Using temporary directory /etc/kubernetes/tmp/kubeadm-kubelet-config4091851113 for kubelet config. To override it set the environment variable KUBEADM_UPGRADE_DRYRUN_DIR
[upgrade] Backing up kubelet config file to /etc/kubernetes/tmp/kubeadm-kubelet-config4091851113/config.yaml
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[upgrade/kubelet-config] The kubelet configuration for this node was successfully upgraded!
[upgrade/bootstrap-token] Configuring bootstrap token and cluster-info RBAC rules
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] Configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] Configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] Configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

[upgrade] SUCCESS! A control plane node of your cluster was upgraded to "v1.33.6".

[upgrade] Now please proceed with upgrading the rest of the nodes by following the right order.
```

### Manually Upgrade CNI Plugin

Check the addons page for CNI upgrades: https://v1-33.docs.kubernetes.io/docs/concepts/cluster-administration/addons/
This step is not required on additional control plane nodes if the CNI provider runs as a DaemonSet.

### Other Control Plane Nodes

```bash
sudo kubeadm upgrade node
```

## KUBELET and KUBECTL Upgrade
This happens for all control plane nodes, one at a time.

### Drain the Node

```bash
kubectl drain <node-to-drain> --ignore-daemonsets
```

### Upgrade Kubelet and Kubectl

```bash
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.33.6-1.1' kubectl='1.33.6-1.1' && \
sudo apt-mark hold kubelet kubectl
```

### Restart the Kubelet

This could be a really good time to patch and restart node
```bash
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
OR
```bash
sudo apt update && sudo apt upgrade -y
sudo reboot
```

### Uncordon the Node

```bash
kubectl uncordon <node-to-uncordon>
```

## Upgrade Worker Nodes

### Upgrade Kubeadm

```bash
sudo apt-mark unhold kubeadm && \  
sudo apt-get update && sudo apt-get install -y kubeadm='1.33.6-1.1' && \
sudo apt-mark hold kubeadm

sudo kubeadm upgrade node
```

### Drain the node

```bash
kubectl drain <node name> --ignore-daemonsets
```

### Upgrade Kubelet and Kubectl

```bash
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.33.6-1.1' kubectl='1.33.6-1.1' && \
sudo apt-mark hold kubelet kubectl
```

### Restart the Kubelet

```bash
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

### Uncordon the Node

```bash
kubectl uncordon <node-to-uncordon>
```

## Verify Cluster Upgrade

```bash
kubectl get nodes
```
