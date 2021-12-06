# Configure OpenShift GitOps

Now that the admin instance of Argo CD has been deployed, you will most likely want to customize it.  This is done by patching the `ArgoCD` custom resource in the `openshift-gitops` namespace.

In the `manifests/gitops-instance` folder is an example patch you can use.  It adds the following configutation:

* Edge terminated route
* Use Dex to integrate OpenShift OAuth for login
* Resource customizations for health checks and to ignore certain differences
* Configures default RBAC

```
oc patch argocd openshift-gitops -n openshift-gitops \
    --type='merge' \
    --patch "$(cat manifests/gitops-instance/argocd-patch.yaml)"
```

Once the patch is applied, the OpenShift GitOps operator will update the current Argo CD instance to reflect the changes.

You're now ready to start doing some GitOps!

**Next:** [Your First GitOps Repository](03-first-gitops-repo.md)