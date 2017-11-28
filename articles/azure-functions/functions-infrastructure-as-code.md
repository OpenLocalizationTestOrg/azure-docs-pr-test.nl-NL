---
title: Automatisering van resource voor een functie-app in Azure Functions | Microsoft Docs
description: "Informatie over het bouwen van een Azure Resource Manager-sjabloon die de functie-app wordt geïmplementeerd."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="4bdfb-104">Implementatie van de resource voor de functie-app in Azure Functions automatiseren</span><span class="sxs-lookup"><span data-stu-id="4bdfb-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="4bdfb-105">U kunt een Azure Resource Manager-sjabloon gebruiken voor het implementeren van een functie-app.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="4bdfb-106">In dit artikel bevat een overzicht van de vereiste resources en de parameters voor doet.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="4bdfb-107">Mogelijk moet u aanvullende resources implementeren afhankelijk van de [triggers en bindingen](functions-triggers-bindings.md) in uw app functie.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="4bdfb-108">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4bdfb-109">Zie voor een voorbeeldsjablonen:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-109">For sample templates, see:</span></span>
- <span data-ttu-id="4bdfb-110">[functie-app van verbruik plan]</span><span class="sxs-lookup"><span data-stu-id="4bdfb-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="4bdfb-111">[functie-app in Azure App Service-plan]</span><span class="sxs-lookup"><span data-stu-id="4bdfb-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="4bdfb-112">Vereiste resources</span><span class="sxs-lookup"><span data-stu-id="4bdfb-112">Required resources</span></span>

<span data-ttu-id="4bdfb-113">Een functie-app is vereist voor deze resources:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-113">A function app requires these resources:</span></span>

* <span data-ttu-id="4bdfb-114">Een [Azure Storage](../storage/index.md) account</span><span class="sxs-lookup"><span data-stu-id="4bdfb-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="4bdfb-115">Een hosting-indeling (verbruik plan of App Service-abonnement)</span><span class="sxs-lookup"><span data-stu-id="4bdfb-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="4bdfb-116">Een functie-app</span><span class="sxs-lookup"><span data-stu-id="4bdfb-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="4bdfb-117">Storage-account</span><span class="sxs-lookup"><span data-stu-id="4bdfb-117">Storage account</span></span>

