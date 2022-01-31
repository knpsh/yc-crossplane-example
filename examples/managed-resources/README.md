# Managed Resources

Managed Resources can be created directly by editing Managed Resources yaml files and applying with `kubectl apply -f`.

For example, here I create a new Folder:
```
apiVersion: resourcemanager.yandex-cloud.jet.crossplane.io/v1alpha1
kind: Folder
metadata:
  name: demo-folder
spec:
  forProvider:
    name: demo-folder
    cloudId: <CLOUD_ID>
    description: Demo folder for crossplane
  providerConfigRef:
    name: yandex-cloud # ProviderConfig name here
```