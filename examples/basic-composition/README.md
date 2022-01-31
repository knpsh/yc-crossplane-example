# Basic composition

First, we create our CompositeResourceDefinition. We define API address, names, and schema.
Please see `xrd.yaml` for further information.

Edit the file if neccessary, and apply with `kubectl apply` command:
```
kubectl apply -f xrd.yaml
```

Next we need to define our Composition. Basically, we reference our CompositeResource we've created earlier, and add the ManagedResources that should be deployed.
Please see `composition.yaml` for further information and examples.

Apply the composition with `kubectl apply` command:
```
kubectl apply -f composition.yaml
```

> Note that providerConfigRef used in composition file is called **yandex-cloud**. Replace if necessary, if you've defined some other name for your Yandex.Cloud ProviderConfig.

After that, our resources can be created with a simple claim (format of which we've defined in XRD).
Edit the file `claim.yaml` to add cloud_id parameter, and apply with `kubectl apply`.
```
kubectl apply -f claim.yaml
```

As a result you should see your Infra type resources with the following commands:
```
$ kubectl get infras

NAME     READY   CONNECTION-SECRET   AGE
test-5   True                        25m
```

```
$ kubectl get composite
NAME           READY   COMPOSITION                          AGE
test-5-n48jf   True    xinfras.cloud.yandex.crossplane.io   25m
```

```
$ kubectl get managed

NAME                                                          READY   SYNCED   EXTERNAL-NAME          AGE
instance.compute.yandex-cloud.jet.crossplane.io/test-5-vm-a   True    True     fhm29pgamlkp6j48m6uf   26m

NAME                                                                  READY   SYNCED   EXTERNAL-NAME          AGE
folder.resourcemanager.yandex-cloud.jet.crossplane.io/test-5-folder   True    True     b1ge9u8pdfjkaek0bhtf   26m

NAME                                                    READY   SYNCED   EXTERNAL-NAME          AGE
network.vpc.yandex-cloud.jet.crossplane.io/test-5-vpc   True    True     enphu387pe5ngpfi8cjt   26m

NAME                                                        READY   SYNCED   EXTERNAL-NAME          AGE
subnet.vpc.yandex-cloud.jet.crossplane.io/test-5-subnet-a   True    True     e9bmunn0cau29tk415h5   26m
subnet.vpc.yandex-cloud.jet.crossplane.io/test-5-subnet-b   True    True     e2lgpr4kgchv92smm6vn   26m
subnet.vpc.yandex-cloud.jet.crossplane.io/test-5-subnet-c   True    True     b0ctaokv1bjnkrc68n2o   26m
```

These resources should be seen in Yandex.Cloud management console too (of course).
