---
title: Koppelen van een volume van de Azure-bestanden in Azure Containerexemplaren
description: Meer informatie over het koppelen van een Azure-bestanden volume om te blijven behouden status met exemplaren van Azure-Container
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 4248a3769ba8a0fb067b3904d55d487fe67e5778
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="5b389-103">Koppelen van een Azure-bestandsshare met exemplaren van Azure-Container</span><span class="sxs-lookup"><span data-stu-id="5b389-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="5b389-104">Standaard zijn exemplaren van Azure-Container staatloze.</span><span class="sxs-lookup"><span data-stu-id="5b389-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="5b389-105">Als de container vastloopt of stopt, gaat alle van de status verloren.</span><span class="sxs-lookup"><span data-stu-id="5b389-105">If the container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="5b389-106">Om te blijven behouden status afgezien van de levensduur van de container, moet u een volume koppelen vanuit een externe winkel.</span><span class="sxs-lookup"><span data-stu-id="5b389-106">To persist state beyond the lifetime of the container, you must mount a volume from an external store.</span></span> <span data-ttu-id="5b389-107">In dit artikel laat zien hoe een Azure-bestandsshare voor gebruik met Azure Containerexemplaren te koppelen.</span><span class="sxs-lookup"><span data-stu-id="5b389-107">This article shows how to mount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="5b389-108">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="5b389-108">Create an Azure file share</span></span>

<span data-ttu-id="5b389-109">Voordat u een Azure-bestandsshare met exemplaren van Azure-Container, moet u deze maken.</span><span class="sxs-lookup"><span data-stu-id="5b389-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="5b389-110">Voer het volgende script voor het maken van een opslagaccount voor het hosten van de bestandsshare en de share zelf.</span><span class="sxs-lookup"><span data-stu-id="5b389-110">Run the following script to create a storage account to host the file share and the share itself.</span></span> <span data-ttu-id="5b389-111">Houd er rekening mee dat de opslagaccountnaam moet globaal uniek zijn, zodat het script voegt een willekeurige waarde toe aan de basis-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5b389-111">Note that the storage account name must be globally unique, so the script adds a random value to the base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create the storage account with the parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="5b389-112">De accountdetails toegang tot opslag verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5b389-112">Acquire storage account access details</span></span>

<span data-ttu-id="5b389-113">Een Azure-bestandsshare als een volume in Azure Containerexemplaren koppelen, moet u drie waarden: naam van het opslagaccount, de sharenaam van de en de toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="5b389-113">To mount an Azure file share as a volume in Azure Container Instances, you need three values: the storage account name, the share name, and the storage access key.</span></span> 

<span data-ttu-id="5b389-114">Als u het bovenstaande script gebruikt, wordt de naam van het opslagaccount is gemaakt met een willekeurige waarde aan het einde.</span><span class="sxs-lookup"><span data-stu-id="5b389-114">If you used the script above, the storage account name was created with a random value at the end.</span></span> <span data-ttu-id="5b389-115">Om te vragen van de laatste tekenreeks (inclusief het willekeurig gedeelte), gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5b389-115">To query the final string (including the random portion), use the following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="5b389-116">Al bekend is de sharenaam (is *acishare* in het bovenstaande script), zodat alle dat u hoeft alleen nog de opslagaccountsleutel die kan worden gevonden met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5b389-116">The share name is already known (it is *acishare* in the script above), so all that remains is the storage account key, which can be found using the following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="5b389-117">Storage-account toegangsgegevens met Azure sleutelkluis opslaan</span><span class="sxs-lookup"><span data-stu-id="5b389-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="5b389-118">Toegangscodes voor opslag beveiligen toegang tot uw gegevens, zodat we het beste opslaan in een Azure sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="5b389-118">Storage account keys protect access to your data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="5b389-119">Een sleutelkluis maken met de Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5b389-119">Create a key vault with the Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="5b389-120">De `enabled-for-template-deployment` switch kunt Azure Resource Manager pull geheimen van de sleutelkluis tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="5b389-120">The `enabled-for-template-deployment` switch allows Azure Resource Manager to pull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="5b389-121">De opslagaccountsleutel opslaan als een nieuwe geheim in de sleutelkluis:</span><span class="sxs-lookup"><span data-stu-id="5b389-121">Store the storage account key as a new secret in the key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-the-volume"></a><span data-ttu-id="5b389-122">Het volume koppelen</span><span class="sxs-lookup"><span data-stu-id="5b389-122">Mount the volume</span></span>

