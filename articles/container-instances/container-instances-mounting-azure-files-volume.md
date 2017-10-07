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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Koppelen van een Azure-bestandsshare met exemplaren van Azure-Container

Standaard zijn exemplaren van Azure-Container staatloze. Als Hallo container vastloopt of stopt, gaat alle van de status verloren. toopersist status buiten Hallo levensduur van Hallo-container, moet u een volume koppelen vanuit een externe winkel. Dit artikel laat zien hoe toomount een Azure-bestandsshare voor gebruik met Azure Containerexemplaren.

## <a name="create-an-azure-file-share"></a>Een Azure-bestandsshare maken

Voordat u een Azure-bestandsshare met exemplaren van Azure-Container, moet u deze maken. Uitvoeren van script toocreate na Hallo een account toohost hello opslagbestandsshare en Hallo delen zelf. Houd er rekening mee dat Hallo opslagaccountnaam moet globaal uniek zijn, dus Hallo script een willekeurige waarde toohello base-tekenreeks voegt.

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

## <a name="acquire-storage-account-access-details"></a>De accountdetails toegang tot opslag verkrijgen

toomount een Azure-bestandsshare als een volume in Azure Containerexemplaren, moet u drie waarden: Hallo opslagaccountnaam Hallo sharenaam en Hallo-toegangssleutel voor opslag. 

Als u bovenstaande Hallo-script gebruikt, is met een willekeurige waarde aan einde Hallo Hallo opslagaccountnaam gemaakt. tooquery hello laatste tekenreeks (inclusief Hallo willekeurige gedeelte), gebruikt u Hallo volgende opdrachten:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Hallo sharenaam al bekend is (is *acishare* in Hallo script hierboven), zodat alles wat u hoeft alleen nog Hallo opslagaccountsleutel, die kan worden gevonden met Hallo volgende opdracht:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Storage-account toegangsgegevens met Azure sleutelkluis opslaan

Toegangscodes voor opslag beveiligen tooyour toegangsgegevens, zodat we het beste opslaan in een Azure sleutelkluis. 

Een sleutelkluis maken Hello Azure CLI:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Hallo `enabled-for-template-deployment` switch biedt de mogelijkheid Azure Resource Manager toopull geheimen van de sleutelkluis tijdens de implementatie.

Hallo opslagaccountsleutel opslaan als een nieuwe geheim in de sleutelkluis Hallo:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Hallo volume koppelen

Koppelen van een Azure-bestandsshare als een volume in een container is een proces. Eerst bieden Hallo details van de share als onderdeel van het definiëren van de containergroep Hallo Hallo daarna u hoe u Hallo volume is gekoppeld in één of meer containers in de groep Hallo Hallo wilt opgeven.

toodefine hello volumes toomake beschikbaar voor gewenste koppelen, Voeg een `volumes` matrix toohello container groepsdefinitie in hello Azure Resource Manager-sjabloon en klik vervolgens in Hallo definitie van de afzonderlijke containers Hallo verwijzing.

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

Hallo-sjabloon bevat Hallo opslagaccountnaam en sleutel als parameters die in een afzonderlijke parameterbestand kunnen worden opgegeven. toopopulate hello parameterbestand, moet u drie waarden: Hallo opslagaccountnaam en geheime sleutelkluisnaam die u hebt gebruikt toostore hello opslagsleutel Hallo Hallo bron-ID van uw Azure sleutelkluis. Als u de vorige stappen hebt gevolgd, kunt u deze waarden kunt krijgen met Hallo script volgen:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Hallo waarden invoegen in het parameterbestand Hallo:

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

## <a name="deploy-hello-container-and-manage-files"></a>Hallo-container implementeren en beheren van bestanden

U kunt met het Hallo-sjabloon is gedefinieerd, Hallo container maken en koppelen van het volume met behulp van hello Azure CLI. Ervan uitgaande dat hello sjabloonbestand heet *azuredeploy.json* en de naam van dat bestand van de parameters Hallo *azuredeploy.parameters.json*, dan is Hallo vanaf de opdrachtregel:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Zodra het Hallo-container wordt gestart, kunt u Hallo eenvoudige web-app is geïmplementeerd via Hallo **aci-seanmckenna-hellofiles** afbeelding toohello beheren van bestanden in Azure Hallo-bestandsshare op Hallo koppelpad die u hebt opgegeven. Hallo IP-adres voor web-app via de volgende Hallo Hallo verkrijgen:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

U kunt een hulpprogramma zoals Hallo [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve en Hallo writen toohello bestand bestandsshare controleren.

>[!NOTE]
> Zie toolearn meer over het gebruik van Azure Resource Manager-sjablonen, parameterbestanden, en implementeren met Azure CLI Hallo [implementeren van resources met Resource Manager-sjablonen en Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Volgende stappen

- Implementeren voor uw eerste container met hello Azure Container instanties [snel starten](container-instances-quickstart.md)
- Meer informatie over Hallo [relatie tussen Azure Containerexemplaren en container orchestrators](container-instances-orchestrator-relationship.md)
