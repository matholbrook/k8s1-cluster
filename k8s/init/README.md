# How To

Set up multiple control plane nodes and use a VIP to access them

## URL
https://www.tpisoftware.com/tpu/articleDetails/2445



yum -y install ipvsadm
(why do we need this?)

## Disable Swap
swapoff -a && sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab


## HAproxy
mkdir /etc/haproxy
cat > /etc/haproxy/haproxy.cfg <<EOF
frontend kube-apiserver-https
   mode tcp
   bind :8443
   default_backend kube-apiserver-backend

backend kube-apiserver-backend
    mode tcp
    balance roundrobin
    stick-table type ip size 200k expire 30m
    stick on src
    server k8s-01-master-node-01 192.168.218.44:6443 check
    server k8s-01-master-node-02 192.168.218.60:6443 check
    server k8s-01-master-node-03 192.168.218.59:6443 check
EOF

cat > /etc/kubernetes/manifests/haproxy.yaml <<EOF2
kind: Pod
apiVersion: v1
metadata:
  annotations:
    scheduler.alpha.kubernetes.io/critical-pod: ""
  labels:
    component: haproxy
    tier: control-plane
  name: kube-haproxy
  namespace: kube-system
spec:
  hostNetwork: true
  priorityClassName: system-cluster-critical
  containers:
  - name: kube-haproxy
    image: docker.io/haproxy:2.3.10
    resources:
      requests:
        cpu: 100m
    volumeMounts:
    - name: haproxy-cfg
      readOnly: true
      mountPath: /usr/local/etc/haproxy/haproxy.cfg
  volumes:
  - name: haproxy-cfg
    hostPath:
      path: /etc/haproxy/haproxy.cfg
      type: FileOrCreate
EOF2

## Keepalived

cat > /etc/kubernetes/manifests/keepalived.yaml <<EOF3
kind: Pod
apiVersion: v1
metadata:
  annotations:
    scheduler.alpha.kubernetes.io/critical-pod: ""
  labels:
    component: keepalived
    tier: control-plane
  name: kube-keepalived
  namespace: kube-system
spec:
  hostNetwork: true
  priorityClassName: system-cluster-critical
  containers:
  - name: kube-keepalived
    image: docker.io/osixia/keepalived:2.0.17
    env:
    - name: KEEPALIVED_VIRTUAL_IPS
      value: 192.168.218.100
    - name: KEEPALIVED_INTERFACE
      value: ens33
    - name: KEEPALIVED_UNICAST_PEERS
      value: "#PYTHON2BASH:['192.168.218.44', '192.168.218.60', '192.168.218.59']"
    - name: KEEPALIVED_PASSWORD
      value: crio
    - name: KEEPALIVED_PRIORITY
      value: "100"
    - name: KEEPALIVED_ROUTER_ID
      value: "51"
    resources:
      requests:
        cpu: 100m
    securityContext:
      privileged: true
      capabilities:
        add:
        - NET_ADMIN
EOF3


## Create k8s cluster yaml file

kubeadm config print init-defaults > kubeadm-config.yaml

(modify the file)

## Create the cluster from the file
kubeadm init --upload-certs --config=kubeadm-config.yaml

## Configure CNI

calico

## Configure metrics server

foo


## Nginx Ingress for Bare Metal
This is a testing only step so not actually needed
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.46.0/deploy/static/provider/baremetal/deploy.yaml








