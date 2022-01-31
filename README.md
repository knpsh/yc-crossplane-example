# yc-crossplane-example
Crossplane Composition example using Yandex.Cloud provider

## Installation

### Install Crossplane

```
kubectl create namespace crossplane-system

helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update
helm install crossplane --namespace crossplane-system crossplane-stable/crossplane
```

Check status:
```
helm list -n crossplane-system
kubectl get all -n crossplane-system
```

### Install provider

Install provider:
```
kubectl crossplane install provider cr.yandex/crp0kch415f0lke009ft/crossplane/provider-jet-yc:v0.1.14
```

Create a service account:
```
yc iam service-account create --name crossplane-sa
yc resource-manager cloud add-access-binding <CLOUD_ID> --service-account-id <SERVICE_ACCOUNT_ID> --role admin
```

Get service account key and create K8S secret:
```
yc iam key create --service-account-name crossplane-sa --output key.json
kubectl create secret generic yc-creds -n "crossplane-system" --from-file=credentials=./key.json
```

Apply ProviderConfig:
```
kubectl apply -f examples/managed-resources/providerconfig/providerconfig.yaml
```

ProviderConfig.yaml example:
```
apiVersion: yandex-cloud.jet.crossplane.io/v1alpha1
kind: ProviderConfig
metadata:
  name: yandex-cloud
spec:
  credentials:
    source: Secret
    secretRef:
      name: yc-creds
      namespace: crossplane-system
      key: credentials
```