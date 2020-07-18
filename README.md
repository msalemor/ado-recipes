
# ADO Recipies

## Azure Services

- Azure DevOps (ADO)

## General Information

### Yaml pipelines vs legacy experience

- Recommended to use Yaml pipelines instead of legacy experience

### GitFlow branching strategy

- "The Gitflow Workflow defines a strict branching model designed around the project release. This provides a robust framework for managing larger projects."
  - https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow  

### Branch Policies

- Enable branch policies with reviewers
- Enabling policies will require pull requests

### Secret Management

- Leverage Key Vault as for variables in the pipelines
- Use Managed Identity (no secrets)

### Variables in pipelines

- There are local and global variables (i.e. Build.BuildId).
- Make sure to work with the correct variables in CI and CD pipelines.
- ADO can store secrets, but it is best to integrate with Key Vault.

### Yaml Templates

- Yaml templates can be used to create custom steps in a Yaml pipeline
- If many pipelines exists and these share common steps, the common steps can be extracted to a template

### Tasks

- There are many pre-built tasks available.
- There's a market place with more extensions for additional functionality.
- You can alway create your own custom scripts with powershell, Azure CLI, Bash, etc.

### General Code Building Steps

- Build
  - The code is compiled
- Test
  - Unit tests run
  - If the tests fail the pipeline stops (this is configurable)
- Copy Airtifacts
  - Copies the output of the building step (i.e. the executable, DLLs, zip, et.c) to the publishing staging area
- Publish Artifacts
  - Publish the artifcats in the staging area to the drop location

### General Image building, tagging, pubshing and deploying steps

- Build the image from the DockerFile
- Tag the image with the new tag
- Push the image to the repository
- Deploy the manifest file (i.e AKS) with the new tagged image


### Releasing non-buildable code (ARM Templates, etc.)

- Trigger release pipeline from approving a pull request
- In the release pipeline add code a step to for example copy the files or to deploy the files to a target environment

## Recipies

- [ARM Template](arm-template.md)
- [ARM Template, C# APP Service, SQL](arm-appservice-sql.md)
- [REACT Application to Storage Account Static Page](spa-to-staticpage.md)
- [Build docker image and deploy to AKS](docker-build-aks.md)
- [Docker image with ConfigMap and AKS](docker-aks-config-map.md)
- [API and Azure Functions](apim-functions.md)

## Tips and Trics

- [Tips and tricks](tips-and-tricks.md)