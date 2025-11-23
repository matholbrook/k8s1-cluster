# How To

$ trivy k8s --report summary --kubeconfig ~/.kube/k8s1-config

2025-11-06T21:38:14Z	INFO	Node scanning is enabled
2025-11-06T21:38:14Z	INFO	If you want to disable Node scanning via an in-cluster Job, please try '--disable-node-collector' to disable the Node-Collector job.
2025-11-06T21:38:14Z	INFO	[vulndb] Need to update DB
2025-11-06T21:38:14Z	INFO	[vulndb] Downloading vulnerability DB...
2025-11-06T21:38:14Z	INFO	[vulndb] Downloading artifact...	repo="mirror.gcr.io/aquasec/trivy-db:2"
74.29 MiB / 74.29 MiB [-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------] 100.00% 5.98 MiB p/s 13s
2025-11-06T21:38:28Z	INFO	[vulndb] Artifact successfully downloaded	repo="mirror.gcr.io/aquasec/trivy-db:2"
2025-11-06T21:38:28Z	INFO	Scanning K8s...	K8s="kubernetes-admin@kubernetes"
233 / 233 [------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------] 100.00% 3 p/s

Summary Report for kubernetes-admin@kubernetes


Workload Assessment
┌───────────┬───────────────────────────┬───────────────────┬───────────────────┬───────────────────┐
│ Namespace │         Resource          │  Vulnerabilities  │ Misconfigurations │      Secrets      │
│           │                           ├───┬───┬───┬───┬───┼───┬───┬───┬───┬───┼───┬───┬───┬───┬───┤
│           │                           │ C │ H │ M │ L │ U │ C │ H │ M │ L │ U │ C │ H │ M │ L │ U │
├───────────┼───────────────────────────┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┤
│           │ Cluster/k8s.io/kubernetes │   │   │ 1 │   │   │   │   │   │   │   │   │   │   │   │   │
└───────────┴───────────────────────────┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
Severities: C=CRITICAL H=HIGH M=MEDIUM L=LOW U=UNKNOWN


Infra Assessment
┌─────────────┬──────────────────────────────────────────────┬────────────────────────┬──────────────────────┬───────────────────┐
│  Namespace  │                   Resource                   │    Vulnerabilities     │  Misconfigurations   │      Secrets      │
│             │                                              ├───┬─────┬─────┬────┬───┼───┬────┬────┬────┬───┼───┬───┬───┬───┬───┤
│             │                                              │ C │  H  │  M  │ L  │ U │ C │ H  │ M  │ L  │ U │ C │ H │ M │ L │ U │
├─────────────┼──────────────────────────────────────────────┼───┼─────┼─────┼────┼───┼───┼────┼────┼────┼───┼───┼───┼───┼───┼───┤
│ kube-system │ Pod/kube-apiserver-k8s1-vm1                  │ 1 │ 15  │ 11  │    │   │   │ 2  │ 5  │ 17 │   │   │   │   │   │   │
│ kube-system │ ControlPlaneComponents/k8s.io/apiserver      │   │     │     │ 1  │   │   │    │    │    │   │   │   │   │   │   │
│ kube-system │ ConfigMap/extension-apiserver-authentication │   │     │     │    │   │   │    │ 1  │    │   │   │   │   │   │   │
│ kube-system │ DaemonSet/calico-node                        │   │ 162 │ 240 │ 70 │   │   │ 10 │ 14 │ 35 │   │   │   │   │   │   │
│ kube-system │ Deployment/calico-kube-controllers           │   │ 15  │ 17  │    │   │   │ 1  │ 3  │ 9  │   │   │   │   │   │   │
│ kube-system │ Deployment/coredns                           │ 1 │ 12  │ 17  │ 1  │ 3 │   │ 1  │ 6  │ 4  │   │   │   │   │   │   │
│ kube-system │ Pod/kube-scheduler-k8s1-vm1                  │ 1 │ 14  │ 10  │    │   │   │ 2  │ 4  │ 8  │   │   │   │   │   │   │
│ kube-system │ Deployment/metrics-server                    │ 1 │ 10  │ 15  │    │   │   │ 1  │ 2  │ 4  │   │   │   │   │   │   │
│ kube-system │ Service/metrics-server                       │   │     │     │    │   │   │    │ 1  │    │   │   │   │   │   │   │
│ kube-system │ Pod/etcd-k8s1-vm1                            │ 4 │ 43  │ 63  │ 4  │   │   │ 2  │ 4  │ 7  │   │   │   │   │   │   │
│ kube-system │ Pod/kube-controller-manager-k8s1-vm1         │ 1 │ 18  │ 11  │    │   │   │ 2  │ 4  │ 10 │   │   │   │   │   │   │
│ kube-system │ DaemonSet/kube-proxy                         │ 1 │ 18  │ 12  │ 17 │   │   │ 4  │ 6  │ 10 │   │   │   │   │   │   │
│ kube-system │ Service/kube-dns                             │   │     │     │    │   │   │    │ 1  │    │   │   │   │   │   │   │
│             │ Node/k8s1-vm2                                │   │  1  │     │    │   │   │ 2  │    │    │   │   │   │   │   │   │
│             │ Node/k8s1-vm1                                │   │  1  │     │    │   │ 1 │ 2  │    │ 1  │   │   │   │   │   │   │
│             │ Node/k8s1-vm3                                │   │  1  │     │    │   │   │ 2  │    │    │   │   │   │   │   │   │
└─────────────┴──────────────────────────────────────────────┴───┴─────┴─────┴────┴───┴───┴────┴────┴────┴───┴───┴───┴───┴───┴───┘
Severities: C=CRITICAL H=HIGH M=MEDIUM L=LOW U=UNKNOWN


