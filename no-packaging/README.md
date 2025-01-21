# No Packing 

This example does not use any K8s packaging software, so there is no use of helm or carvel etc. This approach uses Kustomize and native k8s resources like `Deployments`. This is a good approach if you are looking to just use Kustomize and want to manage K8s resources without any abstraction around them. This example has been simplified so it only handles one clustergroup, project and space. This could easily be extended into a larger repos with multiple of each.



# Structure

`bootstrap` - contains the initial boostrap resources, this sets up the kustomization to sync all of the resources
`flux-resources` -  this is what the boostrap targets, this imports the kubeconfig secrets  and creates a kustomization per context(space,clustergroup,project)
`space` - contains all resources applied to a space, in this case the raw k8s yaml to be applied to the space.
`project` - contains all resources applied to the project, this creates the space.
`clustergroup` -  contains all resources applied to the clustergroup, in this case it adds the required capabilities for deployments.

# Architecture




# Setup

If you have not already followed [the setup in the main Readme](../README.md#setup), do that now.


1. apply the base flux kustomization, if you already have a full gitops setup you do not need to run this manually and can add it to your existing repo. This bootstrap will create a kustomization that will bootstrap the entire process. 

```bash
kubectl apply -k bootstrap
```