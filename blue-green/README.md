# Blue Green

Implementing the blue green strategy using Argo rollouts

1. Install Argo Rollouts controller and kubectl plugin: https://github.com/argoproj/argo-rollouts#installation

2. Create a sample application and sync it.

```
argocd app create --name blue-green --repo https://github.com/vineet-007/examples --dest-server https://kubernetes.default.svc --dest-namespace default --path blue-green && argocd app sync blue-green
```

Once the application is synced you can access it using `rolloutService` service.

[![Screenshot-2023-06-06-130745.png](https://i.postimg.cc/6p0yg36C/Screenshot-2023-06-06-130745.png)](https://postimg.cc/XrrjynCv)

[![Screenshot-2023-06-06-131257.png](https://i.postimg.cc/G2NBK5LN/Screenshot-2023-06-06-131257.png)](https://postimg.cc/G8FhhzsJ)


3. Change image version parameter to trigger blue-green deployment process or alternatively run the following command if you are not using argoCD:
```
kubectl argo rollouts set image sample-rollout color=argoproj/rollouts-demo:green
```
Now application runs `argoproj/rollouts-demo:blue` and `argoproj/rollouts-demo:green` images simultaneously.
The `argoproj/rollouts-demo:green` is available only via preview service `rolloutService-preview`.

[![Microsoft-Teams-image-11.png](https://i.postimg.cc/tThfNYHV/Microsoft-Teams-image-11.png)](https://postimg.cc/HckBpWnp)

[![Screenshot-2023-06-06-131755.png](https://i.postimg.cc/WzwnhZcX/Screenshot-2023-06-06-131755.png)](https://postimg.cc/tn7PcYTx)

4. Promote `argoproj/rollouts-demo:green` to `green` manually incase autoPromotionEnabled flag was set to false:

```
kubectl argo rollouts promote sample-rollout
```

This promotes `argoproj/rollouts-demo:green` to `green` status and `Rollout` deletes old replica which runs `argoproj/rollouts-demo:blue`.

[![Screenshot-2023-06-06-132040.png](https://i.postimg.cc/YSyqBD4x/Screenshot-2023-06-06-132040.png)](https://postimg.cc/Ff3QjZVf)
