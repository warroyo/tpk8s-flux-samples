# TPK8s Flux samples


This repo has a collection of different approaches to using flux with Tanzu platform for K8s. This does not cover the base setup of Flux, Flux can be installed using the standard OSS docs or if you are using TMC(Tanzu Mission Control) you can use that to provide flux.



# Setup
This section can be used to setup the components needed to integrate flux with TPK8s. This is a common setup that will be needed for each sample to work. 

## pre-reqs

This section is done manually but if you have an existing gitops env with secrets management, you can instead use gitosp to install the pre-reqs. This will install the necessary software to be able to use flux with Tanzu Platform.

1. update the [kubeconfigs](./common/kubeconfigs/) to use your server urls. Each url can be found by running the following per context. below is an example for project context.

```bash
tanzu project use AMER-West
export KUBECONFIG=~/.config/tanzu/kube/config
kubectl config view --minify -o json | jq -r '.clusters[0].cluster.server'
```

2. create the secret needed for the token controller. this should be your CSP token.

```bash
cat <<'EOF' >common/pre-reqs/generator.env
CSP_TOKEN=<your-token>
EOF
```

3. deploy the namespace, secret for the controller,  along with a flux kustomization to sync the controller, ESO, and kubconfigs.

```bash
kubectl apply -k common/pre-reqs              
```


## Samples

Follow the readme in each sample for how to deploy. 

[secrets-mgmt](./secrets-mgmt/) - This exmaple shows how to manage secrets in a gitops way using [ESO](https://external-secrets.io/latest/) and TPK8s. 


[basic-helm](./basic-helm/) -  this example has a basic helm chart that install an app via helm release and has a containerapp to track the resources created by helm.
