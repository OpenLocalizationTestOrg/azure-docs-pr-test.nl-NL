---
title: High-density hosten op Azure App Service | Microsoft Docs
description: High-density hosten op Azure App Service
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="528d8-103">High-density hosten op Azure App Service</span><span class="sxs-lookup"><span data-stu-id="528d8-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="528d8-104">Wanneer u App Service, wordt uw toepassing losgekoppeld van de capaciteit toegewezen door twee concepten:</span><span class="sxs-lookup"><span data-stu-id="528d8-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="528d8-105">**De toepassing:** vertegenwoordigt de app en de configuratie van de runtime.</span><span class="sxs-lookup"><span data-stu-id="528d8-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="528d8-106">Bevat bijvoorbeeld de versie van .NET die de runtime moet worden geladen, wordt de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="528d8-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="528d8-107">**De App Service-abonnement:** definieert de eigenschappen van de capaciteit, de beschikbare functieset en de plaats van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="528d8-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="528d8-108">Kenmerken zijn mogelijk grote (vier kernen)-machine, vier exemplaren, Premium-functies in VS-Oost.</span><span class="sxs-lookup"><span data-stu-id="528d8-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="528d8-109">Een app altijd aan een App Service-abonnement is gekoppeld, maar een App Service-plan capaciteit om een of meer apps te kan bieden.</span><span class="sxs-lookup"><span data-stu-id="528d8-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="528d8-110">Het platform biedt daardoor de flexibiliteit om te isoleren van een enkele app of meerdere apps die resources delen door het delen van een App Service-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="528d8-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="528d8-111">Echter, wanneer meerdere apps een App Service-abonnement deelt, een exemplaar van die app wordt uitgevoerd op elke instantie van deze App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="528d8-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="528d8-112">Per app schalen</span><span class="sxs-lookup"><span data-stu-id="528d8-112">Per app scaling</span></span>
<span data-ttu-id="528d8-113">*Per app schalen* is een functie die kan worden ingeschakeld op het niveau van de App Service-plan en vervolgens gebruikt per toepassing.</span><span class="sxs-lookup"><span data-stu-id="528d8-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="528d8-114">Per app schaalt schalen een app onafhankelijk van de App Service-abonnement die als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="528d8-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="528d8-115">Op deze manier een App Service-abonnement kan worden geschaald tot 10 exemplaren, maar een app kan worden ingesteld op slechts vijf gebruiken.</span><span class="sxs-lookup"><span data-stu-id="528d8-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="528d8-116">Per app schalen is alleen beschikbaar voor **Premium** SKU App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="528d8-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="528d8-117">Per app schalen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="528d8-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="528d8-118">Kunt u een plan dat is geconfigureerd als een *Per app schalen* plan door door te geven in de ```-perSiteScaling $true``` kenmerk de ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="528d8-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="528d8-119">Als u bijwerken van een bestaand App Service-abonnement om deze functie te gebruiken wilt:</span><span class="sxs-lookup"><span data-stu-id="528d8-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="528d8-120">het doel-plan ophalen```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="528d8-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="528d8-121">de eigenschap lokaal wijzigen```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="528d8-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="528d8-122">publiceren van uw wijzigingen naar azure```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="528d8-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="528d8-123">Op het niveau van de app moeten we het aantal exemplaren die de app in app service-abonnement kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="528d8-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="528d8-124">In het onderstaande voorbeeld is de app beperkt tot twee instanties, ongeacht hoe vaak het onderliggende app service-abonnement uitgeschaald aan.</span><span class="sxs-lookup"><span data-stu-id="528d8-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="528d8-125">$newapp. SiteConfig.NumberOfWorkers is verschillende vormen $newapp. MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="528d8-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="528d8-126">Per app schalen maakt gebruik van $newapp. SiteConfig.NumberOfWorkers om te bepalen van de kenmerken van de schaal van de app.</span><span class="sxs-lookup"><span data-stu-id="528d8-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="528d8-127">Per app schalen met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="528d8-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="528d8-128">De volgende *Azure Resource Manager-sjabloon* maakt:</span><span class="sxs-lookup"><span data-stu-id="528d8-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="528d8-129">Een App Service-abonnement wordt uitgebreid naar 10 exemplaren</span><span class="sxs-lookup"><span data-stu-id="528d8-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="528d8-130">een app die geconfigureerd voor het schalen van maximaal vijf exemplaren.</span><span class="sxs-lookup"><span data-stu-id="528d8-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="528d8-131">Het instellen van de App Service-abonnement de **PerSiteScaling** eigenschap op true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="528d8-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="528d8-132">Het instellen van de app de **aantal werknemers** met 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="528d8-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="528d8-133">Aanbevolen configuratie voor het hosten van high-density</span><span class="sxs-lookup"><span data-stu-id="528d8-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="528d8-134">Per app schalen is een functie die in App Service-omgevingen en globale Azure-regio's is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="528d8-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="528d8-135">De aanbevolen strategie is echter het gebruik van App Service-omgevingen om te profiteren van de geavanceerde functies en de grotere groepen van capaciteit.</span><span class="sxs-lookup"><span data-stu-id="528d8-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="528d8-136">Volg deze stappen voor het configureren van high-density die als host fungeert voor uw apps:</span><span class="sxs-lookup"><span data-stu-id="528d8-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="528d8-137">De App-serviceomgeving configureren en kies een werknemersgroep die is aan het high-density hosting scenario toegewezen.</span><span class="sxs-lookup"><span data-stu-id="528d8-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="528d8-138">Een enkele App Service-abonnement maken en schalen voor gebruik van de beschikbare capaciteit op de worker-groep.</span><span class="sxs-lookup"><span data-stu-id="528d8-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="528d8-139">De PerSiteScaling-vlag ingesteld op true in de App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="528d8-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="528d8-140">Nieuwe apps zijn gemaakt en toegewezen aan deze App Service-abonnement met de **numberOfWorkers** eigenschap ingesteld op **1**.</span><span class="sxs-lookup"><span data-stu-id="528d8-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="528d8-141">Met deze configuratie levert de hoogst mogelijke dichtheid in deze worker-groep.</span><span class="sxs-lookup"><span data-stu-id="528d8-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="528d8-142">Het aantal werknemers kan afzonderlijk worden geconfigureerd per app verlenen aanvullende resources naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="528d8-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="528d8-143">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="528d8-143">For example:</span></span>
    - <span data-ttu-id="528d8-144">Een app intensief gebruik kunt stellen **numberOfWorkers** naar **3** hebben meer verwerkingscapaciteit voor die app.</span><span class="sxs-lookup"><span data-stu-id="528d8-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="528d8-145">Laag gebruik apps stelt **numberOfWorkers** naar **1**.</span><span class="sxs-lookup"><span data-stu-id="528d8-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="528d8-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="528d8-146">Next Steps</span></span>

- [<span data-ttu-id="528d8-147">Gedetailleerd overzicht van Azure App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="528d8-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="528d8-148">Inleiding tot de App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="528d8-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)