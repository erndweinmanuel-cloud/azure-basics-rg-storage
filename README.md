# azure-basics-rg-storage
Basic Azure Project - Resource Group + Storage Account + Blob Container using Azure CLI

This project demonstrates the creation of foundational Azure resources using the Azure CLI
It represents the starting point of my journey to be an Azure Administrator (AZ-104)

Main goals of this Project
- deploy a resource group
- deploy a storage account
- deploy a Blob container

 no portal clicks

 # Project Overview

 - Logging into Azure
 - creating a resource group, a storage account, creating a blob container, then verifying the deployments, cleaning up the resources at the end

   # Why this project

   - my first hands-on project
   - first CLI experience
   - prep for my AZ-104 Certification

     Let's start!
  
     # Deploy Resource-Group

     manuel [ ~ ]$ az group create --name rg-basic-storage --location westeurope
{
  "id": "/subscriptions/a51a94c7-ee9c-48b6-8880-e0c4c1452650/resourceGroups/rg-basic-storage",
  "location": "westeurope",
  "managedBy": null,
  "name": "rg-basic-storage",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
manuel [ ~ ]$

# Deploy Storage Account

manuel [ ~ ]$ az storage account create --name manuelsfirststorage1 --resource-group rg-basic-storage --location westeurope --sku Standard_LRS
{
  "accessTier": "Hot",
  "accountMigrationInProgress": null,
  "allowBlobPublicAccess": false,
  "allowCrossTenantReplication": false,
  "allowSharedKeyAccess": null,
  "allowedCopyScope": null,
  "azureFilesIdentityBasedAuthentication": null,
  "blobRestoreStatus": null,
  "creationTime": "2025-11-16T19:04:19.884111+00:00",
  "customDomain": null,
  "defaultToOAuthAuthentication": null,
  "dnsEndpointType": null,
  "enableExtendedGroups": null,
  "enableHttpsTrafficOnly": true,
  "enableNfsV3": null,
  "encryption": {
    "encryptionIdentity": null,
    "keySource": "Microsoft.Storage",
    "keyVaultProperties": null,
    "requireInfrastructureEncryption": null,
    "services": {
      "blob": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2025-11-16T19:04:20.212184+00:00"
      },
      "file": {
        "enabled": true,
        "keyType": "Account",
        "lastEnabledTime": "2025-11-16T19:04:20.212184+00:00"
      },
      "queue": null,
      "table": null
    }
  },
  "extendedLocation": null,
  "failoverInProgress": null,
  "geoReplicationStats": null,
  "id": "/subscriptions/a51a94c7-ee9c-48b6-8880-e0c4c1452650/resourceGroups/rg-basic-storage/providers/Microsoft.Storage/storageAccounts/manuelsfirststorage1",
  "identity": null,
  "immutableStorageWithVersioning": null,
  "isHnsEnabled": null,
  "isLocalUserEnabled": null,
  "isSftpEnabled": null,
  "isSkuConversionBlocked": null,
  "keyCreationTime": {
    "key1": "2025-11-16T19:04:20.212184+00:00",
    "key2": "2025-11-16T19:04:20.212184+00:00"
  },
  "keyPolicy": null,
  "kind": "StorageV2",
  "largeFileSharesState": null,
  "lastGeoFailoverTime": null,
  "location": "westeurope",
  "minimumTlsVersion": "TLS1_0",
  "name": "manuelsfirststorage1",
  "networkRuleSet": {
    "bypass": "AzureServices",
    "defaultAction": "Allow",
    "ipRules": [],
    "ipv6Rules": [],
    "resourceAccessRules": null,
    "virtualNetworkRules": []
  },
 
{
  
}
```  
# deploy a Blob-Container

  generate the key

  manuel [ ~ ]$ az storage account keys list --account-name manuelsfirststorage1 --resource-group rg-basic-storage --query "[0].value" -o tsv

export AZURE_STORAGE_KEY=""
manuel [ ~ ]$ echo $AZURE_STORAGE_KEY | head -c 20; echo
fvhB8us9/qVp3wBRW9Zc

manuel [ ~ ]$ export AZURE_STORAGE_ACCOUNT="manuelsfirststorage1"
manuel [ ~ ]$ echo $AZURE_STORAGE_ACCOUNT

Deploy the blob container

manuel [ ~ ]$ az storage container create --name myfirstcontainer --account-name $AZURE_STORAGE_ACCOUNT --account-key "$AZURE_STORAGE_KEY"
{
  "created": true
}
manuel [ ~ ]$ 

# delete all

manuel [ ~ ]$ az group delete --name rg-basic-storage --yes --no-wait
manuel [ ~ ]$ az group list -o table
Name                            Location    Status
------------------------------  ----------  ---------
cloud-shell-storage-westeurope  westeurope  Succeeded
rg-basic-storage                westeurope  Deleting



