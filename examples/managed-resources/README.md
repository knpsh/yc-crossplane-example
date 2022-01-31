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

You can get a list of available resources with `kubectl api-resources` command:
```
$ kubectl api-resources | grep yandex-cloud

instances                                      compute.yandex-cloud.jet.crossplane.io/v1alpha1           false        Instance
registries                                     container.yandex-cloud.jet.crossplane.io/v1alpha1         false        Registry
repositories                                   container.yandex-cloud.jet.crossplane.io/v1alpha1         false        Repository
recordsets                                     dns.yandex-cloud.jet.crossplane.io/v1alpha1               false        Recordset
zones                                          dns.yandex-cloud.jet.crossplane.io/v1alpha1               false        Zone
serviceaccountiammembers                       iam.yandex-cloud.jet.crossplane.io/v1alpha1               false        ServiceAccountIAMMember
serviceaccountkeys                             iam.yandex-cloud.jet.crossplane.io/v1alpha1               false        ServiceAccountKey
serviceaccounts                                iam.yandex-cloud.jet.crossplane.io/v1alpha1               false        ServiceAccount
serviceaccountstaticaccesskeys                 iam.yandex-cloud.jet.crossplane.io/v1alpha1               false        ServiceAccountStaticAccessKey
symmetrickeys                                  kms.yandex-cloud.jet.crossplane.io/v1alpha1               false        SymmetricKey
clusters                                       kubernetes.yandex-cloud.jet.crossplane.io/v1alpha1        false        Cluster
nodegroups                                     kubernetes.yandex-cloud.jet.crossplane.io/v1alpha1        false        NodeGroup
mongodbclusters                                mdb.yandex-cloud.jet.crossplane.io/v1alpha1               false        MongodbCluster
postgresqlclusters                             mdb.yandex-cloud.jet.crossplane.io/v1alpha1               false        PostgresqlCluster
redisclusters                                  mdb.yandex-cloud.jet.crossplane.io/v1alpha1               false        RedisCluster
folderiambindings                              resourcemanager.yandex-cloud.jet.crossplane.io/v1alpha1   false        FolderIAMBinding
folderiammembers                               resourcemanager.yandex-cloud.jet.crossplane.io/v1alpha1   false        FolderIAMMember
folders                                        resourcemanager.yandex-cloud.jet.crossplane.io/v1alpha1   false        Folder
buckets                                        storage.yandex-cloud.jet.crossplane.io/v1alpha1           false        Bucket
objects                                        storage.yandex-cloud.jet.crossplane.io/v1alpha1           false        Object
networks                                       vpc.yandex-cloud.jet.crossplane.io/v1alpha1               false        Network
subnets                                        vpc.yandex-cloud.jet.crossplane.io/v1alpha1               false        Subnet
providerconfigs                                yandex-cloud.jet.crossplane.io/v1alpha1                   false        ProviderConfig
providerconfigusages                           yandex-cloud.jet.crossplane.io/v1alpha1                   false        ProviderConfigUsage
```

You can also check supportable parameters within a resource with `kubectl explain` command:
```
$ kubectl explain Instance.spec.forProvider
KIND:     Instance
VERSION:  compute.yandex-cloud.jet.crossplane.io/v1alpha1
RESOURCE: forProvider <Object>
DESCRIPTION: <empty>

FIELDS:
   allowStoppingForUpdate       <boolean>
   bootDisk     <[]Object> -required-
   description  <string>
   folderId     <string>
   folderIdRef  <Object>
     A Reference to a named object.
   folderIdSelector     <Object>
     A Selector selects an object.
   hostname     <string>
   labels       <map[string]string>
   metadata     <map[string]string>
   name <string>
   networkAccelerationType      <string>
   networkInterface     <[]Object> -required-
   placementPolicy      <[]Object>
   platformId   <string>
   resources    <[]Object> -required-
   schedulingPolicy     <[]Object>
   secondaryDisk        <[]Object>
   serviceAccountId     <string>
   serviceAccountIdRef  <Object>
     A Reference to a named object.
   serviceAccountIdSelector     <Object>
     A Selector selects an object.
   zone <string>
```