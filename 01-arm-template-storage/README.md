# Azure ARM Template - Storage Account

## Objective
Deploy an Azure Storage Account using an Azure Resource Manager (ARM) template and Azure CLI.

## What I Did
- Created an Azure Resource Group
- Created an ARM template using JSON
- Deployed the ARM template using Azure CLI
- Added an Azure Storage Account to the ARM template
- Successfully deployed the Storage Account to Azure

## Technologies
- Microsoft Azure
- Azure Resource Manager (ARM)
- Azure CLI
- JSON
- Infrastructure as Code (IaC)

## Resources
- Resource Group: `sean-arm-lab`
- Storage Account: `seanaz104storage001`

## Key Concepts Learned
- ARM templates
- Declarative infrastructure
- Infrastructure as Code
- Resource groups
- Azure CLI deployments
- Incremental deployments


## Update: Parameters and Outputs

Expanded the ARM template to make the Storage Account deployment more reusable and configurable.

### Parameters

Added a `storageAccountType` parameter to allow the Storage Account SKU to be selected during deployment instead of hardcoding the value.

Allowed values:

- Standard_LRS
- Standard_GRS
- Standard_ZRS
- Premium_LRS

### Outputs

Added an ARM template output using the `reference()` function to retrieve the Storage Account's primary endpoints after deployment.

### Deployment

Deployed the updated template using Azure CLI through Azure Cloud Shell:

```bash
az deployment group create \
  --resource-group sean-arm-lab \
  --template-file azuredeploy.json \
  --parameters storageAccountType=Standard_LRS
