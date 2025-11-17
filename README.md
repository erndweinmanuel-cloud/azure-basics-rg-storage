# azure-basics-rg-storage
Basic Azure Project - Resource Group + Storage Account + Blob Container using Azure CLI

This project demonstrates the creation of foundational Azure resources using the Azure CLI
It represents the starting point of my journey to be an Azure Administrator (AZ-104)

Main goals of this Project
- deploy a resource group
- deploy a storage account
- deploy a Blob container

 no portal clicks

# deploy a Resource Group

command:
az group create --name rg-basic-storage --location westeurope --output table


# deploy a storage account

command:
az storage account create --name basicstorage$RANDOM --resource-group rg-basic-storage --location westeurope --sku standard_LRS --kind StorageV2 --output table

# set the account-name

command:
STORAGE_ACCOUNT=basicstorage$RANDOM

# generate key with account-name

# deploy blob container

command:
az storage container create --name demo-container --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --public-access off --output table


# upload test-file

command:
az storage blob upload --container-name demo-container --file hello.txt --name hello.txt --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --output table


# verify blob upload

 command:
 az storage blob list --container-name demo-container --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --output table

# cleanup

command:
az group delete --name rg-basic-storage --yes --no-wait









