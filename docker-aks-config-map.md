# Deploy Docker Image to AKS with a ConfigMap


## Objective 

- Deploy a docker image that leverages a ConfigMap as a settings file. 
- Under this configuration a new image is tagged with a new release and can be deployed when the ConfigMap is updated or when a new image is available.

## Azure Services

- Azure Kubernetes Service (AKS)
- Azure Container Registry (ACR)
  - Enable the admin account 
  - Remember to add pull RBAC to the AKS SP (Service Principal)
- KeyVault
- Azure DevOPs

## ADO Configuration and best practices

- Enable policies on branches to require reviews during pull requests.
- Use a GitFlow strategy to manage branching, release, and hot fix strategies.
- Use KeyVault to manage secrets or leverage Managed Identities

## Deploy code to Repo

- Use GitFlow strategy
- Checkin in the settings file in main
- Checking k8s service manifest file main
- Create a develop branch from main
- Create a release branch from the develop branch
- Submit pull request

## Secrets

- Create Key Vault
- Add secrets to Key vault (i.e. docker user id/pwd)

## Release pipeline

- Enable continus deployment from the repo on release/*
- Create a bash release step
- Create the variable for the release associated with kv
- Get the secrets from the variables associated with kv
- Login into docker with credentials
- Pull the latest image
- Tag latest image with the build number
- Push the image to ACR or docker hub
- Update the manifest file with the latest tag
- Apply the new manifest in kubernetes
- To deploy to higher environments enable X with approvals

