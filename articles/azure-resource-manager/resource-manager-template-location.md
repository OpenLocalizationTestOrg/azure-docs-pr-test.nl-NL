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
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="7fc59-103">Locatie van de bron instellen in Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7fc59-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="7fc59-104">Bij het implementeren van een sjabloon, moet u een locatie voor elke resource opgeven.</span><span class="sxs-lookup"><span data-stu-id="7fc59-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="7fc59-105">Dit onderwerp leest hoe toodetermine Hallo locaties beschikbaar tooyour abonnement voor elke resource typt.</span><span class="sxs-lookup"><span data-stu-id="7fc59-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="7fc59-106">Ondersteunde locaties bepalen</span><span class="sxs-lookup"><span data-stu-id="7fc59-106">Determine supported locations</span></span>

<span data-ttu-id="7fc59-107">Zie voor een volledige lijst van ondersteunde locaties voor elk resourcetype [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="7fc59-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="7fc59-108">Uw abonnement mogelijk echter geen locaties voor toegang tot tooall Hallo in de lijst.</span><span class="sxs-lookup"><span data-stu-id="7fc59-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="7fc59-109">toosee een aangepaste lijst met locaties beschikbaar tooyour abonnement, Azure PowerShell of Azure CLI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7fc59-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="7fc59-110">Hallo volgende voorbeeld wordt met PowerShell tooget Hallo locaties voor Hallo `Microsoft.Web\sites` brontype:</span><span class="sxs-lookup"><span data-stu-id="7fc59-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="7fc59-111">Hallo volgende voorbeeld maakt gebruik van Azure CLI 2.0 tooget Hallo locaties voor Hallo `Microsoft.Web\sites` brontype:</span><span class="sxs-lookup"><span data-stu-id="7fc59-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="7fc59-112">Locatie instellen in sjabloon</span><span class="sxs-lookup"><span data-stu-id="7fc59-112">Set location in template</span></span>

<span data-ttu-id="7fc59-113">Na het vaststellen van Hallo ondersteunde locaties voor uw resources, moet u tooset die locatie in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7fc59-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="7fc59-114">Hallo gemakkelijkste manier tooset deze waarde is een resourcegroep in een locatie die ondersteuning biedt voor resourcetypen Hallo toocreate en elke locatie te ingesteld`[resourceGroup().location]`.</span><span class="sxs-lookup"><span data-stu-id="7fc59-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="7fc59-115">U kunt implementeren Hallo sjabloon tooresource groepen op verschillende locaties en waarden in de sjabloon Hallo of parameters niet wijzigt.</span><span class="sxs-lookup"><span data-stu-id="7fc59-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="7fc59-116">Hallo volgende voorbeeld ziet u een opslagaccount dat is geïmplementeerd toohello dezelfde locatie als Hallo resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="7fc59-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="7fc59-117">Als u toohardcode Hallo locatie in de sjabloon moet, Hallo naam opgeven van een van de Hallo ondersteunde regio's.</span><span class="sxs-lookup"><span data-stu-id="7fc59-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="7fc59-118">Hallo volgende voorbeeld ziet u een opslagaccount die altijd is geïmplementeerd in VS-midden tooNorth:</span><span class="sxs-lookup"><span data-stu-id="7fc59-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7fc59-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7fc59-119">Next steps</span></span>
* <span data-ttu-id="7fc59-120">Voor aanbevelingen over het toocreate sjablonen, Zie [aanbevolen procedures voor het maken van Azure Resource Manager-sjablonen](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7fc59-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

