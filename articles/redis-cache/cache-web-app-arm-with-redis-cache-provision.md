---
title: aaaProvision Web-App met Redis-Cache
description: Azure Resource Manager-sjabloon toodeploy web-app met Redis-Cache gebruiken.
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="a867e-103">Een Web-App plus Redis-Cache met behulp van een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a867e-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="a867e-104">In dit onderwerp leert u hoe toocreate een Azure Resource Manager-sjabloon die u een Azure-Web-App met Redis-cache implementeert.</span><span class="sxs-lookup"><span data-stu-id="a867e-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="a867e-105">U leert hoe toodefine welke resources zijn geïmplementeerd en hoe toodefine parameters die zijn opgegeven wanneer het Hallo-implementatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a867e-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="a867e-106">U kunt deze sjabloon voor uw eigen implementaties gebruiken of aanpassen toomeet uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="a867e-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="a867e-107">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a867e-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a867e-108">Zie voor de volledige sjabloon hello, [Web-App met Redis-Cache sjabloon](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a867e-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="a867e-109">Wat u wilt implementeren</span><span class="sxs-lookup"><span data-stu-id="a867e-109">What you will deploy</span></span>
<span data-ttu-id="a867e-110">In deze sjabloon gaat u implementeren:</span><span class="sxs-lookup"><span data-stu-id="a867e-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="a867e-111">Azure Web App</span><span class="sxs-lookup"><span data-stu-id="a867e-111">Azure Web App</span></span>
* <span data-ttu-id="a867e-112">Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="a867e-112">Azure Redis Cache.</span></span>

<span data-ttu-id="a867e-113">toorun implementatie automatisch Hallo, klikt u op de knop volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="a867e-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="a867e-114">[![TooAzure implementeren](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a867e-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="a867e-115">Parameters toospecify</span><span class="sxs-lookup"><span data-stu-id="a867e-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="a867e-116">Variabelen voor de namen</span><span class="sxs-lookup"><span data-stu-id="a867e-116">Variables for names</span></span>
<span data-ttu-id="a867e-117">Deze sjabloon maakt gebruik van variabelen tooconstruct namen voor Hallo bronnen.</span><span class="sxs-lookup"><span data-stu-id="a867e-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="a867e-118">Hierbij Hallo [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) werken tooconstruct een waarde op basis van de resource-id.</span><span class="sxs-lookup"><span data-stu-id="a867e-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="a867e-119">Resources toodeploy</span><span class="sxs-lookup"><span data-stu-id="a867e-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="a867e-120">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="a867e-120">Redis Cache</span></span>
<span data-ttu-id="a867e-121">Hello Azure Redis-Cache die wordt gebruikt met Hallo web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="a867e-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="a867e-122">Hallo-naam van de cache Hallo is opgegeven in Hallo **cacheName** variabele.</span><span class="sxs-lookup"><span data-stu-id="a867e-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="a867e-123">Hallo-sjabloon maakt Hallo cache in Hallo dezelfde locatie als Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a867e-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="a867e-124">Web-app</span><span class="sxs-lookup"><span data-stu-id="a867e-124">Web app</span></span>
<span data-ttu-id="a867e-125">Hallo-web-app maakt met de naam opgegeven in Hallo **Websitenaam** variabele.</span><span class="sxs-lookup"><span data-stu-id="a867e-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="a867e-126">U ziet dat Hallo web-app is geconfigureerd met de app instellen van eigenschappen waarmee het toowork Hello Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="a867e-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="a867e-127">Deze app instellingen worden dynamisch gemaakt op basis van waarden die zijn opgegeven tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a867e-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="a867e-128">Opdrachten toorun implementatie</span><span class="sxs-lookup"><span data-stu-id="a867e-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="a867e-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a867e-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="a867e-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a867e-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
