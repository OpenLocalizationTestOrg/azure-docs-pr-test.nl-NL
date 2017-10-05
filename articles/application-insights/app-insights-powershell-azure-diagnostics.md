---
title: PowerShell gebruiken om Application Insights in te stellen in Azure | Microsoft Docs
description: Automatiseer het configureren van diagnostische Azure-gegevens, zodat deze worden doorgestuurd naar Application Insights.
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="5b539-103">PowerShell gebruiken om Application Insights in te stellen voor een Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="5b539-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="5b539-104">[Microsoft Azure](https://azure.com) kan zo [worden geconfigureerd dat er diagnostische Azure-gegevens worden verzonden](app-insights-azure-diagnostics.md) naar [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b539-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5b539-105">De diagnostische gegevens hebben betrekking op Azure Cloud Services en virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="5b539-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="5b539-106">Ze vormen een aanvulling op de telemetrie die u vanuit de app verzendt met behulp van de Application Insights-SDK.</span><span class="sxs-lookup"><span data-stu-id="5b539-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="5b539-107">Als onderdeel van het automatiseringsproces voor het maken van nieuwe resources in Azure kunt u het verzenden van diagnostische gegevens configureren met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b539-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="5b539-108">Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="5b539-108">Azure template</span></span>
<span data-ttu-id="5b539-109">Als de web-app in Azure wordt uitgevoerd en u uw resources maakt met een Azure Resource Manager-sjabloon, kunt u Application Insights configureren door dit aan het resource-knooppunt toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="5b539-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="5b539-110">`nameOfAIAppResource`: een naam voor de Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="5b539-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="5b539-111">`myWebAppName`: de id van de web-app</span><span class="sxs-lookup"><span data-stu-id="5b539-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="5b539-112">De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="5b539-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="5b539-113">De cmdlet `New-AzureDeployment` bevat de parameter `ExtensionConfiguration`, die overweg kan met vele configuraties voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="5b539-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="5b539-114">Deze kunnen worden gemaakt met de cmdlet `New-AzureServiceDiagnosticsExtensionConfig`.</span><span class="sxs-lookup"><span data-stu-id="5b539-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="5b539-115">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5b539-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="5b539-116">De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice</span><span class="sxs-lookup"><span data-stu-id="5b539-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="5b539-117">Gebruik `Set-AzureServiceDiagnosticsExtension` voor een bestaande service.</span><span class="sxs-lookup"><span data-stu-id="5b539-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="5b539-118">De huidige configuratie van de extensie voor diagnostische gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="5b539-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="5b539-119">De extensie voor diagnostische gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="5b539-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="5b539-120">Als u de extensie voor diagnostische gegevens hebt ingeschakeld met `Set-AzureServiceDiagnosticsExtension` of `New-AzureServiceDiagnosticsExtensionConfig`, zonder de parameter Rol te gebruiken, kunt u de extensie verwijderen met `Remove-AzureServiceDiagnosticsExtension`, zonder de parameter Rol.</span><span class="sxs-lookup"><span data-stu-id="5b539-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="5b539-121">Als de parameter Rol is gebruikt bij het inschakelen van de extensie, moet deze ook worden gebruikt bij het verwijderen hiervan.</span><span class="sxs-lookup"><span data-stu-id="5b539-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="5b539-122">De extensie voor diagnostische gegevens verwijderen voor elke afzonderlijke rol:</span><span class="sxs-lookup"><span data-stu-id="5b539-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="5b539-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5b539-123">See also</span></span>
* [<span data-ttu-id="5b539-124">Azure Cloud Services-apps bewaken met Application Insights</span><span class="sxs-lookup"><span data-stu-id="5b539-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="5b539-125">Diagnostische Azure-gegevens verzenden naar Application Insights</span><span class="sxs-lookup"><span data-stu-id="5b539-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="5b539-126">Het configureren van waarschuwingen automatiseren</span><span class="sxs-lookup"><span data-stu-id="5b539-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

