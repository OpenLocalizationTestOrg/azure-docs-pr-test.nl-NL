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
# <a name="high-density-hosting-on-azure-app-service"></a>High-density hosten op Azure App Service
Wanneer u App Service, wordt uw toepassing ontkoppeld van Hallo capaciteit tooit toegewezen door twee concepten:

* **Hallo toepassing:** Hallo-app en de configuratie van de runtime vertegenwoordigt. Bevat bijvoorbeeld het Hallo-versie van .NET runtime Hallo moet laden, Hallo app-instellingen.
* **App Service-Plan Hallo:** Hallo kenmerken Hallo capaciteit en beschikbare functieset plaats van de toepassing hello worden gedefinieerd. Kenmerken zijn mogelijk grote (vier kernen)-machine, vier exemplaren, Premium-functies in VS-Oost.

Een app is altijd gekoppelde tooan App Service-abonnement, maar een App Service-abonnement kunt capaciteit tooone of meer apps bieden.

Als gevolg hiervan Hallo-platform biedt Hallo flexibiliteit tooisolate een enkele app of meerdere apps die resources delen door het delen van een App Service-abonnement hebben.

Echter, wanneer meerdere apps een App Service-abonnement deelt, een exemplaar van die app wordt uitgevoerd op elke instantie van deze App Service-abonnement.

## <a name="per-app-scaling"></a>Per app schalen
*Per app schalen* is een functie die kan worden ingeschakeld op het niveau van de App Service-plan en vervolgens gebruikt per toepassing.

Per app schaalt schalen een app onafhankelijk van de App Service-abonnement die als host fungeert. Op deze manier een App Service plan kan worden geschaald too10 exemplaren, maar slechts vijf toouse door een app kan worden ingesteld.

   >[!NOTE]
   >Per app schalen is alleen beschikbaar voor **Premium** SKU App Service-plannen
   >

### <a name="per-app-scaling-using-powershell"></a>Per app schalen met behulp van PowerShell

Kunt u een plan dat is geconfigureerd als een *Per app schalen* plan door door te geven in Hallo ```-perSiteScaling $true``` toohello kenmerk ```New-AzureRmAppServicePlan``` commandlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Als u wilt dat tooupdate een bestaande App Service plan toouse deze functie: 

- Hallo doel plan ophalen```Get-AzureRmAppServicePlan```
- lokaal Hallo-eigenschap```$newASP.PerSiteScaling = $true```
- uw wijzigingen back tooazure boeken```Set-AzureRmAppServicePlan``` 

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

Op het niveau app hello moeten we tooconfigure Hallo aantal instanties Hallo app in Hallo-app service-abonnement gebruiken kunt.

In onderstaand voorbeeld Hallo is Hallo-app beperkt tootwo exemplaren ongeacht hoeveel exemplaren Hallo onderliggende app service-abonnement kan worden geschaald uit te.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp. SiteConfig.NumberOfWorkers is verschillende vormen $newapp. MaxNumberOfWorkers. Per app schalen maakt gebruik van $newapp. SiteConfig.NumberOfWorkers toodetermine Hallo scale kenmerken van het Hallo-app.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Per app schalen met Azure Resource Manager

Hallo volgende *Azure Resource Manager-sjabloon* maakt:

- Een App Service-abonnement too10 exemplaren wordt uitgebreid
- een app die tooscale tooa maximaal vijf exemplaren is geconfigureerd.

Hallo App Service-abonnement is bezig met het Hallo **PerSiteScaling** eigenschap tootrue ```"perSiteScaling": true```. Hallo-app is bezig met het Hallo **aantal werknemers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Aanbevolen configuratie voor het hosten van high-density
Per app schalen is een functie die in App Service-omgevingen en globale Azure-regio's is ingeschakeld. Hallo echter aanbevolen strategie is het gebruik van App Service-omgevingen tootake profiteren van de geavanceerde functies en grotere groepen Hallo van capaciteit.  

Volg deze stappen tooconfigure high-density die als host fungeert voor uw apps:

1. Hallo App Service-omgeving te configureren en kies een worker-groep die is toegewezen toohello high-density scenario hosten.
1. Een enkele App Service-abonnement maken en schalen toouse alle beschikbare capaciteit in werknemersgroep Hallo Hallo.
1. Hallo PerSiteScaling vlag tootrue niet instellen op Hallo App Service-abonnement.
1. Nieuwe apps zijn gemaakt en toegewezen toothat App Service-abonnement met de **numberOfWorkers** eigenschappenset te**1**. Met deze configuratie levert Hallo hoogste dichtheid mogelijk in deze worker-groep.
1. het aantal werknemers Hallo kan afzonderlijk worden geconfigureerd per app toogrant aanvullende resources naar behoefte. Bijvoorbeeld:
    - Een app intensief gebruik kunt stellen **numberOfWorkers** te**3** toohave meer capaciteit voor die app verwerken. 
    - Laag gebruik apps stelt **numberOfWorkers** te**1**.

## <a name="next-steps"></a>Volgende stappen

- [Gedetailleerd overzicht van Azure App Service-plannen](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Inleiding tooApp Service-omgeving](../app-service-web/app-service-app-service-environment-intro.md)
