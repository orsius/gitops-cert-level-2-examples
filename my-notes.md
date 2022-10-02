# GitOps at Scale
> ℹ️ https://learning.codefresh.io/path-player?courseid=gitops-at-scale

## 2. Handling multiple Applications

### live exercise: app of apps

```bash
kubectl apply -f https://raw.githubusercontent.com/<your user>/gitops-cert-level-2-examples/main/app-of-apps/root-app/my-application.yml -n argocd
```

> By using GitOps to manage the root application, you can modify the list of default applications installed in a cluster by simply using git *(without resorting to the ArgoCD CLI or UI)*.

### Multi-cluster Management
```
argocd cluster add <context name>
argocd cluster list        # This command will list all clusters with their name and server
argocd cluster rm <server>
```

### Managing grouped Argo CD instances with multiple clusters

```
argocd proj add-destination <project> <cluster>,<namespace>
argocd proj remove-destination <project> <cluster>,<namespace>
```
>  example application can be found at https://github.com/codefresh-contrib/gitops-cert-level-2-examples/tree/main/simple-application

```
argocd login kubernetes-vm:30443 --insecure --username admin --password <admin-password>
argocd cluster add default --name cluster-2
```

`kubectl get serviceaccount argocd-manager -n kube-system`

> ℹ️ Deploying an application to an external cluster is a similar process to deploying applications to the internal cluster

```
kubectl config view
kubectl get all
```
server ip: `https://10.5.1.5:6443`

> ℹ️ An Argo CD instance managing external clusters can still deploy applications to the same cluster it is running on.



## 3. Promoting releases with GitOps

### 

## 4. Common operations

### 

## Summary
