---
title: aaaAutomate resources implementeren voor een functie-app in Azure Functions | Microsoft Docs
description: "Meer informatie over hoe toobuild een Azure Resource Manager-sjabloon die de functie-app wordt geïmplementeerd."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, zonder server architectuur, infrastructuur als code, azure resourcemanager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="ab0d1-104">Implementatie van de resource voor de functie-app in Azure Functions automatiseren</span><span class="sxs-lookup"><span data-stu-id="ab0d1-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="ab0d1-105">U kunt een Azure Resource Manager-sjabloon toodeploy een functie-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="ab0d1-106">In dit artikel bevat een overzicht van Hallo vereiste resources en parameters voor doet.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="ab0d1-107">Mogelijk moet u aanvullende bronnen voor toodeploy, afhankelijk van Hallo [triggers en bindingen](functions-triggers-bindings.md) in uw app functie.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="ab0d1-108">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ab0d1-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ab0d1-109">Zie voor een voorbeeldsjablonen:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-109">For sample templates, see:</span></span>
- <span data-ttu-id="ab0d1-110">[functie-app van verbruik plan]</span><span class="sxs-lookup"><span data-stu-id="ab0d1-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="ab0d1-111">[functie-app in Azure App Service-plan]</span><span class="sxs-lookup"><span data-stu-id="ab0d1-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="ab0d1-112">Vereiste resources</span><span class="sxs-lookup"><span data-stu-id="ab0d1-112">Required resources</span></span>

<span data-ttu-id="ab0d1-113">Een functie-app is vereist voor deze resources:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-113">A function app requires these resources:</span></span>

* <span data-ttu-id="ab0d1-114">Een [Azure Storage](../storage/index.md) account</span><span class="sxs-lookup"><span data-stu-id="ab0d1-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="ab0d1-115">Een hosting-indeling (verbruik plan of App Service-abonnement)</span><span class="sxs-lookup"><span data-stu-id="ab0d1-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="ab0d1-116">Een functie-app</span><span class="sxs-lookup"><span data-stu-id="ab0d1-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="ab0d1-117">Storage-account</span><span class="sxs-lookup"><span data-stu-id="ab0d1-117">Storage account</span></span>

