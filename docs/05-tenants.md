# Tenants

Most OpenShift clusters are considered "multi-tenant".  For the purposes of this tutorial, a "Tenant" can be considered a development team that has access to one or more namespaces.

For this example, we will consider a project team "alpha" that has four namespaces: `alpha-cicd`, `alpha-dev`, `alpha-test`, and `alpha-prod`.

Looking at the directory structure of our GitOps mono-repo, these would fall under the *tenants* top level directory like so:

```
argocd/
tenants/
├── alpha/
│   └──  namespaces/
│   │   └── alpha-cicd/
│   │   └── alpha-dev/
│   │   └── alpha-test/
│   │   └── alpha-prod/
│   │   └── kustomization.yaml
│   └──  group-membership/
```

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




**Next:** [Tenants](05-tenants.md)