# Crossplane setup

1. Enable the crossplane helm chart repo

```
helm repo add \
crossplane-stable https://charts.crossplane.io/stable
helm repo update
```

2. Install the crossplane components

```
helm install crossplane \
crossplane-stable/crossplane \
--namespace crossplane-system \
--create-namespace
```

3. IRSA Configurations
  - Enable the IAM OIDC provider for EKS.
  - Creating an IAM policy granting the AWS provider access to AWS resources.


4. Creating an IAM role for the AWS provider to associate with the AWS provider.

check crossplane-role-trust-relationship.json for reference, just change the account number and oidc link.

5. Create and apply a ControllerConfig to associate the IAM role ARN.

```
kubectl apply -f controllerconfig.yaml
```

6. Apply the provider and then providerconfig yamls

```
kubectl apply -f provider.yaml
```

Note - It may take up to five minutes for the provider to list HEALTHY as True. Apply providerconfig file after that

```
kubectl apply -f providerconfig.yaml
```