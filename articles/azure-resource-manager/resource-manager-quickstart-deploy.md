---
title: aaaDeploy resources tooAzure | Microsoft Docs
description: Gebruik Azure PowerShell of Azure CLI toodeploy resources tooAzure. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a>Resources tooAzure implementeren

Dit onderwerp wordt beschreven hoe toodeploy resources tooyour Azure-abonnement. U kunt Azure PowerShell of Azure CLI toodeploy Resource Manager-sjabloon die Hallo-infrastructuur voor uw oplossing definieert.

Zie voor een inleiding tooconcepts van Resource Manager, [overzicht van Azure Resource Manager](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Stappen voor implementatie

In dit onderwerp wordt ervan uitgegaan dat u implementeert Hallo [opslag voorbeeldsjabloon](#example-storage-template) in dit onderwerp. U kunt een andere sjabloon, maar Hallo-parameters die u doorgeeft anders zijn dan wat in dit onderwerp wordt weergegeven.

Na het maken van een sjabloon zijn Hallo algemene stappen voor het implementeren van uw sjabloon:

1. Meld u bij tooyour account
2. Selecteer Hallo abonnement toouse (alleen nodig als u meerdere abonnementen hebt en u wilt dat toouse een die niet Hallo standaardabonnement)
3. Een resourcegroep maken
4. Hallo-sjabloon implementeren
5. De implementatiestatus controleren

Hallo volgende secties wordt uitgelegd hoe tooperform die stappen waarbij [PowerShell](#powershell) of [Azure CLI](#azure-cli).

## <a name="powershell"></a>PowerShell

1. Zie tooinstall Azure PowerShell [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).

2. tooquickly aan de slag met de implementatie, Hallo cmdlets volgende gebruiken:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Hallo `Set-AzureRmContext` cmdlet is alleen nodig als u wilt dat een abonnement toouse dan uw standaardabonnement. toosee al uw abonnementen en hun id's gebruiken:

  ```powershell
  Get-AzureRmSubscription
  ```

3. Hallo-implementatie kan toocomplete van enkele minuten duren. Als deze is voltooid, ziet u een bericht dat lijkt op:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee die uw resource groep en storage-account zijn geïmplementeerd tooyour abonnement, gebruiken:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. U kunt sjabloonparameters opgeven als PowerShell-parameters bij het implementeren van een sjabloon. Hallo bevat eerdere voorbeeld geen Sjabloonparameters, zodat de standaardwaarden Hallo in Hallo sjabloon zijn gebruikt. toodeploy opslag op een andere account en parameterwaarden opgeven voor voorvoegsel Hallo van opslag en het opslagaccount Hallo SKU, gebruiken:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  U hebt nu twee opslagaccounts in de resourcegroep. 

## <a name="azure-cli"></a>Azure CLI

1. Zie tooinstall Azure CLI [2.0 voor Azure CLI installeren](/cli/azure/install-az-cli2).

2. tooquickly aan de slag met de implementatie, Hallo volgende opdrachten gebruiken:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Hallo `az account set` opdracht is alleen nodig als u wilt dat een abonnement toouse dan uw standaardabonnement. toosee al uw abonnementen en hun id's gebruiken:

  ```azurecli
  az account list
  ```

3. Hallo-implementatie kan toocomplete van enkele minuten duren. Als deze is voltooid, ziet u een bericht dat lijkt op:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee die uw resource groep en storage-account zijn geïmplementeerd tooyour abonnement, gebruiken:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. U kunt sjabloonparameters opgeven als PowerShell-parameters bij het implementeren van een sjabloon. Hallo bevat eerdere voorbeeld geen Sjabloonparameters, zodat de standaardwaarden Hallo in Hallo sjabloon zijn gebruikt. toodeploy opslag op een andere account en parameterwaarden opgeven voor voorvoegsel Hallo van opslag en het opslagaccount Hallo SKU, gebruiken:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  U hebt nu twee opslagaccounts in de resourcegroep. 

## <a name="example-storage-template"></a>Voorbeeldopslagsjabloon

Hallo voorbeeld sjabloon toodeploy een tooyour voor opslagaccountabonnement volgende gebruiken:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a>Volgende stappen

* Zie voor gedetailleerde informatie over het gebruik van PowerShell toodeploy sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Zie voor gedetailleerde informatie over het gebruik van Azure CLI toodeploy sjablonen [implementeren van resources met Resource Manager-sjablonen en Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).



