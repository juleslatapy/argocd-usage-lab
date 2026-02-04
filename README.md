# ArgoCD Usage Lab

This repository contains a baseline to test out ArgoCD features. It is meant to be forked & experimented with.

We are assuming ArgoCD is already deployed in the cluster we use.

## Prerequisites

- Verify you are using the correct `kubectl` context for the cluster before applying files.

## Content

- This `README.md` file containing lab instructions;
- `/manifests` folder containing deployments definitions to apply in Kubernetes.

## How to deploy the app

1. Create a namespace for your resources: `kubectl create namespace my-namespace  # rename`
2. Deploy the app's 1st version using `kubectl`: `kubectl apply -f ./manifests/deployment-app.yaml -n my-namespace`

To verify that it is successfully deployed, port-forwarding is required:

```sh
# replace your namespace name
kubectl port-forward deployment/lab-frontend-app -n my-namespace 8080:80
```

Then, navigate to http://localhost:8080 to access your pod.

## Registering the app in ArgoCD

Port-forwarding is going to be necessary to access the ArgoCD console as well.

Cancel the previous port-forward and initiate a new one to ArgoCD web UI:

```shell
# TODO review below names
kubectl port-forward deployment/argocd-web -n argocd 3000:80
```

Register the app inside of this web UI.