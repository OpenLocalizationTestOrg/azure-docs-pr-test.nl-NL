---
title: aaaPowerShell script toocreate Application Insights-resource | Microsoft Docs
description: Maken van de Application Insights-resources automatiseren.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>PowerShell-script toocreate Application Insights-resource


Als u wilt dat toomonitor een nieuwe toepassing- of een nieuwe versie van een toepassing - met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), instellen van een nieuwe resource in Microsoft Azure. Deze resource wordt waarbij Hallo-telemetriegegevens vanuit uw app geanalyseerd en weergegeven. 

U kunt Hallo maken van een nieuwe bron automatiseren met behulp van PowerShell.

Als u een mobiel apparaat-app ontwikkelt, is het bijvoorbeeld waarschijnlijk dat op elk gewenst moment zal er verschillende versies van uw app wordt gebruikt door uw klanten zijn gepubliceerd. Wilt u tooget Hallo telemetrie resultaten van verschillende versies verward niet. Zodat u uw toocreate build-proces een nieuwe bron voor elke build ophalen.

> [!NOTE]
> Als u wilt dat toocreate een set resources alles op Hallo dezelfde tijd, overweeg dan [Hallo-resources met behulp van een Azure-sjabloon maken](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Script toocreate Application Insights-resource
Zie Hallo relevante cmdlet specificaties:

* [Nieuwe AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*PowerShell-Script*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Welke toodo met Hallo iKey
Elke bron wordt geïdentificeerd door de instrumentatiesleutel (iKey). Hallo iKey is uitvoer van Hallo-script voor het maken van resource. Uw script build leveren Hallo iKey toohello die Application Insights-SDK is ingesloten in uw app.

Er zijn twee manieren toomake Hallo iKey beschikbaar toohello SDK:

* In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*iKey*`</instrumentationkey>`
* Of in [initialisatiecode](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Zie ook
* [Application Insights en test webbronnen van sjablonen maken](app-insights-powershell.md)
* [Instellen van de bewaking van Azure diagnostics met PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Waarschuwingen instellen met behulp van PowerShell](app-insights-powershell-alerts.md)

