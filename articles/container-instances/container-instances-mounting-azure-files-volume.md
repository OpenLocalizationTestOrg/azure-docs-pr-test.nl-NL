---
title: een Azure-bestanden volume in Azure Containerexemplaren aaaMounting
description: Meer informatie over hoe toomount een Azure-bestanden volume toopersist status met exemplaren van Azure-Container
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
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="09314-103">Koppelen van een Azure-bestandsshare met exemplaren van Azure-Container</span><span class="sxs-lookup"><span data-stu-id="09314-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="09314-104">Standaard zijn exemplaren van Azure-Container staatloze.</span><span class="sxs-lookup"><span data-stu-id="09314-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="09314-105">Als Hallo container vastloopt of stopt, gaat alle van de status verloren.</span><span class="sxs-lookup"><span data-stu-id="09314-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="09314-106">toopersist status buiten Hallo levensduur van Hallo-container, moet u een volume koppelen vanuit een externe winkel.</span><span class="sxs-lookup"><span data-stu-id="09314-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="09314-107">Dit artikel laat zien hoe toomount een Azure-bestandsshare voor gebruik met Azure Containerexemplaren.</span><span class="sxs-lookup"><span data-stu-id="09314-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="09314-108">Een Azure-bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="09314-108">Create an Azure file share</span></span>

<span data-ttu-id="09314-109">Voordat u een Azure-bestandsshare met exemplaren van Azure-Container, moet u deze maken.</span><span class="sxs-lookup"><span data-stu-id="09314-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="09314-110">Uitvoeren van script toocreate na Hallo een account toohost hello opslagbestandsshare en Hallo delen zelf.</span><span class="sxs-lookup"><span data-stu-id="09314-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="09314-111">Houd er rekening mee dat Hallo opslagaccountnaam moet globaal uniek zijn, dus Hallo script een willekeurige waarde toohello base-tekenreeks voegt.</span><span class="sxs-lookup"><span data-stu-id="09314-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="09314-112">De accountdetails toegang tot opslag verkrijgen</span><span class="sxs-lookup"><span data-stu-id="09314-112">Acquire storage account access details</span></span>

<span data-ttu-id="09314-113">toomount een Azure-bestandsshare als een volume in Azure Containerexemplaren, moet u drie waarden: Hallo opslagaccountnaam Hallo sharenaam en Hallo-toegangssleutel voor opslag.</span><span class="sxs-lookup"><span data-stu-id="09314-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="09314-114">Als u bovenstaande Hallo-script gebruikt, is met een willekeurige waarde aan einde Hallo Hallo opslagaccountnaam gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09314-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="09314-115">tooquery hello laatste tekenreeks (inclusief Hallo willekeurige gedeelte), gebruikt u Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="09314-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="09314-116">Hallo sharenaam al bekend is (is *acishare* in Hallo script hierboven), zodat alles wat u hoeft alleen nog Hallo opslagaccountsleutel, die kan worden gevonden met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="09314-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="09314-117">Storage-account toegangsgegevens met Azure sleutelkluis opslaan</span><span class="sxs-lookup"><span data-stu-id="09314-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="09314-118">Toegangscodes voor opslag beveiligen tooyour toegangsgegevens, zodat we het beste opslaan in een Azure sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="09314-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="09314-119">Een sleutelkluis maken Hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="09314-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="09314-120">Hallo `enabled-for-template-deployment` switch biedt de mogelijkheid Azure Resource Manager toopull geheimen van de sleutelkluis tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="09314-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="09314-121">Hallo opslagaccountsleutel opslaan als een nieuwe geheim in de sleutelkluis Hallo:</span><span class="sxs-lookup"><span data-stu-id="09314-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="09314-122">Hallo volume koppelen</span><span class="sxs-lookup"><span data-stu-id="09314-122">Mount hello volume</span></span>

<span data-ttu-id="09314-123">Koppelen van een Azure-bestandsshare als een volume in een container is een proces.</span><span class="sxs-lookup"><span data-stu-id="09314-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="09314-124">Eerst bieden Hallo details van de share als onderdeel van het definiëren van de containergroep Hallo Hallo daarna u hoe u Hallo volume is gekoppeld in één of meer containers in de groep Hallo Hallo wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="09314-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="09314-125">toodefine hello volumes toomake beschikbaar voor gewenste koppelen, Voeg een `volumes` matrix toohello container groepsdefinitie in hello Azure Resource Manager-sjabloon en klik vervolgens in Hallo definitie van de afzonderlijke containers Hallo verwijzing.</span><span class="sxs-lookup"><span data-stu-id="09314-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="09314-126">Hallo-sjabloon bevat Hallo opslagaccountnaam en sleutel als parameters die in een afzonderlijke parameterbestand kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="09314-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="09314-127">toopopulate hello parameterbestand, moet u drie waarden: Hallo opslagaccountnaam en geheime sleutelkluisnaam die u hebt gebruikt toostore hello opslagsleutel Hallo Hallo bron-ID van uw Azure sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="09314-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="09314-128">Als u de vorige stappen hebt gevolgd, kunt u deze waarden kunt krijgen met Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="09314-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="09314-129">Hallo waarden invoegen in het parameterbestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="09314-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="09314-130">Hallo-container implementeren en beheren van bestanden</span><span class="sxs-lookup"><span data-stu-id="09314-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="09314-131">U kunt met het Hallo-sjabloon is gedefinieerd, Hallo container maken en koppelen van het volume met behulp van hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="09314-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="09314-132">Ervan uitgaande dat hello sjabloonbestand heet *azuredeploy.json* en de naam van dat bestand van de parameters Hallo *azuredeploy.parameters.json*, dan is Hallo vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="09314-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="09314-133">Zodra het Hallo-container wordt gestart, kunt u Hallo eenvoudige web-app is geïmplementeerd via Hallo **aci-seanmckenna-hellofiles** afbeelding toohello beheren van bestanden in Azure Hallo-bestandsshare op Hallo koppelpad die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="09314-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="09314-134">Hallo IP-adres voor web-app via de volgende Hallo Hallo verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="09314-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="09314-135">U kunt een hulpprogramma zoals Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve en Hallo writen toohello bestand bestandsshare controleren.</span><span class="sxs-lookup"><span data-stu-id="09314-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="09314-136">Zie toolearn meer over het gebruik van Azure Resource Manager-sjablonen, parameterbestanden, en implementeren met Azure CLI Hallo [implementeren van resources met Resource Manager-sjablonen en Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="09314-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09314-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09314-137">Next steps</span></span>

- <span data-ttu-id="09314-138">Implementeren voor uw eerste container met hello Azure Container instanties [snel starten](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="09314-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="09314-139">Meer informatie over Hallo [relatie tussen Azure Containerexemplaren en container orchestrators](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="09314-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
