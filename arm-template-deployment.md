# ARM Template Deploymanet

## Benefits And Best Practicies

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview#why-choose-arm-templates
- https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-best-practices

## Sample ARM Template

- [azuredeploy.json](azuredeploy.json)

```bash
# Manual deployment using Azure CLI
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-file "$HOME/azuredeploy.json"
```