# No Packing 

This example does not use any K8s packaging software, so there is no use of helm or carvel etc. This approach uses Kustomize and native k8s resources like `Deployments`. This is a good approach if you are looking to just use Kustomize and want to manage K8s resources without any abstraction around them. This example has been simplified so it only handles one clustergroup, project and space. This could easily be extended into a larger repos with multiple of each.




# Architecture




# Setup

This assumes you have already installed Flux. 