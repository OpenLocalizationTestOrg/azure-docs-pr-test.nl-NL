---
title: Azure Resource Manager gebaseerde PowerShell-opdrachten voor Azure-Web-App | Microsoft Docs
description: Informatie over het gebruiken van de nieuwe Azure Resource Manager gebaseerde PowerShell-opdrachten voor het beheren van uw Azure-Web-Apps.
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a><span data-ttu-id="9a7a3-103">Azure-Web-Apps beheren met behulp van Azure Resource Manager gebaseerde PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a7a3-103">Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a7a3-104">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="9a7a3-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="9a7a3-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a7a3-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

<span data-ttu-id="9a7a3-106">Met Microsoft Azure PowerShell versie 1.0.0 zijn nieuwe opdrachten toegevoegd, die de gebruiker wilt geven op basis van Azure Resource Manager PowerShell-opdrachten gebruiken voor het beheren van Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-106">With Microsoft Azure PowerShell version 1.0.0 new commands have been added, that give the user the ability to use Azure Resource Manager-based PowerShell commands to manage Web Apps.</span></span>

<span data-ttu-id="9a7a3-107">Zie voor meer informatie over het beheren van resourcegroepen, [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9a7a3-107">To learn about managing Resource Groups, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span> 

<span data-ttu-id="9a7a3-108">Zie voor meer informatie over de volledige lijst met parameters en opties voor de PowerShell-cmdlets, de [volledige Cmdlet-verwijzing op basis van een Web App Azure Resource Manager PowerShell-Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-108">To learn about the full list of parameters and options for the PowerShell cmdlets, see the [full Cmdlet Reference of Web App Azure Resource Manager-based PowerShell Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>

## <a name="managing-app-service-plans"></a><span data-ttu-id="9a7a3-109">Het beheren van App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-109">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="9a7a3-110">Een App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="9a7a3-110">Create an App Service Plan</span></span>
<span data-ttu-id="9a7a3-111">Gebruik voor het maken van een app service-plan de **nieuw AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-111">To create an app service plan, use the **New-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9a7a3-112">Hieronder volgen beschrijvingen van de verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-112">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="9a7a3-113">**Naam**: naam van het app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-113">**Name**: name of the app service plan.</span></span>
* <span data-ttu-id="9a7a3-114">**Locatie**: service-plan locatie.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-114">**Location**: service plan location.</span></span>
* <span data-ttu-id="9a7a3-115">**ResourceGroupName**: resourcegroep met de nieuwe app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-115">**ResourceGroupName**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="9a7a3-116">**Laag**: de gewenste prijscategorie (standaardwaarde is gratis, andere opties zijn gedeeld, Basic, Standard en Premium)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-116">**Tier**:  the desired pricing tier (Default is Free, other options are Shared, Basic, Standard, and Premium.)</span></span>
* <span data-ttu-id="9a7a3-117">**WorkerSize**: de grootte van de werknemers (de standaardwaarde is klein als de parameter lagen is opgegeven als Basic, Standard of Premium.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-117">**WorkerSize**: the size of workers (Default is small if the Tier parameter was specified as Basic, Standard, or Premium.</span></span> <span data-ttu-id="9a7a3-118">Andere opties zijn Medium en Large.)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-118">Other options are Medium, and Large.)</span></span>
* <span data-ttu-id="9a7a3-119">**NumberofWorkers**: het aantal werknemers in de app service plan (de standaardwaarde is 1).</span><span class="sxs-lookup"><span data-stu-id="9a7a3-119">**NumberofWorkers**: the number of workers in the app service plan (Default value is 1).</span></span> 

<span data-ttu-id="9a7a3-120">Voorbeeld van deze cmdlet gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-120">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a><span data-ttu-id="9a7a3-121">Een App Service-abonnement maken in App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="9a7a3-121">Create an App Service Plan in an App Service Environment</span></span>
<span data-ttu-id="9a7a3-122">Gebruik dezelfde opdracht voor het maken van een app service-abonnement in een app service-omgeving, **nieuw AzureRmAppServicePlan** opdracht met extra parameters van de as-omgeving naam en de naam van de as-omgeving resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-122">To create an app service plan in an app service environment, use the same command **New-AzureRmAppServicePlan** command with extra parameters to specify the ASE's name and ASE's resource group name.</span></span>

<span data-ttu-id="9a7a3-123">Voorbeeld van deze cmdlet gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-123">Example to use this cmdlet:</span></span>

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

<span data-ttu-id="9a7a3-124">Controleer voor meer informatie over app service-omgeving, [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-124">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="9a7a3-125">Lijst met bestaande App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-125">List Existing App Service Plans</span></span>
<span data-ttu-id="9a7a3-126">U kunt de bestaande app-serviceabonnementen gebruiken **Get-AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-126">To list the existing app service plans, use **Get-AzureRmAppServicePlan** cmdlet.</span></span>

<span data-ttu-id="9a7a3-127">U kunt alle app-serviceabonnementen onder uw abonnement gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-127">To list all app service plans under your subscription, use:</span></span> 

    Get-AzureRmAppServicePlan

<span data-ttu-id="9a7a3-128">U kunt alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-128">To list all app service plans under a specific resource group, use:</span></span>

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9a7a3-129">Als u een specifieke app service-abonnement, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-129">To get a specific app service plan, use:</span></span>

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="9a7a3-130">Een bestaand App Service-Plan configureren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-130">Configure an existing App Service Plan</span></span>
<span data-ttu-id="9a7a3-131">U kunt de instellingen voor een bestaand app service-abonnement wijzigen met de **Set AzureRmAppServicePlan** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-131">To change the settings for an existing app service plan, use the **Set-AzureRmAppServicePlan** cmdlet.</span></span> <span data-ttu-id="9a7a3-132">U kunt de laag, worker grootte en het aantal werknemers wijzigen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-132">You can change the tier, worker size, and the number of workers</span></span> 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="9a7a3-133">Schalen van een App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="9a7a3-133">Scaling an App Service Plan</span></span>
<span data-ttu-id="9a7a3-134">Als u wilt schalen met een bestaand App Service Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-134">To scale an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a><span data-ttu-id="9a7a3-135">De grootte van de werknemer van een App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-135">Changing the worker size of an App Service Plan</span></span>
<span data-ttu-id="9a7a3-136">Als de grootte van de werknemers in een bestaand App Service Plan wijzigen, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-136">To change the size of workers in an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a><span data-ttu-id="9a7a3-137">De laag van een App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-137">Changing the Tier of an App Service Plan</span></span>
<span data-ttu-id="9a7a3-138">Als u wilt wijzigen van de laag van een bestaand App Service Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-138">To change the tier of an existing App Service Plan, use:</span></span>

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="9a7a3-139">Verwijder een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="9a7a3-139">Delete an existing App Service Plan</span></span>
<span data-ttu-id="9a7a3-140">Als u wilt verwijderen van een bestaand app service-abonnement, moeten alle toegewezen web-apps worden verplaatst of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-140">To delete an existing app service plan, all assigned web apps need to be moved or deleted first.</span></span> <span data-ttu-id="9a7a3-141">Klik met de **verwijderen AzureRmAppServicePlan** cmdlet kunt u het app service-abonnement verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-141">Then using the **Remove-AzureRmAppServicePlan** cmdlet you can delete the app service plan.</span></span>

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a><span data-ttu-id="9a7a3-142">App Service-Web-Apps beheren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-142">Managing App Service Web Apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="9a7a3-143">Een web-app maken</span><span class="sxs-lookup"><span data-stu-id="9a7a3-143">Create a Web App</span></span>
<span data-ttu-id="9a7a3-144">Voor het maken van een web-app gebruikt de **nieuw AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-144">To create a web app, use the **New-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9a7a3-145">Hieronder volgen beschrijvingen van de verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-145">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="9a7a3-146">**Naam**: naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-146">**Name**: name for the web app.</span></span>
* <span data-ttu-id="9a7a3-147">**AppServicePlan**: naam van de service-plan dat is gebruikt voor het hosten van de web-app.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-147">**AppServicePlan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="9a7a3-148">**ResourceGroupName**: resourcegroep die als host fungeert voor het App service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-148">**ResourceGroupName**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="9a7a3-149">**Locatie**: de locatie van web-app.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-149">**Location**: the web app location.</span></span>

<span data-ttu-id="9a7a3-150">Voorbeeld van deze cmdlet gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-150">Example to use this cmdlet:</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a><span data-ttu-id="9a7a3-151">Een Web-App maken in App Service-omgeving</span><span class="sxs-lookup"><span data-stu-id="9a7a3-151">Create a Web App in an App Service Environment</span></span>
<span data-ttu-id="9a7a3-152">Een WebApp maken in een App Service omgeving (as-omgeving).</span><span class="sxs-lookup"><span data-stu-id="9a7a3-152">To create a web app in an App Service Environment (ASE).</span></span> <span data-ttu-id="9a7a3-153">Gebruik van dezelfde **nieuw AzureRmWebApp** opdracht met extra parameters om op te geven met de naam van de as-omgeving en de resourcegroep een naam die de as-omgeving behoort.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-153">Use the same **New-AzureRmWebApp** command with extra parameters to specify the ASE name and the resource group name that the ASE belongs to.</span></span>

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

<span data-ttu-id="9a7a3-154">Controleer voor meer informatie over app service-omgeving, [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-154">To learn more about app service environment, check [Introduction to App Service Environment](app-service-app-service-environment-intro.md)</span></span>

### <a name="delete-an-existing-web-app"></a><span data-ttu-id="9a7a3-155">Een bestaande Web-App verwijderen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-155">Delete an existing Web App</span></span>
<span data-ttu-id="9a7a3-156">Verwijderen van een bestaande web-app kunt u de **verwijderen AzureRmWebApp** cmdlet, moet u de naam van de web-app en de naam van de resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-156">To delete an existing web app you can use the **Remove-AzureRmWebApp** cmdlet, you need to specify the name of the web app and the resource group name.</span></span>

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a><span data-ttu-id="9a7a3-157">Lijst met bestaande Web-Apps</span><span class="sxs-lookup"><span data-stu-id="9a7a3-157">List existing Web Apps</span></span>
<span data-ttu-id="9a7a3-158">U kunt de bestaande web-apps gebruiken de **Get-AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-158">To list the existing web apps, use the **Get-AzureRmWebApp** cmdlet.</span></span>

<span data-ttu-id="9a7a3-159">U kunt alle web-apps in uw abonnement gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-159">To list all web apps under your subscription, use:</span></span>

    Get-AzureRmWebApp

<span data-ttu-id="9a7a3-160">U kunt alle web-apps onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-160">To list all web apps under a specific resource group, use:</span></span>

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

<span data-ttu-id="9a7a3-161">Als u een specifieke web-app, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-161">To get a specific web app, use:</span></span>

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a><span data-ttu-id="9a7a3-162">Een bestaande Web-App configureren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-162">Configure an existing Web App</span></span>
<span data-ttu-id="9a7a3-163">U kunt de instellingen en configuraties voor een bestaande web-app wijzigen met de **Set AzureRmWebApp** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-163">To change the settings and configurations for an existing web app, use the **Set-AzureRmWebApp** cmdlet.</span></span> <span data-ttu-id="9a7a3-164">Controleer voor een volledige lijst met parameters, de [Cmdlet verwijzende koppeling](https://msdn.microsoft.com/library/mt652487.aspx)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-164">For a full list of parameters, check the [Cmdlet reference link](https://msdn.microsoft.com/library/mt652487.aspx)</span></span>

<span data-ttu-id="9a7a3-165">Voorbeeld (1): Gebruik deze cmdlet verbindingsreeksen wijzigen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-165">Example (1): use this cmdlet to change connection strings</span></span>

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

<span data-ttu-id="9a7a3-166">(2) voorbeeld: toevoegen of wijzigen van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-166">Example (2): add or change app settings</span></span>

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


<span data-ttu-id="9a7a3-167">(3) voorbeeld: Stel de web-app in 64-bits modus uit te voeren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-167">Example (3):  set the web app to run in 64-bit mode</span></span>

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a><span data-ttu-id="9a7a3-168">Wijzig de status van een bestaande Web-App</span><span class="sxs-lookup"><span data-stu-id="9a7a3-168">Change the state of an existing Web App</span></span>
#### <a name="restart-a-web-app"></a><span data-ttu-id="9a7a3-169">Een web-app starten</span><span class="sxs-lookup"><span data-stu-id="9a7a3-169">Restart a web app</span></span>
<span data-ttu-id="9a7a3-170">Om opnieuw te starten in een web-app, moet u de groep en de bron van de web-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-170">To restart a web app, you must specify the name and resource group of the web app.</span></span>

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a><span data-ttu-id="9a7a3-171">Een web-app stoppen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-171">Stop a web app</span></span>
<span data-ttu-id="9a7a3-172">Als u wilt stoppen met een web-app, moet u de groep en de bron van de web-app opgeven.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-172">To stop a web app, you must specify the name and resource group of the web app.</span></span>

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a><span data-ttu-id="9a7a3-173">Een web-app starten</span><span class="sxs-lookup"><span data-stu-id="9a7a3-173">Start a web app</span></span>
<span data-ttu-id="9a7a3-174">U kunt de groep en de bron van de web-app moet opgeven voor het starten van een web-app.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-174">To start a web app, you must specify the name and resource group of the web app.</span></span>

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a><span data-ttu-id="9a7a3-175">Web-App Publishing profielen beheren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-175">Manage Web App Publishing profiles</span></span>
<span data-ttu-id="9a7a3-176">Elke web-app heeft een publicatieprofiel die kan worden gebruikt voor het publiceren van uw apps en verschillende bewerkingen kunnen worden uitgevoerd op het publiceren van profielen.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-176">Each web app has a publishing profile that can be used to publish your apps, several operations can be executed on publishing profiles.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="9a7a3-177">Krijg profiel</span><span class="sxs-lookup"><span data-stu-id="9a7a3-177">Get Publishing Profile</span></span>
<span data-ttu-id="9a7a3-178">Als u het publicatieprofiel voor een web-app, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-178">To get the publishing profile for a web app, use:</span></span>

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

<span data-ttu-id="9a7a3-179">Met deze opdracht geeft het publicatieprofiel aan de opdrachtregel als goed uitvoergegevens het publicatieprofiel in een tekstbestand.</span><span class="sxs-lookup"><span data-stu-id="9a7a3-179">This command echoes the publishing profile to the command line as well output the publishing profile to a text file.</span></span>

#### <a name="reset-publishing-profile"></a><span data-ttu-id="9a7a3-180">Opnieuw instellen van profiel publiceren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-180">Reset Publishing Profile</span></span>
<span data-ttu-id="9a7a3-181">Om in te stellen op zowel het publishing wachtwoord voor FTP en web implementeren voor een web-app gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9a7a3-181">To reset both the publishing password for FTP and web deploy for a web app, use:</span></span>

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a><span data-ttu-id="9a7a3-182">Web-App certificaten beheren</span><span class="sxs-lookup"><span data-stu-id="9a7a3-182">Manage Web App Certificates</span></span>
<span data-ttu-id="9a7a3-183">Zie voor meer informatie over het beheren van certificaten voor web-app, [SSL-certificaten binding met behulp van PowerShell](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-183">To learn about how to manage web app certificates, see [SSL Certificates binding using PowerShell](app-service-web-app-powershell-ssl-binding.md)</span></span>

### <a name="next-steps"></a><span data-ttu-id="9a7a3-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9a7a3-184">Next Steps</span></span>
* <span data-ttu-id="9a7a3-185">Zie voor meer informatie over Azure Resource Manager PowerShell-ondersteuning, [Azure PowerShell gebruiken met Azure Resource Manager.](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-185">To learn about Azure Resource Manager PowerShell support, see [Using Azure PowerShell with Azure Resource Manager.](../powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="9a7a3-186">Zie voor meer informatie over App Service-omgevingen, [Inleiding tot de App Service-omgeving.](app-service-app-service-environment-intro.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-186">To learn about App Service Environments, see [Introduction to App Service Environment.](app-service-app-service-environment-intro.md)</span></span>
* <span data-ttu-id="9a7a3-187">Zie voor meer informatie over het beheren van App Service SSL-certificaten met behulp van PowerShell, [SSL-certificaten binding met behulp van PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-187">To learn about managing App Service SSL certificates using PowerShell, see [SSL Certificates binding using PowerShell.](app-service-web-app-powershell-ssl-binding.md)</span></span>
* <span data-ttu-id="9a7a3-188">Zie voor meer informatie over de volledige lijst met Azure Resource Manager gebaseerde PowerShell-cmdlets voor Azure-Web-Apps, [naslaginformatie over Azure-cmdlets van Web Apps in Azure Resource Manager PowerShell-Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-188">To learn about the full list of Azure Resource Manager-based PowerShell cmdlets for Azure Web Apps, see [Azure Cmdlet Reference of Web Apps Azure Resource Manager PowerShell Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)</span></span>
* * <span data-ttu-id="9a7a3-189">Zie voor meer informatie over het beheren van App Service met CLI, [Using Azure Resource Manager-Based XPlat CLI voor Azure-Web-App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9a7a3-189">To learn about managing App Service using CLI, see [Using Azure Resource Manager-Based XPlat CLI for Azure Web App.](app-service-web-app-azure-resource-manager-xplat-cli.md)</span></span>

