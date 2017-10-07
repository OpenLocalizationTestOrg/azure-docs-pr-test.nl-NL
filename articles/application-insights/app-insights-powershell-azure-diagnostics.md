---
title: aaaUsing PowerShell toosetup Application Insights in een Azure | Microsoft Docs
description: Configureren Azure Diagnostics toopipe tooApplication Insights automatiseren.
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
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="2ec02-103">Met behulp van PowerShell tooset van Application Insights voor een Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="2ec02-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="2ec02-104">[Microsoft Azure](https://azure.com) kan [toosend Azure Diagnostics geconfigureerd](app-insights-azure-diagnostics.md) te[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ec02-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2ec02-105">Hallo diagnostische gegevens hebben betrekking tooAzure Cloud Services en virtuele Azure-machines.</span><span class="sxs-lookup"><span data-stu-id="2ec02-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="2ec02-106">Ze vormen een aanvulling Hallo telemetrie die u verzendt vanuit Hallo-app met behulp van Hallo Application Insights-SDK.</span><span class="sxs-lookup"><span data-stu-id="2ec02-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="2ec02-107">Als onderdeel van het Hallo-proces voor het maken van nieuwe resources in Azure automatiseert, kunt u met behulp van PowerShell diagnostische gegevens configureren.</span><span class="sxs-lookup"><span data-stu-id="2ec02-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="2ec02-108">Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="2ec02-108">Azure template</span></span>
<span data-ttu-id="2ec02-109">Als het Hallo-web-app in Azure en u uw resources met een Azure Resource Manager-sjabloon maakt, kunt u Application Insights configureren door dit knooppunt van de resources toohello toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="2ec02-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="2ec02-110">`nameOfAIAppResource`-een naam op voor Hallo Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="2ec02-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="2ec02-111">`myWebAppName`-Hallo Hallo web-app-id</span><span class="sxs-lookup"><span data-stu-id="2ec02-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="2ec02-112">De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="2ec02-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="2ec02-113">Hallo `New-AzureDeployment` cmdlet heeft een parameter `ExtensionConfiguration`, die overweg van configuraties voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2ec02-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="2ec02-114">Deze kunnen worden gemaakt met behulp van Hallo `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ec02-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="2ec02-115">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2ec02-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="2ec02-116">De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice</span><span class="sxs-lookup"><span data-stu-id="2ec02-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="2ec02-117">Gebruik `Set-AzureServiceDiagnosticsExtension` voor een bestaande service.</span><span class="sxs-lookup"><span data-stu-id="2ec02-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="2ec02-118">De huidige configuratie van de extensie voor diagnostische gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="2ec02-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="2ec02-119">De extensie voor diagnostische gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="2ec02-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="2ec02-120">Als u Hallo extensie voor diagnostische gegevens met behulp van ingeschakeld `Set-AzureServiceDiagnosticsExtension` of `New-AzureServiceDiagnosticsExtensionConfig` zonder de parameter rol hello, klikt u vervolgens kunt u Hallo uitbreiding met behulp van `Remove-AzureServiceDiagnosticsExtension` zonder de parameter rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ec02-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="2ec02-121">Als de parameter rol Hallo is gebruikt bij het inschakelen van extensie Hallo moet vervolgens het ook worden gebruikt bij het verwijderen van extensie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ec02-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="2ec02-122">tooremove hello extensie voor diagnostische gegevens van elke afzonderlijke rol:</span><span class="sxs-lookup"><span data-stu-id="2ec02-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="2ec02-123">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2ec02-123">See also</span></span>
* [<span data-ttu-id="2ec02-124">Azure Cloud Services-apps bewaken met Application Insights</span><span class="sxs-lookup"><span data-stu-id="2ec02-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="2ec02-125">Azure Diagnostics tooApplication Insights verzenden</span><span class="sxs-lookup"><span data-stu-id="2ec02-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="2ec02-126">Het configureren van waarschuwingen automatiseren</span><span class="sxs-lookup"><span data-stu-id="2ec02-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