RBAC Assessment
┌─────────────┬────────────────────────────────────────────────────────────────────┬───────────────────┐
│  Namespace  │                              Resource                              │  RBAC Assessment  │
│             │                                                                    ├───┬───┬───┬───┬───┤
│             │                                                                    │ C │ H │ M │ L │ U │
├─────────────┼────────────────────────────────────────────────────────────────────┼───┼───┼───┼───┼───┤
│ kube-system │ Role/system:controller:token-cleaner                               │   │   │ 1 │   │   │
│ kube-system │ Role/system::leader-locking-kube-controller-manager                │   │   │ 1 │   │   │
│ kube-system │ Role/system:controller:bootstrap-signer                            │   │   │ 1 │   │   │
│ kube-system │ Role/system::leader-locking-kube-scheduler                         │   │   │ 1 │   │   │
│ kube-system │ Role/system:controller:cloud-provider                              │   │   │ 1 │   │   │
│ kube-public │ RoleBinding/kubeadm:bootstrap-signer-clusterinfo                   │ 1 │   │   │   │   │
│ kube-public │ Role/system:controller:bootstrap-signer                            │   │   │ 1 │   │   │
│             │ ClusterRole/system:controller:horizontal-pod-autoscaler            │ 2 │   │   │   │   │
│             │ ClusterRole/system:kube-scheduler                                  │   │   │ 1 │   │   │
│             │ ClusterRole/edit                                                   │ 2 │ 4 │ 6 │   │   │
│             │ ClusterRole/system:controller:replication-controller               │   │   │ 2 │   │   │
│             │ ClusterRoleBinding/kubeadm:cluster-admins                          │   │   │ 1 │   │   │
│             │ ClusterRole/system:controller:ttl-after-finished-controller        │   │   │ 1 │   │   │
│             │ ClusterRole/system:controller:root-ca-cert-publisher               │   │   │ 1 │   │   │
│             │ ClusterRole/system:kube-controller-manager                         │ 5 │   │   │   │   │
│             │ ClusterRole/system:controller:cronjob-controller                   │   │   │ 3 │   │   │
│             │ ClusterRole/system:controller:endpointslicemirroring-controller    │   │ 1 │   │   │   │
│             │ ClusterRole/system:controller:job-controller                       │   │   │ 2 │   │   │
│             │ ClusterRole/system:controller:resourcequota-controller             │ 1 │   │   │   │   │
│             │ ClusterRoleBinding/cluster-admin                                   │   │   │ 1 │   │   │
│             │ ClusterRole/system:aggregate-to-edit                               │ 2 │ 4 │ 6 │   │   │
│             │ ClusterRole/system:controller:replicaset-controller                │   │   │ 2 │   │   │
│             │ ClusterRole/system:controller:endpoint-controller                  │   │ 1 │   │   │   │
│             │ ClusterRole/system:controller:statefulset-controller               │   │   │ 1 │   │   │
│             │ ClusterRole/admin                                                  │ 3 │ 4 │ 6 │   │   │
│             │ ClusterRole/cluster-admin                                          │ 2 │   │   │   │   │
│             │ ClusterRole/system:aggregate-to-admin                              │ 1 │   │   │   │   │
│             │ ClusterRole/system:controller:generic-garbage-collector            │ 1 │   │   │   │   │
│             │ ClusterRole/system:controller:endpointslice-controller             │   │ 1 │   │   │   │
│             │ ClusterRole/system:controller:legacy-service-account-token-cleaner │ 1 │   │   │   │   │
│             │ ClusterRole/system:controller:namespace-controller                 │ 1 │   │   │   │   │
│             │ ClusterRole/system:controller:node-controller                      │   │   │ 1 │   │   │
│             │ ClusterRole/system:node                                            │ 1 │   │ 1 │   │   │
│             │ ClusterRole/system:controller:deployment-controller                │   │   │ 3 │   │   │
│             │ ClusterRole/system:controller:persistent-volume-binder             │   │   │ 1 │   │   │
│             │ ClusterRole/system:controller:pod-garbage-collector                │   │   │ 1 │   │   │
│             │ ClusterRole/system:controller:daemon-set-controller                │   │   │ 1 │   │   │
└─────────────┴────────────────────────────────────────────────────────────────────┴───┴───┴───┴───┴───┘
Severities: C=CRITICAL H=HIGH M=MEDIUM L=LOW U=UNKNOW
