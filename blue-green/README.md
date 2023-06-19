# Blue Green

Implementing the blue green strategy using Argo rollouts

1. Install Argo Rollouts controller and kubectl plugin: https://github.com/argoproj/argo-rollouts#installation

2. Create a sample application and sync it.

```
argocd app create --name blue-green --repo https://github.com/vineet-007/examples --dest-server https://kubernetes.default.svc --dest-namespace default --path blue-green && argocd app sync blue-green
```