<span data-ttu-id="4bdfb-118">Een Azure storage-account is vereist voor een functie-app.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="4bdfb-119">U moet een account voor algemene doeleinden die ondersteuning biedt voor blobs, tabellen, wachtrijen en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="4bdfb-120">Zie voor meer informatie [-account voor Azure Functions opslagvereisten](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="4bdfb-121">Daarnaast biedt de eigenschappen `AzureWebJobsStorage` en `AzureWebJobsDashboard` moet worden opgegeven als de app-instellingen in de siteconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="4bdfb-122">De Azure Functions-runtime gebruikt de `AzureWebJobsStorage` verbindingsreeks interne wachtrijen maken.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="4bdfb-123">De verbindingsreeks `AzureWebJobsDashboard` wordt gebruikt voor aanmelding tot Azure Table storage en power de **Monitor** tabblad in de portal.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="4bdfb-124">Deze eigenschappen zijn opgegeven in de `appSettings` verzameling in de `siteConfig` object:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="4bdfb-125">Hosting-plan</span><span class="sxs-lookup"><span data-stu-id="4bdfb-125">Hosting plan</span></span>

<span data-ttu-id="4bdfb-126">De definitie van het plan hosting varieert, afhankelijk van of u een verbruik of App Service-abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="4bdfb-127">Zie [implementeren van een functie-app op het plan verbruik](#consumption) en [implementeren van een functie-app op het App Service-abonnement](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="4bdfb-128">Functie-app</span><span class="sxs-lookup"><span data-stu-id="4bdfb-128">Function app</span></span>

<span data-ttu-id="4bdfb-129">De resource voor de functie-app wordt gedefinieerd door middel van een bron van het type **Microsoft.Web/Site** en type **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="4bdfb-130">Een functie-app op het plan verbruik implementeren</span><span class="sxs-lookup"><span data-stu-id="4bdfb-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="4bdfb-131">U kunt een functie-app uitvoeren in twee verschillende modi: het plan verbruik en de App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="4bdfb-132">Het plan verbruik wijst automatisch rekencapaciteit wanneer uw code wordt uitgevoerd, indien nodig om belasting te verwerken uitgeschaald en vervolgens omlaag geschaald wanneer de code wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="4bdfb-133">Dus u hoeft te betalen voor niet-actieve virtuele machines en u hoeft te worden van tevoren capaciteit reserveren.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="4bdfb-134">Zie voor meer informatie over hostingplannen, [Azure Functions gebruiks- en App Service-plannen](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="4bdfb-135">Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app van verbruik plan].</span><span class="sxs-lookup"><span data-stu-id="4bdfb-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="4bdfb-136">Maak een plan verbruik</span><span class="sxs-lookup"><span data-stu-id="4bdfb-136">Create a Consumption plan</span></span>

<span data-ttu-id="4bdfb-137">Een plan verbruik is een speciaal type resource 'serverfarm'.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="4bdfb-138">U het opgeeft via de `Dynamic` waarde voor de `computeMode` en `sku` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="4bdfb-139">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="4bdfb-139">Create a function app</span></span>

<span data-ttu-id="4bdfb-140">Bovendien een plan verbruik vereist twee extra instellingen in de siteconfiguratie: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` en `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="4bdfb-141">Deze eigenschappen configureren voor de storage-account en het bestandspad waar de functie app-code en de configuratie zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="4bdfb-142">Implementeren van een functie-app op het App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="4bdfb-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="4bdfb-143">In de App Service-abonnement functie-app uitgevoerd via exclusieve virtuele machines op Basic, Standard en Premium-SKU's, vergelijkbaar met web-apps.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="4bdfb-144">Zie voor meer informatie over de werking van de App Service-abonnement de [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4bdfb-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="4bdfb-145">Zie voor een Azure Resource Manager voorbeeldsjabloon [functie-app in Azure App Service-plan].</span><span class="sxs-lookup"><span data-stu-id="4bdfb-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="4bdfb-146">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="4bdfb-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="4bdfb-147">Een functie-app maken</span><span class="sxs-lookup"><span data-stu-id="4bdfb-147">Create a function app</span></span> 

<span data-ttu-id="4bdfb-148">Nadat u een optie schaling hebt geselecteerd, maakt u een functie-app.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="4bdfb-149">De app is de container waarin alle uw functies.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="4bdfb-150">Een functie-app heeft veel onderliggende resources die u in uw implementatie gebruiken kunt, met inbegrip van app-instellingen en opties voor beheer.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="4bdfb-151">U kunt desgewenst ook verwijderen de **sourcecontrols** onderliggende resource, en gebruik een andere [Implementatieoptie](functions-continuous-deployment.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bdfb-152">Als u wilt uw toepassing implementeren met behulp van Azure Resource Manager, is het belangrijk te begrijpen hoe resources worden geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="4bdfb-153">In het volgende voorbeeld wordt op het hoogste niveau configuraties zijn toegepast met behulp van **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="4bdfb-154">Het is belangrijk dat deze configuraties ingesteld op het hoogste niveau, omdat ze gegevens naar de runtime en implementatie-engine van functies worden beschouwd.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="4bdfb-155">Op het hoogste niveau informatie is vereist voordat de onderliggende **sourcecontrols of web** resource wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="4bdfb-156">Hoewel het mogelijk deze instellingen te configureren in het onderliggende niveau **config/appSettings** bron, in sommige gevallen functie-app moet worden geïmplementeerd *voordat* **config/appSettings** wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="4bdfb-157">Bijvoorbeeld, wanneer u werkt in combinatie met gebruikt [Logic Apps](../logic-apps/index.md), uw functies zijn afhankelijk van een andere resource.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="4bdfb-158">Deze sjabloon worden gebruikt voor de [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) waarde van app-instellingen, waarmee de basismap waarin de implementatie-engine van functies (Kudu) wordt gezocht voor implementeerbare code wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="4bdfb-159">In onze opslagplaats onze functies zijn in een submap van de **src** map.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="4bdfb-160">Dus in het voorgaande voorbeeld wordt de app instellingen waarde instelt op `src`.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="4bdfb-161">Als uw functies in de hoofdmap van uw opslagplaats, of als u niet vanuit resourcebeheer implementeert, kunt u de waarde van deze app-instellingen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="4bdfb-162">De sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="4bdfb-162">Deploy your template</span></span>

<span data-ttu-id="4bdfb-163">U kunt een van de volgende manieren om uw sjabloon te implementeren:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="4bdfb-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bdfb-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="4bdfb-165">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="4bdfb-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="4bdfb-166">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4bdfb-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="4bdfb-167">REST API</span><span class="sxs-lookup"><span data-stu-id="4bdfb-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="4bdfb-168">Implementeren naar Azure-knop</span><span class="sxs-lookup"><span data-stu-id="4bdfb-168">Deploy to Azure button</span></span>

<span data-ttu-id="4bdfb-169">Vervang ```<url-encoded-path-to-azuredeploy-json>``` met een [URL-codering](https://www.bing.com/search?q=url+encode) versie van het pad onbewerkte van uw `azuredeploy.json` -bestand in GitHub.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="4bdfb-170">Hier volgt een voorbeeld die gebruikmaakt van markdown:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="4bdfb-171">Hier volgt een voorbeeld waarin HTML wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="4bdfb-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="4bdfb-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4bdfb-172">Next steps</span></span>

<span data-ttu-id="4bdfb-173">Meer informatie over het ontwikkelen en configureren van Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="4bdfb-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="4bdfb-174">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="4bdfb-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="4bdfb-175">Het Azure-functie app-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="4bdfb-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="4bdfb-176">Uw eerste Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="4bdfb-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[functie-app van verbruik plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[functie-app in Azure App Service-plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
