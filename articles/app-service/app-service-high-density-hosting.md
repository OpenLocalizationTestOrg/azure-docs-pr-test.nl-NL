---
title: aaaHigh dichtheid hosten op Azure App Service | Microsoft Docs
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="8f077-103">High-density hosten op Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8f077-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="8f077-104">Wanneer u App Service, wordt uw toepassing ontkoppeld van Hallo capaciteit tooit toegewezen door twee concepten:</span><span class="sxs-lookup"><span data-stu-id="8f077-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="8f077-105">**Hallo toepassing:** Hallo-app en de configuratie van de runtime vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="8f077-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="8f077-106">Bevat bijvoorbeeld het Hallo-versie van .NET runtime Hallo moet laden, Hallo app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8f077-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="8f077-107">**App Service-Plan Hallo:** Hallo kenmerken Hallo capaciteit en beschikbare functieset plaats van de toepassing hello worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="8f077-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="8f077-108">Kenmerken zijn mogelijk grote (vier kernen)-machine, vier exemplaren, Premium-functies in VS-Oost.</span><span class="sxs-lookup"><span data-stu-id="8f077-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="8f077-109">Een app is altijd gekoppelde tooan App Service-abonnement, maar een App Service-abonnement kunt capaciteit tooone of meer apps bieden.</span><span class="sxs-lookup"><span data-stu-id="8f077-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="8f077-110">Als gevolg hiervan Hallo-platform biedt Hallo flexibiliteit tooisolate een enkele app of meerdere apps die resources delen door het delen van een App Service-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="8f077-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="8f077-111">Echter, wanneer meerdere apps een App Service-abonnement deelt, een exemplaar van die app wordt uitgevoerd op elke instantie van deze App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8f077-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="8f077-112">Per app schalen</span><span class="sxs-lookup"><span data-stu-id="8f077-112">Per app scaling</span></span>
<span data-ttu-id="8f077-113">*Per app schalen* is een functie die kan worden ingeschakeld op het niveau van de App Service-plan en vervolgens gebruikt per toepassing.</span><span class="sxs-lookup"><span data-stu-id="8f077-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="8f077-114">Per app schaalt schalen een app onafhankelijk van de App Service-abonnement die als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="8f077-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="8f077-115">Op deze manier een App Service plan kan worden geschaald too10 exemplaren, maar slechts vijf toouse door een app kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8f077-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="8f077-116">Per app schalen is alleen beschikbaar voor **Premium** SKU App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="8f077-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="8f077-117">Per app schalen met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f077-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="8f077-118">Kunt u een plan dat is geconfigureerd als een *Per app schalen* plan door door te geven in Hallo ```-perSiteScaling $true``` toohello kenmerk ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="8f077-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="8f077-119">Als u wilt dat tooupdate een bestaande App Service plan toouse deze functie:</span><span class="sxs-lookup"><span data-stu-id="8f077-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="8f077-120">Hallo doel plan ophalen```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="8f077-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="8f077-121">lokaal Hallo-eigenschap```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="8f077-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="8f077-122">uw wijzigingen back tooazure boeken```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="8f077-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="8f077-123">Op het niveau app hello moeten we tooconfigure Hallo aantal instanties Hallo app in Hallo-app service-abonnement gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="8f077-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="8f077-124">In onderstaand voorbeeld Hallo is Hallo-app beperkt tootwo exemplaren ongeacht hoeveel exemplaren Hallo onderliggende app service-abonnement kan worden geschaald uit te.</span><span class="sxs-lookup"><span data-stu-id="8f077-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="8f077-125">$newapp. SiteConfig.NumberOfWorkers is verschillende vormen $newapp. MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="8f077-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="8f077-126">Per app schalen maakt gebruik van $newapp. SiteConfig.NumberOfWorkers toodetermine Hallo scale kenmerken van het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="8f077-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="8f077-127">Per app schalen met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f077-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="8f077-128">Hallo volgende *Azure Resource Manager-sjabloon* maakt:</span><span class="sxs-lookup"><span data-stu-id="8f077-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="8f077-129">Een App Service-abonnement too10 exemplaren wordt uitgebreid</span><span class="sxs-lookup"><span data-stu-id="8f077-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="8f077-130">een app die tooscale tooa maximaal vijf exemplaren is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8f077-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="8f077-131">Hallo App Service-abonnement is bezig met het Hallo **PerSiteScaling** eigenschap tootrue ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="8f077-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="8f077-132">Hallo-app is bezig met het Hallo **aantal werknemers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="8f077-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="8f077-133">Aanbevolen configuratie voor het hosten van high-density</span><span class="sxs-lookup"><span data-stu-id="8f077-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="8f077-134">Per app schalen is een functie die in App Service-omgevingen en globale Azure-regio's is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8f077-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="8f077-135">Hallo echter aanbevolen strategie is het gebruik van App Service-omgevingen tootake profiteren van de geavanceerde functies en grotere groepen Hallo van capaciteit.</span><span class="sxs-lookup"><span data-stu-id="8f077-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="8f077-136">Volg deze stappen tooconfigure high-density die als host fungeert voor uw apps:</span><span class="sxs-lookup"><span data-stu-id="8f077-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="8f077-137">Hallo App Service-omgeving te configureren en kies een worker-groep die is toegewezen toohello high-density scenario hosten.</span><span class="sxs-lookup"><span data-stu-id="8f077-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="8f077-138">Een enkele App Service-abonnement maken en schalen toouse alle beschikbare capaciteit in werknemersgroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f077-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="8f077-139">Hallo PerSiteScaling vlag tootrue niet instellen op Hallo App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8f077-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="8f077-140">Nieuwe apps zijn gemaakt en toegewezen toothat App Service-abonnement met de **numberOfWorkers** eigenschappenset te**1**.</span><span class="sxs-lookup"><span data-stu-id="8f077-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="8f077-141">Met deze configuratie levert Hallo hoogste dichtheid mogelijk in deze worker-groep.</span><span class="sxs-lookup"><span data-stu-id="8f077-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="8f077-142">het aantal werknemers Hallo kan afzonderlijk worden geconfigureerd per app toogrant aanvullende resources naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="8f077-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="8f077-143">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8f077-143">For example:</span></span>
    - <span data-ttu-id="8f077-144">Een app intensief gebruik kunt stellen **numberOfWorkers** te**3** toohave meer capaciteit voor die app verwerken.</span><span class="sxs-lookup"><span data-stu-id="8f077-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="8f077-145">Laag gebruik apps stelt **numberOfWorkers** te**1**.</span><span class="sxs-lookup"><span data-stu-id="8f077-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f077-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f077-146">Next Steps</span></span>

- [<span data-ttu-id="8f077-147">Gedetailleerd overzicht van Azure App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="8f077-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="8f077-148">Inleiding tooApp Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="8f077-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
