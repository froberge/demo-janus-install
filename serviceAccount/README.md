## Folder that contains the different information for creating a service Accounts

### Retrive the service account
```
oc get sa
```

### Create the service account
```
oc apply -f <folder>/<file.yaml>
```

### For OCM
```
oc create clusterrolebinding rhdh-ocm-plugin-binding --clusterrole=rhdh-ocm-plugin
--serviceaccount=default:janus-ocm-sa
```

### For K8s
```
oc create clusterrolebinding rhdh-k8s-plugin-binding --clusterrole=rhdh-k8s-plugin
--serviceaccount=default:janus-k8s-sa
```

### Get the Token
```
oc describe sa <sa-name>
```