---
title: aaaAzure op basis van een Resource Manager PowerShell-opdrachten voor Azure-Web-App | Microsoft Docs
description: Meer informatie over hoe toouse Hallo nieuwe Azure Resource Manager gebaseerde PowerShell-opdrachten toomanage uw Azure-Web-Apps.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a><span data-ttu-id="bf629-103">Met behulp van PowerShell Azure Resource Manager-Based tooManage Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="bf629-103">Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf629-104">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="bf629-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="bf629-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf629-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="bf629-106">Met Microsoft Azure PowerShell versie 1.0.0 zijn nieuwe opdrachten toegevoegd, die geven Hallo gebruiker Hallo mogelijkheid toouse op basis van Azure Resource Manager PowerShell-opdrachten toomanage Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="bf629-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage Web Apps.</span></span>

<span data-ttu-id="bf629-107">toolearn over het beheren van resourcegroepen, Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bf629-107">toolearn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="bf629-108">toolearn over Hallo volledige lijst met parameters en opties voor Hallo PowerShell-cmdlets, Zie Hallo [volledige Cmdlet-verwijzing op basis van een Web App Azure Resource Manager PowerShell-Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf629-108">toolearn about hello full list of parameters and options for hello PowerShell cmdlets, see hello [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="bf629-109">Het beheren van App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="bf629-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="bf629-110">Een App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="bf629-110">Create an App Service Plan</span></span>
<span data-ttu-id="bf629-111">een app service-plan toocreate gebruiken Hallo **nieuw AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-111">toocreate an app service plan, use hello **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="bf629-112">Hieronder volgen beschrijvingen van de verschillende parameters Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf629-112">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="bf629-113">**Naam**: naam van het Hallo-app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf629-113">**Name**: name of hello app service plan.</span></span>
* <span data-ttu-id="bf629-114">**Locatie**: service-plan locatie.</span><span class="sxs-lookup"><span data-stu-id="bf629-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="bf629-115">**ResourceGroupName**: bronnengroep met Hallo nieuwe app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf629-115">**ResourceGroupName**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="bf629-116">**Laag**: Hallo gewenste prijscategorie (standaardwaarde is gratis, andere opties zijn gedeeld, Basic, Standard en Premium)</span><span class="sxs-lookup"><span data-stu-id="bf629-116">**Tier**:  hello desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="bf629-117">**WorkerSize**: Hallo grootte van de werknemers (de standaardwaarde is klein als Hallo laag parameter is opgegeven als Basic, Standard of Premium.</span><span class="sxs-lookup"><span data-stu-id="bf629-117">**WorkerSize**: hello size of workers (Default is small if hello Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="bf629-118">Andere opties zijn Medium en Large.)</span><span class="sxs-lookup"><span data-stu-id="bf629-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="bf629-119">**NumberofWorkers**: aantal werknemers Hallo in Hallo-app service-abonnement (de standaardwaarde is 1).</span><span class="sxs-lookup"><span data-stu-id="bf629-119">**NumberofWorkers**: hello number of workers in hello app service plan (Default value is 1).</span></span> 

<span data-ttu-id="bf629-120">Voorbeeld toouse deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bf629-120">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="bf629-121">Een App Service-abonnement maken in App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="bf629-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="bf629-122">toocreate van een app service plan bent in een app service-omgeving, gebruik Hallo dezelfde opdracht **nieuw AzureRmAppServicePlan** opdracht met de naam van de extra parameters toospecify Hallo van as-omgeving en de naam van de as-omgeving resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bf629-122">toocreate an app service plan in an app service environment, use hello same command **New-AzureRmAppServicePlan** command with extra parameters toospecify hello ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="bf629-123">Voorbeeld toouse deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bf629-123">Example toouse this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="bf629-124">meer informatie over app service-omgeving, selectievakje toolearn [inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-124">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="bf629-125">Lijst met bestaande App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="bf629-125">List Existing App Service Plans</span></span>
<span data-ttu-id="bf629-126">Gebruik toolist Hallo bestaande app-serviceabonnementen **Get-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-126">toolist hello existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="bf629-127">toolist gebruiken voor alle app-serviceabonnementen onder uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="bf629-127">toolist all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="bf629-128">toolist alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-128">toolist all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="bf629-129">tooget een specifieke app service-abonnement gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-129">tooget a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="bf629-130">Een bestaand App Service-Plan configureren</span><span class="sxs-lookup"><span data-stu-id="bf629-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="bf629-131">toochange Hallo-instellingen voor een bestaand app service-abonnement gebruiken Hallo **Set AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-131">toochange hello settings for an existing app service plan, use hello **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="bf629-132">U kunt Hallo laag, de grootte van de werknemer en Hallo aantal werknemers wijzigen</span><span class="sxs-lookup"><span data-stu-id="bf629-132">You can change hello tier, worker size, and hello number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="bf629-133">Schalen van een App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="bf629-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="bf629-134">een bestaand App Service-Plan, tooscale gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-134">tooscale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a><span data-ttu-id="bf629-135">Hallo worker grootte wijzigen van een App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="bf629-135">Changing hello worker size of an App Service Plan</span></span>
<span data-ttu-id="bf629-136">toochange hello grootte van de werknemers in een bestaand App Service-Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-136">toochange hello size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a><span data-ttu-id="bf629-137">Hallo laag van een App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="bf629-137">Changing hello Tier of an App Service Plan</span></span>
<span data-ttu-id="bf629-138">toochange hello laag van een bestaande App Service-Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-138">toochange hello tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="bf629-139">Verwijder een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="bf629-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="bf629-140">een bestaand app service-abonnement toodelete, worden alle web-apps nodig toobe verplaatst of verwijderd eerst toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bf629-140">toodelete an existing app service plan, all assigned web apps need toobe moved or deleted first.</span></span> <span data-ttu-id="bf629-141">Met behulp van Hallo **verwijderen AzureRmAppServicePlan** cmdlet kunt u Hallo-app service-abonnement verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bf629-141">Then using hello **Remove-AzureRmAppServicePlan** cmdlet you can delete hello app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="bf629-142">App Service-Web-Apps beheren</span><span class="sxs-lookup"><span data-stu-id="bf629-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="bf629-143">Een web-app maken</span><span class="sxs-lookup"><span data-stu-id="bf629-143">Create a Web App</span></span>
<span data-ttu-id="bf629-144">een web-app toocreate gebruiken Hallo **nieuw AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-144">toocreate a web app, use hello **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="bf629-145">Hieronder volgen beschrijvingen van de verschillende parameters Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf629-145">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="bf629-146">**Naam**: naam in voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="bf629-146">**Name**: name for hello web app.</span></span>
* <span data-ttu-id="bf629-147">**AppServicePlan**: Geef een naam voor service-abonnement Hallo toohost Hallo web-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bf629-147">**AppServicePlan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="bf629-148">**ResourceGroupName**: resourcegroep die als host fungeert voor Hallo-App service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bf629-148">**ResourceGroupName**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="bf629-149">**Locatie**: Hallo web-app-locatie.</span><span class="sxs-lookup"><span data-stu-id="bf629-149">**Location**: hello web app location.</span></span>

<span data-ttu-id="bf629-150">Voorbeeld toouse deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bf629-150">Example toouse this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="bf629-151">Een Web-App maken in App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="bf629-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="bf629-152">toocreate een web-app in een App Service omgeving (as-omgeving).</span><span class="sxs-lookup"><span data-stu-id="bf629-152">toocreate a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="bf629-153">Gebruik dezelfde Hallo **nieuw AzureRmWebApp** opdracht met extra parameters toospecify Hallo as-omgeving naam en Hallo Resourcegroepnaam behorend Hallo as-omgeving.</span><span class="sxs-lookup"><span data-stu-id="bf629-153">Use hello same **New-AzureRmWebApp** command with extra parameters toospecify hello ASE name and hello resource group name that hello ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="bf629-154">meer informatie over app service-omgeving, selectievakje toolearn [inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-154">toolearn more about app service environment, check [Introduction tooApp Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="bf629-155">Een bestaande Web-App verwijderen</span><span class="sxs-lookup"><span data-stu-id="bf629-155">Delete an existing Web App</span></span>
<span data-ttu-id="bf629-156">een bestaande web-app kunt u Hallo toodelete **verwijderen AzureRmWebApp** cmdlet, moet u toospecify Hallo naam van Hallo web-app en de naam van resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf629-156">toodelete an existing web app you can use hello **Remove-AzureRmWebApp** cmdlet, you need toospecify hello name of hello web app and hello resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="bf629-157">Lijst met bestaande Web-Apps</span><span class="sxs-lookup"><span data-stu-id="bf629-157">List existing Web Apps</span></span>
<span data-ttu-id="bf629-158">toolist hello bestaande WebApps gebruiken Hallo **Get-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-158">toolist hello existing web apps, use hello **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="bf629-159">toolist gebruiken voor alle web-apps in uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="bf629-159">toolist all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="bf629-160">toolist alle web-apps onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-160">toolist all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="bf629-161">tooget een specifieke web-app gebruiken:</span><span class="sxs-lookup"><span data-stu-id="bf629-161">tooget a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="bf629-162">Een bestaande Web-App configureren</span><span class="sxs-lookup"><span data-stu-id="bf629-162">Configure an existing Web App</span></span>
<span data-ttu-id="bf629-163">toochange hello instellingen en configuraties voor een bestaande web-app gebruiken Hallo **Set AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf629-163">toochange hello settings and configurations for an existing web app, use hello **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="bf629-164">Controleer voor een volledige lijst met parameters Hallo [Cmdlet verwijzende koppeling](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf629-164">For a full list of parameters, check hello [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="bf629-165">Voorbeeld (1): Gebruik deze cmdlet toochange-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="bf629-165">Example (1): use this cmdlet toochange connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="bf629-166">(2) voorbeeld: toevoegen of wijzigen van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="bf629-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="bf629-167">(3) voorbeeld: Hallo web app toorun in 64-bits modus instellen</span><span class="sxs-lookup"><span data-stu-id="bf629-167">Example (3):  set hello web app toorun in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a><span data-ttu-id="bf629-168">Hallo-status van een bestaande Web-App wijzigen</span><span class="sxs-lookup"><span data-stu-id="bf629-168">Change hello state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="bf629-169">Een web-app starten</span><span class="sxs-lookup"><span data-stu-id="bf629-169">Restart a web app</span></span>
<span data-ttu-id="bf629-170">toorestart een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf629-170">toorestart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="bf629-171">Een web-app stoppen</span><span class="sxs-lookup"><span data-stu-id="bf629-171">Stop a web app</span></span>
<span data-ttu-id="bf629-172">toostop een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf629-172">toostop a web app, you must specify hello name and resource group of hello web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="bf629-173">Een web-app starten</span><span class="sxs-lookup"><span data-stu-id="bf629-173">Start a web app</span></span>
<span data-ttu-id="bf629-174">toostart een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf629-174">toostart a web app, you must specify hello name and resource group of hello web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="bf629-175">Web-App Publishing profielen beheren</span><span class="sxs-lookup"><span data-stu-id="bf629-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="bf629-176">Elke web-app heeft een publicatieprofiel die gebruikt toopublish worden kan uw apps en verschillende bewerkingen kunnen worden uitgevoerd op het publiceren van profielen.</span><span class="sxs-lookup"><span data-stu-id="bf629-176">Each web app has a publishing profile that can be used toopublish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="bf629-177">Krijg profiel</span><span class="sxs-lookup"><span data-stu-id="bf629-177">Get Publishing Profile</span></span>
<span data-ttu-id="bf629-178">tooget hello profiel voor een web-app, gebruik publiceren:</span><span class="sxs-lookup"><span data-stu-id="bf629-178">tooget hello publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="bf629-179">Met deze opdracht geeft Hallo profiel toohello opdrachtregel ook publiceren uitvoer Hallo profiel tooa tekstbestand publiceren.</span><span class="sxs-lookup"><span data-stu-id="bf629-179">This command echoes hello publishing profile toohello command line as well output hello publishing profile tooa text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="bf629-180">Opnieuw instellen van profiel publiceren</span><span class="sxs-lookup"><span data-stu-id="bf629-180">Reset Publishing Profile</span></span>
<span data-ttu-id="bf629-181">tooreset beide publishing wachtwoord Hallo voor FTP en web implementeren voor een web-app gebruikt:</span><span class="sxs-lookup"><span data-stu-id="bf629-181">tooreset both hello publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="bf629-182">Web-App certificaten beheren</span><span class="sxs-lookup"><span data-stu-id="bf629-182">Manage Web App Certificates</span></span>
<span data-ttu-id="bf629-183">toolearn over hoe toomanage web-app-certificaten, Zie [SSL-certificaten binding met behulp van PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-183">toolearn about how toomanage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="bf629-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf629-184">Next Steps</span></span>
* <span data-ttu-id="bf629-185">toolearn over Azure Resource Manager PowerShell-ondersteuning, Zie [Azure PowerShell gebruiken met Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-185">toolearn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="bf629-186">toolearn over App Service-omgevingen, Zie [inleiding tooApp Service-omgeving.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-186">toolearn about App Service Environments, see [Introduction tooApp Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="bf629-187">toolearn over het beheren van App Service SSL-certificaten met behulp van PowerShell, Zie [SSL-certificaten binding met behulp van PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-187">toolearn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="bf629-188">toolearn over Hallo volledige lijst met Azure Resource Manager gebaseerde PowerShell-cmdlets voor Azure Web Apps, Zie [naslaginformatie over Azure-cmdlets van Web Apps in Azure Resource Manager PowerShell-Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf629-188">toolearn about hello full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="bf629-189">toolearn over het beheren van App Service met CLI, Zie [Using Azure Resource Manager-Based XPlat CLI voor Azure-Web-App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bf629-189">toolearn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

