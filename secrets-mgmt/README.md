# Basic Helm

This example shows how to setup TPK8s with flux for deploying a simple helm chart. It covers setting up the capabilties needs, a space with the correct profiles, and deploying the app to that space.


# Structure

`app-chart` - simple helm chart for the app
`bootstrap` - contains the initial boostrap resources, this sets up the kustomization to sync all of the resources
`flux-resources` -  this is what the boostrap targets, this imports the kubeconfig secrets  and creates a kustomization per context(space,clustergroup,project)
`space` - contains all resources applied to a space, in this case the helm release and a containerapp
`project` - contains all resources applied to the project, this creates the space.
`clustergroup` -  contains all resources applied to the clustergroup, in this case it adds the  required flux capabilties for helm and source.

# Architecture




# Setup

If you have not already followed [the setup in the main Readme](../README.md#setup), do that now.


1. apply the base flux kustomization, if you already have a full gitops setup you do not need to run this manually and can add it to your existing repo. This bootstrap will create a kustomization that will bootstrap the entire process. 

```bash
kubectl apply -k bootstrap
```