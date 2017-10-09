---
title: aaaDeploy Azure-resources toomultiple resourcegroepen | Microsoft Docs
description: "Toont hoe tootarget meer dan één Azure-resource groep tijdens de implementatie."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Azure-resources toomore dan één resourcegroep implementeren

Normaal gesproken implementeren u alle Hallo resources in uw sjabloon tooa één resource-groep. Er zijn echter scenario's waarbij u toodeploy een set resources samen, maar in verschillende resourcegroepen plaatsen. U kunt bijvoorbeeld toodeploy Hallo back-virtuele machine voor Azure Site Recovery tooa afzonderlijke resourcegroep en locatie. Resource Manager kunt u toouse geneste sjablonen tootarget verschillende resourcegroepen bevinden dan Hallo resourcegroep gebruikt voor Hallo bovenliggende sjabloon.

Hallo-resourcegroep is Hallo lifecycle container voor de toepassing hello en de verzameling van resources. U de resourcegroep Hallo buiten Hallo-sjabloon maken en Hallo resource groep tootarget opgeven tijdens de implementatie. Zie voor een inleiding tooresource groepen, [overzicht van Azure Resource Manager](resource-group-overview.md).

## <a name="example-template"></a>Van de voorbeeldsjabloon

een andere resource tootarget, moet u een sjabloon geneste of gekoppelde gebruiken tijdens de implementatie. Hallo `Microsoft.Resources/deployments` brontype beschikt over een `resourceGroup` parameter waarmee u een andere resourcegroep voor Hallo toospecify geneste implementatie. Alle brongroepen voor Hallo moeten bestaan voordat Hallo-implementatie wordt uitgevoerd. Hallo volgende voorbeeld implementeert twee storage-accounts: een in de resourcegroep Hallo opgegeven tijdens de implementatie, en één in een resourcegroep met de naam `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Als u instelt `resourceGroup` toohello-naam van een resourcegroep die niet bestaat, Hallo implementatie mislukt. Als u een waarde op voor geen specifieke `resourceGroup`, Hallo bovenliggende resourcegroep maakt gebruik van Resource Manager.  

## <a name="deploy-hello-template"></a>Hallo-sjabloon implementeren

toodeploy hello voorbeeldsjabloon, kunt u Hallo-portal, Azure PowerShell of Azure CLI. Voor Azure PowerShell of Azure CLI, moet u een release in mei 2017 of hoger. Hallo voorbeelden wordt ervan uitgegaan dat u hebt Hallo sjabloon lokaal opgeslagen als een bestand met de naam **crossrgdeployment.json**.

Voor PowerShell:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Voor Azure CLI:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Nadat de implementatie is voltooid, ziet u twee resourcegroepen. Elke resourcegroep bevat een opslagaccount.

## <a name="use-resourcegroup-function"></a>Gebruik de functie resourceGroup()

Voor cross-resourcegroepimplementaties, hello [resouceGroup() functie](resource-group-template-functions-resource.md#resourcegroup) wordt omgezet is anders op basis van hoe u Hallo geneste sjabloon opgeven. 

Als u een sjabloon in een andere sjabloon insluit, opgelost resouceGroup() in geneste sjabloon Hallo toohello bovenliggende resourcegroep. Een ingesloten sjabloon maakt gebruik van Hallo volgende indeling:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Als u afzonderlijke sjabloon tooa koppelt, oplossing resouceGroup() in de gekoppelde sjabloon Hallo toohello geneste resourcegroep. Een gekoppelde sjabloon maakt gebruik van Hallo volgende indeling:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Volgende stappen

* hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).
* Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).
