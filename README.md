# TPK8s Flux samples


This repo has a collection of different approaches to using flux with Tanzu platform for K8s. This does not cover the base setup of Flux, Flux can be installed using the standard OSS docs or if you are using TMC(Tanzu Mission Control) you can use that to provide flux. [This repo](https://github.com/warroyo/tpk8s-gitops) can be referenced for how to setup flux to work with TPK8s. 



# Setup

This repo assumes that you have setup Flux to connect to TPK8s. Specifically you will need to follow the instructions [here](https://github.com/warroyo/tpk8s-gitops) to setup the controller that handles getting a token to talk to the TPK8s API that will be used by Flux. 

## Samples


[no packaging](./no-packaging/) - This example does not use any k8s packaging(carve;, helm etc.) it just uses native K8s CRDs and Kustomize for any customizations. 



