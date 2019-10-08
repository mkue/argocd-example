### Steps to deploy Argo CD

1. Run `kubectl apply -k argocd` from the root of this project
2. Run `kubectl port-forward svc/argocd-server -n argocd 8080:80` and then go to [http://localhost:8080]()
3. Add the `git@github.com:mkue/argocd-example.git` repository manually in the web interface. 
4. Add following application in the Argo CD web interface:

```yaml
apiVersion: argoproj.io/v1alpha1
metadata:
  name: argo-apps
spec:
  destination:
    namespace: default
    server: 'https://kubernetes.default.svc'
  source:
    path: argo-apps
    repoURL: 'git@github.com:mkue/argocd-example.git'
    targetRevision: master
    directory:
      recurse: true
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```
