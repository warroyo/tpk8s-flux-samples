# Templated Spaces

This example shows how to structure a flux repo for re-use when deploying multiple spaces as well as deploying into those spaces. 


# Structure

`base` - contains the base templates that will be used by downstream kustomizations
`boostrap` - this is mostly used in the context of this exmaple, this creates the initial flux kustomization to start the syncing process.
`project` - top level folder for the project. all resources reside in this folder except for base templates
`*/setup` -  any folder titled "setup" contains the resources for setting up that particualr object on the local bootstrap cluster. These resources are never installed in Tanzu Platform but rather are used to setup the objects needed to be able to deploy to the platform.
`spaces` - all spaces will have folders nested under this

# Setup

If you have not already followed [the setup in the main Readme](../README.md#setup), do that now.


1. apply the base flux kustomization, if you already have a full gitops setup you do not need to run this manually and can add it to your existing repo. This bootstrap will create a kustomization that will bootstrap the entire process. 

```bash
kubectl apply -k bootstrap
```