# ArgoCD

```
---
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: media-fe
  namespace: argocd
  annotations:
    argocd-image-updater.argoproj.io/image-list: anhmhtera/media-fe:~v0.1
  # finalizers:
  #   - resources-finalizer.argocd.argoproj.to
spec:
  project: default
  source:
    repoURL: https://github.com/hiepzinza/argocd-fe.git
    targetRevision: main
    path: media-fe
    helm:
      parameters:
        - name: "image.repository"
          value: anhmhtera/media-fe
        - name: "image.tag"
          value: v0.1.3
  destination:
    server: https://kubernetes.default.svc
    namespace: myapp
  syncPolicy:
    automated:
      prune: true
```