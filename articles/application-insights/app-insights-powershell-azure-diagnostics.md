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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Met behulp van PowerShell tooset van Application Insights voor een Azure-web-app
[Microsoft Azure](https://azure.com) kan [toosend Azure Diagnostics geconfigureerd](app-insights-azure-diagnostics.md) te[Azure Application Insights](app-insights-overview.md). Hallo diagnostische gegevens hebben betrekking tooAzure Cloud Services en virtuele Azure-machines. Ze vormen een aanvulling Hallo telemetrie die u verzendt vanuit Hallo-app met behulp van Hallo Application Insights-SDK. Als onderdeel van het Hallo-proces voor het maken van nieuwe resources in Azure automatiseert, kunt u met behulp van PowerShell diagnostische gegevens configureren.

## <a name="azure-template"></a>Azure-sjabloon
Als het Hallo-web-app in Azure en u uw resources met een Azure Resource Manager-sjabloon maakt, kunt u Application Insights configureren door dit knooppunt van de resources toohello toe te voegen:

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

* `nameOfAIAppResource`-een naam op voor Hallo Application Insights-resource
* `myWebAppName`-Hallo Hallo web-app-id

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice
Hallo `New-AzureDeployment` cmdlet heeft een parameter `ExtensionConfiguration`, die overweg van configuraties voor diagnostische gegevens. Deze kunnen worden gemaakt met behulp van Hallo `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. Bijvoorbeeld:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice
Gebruik `Set-AzureServiceDiagnosticsExtension` voor een bestaande service.

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

## <a name="get-current-diagnostics-extension-configuration"></a>De huidige configuratie van de extensie voor diagnostische gegevens ophalen
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>De extensie voor diagnostische gegevens verwijderen
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Als u Hallo extensie voor diagnostische gegevens met behulp van ingeschakeld `Set-AzureServiceDiagnosticsExtension` of `New-AzureServiceDiagnosticsExtensionConfig` zonder de parameter rol hello, klikt u vervolgens kunt u Hallo uitbreiding met behulp van `Remove-AzureServiceDiagnosticsExtension` zonder de parameter rol Hallo. Als de parameter rol Hallo is gebruikt bij het inschakelen van extensie Hallo moet vervolgens het ook worden gebruikt bij het verwijderen van extensie Hallo.

tooremove hello extensie voor diagnostische gegevens van elke afzonderlijke rol:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Zie ook
* [Azure Cloud Services-apps bewaken met Application Insights](app-insights-cloudservices.md)
* [Azure Diagnostics tooApplication Insights verzenden](app-insights-azure-diagnostics.md)
* [Het configureren van waarschuwingen automatiseren](app-insights-powershell-alerts.md)

