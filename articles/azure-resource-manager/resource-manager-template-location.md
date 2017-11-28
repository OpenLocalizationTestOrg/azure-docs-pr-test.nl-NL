---
title: Locatie van de Azure-resource in de sjabloon | Microsoft Docs
description: Laat zien hoe u een locatie voor een resource in een Azure Resource Manager-sjabloon is ingesteld
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
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="495cd-103">Locatie van de bron instellen in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="495cd-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="495cd-104">Bij het implementeren van een sjabloon, moet u een locatie voor elke resource opgeven.</span><span class="sxs-lookup"><span data-stu-id="495cd-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="495cd-105">Dit onderwerp leest hoe u bepaalt de locaties die beschikbaar voor uw abonnement voor elk resourcetype zijn.</span><span class="sxs-lookup"><span data-stu-id="495cd-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="495cd-106">Ondersteunde locaties bepalen</span><span class="sxs-lookup"><span data-stu-id="495cd-106">Determine supported locations</span></span>

<span data-ttu-id="495cd-107">Zie voor een volledige lijst van ondersteunde locaties voor elk resourcetype [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="495cd-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="495cd-108">Echter, uw abonnement mogelijk geen toegang tot alle locaties in de lijst.</span><span class="sxs-lookup"><span data-stu-id="495cd-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="495cd-109">Als een aangepaste lijst met locaties die beschikbaar voor uw abonnement zijn wilt weergeven, gebruikt u Azure PowerShell of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="495cd-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="495cd-110">Het volgende voorbeeld maakt gebruik van PowerShell om op te halen van de locaties voor de `Microsoft.Web\sites` brontype:</span><span class="sxs-lookup"><span data-stu-id="495cd-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="495cd-111">Het volgende voorbeeld maakt gebruik van Azure CLI 2.0 ophalen van de locaties voor de `Microsoft.Web\sites` brontype:</span><span class="sxs-lookup"><span data-stu-id="495cd-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="495cd-112">Locatie instellen in sjabloon</span><span class="sxs-lookup"><span data-stu-id="495cd-112">Set location in template</span></span>

<span data-ttu-id="495cd-113">Na het vaststellen van de ondersteunde locaties voor uw resources, moet u die locatie in uw sjabloon is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="495cd-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="495cd-114">De eenvoudigste manier om in te stellen van deze waarde is een resourcegroep maken op een locatie die ondersteuning biedt voor de volgende resourcetypen en elke locatie op instellen `[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="495cd-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="495cd-115">U kunt de sjabloon aan resourcegroepen op verschillende locaties opnieuw implementeert en alle waarden in de sjabloon of parameters niet te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="495cd-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="495cd-116">Het volgende voorbeeld ziet u een opslagaccount dat is geïmplementeerd op dezelfde locatie als de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="495cd-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

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

<span data-ttu-id="495cd-117">Als u hardcode voor de locatie in de sjabloon wilt, geef de naam van een van de ondersteunde regio's.</span><span class="sxs-lookup"><span data-stu-id="495cd-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="495cd-118">Het volgende voorbeeld ziet u een opslagaccount die altijd wordt geïmplementeerd op Noordelijk Centraal, VS:</span><span class="sxs-lookup"><span data-stu-id="495cd-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="495cd-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="495cd-119">Next steps</span></span>
* <span data-ttu-id="495cd-120">Zie voor aanbevelingen over het maken van sjablonen [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="495cd-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

