# GitOps repo with OCP Operators manifests

This repo is meant to provide an as-code approach to install OCP Operators using manifests.

Each operator comes with the default settings, that can be overridden using the kustomization template associated with each.

They can easily be referenced in [ArgoCD](https://argo-cd.readthedocs.io/) Applications .

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: example
  namespace: openshift-gitops
spec:
  destination:
    server: https://kubernetes.default.svc
  project: default
  source:
    path: single-sign-on
    repoURL: https://github.com/kubealex/ocp-operators-manifests.git
    targetRevision: HEAD
  syncPolicy:
    retry:
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 3m0s
      limit: 10
```
