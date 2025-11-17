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

Output:
Location    Name
----------  ----------------
westeurope  rg-basic-storage

# deploy a storage account

command:
az storage account create --name basicstorage$RANDOM --resource-group rg-basic-storage --location westeurope --sku standard_LRS --kind StorageV2 --output table

Output:
AccessTier    AllowBlobPublicAccess    AllowCrossTenantReplication    CreationTime                      EnableHttpsTrafficOnly    Kind       Location    MinimumTlsVersion    Name               PrimaryLocation    ProvisioningState    ResourceGroup     StatusOfPrimary
------------  -----------------------  -----------------------------  --------------------------------  ------------------------  ---------  ----------  -------------------  -----------------  -----------------  -------------------  ----------------  -----------------
Hot           False                    False                          2025-11-17T16:14:34.696687+00:00  True                      StorageV2  westeurope  TLS1_0               basicstorage10215  westeurope         Succeeded            rg-basic-storage  available

# generate key

command: 
ACCOUNT_KEY=$(az storage account keys list --resource-group rg-basic-storage --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)

output:
ERROR: argument --account-name/-n: expected one argument

# set the account-name

command:
STORAGE_ACCOUNT="basicstorage10215"

# generate key again with account-name

command:
it works, but it's secret.

# deploy blob container

command:
az storage container create --name demo-container --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --public-access off --output table

output:
Created
---------
True

# upload test-file

command:
az storage blob upload --container-name demo-container --file hello.txt --name hello.txt --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --output table

output
Finished[#############################################################]  100.0000%

# testing test file

 command:
 az storage blob list --container-name demo-container --account-name $STORAGE_ACCOUNT --account-key $ACCOUNT_KEY --output table

output:
Name       Blob Type    Blob Tier    Length    Content Type    Last Modified              Snapshot
---------  -----------  -----------  --------  --------------  -------------------------  ----------
hello.txt  BlockBlob    Hot          30        text/plain

# cleanup

command:
az group delete --name rg-basic-storage --yes --no-wait









