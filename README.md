## Some useful package relocation examples


```bash

#bundle images into tar on internet connected side
imgpkg copy -b extensions.aws-usw2.tmc.cloud.vmware.com/packages/standard/repo:v2023.7.13_update.2 --to-tar standard.tar

#push bundle to harbor
imgpkg copy --tar standard.tar --to-repo harbor.build.h2o-2-18171.h2o.vmware.com/packages/standard --registry-ca-cert-path c.crt --registry-username admin 

#kapp controller needs ca cert for registry
kubectl create secret generic kapp-controller-config \
   --namespace kapp-controller \
   --from-file caCerts=ca.crt

```


```yaml

apiVersion: packaging.carvel.dev/v1alpha1
kind: PackageRepository
metadata:
  name: tanzu-standard
  namespace: tkg-system
spec:
  fetch:
    imgpkgBundle:
      image: harbor.build.h2o-2-18171.h2o.vmware.com/packages/standard:v2023.7.13_update.2

```
