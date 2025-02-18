# Templated Spaces

This example shows how to structure a flux repo for re-use when deploying multiple spaces as well as deploying into those spaces. 


# Structure

`base` - contains the base templates that will be used by downstream kustomizations
`boostrap` - this is mostly used in the context of this exmaple, this creates the initial flux kustomization to start the syncing process.
`project` - top level folder for the project. all resources reside in this folder except for base templates
`*/setup` -  any folder titled "setup" contains the resources for setting up that particualr object on the local bootstrap cluster. These resources are never installed in Tanzu Platform but rather are used to setup the objects needed to be able to deploy to the platform.
`spaces` - all spaces will have folders nested under this

```bash
├── README.md
├── base # base templates for re-use 
│   ├── kubeconfig # kubeconfig base template
│   │   ├── kubeconfig.yml
│   │   ├── kustomization.yml
│   │   └── sample-secret.yml # not used, just shows the secret structure
│   └── space
│       ├── kustomization.yml
│       └── space.yml # base space template
├── bootstrap # intial bootstrap flux kustomization that syncs project/setup
│   ├── base.yml
│   ├── kustomization.yml
│   └── ns.yml
├── project 
│   ├── kustomization.yml # defines any resources that will be deployed into the project on TPK*s. ex. spaces, profiles, etc. 
│   ├── setup # root folder used for project setup, these resources are all install on the local bootstrap cluster. 
│   │   ├── flux-kustomization.yml # flux kustomization for targetting a tpk8s project. 
│   │   ├── kubeconfig # sets up the kubeconfig for talking to the tpk8s project using the base kubeconfig as a template
│   │   │   ├── kubeconfig-patch.yml
│   │   │   └── kustomization.yml
│   │   ├── kustomization.yml # defines the resources that should be installed on the local bootstrap cluster
│   │   ├── project-secret.yml # used for templating the kubeconfig
│   │   └── secretsetup.yml # creates the initial secretstore that is use when generating kubeconfigs
│   └── spaces  # all spaces get a nested folder here
│       ├── space-1
│       │   ├── app.yml #just an example showing how to deploying resources into a space
│       │   ├── definition
│       │   │   └── kustomization.yml # defines the space definition, this is used by the project kustomization to create the space
│       │   ├── kustomization.yml # defines the resources that should be deployed into the space
│       │   └── setup # space setup, these resources are all installed on the local bootstrap cluster. ex. flux kustomziation to target the space and it's kubeconfig
│       │       ├── flux-kustomization.yml
│       │       ├── kubeconfig
│       │       │   ├── kubeconfig-patch.yml
│       │       │   └── kustomization.yml
│       │       ├── kustomization.yml
│       │       └── space-secret.yml
│       └── space-2 # see above
│           ├── app.yml
│           ├── definition
│           │   └── kustomization.yml
│           ├── kustomization.yml
│           └── setup
│               ├── flux-kustomization.yml
│               ├── kubeconfig
│               │   ├── kubeconfig-patch.yml
│               │   └── kustomization.yml
│               ├── kustomization.yml
│               └── space-secret.yml
```

# Setup

If you have not already followed [the setup in the main Readme](../README.md#setup), do that now.


1. apply the base flux kustomization, if you already have a full gitops setup you do not need to run this manually and can add it to your existing repo. This bootstrap will create a kustomization that will bootstrap the entire process. 

```bash
kubectl apply -k bootstrap
```