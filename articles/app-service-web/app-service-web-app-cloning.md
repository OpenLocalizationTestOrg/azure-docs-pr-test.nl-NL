---
title: aaaWeb App klonen met behulp van PowerShell
description: Meer informatie over hoe tooclone uw Web-Apps toonew Web-Apps met behulp van PowerShell.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Azure App Service-App met behulp van PowerShell klonen
Hallo-versie van Microsoft Azure PowerShell versie 1.1.0 een nieuwe optie is toegevoegd tooNew-AzureRMWebApp waardoor aan een bestaande app Web-App-tooa nieuw gemaakt in een andere regio of in Hallo Hallo gebruiker Hallo mogelijkheid tooclone dezelfde regio. Hiermee schakelt u klanten toodeploy een aantal apps over verschillende regio's snel en eenvoudig.

Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen. gebruikt voor nieuwe functie Hallo Hallo dezelfde beperkingen als onderdeel van de back-up van Web Apps, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn over het gebruik van Azure Resource Manager gebaseerde Azure PowerShell-cmdlets toomanage de controle van uw Web-Apps [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Klonen van een bestaande App
Scenario: Een bestaande web-app in de regio Zuid-centraal VS, Hallo gebruiker graag tooclone Hallo inhoud tooa nieuwe web-app in de regio Noord-centraal VS. Dit kan worden bereikt via hello Azure Resource Manager-versie van Hallo PowerShell cmdlet toocreate een nieuwe web-app met Hallo SourceWebApp - optie.

Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo volgende PowerShell-opdracht tooget Hallo bron van web-app-gegevens (in dit geval bron webapp genoemd) gebruiken:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate een nieuwe App Service-Plan, kunnen we de opdracht New-AzureRmAppServicePlan zoals in het volgende voorbeeld Hallo gebruiken

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Met de opdracht Hallo nieuw AzureRmWebApp we Hallo nieuwe web-app maken in Hallo Noordelijk Centraal, VS regio en deze tooan bestaande premium-laag App Service-Plan koppelen, bovendien gebruiken we Hallo dezelfde resource groeperen als Hallo bron web-app of een nieuwe resourcegroep definiëren , Hallo volgende aantoont dat:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

een bestaande web-app met inbegrip van alle bijbehorende implementatiesites Hallo gebruiker moet toouse tooclone Hallo IncludeSourceWebAppSlots parameter, Hallo volgende PowerShell-opdracht laat zien dat parameter Hello nieuw AzureRmWebApp opdracht Hallo gebruikt:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

een bestaande web-app binnen Hallo tooclone dezelfde regio Hallo gebruiker moet een nieuwe resourcegroep en een nieuwe app service-plan in Hallo toocreate dezelfde regio en vervolgens via Hallo volgende PowerShell-opdracht tooclone Hallo web-app

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Klonen van een bestaande App tooan App Service-omgeving
Scenario: Een bestaande web-app in de regio Zuid-centraal VS, Hallo gebruiker graag tooclone Hallo inhoud tooa nieuwe web-app tooan bestaande as-omgeving (App Service omgeving).

Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo volgende PowerShell-opdracht tooget Hallo bron van web-app-gegevens (in dit geval bron webapp genoemd) gebruiken:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Weten Hallo as-omgeving van naam en Hallo Resourcegroepnaam behorend Hallo as-omgeving, kunt Hallo-gebruiker Hallo nieuw AzureRmWebApp opdracht toocreate Hallo nieuwe web-app in Hallo bestaande as-omgeving, Hallo na aantoont dat gebruiken:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

Hallo locatieparameter is vereist vanwege toolegacy reden, maar in geval van een app maken in een as-omgeving Hallo worden genegeerd. 

## <a name="cloning-an-existing-app-slot"></a>Klonen van een bestaande App-sleuf
Scenario: Hallo gebruiker graag tooclone een bestaande Web-Appsite tooeither een nieuwe Web-App of een nieuwe Web-appsite zijn. nieuwe Web-App weergegeven in Hallo worden Hallo dezelfde regio als het oorspronkelijke Web-App sleuf Hallo of in een andere regio.

Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo na tooget Hallo bron web-appsite van gegevens (in dit geval bron webappslot genoemd) gekoppeld tooWeb App bron-webapp PowerShell-opdracht gebruiken:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

Hallo hieronder ziet u een kloon van Hallo bron web app tooa nieuwe web-app maken:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Traffic Manager tijdens het klonen van een App configureren
Meerdere landen/regio-web-apps maken en configureren van Azure Traffic Manager tooroute verkeer tooall deze web-apps, is een n belangrijke scenario tooinsure die klanten apps zijn maximaal beschikbaar bij het klonen van een bestaande web-app die u hebt Hallo optie tooconnect beide web Apps tooeither een traffic manager-profiel of een bestaande - opmerking die alleen Azure Resource Manager-versie van Traffic Manager wordt ondersteund.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Een nieuw Traffic Manager-profiel maken tijdens het klonen van een App
Scenario: Hallo gebruiker graag tooclone een regio tooanother voor web-app tijdens het configureren van een Azure Resource Manager traffic manager-profiel die zijn zowel Webapps. Hallo hieronder ziet u een kloon van Hallo bron web app tooa nieuwe web-app gemaakt tijdens het configureren van een nieuw Traffic Manager-profiel:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Toevoegen van nieuwe gekloonde Web-App tooan bestaande Traffic Manager-profiel
Scenario: Hallo gebruiker al een Azure Resource Manager traffic manager-profiel dat hij wil tooadd zowel web-apps als eindpunten. toodo dus moeten we eerst tooassemble Hallo bestaande traffic manager-profiel-id, moeten we Hallo abonnements-id, de naam van resourcegroep en Hallo bestaande traffic manager profielnaam.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Nadat ik Hallo traffic Manager-id, ziet Hallo volgende u een kloon van Hallo bron web app tooa nieuwe web-app gemaakt tijdens het toevoegen van tooan bestaande Traffic Manager-profiel:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Huidige beperkingen
Deze functie is momenteel in preview, wij werken tooadd nieuwe mogelijkheden gedurende een bepaalde periode, Hallo volgende lijst worden bekende beperkingen voor de huidige versie van het klonen van de app Hallo Hallo:

* Instellingen voor automatisch schalen worden niet gekloond.
* Back-upschema instellingen worden niet gekloond.
* VNET-instellingen worden niet gekloond.
* App Insights worden niet automatisch ingesteld op Hallo bestemming web-app
* Eenvoudige verificatie-instellingen worden niet gekloond.
* Kudu extensie worden niet gekloond.
* TiP regels worden niet gekloond.
* Database-inhoud worden niet gekloond.

### <a name="references"></a>Verwijzingen
* [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)
* [Klonen van Web-App met Azure Portal](app-service-web-app-cloning-portal.md)
* [Back-up van een web-app in Azure App Service](web-sites-backup.md)
* [Azure Resource Manager-ondersteuning voor Azure Traffic Manager-Preview](../traffic-manager/traffic-manager-powershell-arm.md)
* [Inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)
* [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)

