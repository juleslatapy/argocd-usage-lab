# ArgoCD Usage Lab

This repository contains a baseline to test out ArgoCD features. It is meant to be forked & experimented with.

We are assuming ArgoCD is already deployed in the cluster we use.

## Prerequisites

- Verify you are using the correct `kubectl` context for the cluster before applying files.

## Content

- This `README.md` file containing lab instructions;
- `/manifests` folder containing deployments definitions to apply in Kubernetes.

## Accessing the ArgoCD Web UI

Port-forwarding is going to be necessary to access the ArgoCD console as well.

Cancel the previous port-forward and initiate a new one to ArgoCD web UI:

```shell
kubectl port-forward service/argocd-server -n argocd 8080:443
```

To get the default login password to use in the web UI, open another terminal window and run:

```shell
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Login using this password with username `admin`.

You are now able to access the ArgoCD web UI!

## Registering the app in ArgoCD

Accessing the Web UI at first lands you in the `Applications` category.

Register the app inside of this web UI by creating `New App`:

- Give the app a name
- Select project `default`
- Choose a sync policy `Automatic`
- Check `Auto-create Namespace`
- Specify the source URL for your repo (the one that was forked)
- Specify the path to the Kubernetes manifests being used: `manifests/`
- In `Destination`, use the default cluster URL
- In `Destination`, specify a name for your namespace (i.e. `argo-yourname`)

## How to access the deployed app

To verify that it is successfully deployed, port-forwarding is required:

```sh
# replace your namespace name
kubectl port-forward deployment/lab-frontend-app -n my-namespace 8081:8080
```

Then, navigate to http://localhost:8081 to access your pod.
