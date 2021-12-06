# Your First GitOps Repo

As admins, the first GitOps repo you will create will be one to manage admin-level cluster configuration.  This can include:

* Namespace creation and configuration
* Operator installation
* Group creating and management
* Additional Argo CD instances

First, we will focus a bit on repository layout.

Gerald Nunn has a great [GitOps Standards](https://github.com/gnunn-gitops/standards) repository with opinions on how to layout directories and handle tenants.  This repository is heavily influenced by Geralds' document.

## Admins Repository

When first starting with GitOps, it's easiest to take a "mono repo" approach - at least for the adminstrators GitOps repository.

This means that the configuration for all of your clusters will be contained in a single repository, with different Argo CD *Applications* referencing specific environmental *overlays*.  The next section assumes a basic understanding of both Argo CD and Kustomize.

### Structure

The structure of your admins repository depends on what aspects of your clusters you want to control using GitOps / Argo CD.  It's important to note that you can start with one or two of the main concepts, and add them as your process matures.  For now, we will discuss four top-level folders for this repository:

* **argocd:** A directory that contains Argo CD *AppProject* and *Project* resources for all environments.
* **cluster-config:** Cluster configuration (groups, roles, etc...)
* **cluster-services:** User workload monitoring, web terminal, and other operator instances.
* **tentants**: Namespaces and configuration for project teams (tenants).

For the next section we will focus on the **argocd** and **tenants** directories.

**Next:** [App-of-Apps for Cluster Configuration](04-admin-app-of-apps.md)