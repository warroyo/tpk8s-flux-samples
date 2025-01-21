# TPK8s Flux samples


This repo has a collection of different approaches to using flux with Tanzu platform for K8s. This does not cover the base setup of Flux, Flux can be installed using the standard OSS docs or if you are using TMC(Tanzu Mission Control) you can use that to provide flux.



# Setup
This section can be used to setup the components needed to integrate flux with TPK8s. This is a common setup that will be needed for each sample to work. 

## pre-reqs

This section is done manually but if you have an existing gitops env with secrets management, you can instead use gitosp to install the pre-reqs. This will install the necessary software to be able to use flux with Tanzu Platform.


1. create the secret needed for the token controller. this should be your CSP token.

```bash
cat <<'EOF' >common/pre-reqs/generator.env
CSP_TOKEN=<your-token>
EOF
```

2. deploy the namespace, secret for the controller,  along with a flux kustomization to sync the controller and ESO.

```bash
kubectl apply -k common/pre-reqs              
```


## Samples


[no packaging](./no-packaging/) - This example does not use any k8s packaging(carve;, helm etc.) it just uses native K8s CRDs and Kustomize for any customizations. 


[basic-helm](./basic-helm/) -  this example has a basic helm chart that install an app via helm release and has a containerapp to track the resources created by helm.
