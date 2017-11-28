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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="12a2d-103">PowerShell-script toocreate Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="12a2d-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="12a2d-104">Als u wilt dat toomonitor een nieuwe toepassing- of een nieuwe versie van een toepassing - met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), instellen van een nieuwe resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12a2d-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="12a2d-105">Deze resource wordt waarbij Hallo-telemetriegegevens vanuit uw app geanalyseerd en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="12a2d-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="12a2d-106">U kunt Hallo maken van een nieuwe bron automatiseren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12a2d-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="12a2d-107">Als u een mobiel apparaat-app ontwikkelt, is het bijvoorbeeld waarschijnlijk dat op elk gewenst moment zal er verschillende versies van uw app wordt gebruikt door uw klanten zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="12a2d-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="12a2d-108">Wilt u tooget Hallo telemetrie resultaten van verschillende versies verward niet.</span><span class="sxs-lookup"><span data-stu-id="12a2d-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="12a2d-109">Zodat u uw toocreate build-proces een nieuwe bron voor elke build ophalen.</span><span class="sxs-lookup"><span data-stu-id="12a2d-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="12a2d-110">Als u wilt dat toocreate een set resources alles op Hallo dezelfde tijd, overweeg dan [Hallo-resources met behulp van een Azure-sjabloon maken](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="12a2d-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="12a2d-111">Script toocreate Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="12a2d-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="12a2d-112">Zie Hallo relevante cmdlet specificaties:</span><span class="sxs-lookup"><span data-stu-id="12a2d-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="12a2d-113">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="12a2d-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="12a2d-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="12a2d-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="12a2d-115">*PowerShell-Script*</span><span class="sxs-lookup"><span data-stu-id="12a2d-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="12a2d-116">Welke toodo met Hallo iKey</span><span class="sxs-lookup"><span data-stu-id="12a2d-116">What toodo with hello iKey</span></span>
<span data-ttu-id="12a2d-117">Elke bron wordt geïdentificeerd door de instrumentatiesleutel (iKey).</span><span class="sxs-lookup"><span data-stu-id="12a2d-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="12a2d-118">Hallo iKey is uitvoer van Hallo-script voor het maken van resource.</span><span class="sxs-lookup"><span data-stu-id="12a2d-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="12a2d-119">Uw script build leveren Hallo iKey toohello die Application Insights-SDK is ingesloten in uw app.</span><span class="sxs-lookup"><span data-stu-id="12a2d-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="12a2d-120">Er zijn twee manieren toomake Hallo iKey beschikbaar toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="12a2d-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="12a2d-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="12a2d-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="12a2d-122">`<instrumentationkey>`*iKey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="12a2d-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="12a2d-123">Of in [initialisatiecode](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="12a2d-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="12a2d-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="12a2d-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="12a2d-125">Zie ook</span><span class="sxs-lookup"><span data-stu-id="12a2d-125">See also</span></span>
* [<span data-ttu-id="12a2d-126">Application Insights en test webbronnen van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="12a2d-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="12a2d-127">Instellen van de bewaking van Azure diagnostics met PowerShell</span><span class="sxs-lookup"><span data-stu-id="12a2d-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="12a2d-128">Waarschuwingen instellen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="12a2d-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

