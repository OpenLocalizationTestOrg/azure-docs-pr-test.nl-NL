---
title: Klonen van Web-App met behulp van PowerShell
description: Informatie over het klonen van uw Web-Apps naar de nieuwe Web-Apps met behulp van PowerShell.
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
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="165b4-103">Azure App Service-App met behulp van PowerShell klonen</span><span class="sxs-lookup"><span data-stu-id="165b4-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="165b4-104">Met de release van Microsoft Azure PowerShell versie 1.1.0 is een nieuwe optie zijn toegevoegd aan New-AzureRMWebApp die de gebruiker de mogelijkheid geven voor het klonen van een bestaande Web-App naar een nieuwe app in een andere regio of in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="165b4-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="165b4-105">Hiermee schakelt u klanten een aantal apps implementeren in verschillende regio's snel en eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="165b4-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="165b4-106">Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="165b4-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="165b4-107">De nieuwe functie maakt gebruik van dezelfde beperkingen als de functie Web Apps back-up, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="165b4-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="165b4-108">Voor meer informatie over het gebruik van Azure PowerShell-cmdlets voor het beheren van de controle van uw Web-Apps op basis van Azure Resource Manager [PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="165b4-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="165b4-109">Klonen van een bestaande App</span><span class="sxs-lookup"><span data-stu-id="165b4-109">Cloning an existing App</span></span>
<span data-ttu-id="165b4-110">Scenario: Een bestaande web-app in Zuid-centraal VS regio, de gebruiker wil de inhoud naar een nieuwe web-app in de regio Noord-centraal VS klonen.</span><span class="sxs-lookup"><span data-stu-id="165b4-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="165b4-111">Dit kan worden bewerkstelligd met behulp van de Azure Resource Manager-versie van de PowerShell-cmdlet voor het maken van een nieuwe web-app met de optie - SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="165b4-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="165b4-112">Naam van de resourcegroep met de bron-web-app weet, kunnen we de volgende PowerShell-opdracht ophalen van informatie van de bron web-app (in dit geval bron webapp genoemd) gebruiken:</span><span class="sxs-lookup"><span data-stu-id="165b4-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="165b4-113">Voor het maken van een nieuwe App Service-Plan, kunnen we de opdracht New-AzureRmAppServicePlan zoals in het volgende voorbeeld gebruiken</span><span class="sxs-lookup"><span data-stu-id="165b4-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="165b4-114">Met de opdracht New-AzureRmWebApp we kunnen de nieuwe web-app maken in de regio Noord-centraal VS, en deze koppelen aan een bestaand App Service-Plan premium-laag, bovendien we gebruik van dezelfde resourcegroep bevinden als de bron-web-app of een nieuwe resourcegroep definiëren, het volgende voorbeeld toont die:</span><span class="sxs-lookup"><span data-stu-id="165b4-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="165b4-115">Voor het klonen van een bestaande web-app, inclusief alle gekoppelde implementatie sleuven, de gebruiker moet de parameter IncludeSourceWebAppSlots gebruiken, de volgende PowerShell-opdracht laat zien hoe u deze parameter met de opdracht New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="165b4-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="165b4-116">Als u wilt klonen van een bestaande web-app in dezelfde regio, moet de gebruiker een nieuwe resourcegroep en een nieuwe app service maken plannen in dezelfde regio en klik vervolgens met behulp van de volgende PowerShell-opdracht voor het klonen van de web-app</span><span class="sxs-lookup"><span data-stu-id="165b4-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="165b4-117">Klonen van een bestaande App aan een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="165b4-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="165b4-118">Scenario: Een bestaande web-app in Zuid-centraal VS regio, de gebruiker wil graag klonen van de inhoud naar een nieuwe web-app aan een bestaand App Service omgeving (as-omgeving).</span><span class="sxs-lookup"><span data-stu-id="165b4-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="165b4-119">Naam van de resourcegroep met de bron-web-app weet, kunnen we de volgende PowerShell-opdracht ophalen van informatie van de bron web-app (in dit geval bron webapp genoemd) gebruiken:</span><span class="sxs-lookup"><span data-stu-id="165b4-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="165b4-120">De naam van de as-omgeving en de naam van de resourcegroep die deel uitmaakt van de as-omgeving te weten, kunnen gebruikers de opdracht New-AzureRmWebApp gebruiken voor het maken van de nieuwe web-app in de bestaande as-omgeving, het volgende voorbeeld toont die:</span><span class="sxs-lookup"><span data-stu-id="165b4-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="165b4-121">De locatie-parameter is vereist om verouderde reden, maar in het geval van een app maken in een as-omgeving worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="165b4-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="165b4-122">Klonen van een bestaande App-sleuf</span><span class="sxs-lookup"><span data-stu-id="165b4-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="165b4-123">Scenario: De gebruiker wil graag klonen van een bestaande Web-Appsite ofwel een nieuwe Web-App of een nieuwe sleuf voor Web-App.</span><span class="sxs-lookup"><span data-stu-id="165b4-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="165b4-124">De nieuwe Web-App kunnen zich in dezelfde regio bevinden als de oorspronkelijke sleuf voor Web-App of in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="165b4-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="165b4-125">Naam van de resourcegroep met de bron-web-app weet, kunnen we de volgende PowerShell-opdracht gebruiken voor de bron web-appsite van informatie (in dit geval bron webappslot genoemd) gekoppeld aan de bron-Web-App Web-App:</span><span class="sxs-lookup"><span data-stu-id="165b4-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="165b4-126">Het volgende voorbeeld toont het maken van een kloon van de bron-web-app in een nieuwe WebApp:</span><span class="sxs-lookup"><span data-stu-id="165b4-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="165b4-127">Traffic Manager tijdens het klonen van een App configureren</span><span class="sxs-lookup"><span data-stu-id="165b4-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="165b4-128">Meerdere landen/regio-web-apps maken en configureren van Azure Traffic Manager om verkeer te routeren naar alle deze web-apps, is een n belangrijke scenario om ervoor te zorgen dat klanten apps maximaal beschikbaar zijn, wordt bij het klonen van een bestaande web-app hebt u de optie voor beide web-apps naar een traffic manager-profiel of een bestaande verbinding - die alleen Azure Resource Manager-versie van Traffic Manager wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="165b4-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="165b4-129">Een nieuw Traffic Manager-profiel maken tijdens het klonen van een App</span><span class="sxs-lookup"><span data-stu-id="165b4-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="165b4-130">Scenario: De gebruiker wil graag klonen van een web-app naar een andere regio tijdens het configureren van een Azure Resource Manager traffic manager-profiel die zijn zowel Webapps.</span><span class="sxs-lookup"><span data-stu-id="165b4-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="165b4-131">Het volgende voorbeeld toont een kloon van de bron-web-app in een nieuwe WebApp gemaakt tijdens het configureren van een nieuw Traffic Manager-profiel:</span><span class="sxs-lookup"><span data-stu-id="165b4-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="165b4-132">Toevoegen van nieuwe Web-App gekloond aan een bestaand Traffic Manager-profiel</span><span class="sxs-lookup"><span data-stu-id="165b4-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="165b4-133">Scenario: De gebruiker al een Azure Resource Manager traffic manager-profiel dat hij wil graag beide WebApps als eindpunten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="165b4-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="165b4-134">Hiervoor moeten we eerst voor het samenstellen van de bestaande traffic manager-profiel-id, moeten we de abonnements-id, de naam van resourcegroep en de bestaande profielnaam voor traffic manager.</span><span class="sxs-lookup"><span data-stu-id="165b4-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="165b4-135">Nadat ik de traffic Manager-id, het volgende voorbeeld toont een kloon van de bron-web-app in een nieuwe WebApp maakt terwijl het deze toe te voegen aan een bestaand Traffic Manager-profiel:</span><span class="sxs-lookup"><span data-stu-id="165b4-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="165b4-136">Huidige beperkingen</span><span class="sxs-lookup"><span data-stu-id="165b4-136">Current Restrictions</span></span>
<span data-ttu-id="165b4-137">Deze functie is momenteel in preview, wij werken als u wilt toevoegen van nieuwe mogelijkheden na verloop van tijd, in de volgende lijst worden de bekende beperkingen van de huidige versie van het klonen van de app:</span><span class="sxs-lookup"><span data-stu-id="165b4-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="165b4-138">Instellingen voor automatisch schalen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="165b4-139">Back-upschema instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="165b4-140">VNET-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="165b4-141">App Insights worden niet automatisch ingesteld op de doel-web-app</span><span class="sxs-lookup"><span data-stu-id="165b4-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="165b4-142">Eenvoudige verificatie-instellingen worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="165b4-143">Kudu extensie worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="165b4-144">TiP regels worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="165b4-145">Database-inhoud worden niet gekloond.</span><span class="sxs-lookup"><span data-stu-id="165b4-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="165b4-146">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="165b4-146">References</span></span>
* [<span data-ttu-id="165b4-147">PowerShell-opdrachten voor Azure-Web-App op basis van Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="165b4-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="165b4-148">Klonen van Web-App met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="165b4-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="165b4-149">Back-up van een web-app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="165b4-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="165b4-150">Azure Resource Manager-ondersteuning voor Azure Traffic Manager-Preview</span><span class="sxs-lookup"><span data-stu-id="165b4-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="165b4-151">Inleiding tot de App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="165b4-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="165b4-152">Azure PowerShell gebruiken met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="165b4-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

