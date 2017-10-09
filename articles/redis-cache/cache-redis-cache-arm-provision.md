---
title: aaaProvision een Redis-Cache met Azure Resource Manager | Microsoft Docs
description: Azure Resource Manager-sjabloon toodeploy een Azure Redis-Cache gebruiken.
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="9e2e1-103">Een Redis Cache maken op basis van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="9e2e1-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="9e2e1-104">In dit onderwerp leert u hoe toocreate een Azure Resource Manager-sjabloon die wordt geïmplementeerd in een Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="9e2e1-105">Hallo-cache kan worden gebruikt met een bestaande opslag account tookeep diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="9e2e1-106">U leert ook hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="9e2e1-107">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="9e2e1-108">Op dit moment diagnostische instellingen worden gedeeld voor alle caches in Hallo dezelfde regio voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="9e2e1-109">Bijwerken van een cache in Hallo regio is van invloed op alle andere caches in Hallo regio.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="9e2e1-110">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e2e1-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="9e2e1-111">Zie voor de volledige sjabloon hello, [Redis-Cache sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9e2e1-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="9e2e1-112">Resource Manager-sjablonen voor nieuwe Hallo [Premium-laag](cache-premium-tier-intro.md) beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="9e2e1-113">Maken van een Premium Redis-Cache met clustering</span><span class="sxs-lookup"><span data-stu-id="9e2e1-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="9e2e1-114">Premium Redis-Cache met gegevenspersistentie maken</span><span class="sxs-lookup"><span data-stu-id="9e2e1-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="9e2e1-115">Premium Redis-Cache maken met VNet en een optionele clustering</span><span class="sxs-lookup"><span data-stu-id="9e2e1-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="9e2e1-116">toocheck voor de meest recente sjablonen hello, Zie [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/) en zoek naar `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="9e2e1-117">Wat u wilt implementeren</span><span class="sxs-lookup"><span data-stu-id="9e2e1-117">What you will deploy</span></span>
<span data-ttu-id="9e2e1-118">In deze sjabloon implementeert u een Azure Redis-Cache die gebruikmaakt van een bestaand opslagaccount voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="9e2e1-119">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="9e2e1-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="9e2e1-120">[![TooAzure implementeren](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9e2e1-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="9e2e1-121">Parameters</span><span class="sxs-lookup"><span data-stu-id="9e2e1-121">Parameters</span></span>
<span data-ttu-id="9e2e1-122">Met Azure Resource Manager u parameters definiëren voor waarden gewenste toospecify wanneer Hallo sjabloon wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="9e2e1-123">Hallo-sjabloon bevat een sectie met de naam van de Parameters die alle Hallo parameterwaarden bevat.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="9e2e1-124">U moet een parameter voor de waarden die variëren op basis van Hallo-project die u implementeert of op basis van Hallo-omgeving die u om te implementeert definiëren.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="9e2e1-125">Definieer parameters niet voor waarden die altijd blijven Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="9e2e1-126">De waarde van elke parameter wordt gebruikt in Hallo sjabloon toodefine Hallo resources die zijn geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="9e2e1-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="9e2e1-127">redisCacheLocation</span></span>
<span data-ttu-id="9e2e1-128">Hallo-locatie van Hallo Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="9e2e1-129">Voor de beste prestaties Hallo gebruik dezelfde locatie als Hallo app toobe met Hallo cache gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="9e2e1-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="9e2e1-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="9e2e1-131">Hallo de naam van Hallo bestaande storage account toouse voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="9e2e1-132">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="9e2e1-132">enableNonSslPort</span></span>
<span data-ttu-id="9e2e1-133">Een Boolean die aangeeft of tooallow toegang krijgen tot via niet-SSL-poort.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="9e2e1-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="9e2e1-134">diagnosticsStatus</span></span>
<span data-ttu-id="9e2e1-135">Een waarde die aangeeft of diagnostische gegevens is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="9e2e1-136">Gebruik ON of OFF.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="9e2e1-137">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="9e2e1-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="9e2e1-138">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="9e2e1-138">Redis Cache</span></span>
<span data-ttu-id="9e2e1-139">Hiermee maakt u hello Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="9e2e1-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="9e2e1-140">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="9e2e1-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="9e2e1-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e2e1-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="9e2e1-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e2e1-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


