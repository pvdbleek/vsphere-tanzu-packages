```
kubectl get storageclasses.storage.k8s.io
```

```
kubectl patch storageclass vc01cl01-t0compute -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

```
kubectl apply -f tanzu-system-kapp-ctrl-restricted.yaml
kubectl apply -f kapp-controller.yaml
```

```
tanzu package repository add tkg-packages -n tanzu-package-repo-global --url projects.registry.vmware.com/tkg/packages/standard/repo:v1.6.0
```
```
kubectl create ns tkg-packages
```
```
tanzu package install cert-manager --package-name cert-manager.tanzu.vmware.com --namespace tkg-packages --version 1.7.2+vmware.1-tkg.1
```
*** edit contour-default-values.yaml
```
tanzu package install contour \
--package-name contour.tanzu.vmware.com \
--version 1.20.2+vmware.1-tkg.1 \
--values-file contour-default-values.yaml \
--namespace tkg-packages
```
*** edit harbor-default-values.yaml
```
tanzu package install harbor \
--package-name harbor.tanzu.vmware.com \
--version 2.5.3+vmware.1-tkg.1 \
--values-file harbor-default-values.yaml \
--namespace tkg-packages
```
https://projectcontour.io/guides/external-authorization/

https://github.com/projectcontour/contour-authserver