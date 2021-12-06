# Admin "App of Apps"

The "App-of-Apps" pattern is extremely popular in the Argo CD community.  The [ApplicationSet](https://argocd-applicationset.readthedocs.io/en/stable/) will someday replace this pattern, but for now, App-of-Apps is the way to go if you want some form of ordering in the way your GitOps repository is applied to your cluster.  Hint: It uses [Sync Waves](https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/)

The pattern works exactly how it sounds... you have an Argo CD application that creates more Argo CD applications.  This allows you to bootstrap with fewer `oc` or `kubectl` commands, and lets you manage the entire state of a cluster with a root Argo CD *Application*.  Let's dig in.

## The bootstrap AppProject and Application

First, let's talk directory structure.

In your top level `argocd` directory, you will should create a new directory called `clusters`.  Inside this directory, there should be a directory for each cluster you want to manage with Argo CD.  For example:

```
argocd/
├── clusters/
│   ├── non-prod/
│   └── prod/
```

Inside these directories you will see a similar structure to the rest of the top-level structure.  For example, if we expand "non-prod":

```
argocd/
├── clusters/
│   └── non-prod/
│       ├── bootstrap/
│       └── cluster-config/
│       └── cluster-services/
│       └── tenants/
│       └── kustomization.yaml
│   └── prod/
```

For now, we'll keep it simply and only include bootstrap and tenants:

```
argocd/
├── clusters/
│   └── non-prod/
│       ├── bootstrap/
│       └── tenants/
│       └── kustomization.yaml
│   └── prod/
```

The *bootstrap* directory will contain the main `AppProject` and `Project` that will create the rest of the Argo CD projects that make up the cluster.

For example: [Example bootstrap directory](https://github.com/pittar-gitops/gitops-mono-repo-admins/tree/main/01-argocd/01-clusters/nonprod/00-bootstrap)

What you see here is an `AppProject` (called `bootstrap`) that will hold the bootstrap `Application`. The bootstrap `Application` refers to the directory `argocd/clusters/non-prod`, which as a `kustomization.yaml` file that lists the various subdirectories as it's bases (except for `bootstrap`, of course).  These sub directories contain their own `AppProject`, as well as a `kustomization.yaml` file that links to directories with `Applications` specific to the target cluster.


**Next:** [Tenants](05-tenants.md)