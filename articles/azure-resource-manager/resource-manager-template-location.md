---
title: aaaAzure Resourcelocatie in sjabloon | Microsoft Docs
description: Toont hoe tooset een locatie voor een resource in een Azure Resource Manager-sjabloon
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Locatie van de bron instellen in Azure Resource Manager-sjablonen
Bij het implementeren van een sjabloon, moet u een locatie voor elke resource opgeven. Dit onderwerp leest hoe toodetermine Hallo locaties beschikbaar tooyour abonnement voor elke resource typt.

## <a name="determine-supported-locations"></a>Ondersteunde locaties bepalen

Zie voor een volledige lijst van ondersteunde locaties voor elk resourcetype [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/). Uw abonnement mogelijk echter geen locaties voor toegang tot tooall Hallo in de lijst. toosee een aangepaste lijst met locaties beschikbaar tooyour abonnement, Azure PowerShell of Azure CLI gebruiken. 

Hallo volgende voorbeeld wordt met PowerShell tooget Hallo locaties voor Hallo `Microsoft.Web\sites` brontype:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Hallo volgende voorbeeld maakt gebruik van Azure CLI 2.0 tooget Hallo locaties voor Hallo `Microsoft.Web\sites` brontype:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Locatie instellen in sjabloon

Na het vaststellen van Hallo ondersteunde locaties voor uw resources, moet u tooset die locatie in de sjabloon. Hallo gemakkelijkste manier tooset deze waarde is een resourcegroep in een locatie die ondersteuning biedt voor resourcetypen Hallo toocreate en elke locatie te ingesteld`[resourceGroup().location]`. U kunt implementeren Hallo sjabloon tooresource groepen op verschillende locaties en waarden in de sjabloon Hallo of parameters niet wijzigt. 

Hallo volgende voorbeeld ziet u een opslagaccount dat is geïmplementeerd toohello dezelfde locatie als Hallo resourcegroep:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

Als u toohardcode Hallo locatie in de sjabloon moet, Hallo naam opgeven van een van de Hallo ondersteunde regio's. Hallo volgende voorbeeld ziet u een opslagaccount die altijd is geïmplementeerd in VS-midden tooNorth:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a>Volgende stappen
* Voor aanbevelingen over het toocreate sjablonen, Zie [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).

