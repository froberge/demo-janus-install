## Folder that contains the different information for creating a service Accounts

### Add values
```
oc adm policy add-cluster-role-to-user cluster-admin -z openshift-gitops-argocd-application-controller -n openshift-gitops
```


### Add an extra user to OpenShift gitOps adm make it admin

Add this section to the CRD argoCD.
```
...
# Create the user
spec:
    extraConfig:
    accounts.rhdh: apiKey, login
``````

```
...
# add to admin group
  rbac:
    policy: |
      g, system:cluster-admins, role:admin
      g, cluster-admins, role:admin
      g, rhdh, role:admin
```

### Update the password for the new user
:warning: the default password is the admin password.

argocd account update-password --account <user> --new-password <passowrd> --current-password <admin-password> --grpc-web

### Install another argocd to manage the janus argocd
```
oc apply -k setup/base
```

