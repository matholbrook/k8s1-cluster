# How To


## Install with Helm

```bash
$ helm upgrade vcluster-platform vcluster-platform --install \
  --repo https://charts.loft.sh/ \
  --namespace vcluster-platform \
  --create-namespace
Release "vcluster-platform" does not exist. Installing it now.
NAME: vcluster-platform
LAST DEPLOYED: Mon May 12 18:19:05 2025
NAMESPACE: vcluster-platform
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Thank you for installing vcluster-platform.

Your release is named vcluster-platform.

To learn more about the release, try:

  $ helm status vcluster-platform
  $ helm get all vcluster-platform
```

