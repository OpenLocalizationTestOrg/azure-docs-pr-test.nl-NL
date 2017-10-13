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
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a>PowerShell gebruiken om Application Insights in te stellen voor een Azure-web-app
[Microsoft Azure](https://azure.com) kan zo [worden geconfigureerd dat er diagnostische Azure-gegevens worden verzonden](app-insights-azure-diagnostics.md) naar [Azure Application Insights](app-insights-overview.md). De diagnostische gegevens hebben betrekking op Azure Cloud Services en virtuele Azure-machines. Ze vormen een aanvulling op de telemetrie die u vanuit de app verzendt met behulp van de Application Insights-SDK. Als onderdeel van het automatiseringsproces voor het maken van nieuwe resources in Azure kunt u het verzenden van diagnostische gegevens configureren met PowerShell.

## <a name="azure-template"></a>Azure-sjabloon
Als de web-app in Azure wordt uitgevoerd en u uw resources maakt met een Azure Resource Manager-sjabloon, kunt u Application Insights configureren door dit aan het resource-knooppunt toe te voegen:

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

* `nameOfAIAppResource`: een naam voor de Application Insights-resource
* `myWebAppName`: de id van de web-app

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice
De cmdlet `New-AzureDeployment` bevat de parameter `ExtensionConfiguration`, die overweg kan met vele configuraties voor diagnostische gegevens. Deze kunnen worden gemaakt met de cmdlet `New-AzureServiceDiagnosticsExtensionConfig`. Bijvoorbeeld:

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

Als u de extensie voor diagnostische gegevens hebt ingeschakeld met `Set-AzureServiceDiagnosticsExtension` of `New-AzureServiceDiagnosticsExtensionConfig`, zonder de parameter Rol te gebruiken, kunt u de extensie verwijderen met `Remove-AzureServiceDiagnosticsExtension`, zonder de parameter Rol. Als de parameter Rol is gebruikt bij het inschakelen van de extensie, moet deze ook worden gebruikt bij het verwijderen hiervan.

De extensie voor diagnostische gegevens verwijderen voor elke afzonderlijke rol:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Zie ook
* [Azure Cloud Services-apps bewaken met Application Insights](app-insights-cloudservices.md)
* [Diagnostische Azure-gegevens verzenden naar Application Insights](app-insights-azure-diagnostics.md)
* [Het configureren van waarschuwingen automatiseren](app-insights-powershell-alerts.md)

