## Folder that contains the different information for creating a service Accounts

### Retrive the service account
```
oc get sa
```



## For OCM

1. create the serbice account
    ```
    oc create sa rhdh-ocm-sa

    ```
1. Create the Cluster Role
    ```
    oc apply -f ocm/ocm-clusterRole.yaml
    ```
1. Bind the Cluster role and the SA
    ```
    oc create clusterrolebinding rhdh-ocm-plugin-binding --clusterrole=rhdh-ocm-plugin --serviceaccount=default:rhdh-ocm-sa
    ```

1. Create the token
    ```
    oc create token -n default rhdh-ocm-sa --duration=999999s

    
    ```

## For K8s

1. create the serbice account
    ```
    oc create sa rhdh-k8s-sa

    ```
1. Create the Cluster Role
    ```
    oc apply -f k8s/k8s-clusterRole.yaml
    ```
1. Bind the Cluster role and the SA
    ```
    oc create clusterrolebinding rhdh-k8s-plugin-binding --clusterrole=rhdh-k8s-plugin --serviceaccount=default:rhdh-k8s-sa
    ```

1. Create the token
    ```
    oc create token -n default rhdh-k8s-sa --duration=999999s
    ```

### Retrieve token
```
oc describe secret -n default $(oc get secret -n default -o jsonpath="{.items[?(@.metadata.annotations['kubernetes\.io/service-account\.name']=='rhdh-ocm-sa')].metadata.name}")
```
or

```
oc describe secret -n default $(oc get secret -n default -o jsonpath="{.items[?(@.metadata.annotations['kubernetes\.io/service-account\.name']=='rhdh-k8s-sa')].metadata.name}")
```
