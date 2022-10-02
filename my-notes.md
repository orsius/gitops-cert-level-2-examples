# Gitops at scale
> ℹ️ https://learning.codefresh.io/path-player?courseid=gitops-at-scale

## 2. Handling multiple Applications

### live exercise: app of apps

```bash
kubectl apply -f https://raw.githubusercontent.com/<your user>/gitops-cert-level-2-examples/main/app-of-apps/root-app/my-application.yml -n argocd
```

> By using GitOps to manage the root application, you can modify the list of default applications installed in a cluster by simply using git *(without resorting to the ArgoCD CLI or UI)*.