<span data-ttu-id="5b389-123">Koppelen van een Azure-bestandsshare als een volume in een container is een proces.</span><span class="sxs-lookup"><span data-stu-id="5b389-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="5b389-124">Eerst u de details van de share als onderdeel van het definiëren van de containergroep opgeeft, vervolgens u opgeven hoe u het volume dat is gekoppeld in een of meer van de containers in de groep wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5b389-124">First, you provide the details of the share as part of defining the container group, then you specify how you want the volume mounted within one or more of the containers in the group.</span></span>

<span data-ttu-id="5b389-125">Om te definiëren van de volumes die u beschikbaar wilt maken voor het koppelen, Voeg een `volumes` matrix naar de definitie van de container in de Azure Resource Manager-sjabloon en klik vervolgens in de definitie van de afzonderlijke containers verwijzing.</span><span class="sxs-lookup"><span data-stu-id="5b389-125">To define the volumes you want to make available for mounting, add a `volumes` array to the container group definition in the Azure Resource Manager template, then reference them in the definition of the individual containers.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

<span data-ttu-id="5b389-126">De sjabloon bevat de naam van het opslagaccount en de sleutel als parameters die in een afzonderlijke parameterbestand kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5b389-126">The template includes the storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="5b389-127">Om te voorzien van het parameterbestand, moet u drie waarden: naam van het opslagaccount, de bron-ID van uw Azure sleutelkluis en de geheime naam van sleutelkluis die u hebt gebruikt voor het opslaan van de opslagsleutel.</span><span class="sxs-lookup"><span data-stu-id="5b389-127">To populate the parameters file, you will need three values: the storage account name, the resource ID of your Azure key vault, and the key vault secret name that you used to store the storage key.</span></span> <span data-ttu-id="5b389-128">Als u de vorige stappen hebt gevolgd, kunt u deze waarden met het volgende script kunt krijgen:</span><span class="sxs-lookup"><span data-stu-id="5b389-128">If you have followed previous steps, you can get these values with the following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="5b389-129">Voeg de waarden in het parameterbestand:</span><span class="sxs-lookup"><span data-stu-id="5b389-129">Insert the values into the parameters file:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-the-container-and-manage-files"></a><span data-ttu-id="5b389-130">De container implementeren en beheren van bestanden</span><span class="sxs-lookup"><span data-stu-id="5b389-130">Deploy the container and manage files</span></span>

<span data-ttu-id="5b389-131">Met de sjabloon is gedefinieerd, kunt u de container maken en koppelen van het volume met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5b389-131">With the template defined, you can create the container and mount its volume using the Azure CLI.</span></span> <span data-ttu-id="5b389-132">Ervan uitgaande dat de naam van het sjabloonbestand *azuredeploy.json* en met de naam van het parameterbestand *azuredeploy.parameters.json*, dan is de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="5b389-132">Assuming that the template file is named *azuredeploy.json* and that the parameters file is named *azuredeploy.parameters.json*, then the command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="5b389-133">Nadat de container wordt gestart, kunt u de eenvoudige web-app geïmplementeerd de **aci-seanmckenna-hellofiles** installatiekopie naar de bestanden beheren in de Azure-bestandsshare op de koppelpad die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5b389-133">Once the container starts up, you can use the simple web app deployed via the **seanmckenna/aci-hellofiles** image, to the manage files in the Azure file share at the mount path that you specified.</span></span> <span data-ttu-id="5b389-134">Het IP-adres voor de web-app via de volgende verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="5b389-134">Obtain the ip address for the web app via the following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="5b389-135">U kunt een hulpprogramma zoals de [Microsoft Azure Storage Explorer](http://storageexplorer.com) op te halen en het controleren van het bestand writen naar de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="5b389-135">You can use a tool like the [Microsoft Azure Storage Explorer](http://storageexplorer.com) to retrieve and inspect the file writen to the file share.</span></span>

>[!NOTE]
> <span data-ttu-id="5b389-136">Zie voor meer informatie over het gebruik van Azure Resource Manager-sjablonen, parameterbestanden en implementeren met de Azure CLI [implementeren van resources met Resource Manager-sjablonen en Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5b389-136">To learn more about using Azure Resource Manager templates, parameter files, and deploying with the Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b389-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b389-137">Next steps</span></span>

- <span data-ttu-id="5b389-138">Implementeren voor uw eerste container met de Azure-Container instanties [snel starten](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="5b389-138">Deploy for your first container using the Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="5b389-139">Meer informatie over de [relatie tussen Azure Containerexemplaren en container orchestrators](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="5b389-139">Learn about the [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
