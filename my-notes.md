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

### How does an ApplicationSet work?

Below is an example of an ApplicationSet resource that is used to target an Argo CD Application to multiple Kubernetes clusters. Within this example, it’s deploying a guestbook application using a List Generator.
apiVersion: argoproj.io/v1alpha1

```yaml
kind: ApplicationSet
metadata:
  name: guestbook
spec:
  generators:
  - list:
      elements:
      - cluster: engineering-dev
        url: https://kubernetes.default.svc
      - cluster: engineering-prod
        url: https://kubernetes.default.svc
  template:
    metadata:
      name: '{{cluster}}-guestbook'
    spec:
      project: default
      source:
        repoURL: https://github.com/argoproj/applicationset.git
        targetRevision: HEAD
        path: examples/list-generator/guestbook/{{cluster}}
      destination:
        server: '{{url}}'
        namespace: guestbook
```

The ApplicationSet is essentially made up of “generators” that generate Applications. The Generators are responsible for providing a set of key-value pairs, that are then passed into a template with `{{param}}` styled parameters.

Within the example above the List generator is passing the {{cluster}} and {{url}} fields into the Application template as the parameters.
template:

```yaml
    metadata:
      name: '{{cluster}}-guestbook'
    spec:
      project: default
      source:
        repoURL: https://github.com/argoproj/applicationset.git
        targetRevision: HEAD
        path: examples/list-generator/guestbook/{{cluster}}
      destination:
        server: '{{url}}'
        namespace: guestbook
```

These fields will be rendered as two corresponding Argo CD Applications - one for each defined cluster.
spec:
```yaml
  generators:
  - list:
      elements:
      - cluster: engineering-dev
        url: https://kubernetes.default.svc
      - cluster: engineering-prod
        url: https://kubernetes.default.svc
```

## 3. Promoting releases with GitOps

### 

## 4. Common operations

### 

## Summary
