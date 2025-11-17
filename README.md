# azure-basics-rg-storage
Basic Azure Project – Resource Group + Storage Account + Blob Container using Azure CLI

This project demonstrates the creation of foundational Azure resources using the Azure CLI.  
It represents the starting point of my journey to become an Azure Administrator (AZ-104).  
All resources were deployed without using the Azure Portal.

---

## Goals
- Deploy a Resource Group  
- Deploy a Storage Account (StorageV2)  
- Deploy a Blob Container  
- Practice Azure CLI fundamentals  
- Build foundation for future AZ-104 projects  

---

## Prerequisites
- Azure Subscription  
- Azure CLI or Azure Cloud Shell  

---

## Step 1 – Create Resource Group
```bash
az group create --name rg-basic-storage --location westeurope --output table
```

## Step 2 – Define Storage Account Name
```bash
STORAGE_ACCOUNT="basicstorage$RANDOM"
```

## Step 3 – Create Storage Account
```bash
az storage account create \
  --name $STORAGE_ACCOUNT \
  --resource-group rg-basic-storage \
  --location westeurope \
  --sku Standard_LRS \
  --kind StorageV2 \
  --output table
```

## Step 4 – Retrieve Access Key
(key is NOT stored in the repository)
```bash
ACCOUNT_KEY=$(az storage account keys list \
  --resource-group rg-basic-storage \
  --account-name $STORAGE_ACCOUNT \
  --query "[0].value" -o tsv)
```

## Step 5 – Create Blob Container
```bash
az storage container create \
  --name demo-container \
  --account-name $STORAGE_ACCOUNT \
  --account-key $ACCOUNT_KEY \
  --public-access off \
  --output table
```

## Step 6 – Upload Test File (optional)
```bash
echo "Hello Azure" > hello.txt
```
```bash
az storage blob upload \
  --container-name demo-container \
  --file hello.txt \
  --name hello.txt \
  --account-name $STORAGE_ACCOUNT \
  --account-key $ACCOUNT_KEY \
  --output table
```
## Step 7 – Verify Blob Upload
```bash
az storage blob list \
  --container-name demo-container \
  --account-name $STORAGE_ACCOUNT \
  --account-key $ACCOUNT_KEY \
  --output table
```

## Step 8 – Cleanup Resources
```bash
az group delete --name rg-basic-storage --yes --no-wait
```
## Learnings

- First hands-on Azure CLI experience

- Safe handling of environment variables and account keys

- Understanding core Azure resources (Resource Groups, Storage Accounts, Blob Containers)

- Improved command-line workflow

- Solid foundation for upcoming AZ-104 compute/networking projects














