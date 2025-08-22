# newpod-helm

Simple Helm chart to deploy a new pod with.

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: newpod
  namespace: argocd
spec:
  project: default

  source:
    repoURL: https://github.com/newpod/newpod-helm.git
    targetRevision: main
    helm:
      releaseName: newpod
      values: |
        name: newpod
        namespace: newpod

  destination:
    server: https://kubernetes.default.svc
    namespace: newpod

  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```