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
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="65408-103">Azure App Service-App met behulp van PowerShell klonen</span><span class="sxs-lookup"><span data-stu-id="65408-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="65408-104">Hallo-versie van Microsoft Azure PowerShell versie 1.1.0 een nieuwe optie is toegevoegd tooNew-AzureRMWebApp waardoor aan een bestaande app Web-App-tooa nieuw gemaakt in een andere regio of in Hallo Hallo gebruiker Hallo mogelijkheid tooclone dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="65408-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="65408-105">Hiermee schakelt u klanten toodeploy een aantal apps over verschillende regio's snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="65408-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="65408-106">Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="65408-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="65408-107">gebruikt voor nieuwe functie Hallo Hallo dezelfde beperkingen als onderdeel van de back-up van Web Apps, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="65408-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="65408-108">toolearn over het gebruik van Azure Resource Manager gebaseerde Azure PowerShell-cmdlets toomanage de controle van uw Web-Apps [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="65408-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="65408-109">Klonen van een bestaande App</span><span class="sxs-lookup"><span data-stu-id="65408-109">Cloning an existing App</span></span>
<span data-ttu-id="65408-110">Scenario: Een bestaande web-app in de regio Zuid-centraal VS, Hallo gebruiker graag tooclone Hallo inhoud tooa nieuwe web-app in de regio Noord-centraal VS.</span><span class="sxs-lookup"><span data-stu-id="65408-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="65408-111">Dit kan worden bereikt via hello Azure Resource Manager-versie van Hallo PowerShell cmdlet toocreate een nieuwe web-app met Hallo SourceWebApp - optie.</span><span class="sxs-lookup"><span data-stu-id="65408-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="65408-112">Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo volgende PowerShell-opdracht tooget Hallo bron van web-app-gegevens (in dit geval bron webapp genoemd) gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65408-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="65408-113">toocreate een nieuwe App Service-Plan, kunnen we de opdracht New-AzureRmAppServicePlan zoals in het volgende voorbeeld Hallo gebruiken</span><span class="sxs-lookup"><span data-stu-id="65408-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="65408-114">Met de opdracht Hallo nieuw AzureRmWebApp we Hallo nieuwe web-app maken in Hallo Noordelijk Centraal, VS regio en deze tooan bestaande premium-laag App Service-Plan koppelen, bovendien gebruiken we Hallo dezelfde resource groeperen als Hallo bron web-app of een nieuwe resourcegroep definiëren , Hallo volgende aantoont dat:</span><span class="sxs-lookup"><span data-stu-id="65408-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="65408-115">een bestaande web-app met inbegrip van alle bijbehorende implementatiesites Hallo gebruiker moet toouse tooclone Hallo IncludeSourceWebAppSlots parameter, Hallo volgende PowerShell-opdracht laat zien dat parameter Hello nieuw AzureRmWebApp opdracht Hallo gebruikt:</span><span class="sxs-lookup"><span data-stu-id="65408-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="65408-116">een bestaande web-app binnen Hallo tooclone dezelfde regio Hallo gebruiker moet een nieuwe resourcegroep en een nieuwe app service-plan in Hallo toocreate dezelfde regio en vervolgens via Hallo volgende PowerShell-opdracht tooclone Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="65408-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="65408-117">Klonen van een bestaande App tooan App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="65408-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="65408-118">Scenario: Een bestaande web-app in de regio Zuid-centraal VS, Hallo gebruiker graag tooclone Hallo inhoud tooa nieuwe web-app tooan bestaande as-omgeving (App Service omgeving).</span><span class="sxs-lookup"><span data-stu-id="65408-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="65408-119">Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo volgende PowerShell-opdracht tooget Hallo bron van web-app-gegevens (in dit geval bron webapp genoemd) gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65408-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="65408-120">Weten Hallo as-omgeving van naam en Hallo Resourcegroepnaam behorend Hallo as-omgeving, kunt Hallo-gebruiker Hallo nieuw AzureRmWebApp opdracht toocreate Hallo nieuwe web-app in Hallo bestaande as-omgeving, Hallo na aantoont dat gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65408-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="65408-121">Hallo locatieparameter is vereist vanwege toolegacy reden, maar in geval van een app maken in een as-omgeving Hallo worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="65408-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="65408-122">Klonen van een bestaande App-sleuf</span><span class="sxs-lookup"><span data-stu-id="65408-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="65408-123">Scenario: Hallo gebruiker graag tooclone een bestaande Web-Appsite tooeither een nieuwe Web-App of een nieuwe Web-appsite zijn.</span><span class="sxs-lookup"><span data-stu-id="65408-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="65408-124">nieuwe Web-App weergegeven in Hallo worden Hallo dezelfde regio als het oorspronkelijke Web-App sleuf Hallo of in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="65408-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="65408-125">Hallo resource weten groepsnaam die Hallo bron web-app bevat, kunnen we Hallo na tooget Hallo bron web-appsite van gegevens (in dit geval bron webappslot genoemd) gekoppeld tooWeb App bron-webapp PowerShell-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65408-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="65408-126">Hallo hieronder ziet u een kloon van Hallo bron web app tooa nieuwe web-app maken:</span><span class="sxs-lookup"><span data-stu-id="65408-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="65408-127">Traffic Manager tijdens het klonen van een App configureren</span><span class="sxs-lookup"><span data-stu-id="65408-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="65408-128">Meerdere landen/regio-web-apps maken en configureren van Azure Traffic Manager tooroute verkeer tooall deze web-apps, is een n belangrijke scenario tooinsure die klanten apps zijn maximaal beschikbaar bij het klonen van een bestaande web-app die u hebt Hallo optie tooconnect beide web Apps tooeither een traffic manager-profiel of een bestaande - opmerking die alleen Azure Resource Manager-versie van Traffic Manager wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="65408-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="65408-129">Een nieuw Traffic Manager-profiel maken tijdens het klonen van een App</span><span class="sxs-lookup"><span data-stu-id="65408-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="65408-130">Scenario: Hallo gebruiker graag tooclone een regio tooanother voor web-app tijdens het configureren van een Azure Resource Manager traffic manager-profiel die zijn zowel Webapps.</span><span class="sxs-lookup"><span data-stu-id="65408-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="65408-131">Hallo hieronder ziet u een kloon van Hallo bron web app tooa nieuwe web-app gemaakt tijdens het configureren van een nieuw Traffic Manager-profiel:</span><span class="sxs-lookup"><span data-stu-id="65408-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="65408-132">Toevoegen van nieuwe gekloonde Web-App tooan bestaande Traffic Manager-profiel</span><span class="sxs-lookup"><span data-stu-id="65408-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="65408-133">Scenario: Hallo gebruiker al een Azure Resource Manager traffic manager-profiel dat hij wil tooadd zowel web-apps als eindpunten.</span><span class="sxs-lookup"><span data-stu-id="65408-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="65408-134">toodo dus moeten we eerst tooassemble Hallo bestaande traffic manager-profiel-id, moeten we Hallo abonnements-id, de naam van resourcegroep en Hallo bestaande traffic manager profielnaam.</span><span class="sxs-lookup"><span data-stu-id="65408-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="65408-135">Nadat ik Hallo traffic Manager-id, ziet Hallo volgende u een kloon van Hallo bron web app tooa nieuwe web-app gemaakt tijdens het toevoegen van tooan bestaande Traffic Manager-profiel:</span><span class="sxs-lookup"><span data-stu-id="65408-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="65408-136">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="65408-136">Current Restrictions</span></span>
<span data-ttu-id="65408-137">Deze functie is momenteel in preview, wij werken tooadd nieuwe mogelijkheden gedurende een bepaalde periode, Hallo volgende lijst worden bekende beperkingen voor de huidige versie van het klonen van de app Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="65408-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="65408-138">Instellingen voor automatisch schalen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="65408-139">Back-upschema instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="65408-140">VNET-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="65408-141">App Insights worden niet automatisch ingesteld op Hallo bestemming web-app</span><span class="sxs-lookup"><span data-stu-id="65408-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="65408-142">Eenvoudige verificatie-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="65408-143">Kudu extensie worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="65408-144">TiP regels worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="65408-145">Database-inhoud worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="65408-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="65408-146">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="65408-146">References</span></span>
* [<span data-ttu-id="65408-147">PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65408-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="65408-148">Klonen van Web-App met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="65408-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="65408-149">Back-up van een web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="65408-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="65408-150">Azure Resource Manager-ondersteuning voor Azure Traffic Manager-Preview</span><span class="sxs-lookup"><span data-stu-id="65408-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="65408-151">Inleiding tooApp Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="65408-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="65408-152">Azure PowerShell gebruiken met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="65408-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

