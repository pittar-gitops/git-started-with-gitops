# Install and Configure OpenShift GitOps

The first step in the process is installing and configuring [OpenShift GitOps](https://docs.openshift.com/container-platform/4.9/cicd/gitops/understanding-openshift-gitops.html) (Argo CD).

You can either install the *OpenShift GitOps* operator through the OperatorHub UI in the OpenShift Admin console, or you can install it programatically using the `oc` or `kubectl` cli.

When installing you will have the option to install the operator with either the *Automatic* or *Manual* update option.  For core services such as Argo CD, I would suggest choosing the *Manual* option in order to have more control over the update process.

To install the OpenShift GitOps operator using the cli:

```
oc apply -k manifests/gitops-operator
```

After a few minutes, the operator should be installed and you should have a new `openshift-gitops` operator in your cluster that contains a special admin instance of Argo CD.

**Next:** [Configure Argo CD](02-configure-argocd.md)