<span data-ttu-id="ab0d1-118">Een Azure storage-account is vereist voor een functie-app.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="ab0d1-119">U moet een account voor algemene doeleinden die ondersteuning biedt voor blobs, tabellen, wachtrijen en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="ab0d1-120">Zie voor meer informatie [-account voor Azure Functions opslagvereisten](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="ab0d1-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="ab0d1-121">Bovendien Hallo eigenschappen `AzureWebJobsStorage` en `AzureWebJobsDashboard` moet worden opgegeven als de app-instellingen in Hallo site-configuratie.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="ab0d1-122">Hallo maakt gebruik van Azure Functions-runtime Hallo `AzureWebJobsStorage` connection string toocreate interne wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="ab0d1-123">Hallo verbindingsreeks `AzureWebJobsDashboard` gebruikte toolog tooAzure Table-opslag- en stroomkabels Hallo is **Monitor** tabblad in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="ab0d1-124">Deze eigenschappen in opgegeven Hallo `appSettings` verzameling in hello `siteConfig` object:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="ab0d1-125">Hosting-plan</span><span class="sxs-lookup"><span data-stu-id="ab0d1-125">Hosting plan</span></span>

<span data-ttu-id="ab0d1-126">Hallo-definitie van Hallo die als host fungeert voor plan varieert, afhankelijk van of u een verbruik of App Service-abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="ab0d1-127">Zie [implementeren van een functie-app op Hallo verbruik plan](#consumption) en [implementeren van een functie-app op Hallo App Service-abonnement](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="ab0d1-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="ab0d1-128">Functie-app</span><span class="sxs-lookup"><span data-stu-id="ab0d1-128">Function app</span></span>

<span data-ttu-id="ab0d1-129">Hallo functie app-resource is gedefinieerd met behulp van een bron van het type **Microsoft.Web/Site** en type **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="ab0d1-130">Een functie-app op Hallo verbruik plan implementeren</span><span class="sxs-lookup"><span data-stu-id="ab0d1-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="ab0d1-131">U kunt een functie-app uitvoeren in twee verschillende modi: Hallo verbruik plannings- en Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="ab0d1-132">rekencapaciteit Hallo verbruik plan automatisch toegewezen wanneer uw code wordt uitgevoerd, als de belasting van de benodigde toohandle uitgeschaald en vervolgens omlaag geschaald wanneer de code wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="ab0d1-133">Dus u hebt geen toopay voor niet-actieve virtuele machines en u niet van tevoren tooreserve capaciteit hebt.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="ab0d1-134">toolearn meer informatie over hostingplannen, Zie [Azure Functions gebruiks- en App Service-plannen](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ab0d1-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="ab0d1-135">Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app van verbruik plan].</span><span class="sxs-lookup"><span data-stu-id="ab0d1-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="ab0d1-136">Maak een plan verbruik</span><span class="sxs-lookup"><span data-stu-id="ab0d1-136">Create a Consumption plan</span></span>

<span data-ttu-id="ab0d1-137">Een plan verbruik is een speciaal type resource 'serverfarm'.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="ab0d1-138">U het opgeeft met behulp van Hallo `Dynamic` waarde voor Hallo `computeMode` en `sku` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="ab0d1-139">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="ab0d1-139">Create a function app</span></span>

<span data-ttu-id="ab0d1-140">Bovendien een plan verbruik vereist twee extra instellingen van siteconfiguratie Hallo: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` en `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="ab0d1-141">Deze eigenschappen configureren Hallo storage-account en het bestandspad waar Hallo functie app-code en configuratie zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="ab0d1-142">Implementeren van een functie-app op Hallo App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="ab0d1-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="ab0d1-143">In Hallo App Service-abonnement, de functie-app uitgevoerd via exclusieve virtuele machines op een vergelijkbare tooweb apps Basic, Standard en Premium-SKU's.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="ab0d1-144">Zie voor meer informatie over de werking van App Service-abonnement Hallo Hallo [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab0d1-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="ab0d1-145">Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app in Azure App Service-plan].</span><span class="sxs-lookup"><span data-stu-id="ab0d1-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="ab0d1-146">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="ab0d1-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="ab0d1-147">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="ab0d1-147">Create a function app</span></span> 

<span data-ttu-id="ab0d1-148">Nadat u een optie schaling hebt geselecteerd, maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="ab0d1-149">Hallo-app is Hallo-container met alle uw functies.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="ab0d1-150">Een functie-app heeft veel onderliggende resources die u in uw implementatie gebruiken kunt, met inbegrip van app-instellingen en opties voor beheer.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="ab0d1-151">Bovendien kunt u tooremove hello **sourcecontrols** onderliggende resource, en gebruik een andere [Implementatieoptie](functions-continuous-deployment.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ab0d1-152">toosuccessfully uw toepassing implementeren met behulp van Azure Resource Manager, is het belangrijk toounderstand hoe resources worden geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="ab0d1-153">Hallo voorbeeld te volgen, op het hoogste niveau configuraties worden toegepast met behulp van **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="ab0d1-154">Het is belangrijk tooset deze configuraties boven een niveau, omdat ze gegevens toohello functies runtime en implementatie-engine worden beschouwd.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="ab0d1-155">Op het hoogste niveau informatie is vereist voordat de onderliggende hello **sourcecontrols of web** resource wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="ab0d1-156">Hoewel het mogelijk tooconfigure deze instellingen in een onderliggend niveau Hallo **config/appSettings** bron, in sommige gevallen functie-app moet worden geïmplementeerd *voordat* **config/appSettings**  wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="ab0d1-157">Bijvoorbeeld, wanneer u werkt in combinatie met gebruikt [Logic Apps](../logic-apps/index.md), uw functies zijn afhankelijk van een andere resource.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="ab0d1-158">Deze sjabloon maakt gebruik van Hallo [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app-instellingen-waarde ingesteld Hallo-basismap in welke Hallo functies implementatie-engine (Kudu) implementeerbare code zoekt.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="ab0d1-159">In onze opslagplaats onze functies zijn in een submap van Hallo **src** map.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="ab0d1-160">Dus in Hallo voorgaande voorbeeld, we waarde Hallo app instellingen te`src`.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="ab0d1-161">Als uw functies in de hoofdmap van uw opslagplaats hello, of als u niet vanuit resourcebeheer implementeert, kunt u de waarde van deze app-instellingen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="ab0d1-162">De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="ab0d1-162">Deploy your template</span></span>

<span data-ttu-id="ab0d1-163">U kunt een van de volgende manieren toodeploy Hallo uw sjabloon:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="ab0d1-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab0d1-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="ab0d1-165">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="ab0d1-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="ab0d1-166">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ab0d1-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="ab0d1-167">REST API</span><span class="sxs-lookup"><span data-stu-id="ab0d1-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="ab0d1-168">TooAzure implementatieknop</span><span class="sxs-lookup"><span data-stu-id="ab0d1-168">Deploy tooAzure button</span></span>

<span data-ttu-id="ab0d1-169">Vervang ```<url-encoded-path-to-azuredeploy-json>``` met een [URL-codering](https://www.bing.com/search?q=url+encode) versie van onbewerkte pad Hallo van uw `azuredeploy.json` -bestand in GitHub.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="ab0d1-170">Hier volgt een voorbeeld die gebruikmaakt van markdown:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="ab0d1-171">Hier volgt een voorbeeld waarin HTML wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="ab0d1-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="ab0d1-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ab0d1-172">Next steps</span></span>

<span data-ttu-id="ab0d1-173">Meer informatie over het toodevelop en configureren van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ab0d1-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="ab0d1-174">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="ab0d1-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="ab0d1-175">Hoe de app-instellingen voor het functioneren van tooconfigure Azure</span><span class="sxs-lookup"><span data-stu-id="ab0d1-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="ab0d1-176">Uw eerste Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="ab0d1-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[functie-app van verbruik plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[functie-app in Azure App Service-plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
