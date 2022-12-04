
### Deploy and Access the Kubernetes Dashboard

[reffer here](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

``` 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.1/aio/deploy/recommended.yaml
```

### Accessing the Dashboard UI

[reffer here](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)

#### Creating a Service Account
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```
#### Creating a ClusterRoleBinding
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```
#### Getting a Bearer Token
```yaml
kubectl -n kubernetes-dashboard create token admin-user
```
#### Command line proxy 
```
kubectl proxy --address 0.0.0.0
```

#### access Dashboard in browser using below url
```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```
