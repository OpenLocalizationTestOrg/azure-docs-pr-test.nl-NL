---
title: Inrichten van een Redis-Cache met Azure Resource Manager | Microsoft Docs
description: Gebruik Azure Resource Manager-sjabloon voor het implementeren van een Azure Redis-Cache.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="e0e13-103">Een Redis Cache maken op basis van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="e0e13-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="e0e13-104">In dit onderwerp leert u het maken van een Azure Resource Manager-sjabloon die u een Azure Redis-Cache implementeert.</span><span class="sxs-lookup"><span data-stu-id="e0e13-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="e0e13-105">De cache kan worden gebruikt met een bestaand opslagaccount om diagnostische gegevens te behouden.</span><span class="sxs-lookup"><span data-stu-id="e0e13-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="e0e13-106">U leert ook hoe om te definiëren welke bronnen worden geïmplementeerd en het definiëren van de parameters die zijn opgegeven wanneer de implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0e13-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="e0e13-107">U kunt deze sjabloon gebruiken voor uw eigen implementaties of de sjabloon aanpassen aan uw eisen.</span><span class="sxs-lookup"><span data-stu-id="e0e13-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="e0e13-108">Diagnostische instellingen worden op dit moment wordt gedeeld voor alle caches in dezelfde regio voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="e0e13-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="e0e13-109">Bijwerken van een cache in het gebied van invloed op alle andere caches in de regio.</span><span class="sxs-lookup"><span data-stu-id="e0e13-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="e0e13-110">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e0e13-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="e0e13-111">Zie voor de volledige sjabloon [Redis-Cache sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e0e13-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="e0e13-112">Resource Manager-sjablonen voor de nieuwe [Premium-laag](cache-premium-tier-intro.md) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="e0e13-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="e0e13-113">Maken van een Premium Redis-Cache met clustering</span><span class="sxs-lookup"><span data-stu-id="e0e13-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="e0e13-114">Premium Redis-Cache met gegevenspersistentie maken</span><span class="sxs-lookup"><span data-stu-id="e0e13-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="e0e13-115">Premium Redis-Cache maken met VNet en een optionele clustering</span><span class="sxs-lookup"><span data-stu-id="e0e13-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="e0e13-116">Om te controleren of de meest recente sjablonen, Zie [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) en zoek naar `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="e0e13-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="e0e13-117">Wat u wilt implementeren</span><span class="sxs-lookup"><span data-stu-id="e0e13-117">What you will deploy</span></span>
<span data-ttu-id="e0e13-118">In deze sjabloon implementeert u een Azure Redis-Cache die gebruikmaakt van een bestaand opslagaccount voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="e0e13-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="e0e13-119">Klik op de volgende knop om de implementatie automatisch uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e0e13-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="e0e13-120">[![Implementeren in Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e0e13-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e0e13-121">Parameters</span><span class="sxs-lookup"><span data-stu-id="e0e13-121">Parameters</span></span>
<span data-ttu-id="e0e13-122">Met Azure Resource Manager kunt u parameters definiëren voor waarden die u wilt opgeven wanneer de sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e0e13-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="e0e13-123">De sjabloon bevat een sectie met de naam van de Parameters die alle van de parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="e0e13-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="e0e13-124">U moet een parameter definiëren voor de waarden die variëren op basis van het project dat u wilt implementeren of op basis van de omgeving waarin u gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="e0e13-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="e0e13-125">Definieer geen parameters voor waarden die altijd hetzelfde blijven.</span><span class="sxs-lookup"><span data-stu-id="e0e13-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="e0e13-126">De waarde van elke parameter wordt gebruikt in de sjabloon voor het definiëren van de resources die worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e0e13-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="e0e13-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="e0e13-127">redisCacheLocation</span></span>
<span data-ttu-id="e0e13-128">De locatie van de Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="e0e13-128">The location of the Redis Cache.</span></span> <span data-ttu-id="e0e13-129">Voor de beste prestaties gebruik van dezelfde locatie als de app moet worden gebruikt met de cache.</span><span class="sxs-lookup"><span data-stu-id="e0e13-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="e0e13-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e0e13-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="e0e13-131">De naam van het bestaande opslagaccount voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="e0e13-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="e0e13-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="e0e13-132">enableNonSslPort</span></span>
<span data-ttu-id="e0e13-133">Een Boolean die aangeeft of toegang hebben via niet-SSL-poort.</span><span class="sxs-lookup"><span data-stu-id="e0e13-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="e0e13-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="e0e13-134">diagnosticsStatus</span></span>
<span data-ttu-id="e0e13-135">Een waarde die aangeeft of diagnostische gegevens is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e0e13-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="e0e13-136">Gebruik ON of OFF.</span><span class="sxs-lookup"><span data-stu-id="e0e13-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="e0e13-137">Resources om te implementeren</span><span class="sxs-lookup"><span data-stu-id="e0e13-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="e0e13-138">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="e0e13-138">Redis Cache</span></span>
<span data-ttu-id="e0e13-139">Hiermee maakt u de Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="e0e13-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="e0e13-140">Opdrachten om implementatie uit te voeren</span><span class="sxs-lookup"><span data-stu-id="e0e13-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e0e13-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0e13-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="e0e13-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e0e13-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


