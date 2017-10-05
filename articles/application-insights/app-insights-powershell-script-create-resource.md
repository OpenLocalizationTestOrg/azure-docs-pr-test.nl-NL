---
title: PowerShell-script voor het maken van een Application Insights-resource | Microsoft Docs
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="73976-103">PowerShell-script om een Application Insights-resource te maken</span><span class="sxs-lookup"><span data-stu-id="73976-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="73976-104">Als u wilt bewaken van een nieuwe toepassing- of een nieuwe versie van een toepassing - met [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), instellen van een nieuwe resource in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="73976-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="73976-105">Deze resource wordt waarbij de telemetriegegevens vanuit uw app geanalyseerd en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="73976-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="73976-106">U kunt het maken van een nieuwe resource automatiseren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73976-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="73976-107">Als u een mobiel apparaat-app ontwikkelt, is het bijvoorbeeld waarschijnlijk dat op elk gewenst moment zal er verschillende versies van uw app wordt gebruikt door uw klanten zijn gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="73976-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="73976-108">U wilt niet dat de resultaten van de telemetrie van verschillende versies verward ophalen.</span><span class="sxs-lookup"><span data-stu-id="73976-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="73976-109">Zo kunt u uw buildproces voor het maken van een nieuwe bron voor elk build ophalen.</span><span class="sxs-lookup"><span data-stu-id="73976-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="73976-110">Als u maken van een set resources allemaal op hetzelfde moment wilt, overweeg dan [maken van de resources met een Azure-sjabloon](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="73976-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="73976-111">Script voor het maken van een Application Insights-resource</span><span class="sxs-lookup"><span data-stu-id="73976-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="73976-112">Zie de specificaties van de relevante cmdlet:</span><span class="sxs-lookup"><span data-stu-id="73976-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="73976-113">Nieuwe AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="73976-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="73976-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="73976-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="73976-115">*PowerShell-Script*</span><span class="sxs-lookup"><span data-stu-id="73976-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="73976-116">Wat te doen met de sleutel</span><span class="sxs-lookup"><span data-stu-id="73976-116">What to do with the iKey</span></span>
<span data-ttu-id="73976-117">Elke bron wordt geïdentificeerd door de instrumentatiesleutel (iKey).</span><span class="sxs-lookup"><span data-stu-id="73976-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="73976-118">De sleutel is de uitvoer van een script voor het maken van de resource.</span><span class="sxs-lookup"><span data-stu-id="73976-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="73976-119">Uw script build leveren dat de iKey naar Application Insights-SDK is ingesloten in uw app.</span><span class="sxs-lookup"><span data-stu-id="73976-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="73976-120">Er zijn twee manieren om de iKey beschikbaar te maken met de SDK:</span><span class="sxs-lookup"><span data-stu-id="73976-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="73976-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="73976-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="73976-122">`<instrumentationkey>`*iKey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="73976-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="73976-123">Of in [initialisatiecode](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="73976-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="73976-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="73976-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="73976-125">Zie ook</span><span class="sxs-lookup"><span data-stu-id="73976-125">See also</span></span>
* [<span data-ttu-id="73976-126">Application Insights en test webbronnen van sjablonen maken</span><span class="sxs-lookup"><span data-stu-id="73976-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="73976-127">Instellen van de bewaking van Azure diagnostics met PowerShell</span><span class="sxs-lookup"><span data-stu-id="73976-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="73976-128">Waarschuwingen instellen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="73976-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

