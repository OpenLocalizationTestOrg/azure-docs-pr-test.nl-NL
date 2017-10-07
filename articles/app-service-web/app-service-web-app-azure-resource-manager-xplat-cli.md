---
title: aaaAzure Resource Manager gebaseerde platformoverschrijdende opdrachtregel-hulpprogramma's voor Azure-Web-App | Microsoft Docs
description: Meer informatie over hoe toouse Hallo nieuwe hulpprogramma's voor Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel toomanage uw Azure-Web-Apps.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="496b0-103">Met behulp van Azure Resource Manager gebaseerde XPlat CLI voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="496b0-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="496b0-104">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="496b0-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="496b0-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="496b0-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="496b0-106">Hallo-versie van Microsoft Azure platformoverschrijdende opdrachtregelprogramma's versie 0.10.5, zijn nieuwe opdrachten toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="496b0-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="496b0-107">Deze opdrachten geven Hallo gebruiker Hallo mogelijkheid toouse op basis van Azure Resource Manager PowerShell-opdrachten toomanage App Service.</span><span class="sxs-lookup"><span data-stu-id="496b0-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="496b0-108">toolearn over het beheren van resourcegroepen, Zie [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="496b0-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="496b0-109">Bovendien uitproberen [Azure CLI 2.0](https://github.com/Azure/azure-cli), een volgende generatie CLI in Python is geschreven voor Hallo resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="496b0-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="496b0-110">Het beheren van App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="496b0-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="496b0-111">Een App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="496b0-111">Create an App Service Plan</span></span>
<span data-ttu-id="496b0-112">een app service-plan toocreate gebruiken Hallo **azure appserviceplan maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="496b0-113">Hieronder volgen beschrijvingen van de verschillende parameters Hallo:</span><span class="sxs-lookup"><span data-stu-id="496b0-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="496b0-114">**--resourcegroep**: bronnengroep met Hallo nieuwe app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="496b0-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="496b0-115">**--naam**: naam van het Hallo-app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="496b0-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="496b0-116">**--locatie**: app service-plan locatie.</span><span class="sxs-lookup"><span data-stu-id="496b0-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="496b0-117">**--sku**: Hallo gewenste prijscategorie sku (Hallo opties zijn: F1 (gratis).</span><span class="sxs-lookup"><span data-stu-id="496b0-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="496b0-118">D1 (gedeeld).</span><span class="sxs-lookup"><span data-stu-id="496b0-118">D1 (Shared).</span></span> <span data-ttu-id="496b0-119">B1 (Basic klein) B2 (Basic gemiddeld), en B3 (Basic grote).</span><span class="sxs-lookup"><span data-stu-id="496b0-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="496b0-120">S1 (standaard klein) S2 (standaard gemiddeld), en S3 (standaard grote).</span><span class="sxs-lookup"><span data-stu-id="496b0-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="496b0-121">P1 (klein Premium), P2 (Premium gemiddeld), en P3 (grote Premium).)</span><span class="sxs-lookup"><span data-stu-id="496b0-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="496b0-122">**--exemplaren**: aantal werknemers Hallo in Hallo-app service-abonnement (de standaardwaarde is 1).</span><span class="sxs-lookup"><span data-stu-id="496b0-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="496b0-123">Voorbeeld toouse deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="496b0-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="496b0-124">Een Linux-App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="496b0-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="496b0-125">Met behulp van dezelfde Hallo **azure appserviceplan maken** opdracht Hello extra parameter **--islinux waar**.</span><span class="sxs-lookup"><span data-stu-id="496b0-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="496b0-126">Houd er rekening mee Hallo beperkingen en regio's die worden beschreven in [inleiding tooApp-Service op Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="496b0-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="496b0-127">Lijst met bestaande App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="496b0-127">List Existing App Service Plans</span></span>
<span data-ttu-id="496b0-128">Gebruik toolist Hallo bestaande app-serviceabonnementen **azure appserviceplan lijst** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="496b0-129">toolist alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="496b0-130">gebruik van een specifieke app service-abonnement tooget **azure appserviceplan weergeven** opdracht:</span><span class="sxs-lookup"><span data-stu-id="496b0-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="496b0-131">Een bestaand App Service-Plan configureren</span><span class="sxs-lookup"><span data-stu-id="496b0-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="496b0-132">toochange Hallo-instellingen voor een bestaand app service-abonnement gebruiken Hallo **azure appserviceplan config** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="496b0-133">U kunt Hallo sku en het aantal werknemers Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="496b0-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="496b0-134">Schalen van een App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="496b0-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="496b0-135">een bestaand App Service-Plan, tooscale gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="496b0-136">Hallo SKU van een App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="496b0-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="496b0-137">toochange hello sku van een bestaande App Service-Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="496b0-138">Verwijder een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="496b0-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="496b0-139">toodelete een bestaand app service-abonnement, worden alle apps moeten toobe verplaatst of verwijderd eerst toegewezen.</span><span class="sxs-lookup"><span data-stu-id="496b0-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="496b0-140">Met behulp van Hallo **azure webapp verwijderen** opdracht kunt u Hallo-app service-abonnement verwijderen.</span><span class="sxs-lookup"><span data-stu-id="496b0-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="496b0-141">App Service-apps beheren</span><span class="sxs-lookup"><span data-stu-id="496b0-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="496b0-142">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="496b0-142">Create a web app</span></span>
<span data-ttu-id="496b0-143">een web-app toocreate gebruiken Hallo **azure webapp maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="496b0-144">Hieronder volgen beschrijvingen van de verschillende parameters Hallo:</span><span class="sxs-lookup"><span data-stu-id="496b0-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="496b0-145">**--naam**: naam in voor Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="496b0-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="496b0-146">**--plan**: Geef een naam voor service-abonnement Hallo toohost Hallo web-app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="496b0-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="496b0-147">**--resourcegroep**: resourcegroep die als host fungeert voor Hallo-App service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="496b0-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="496b0-148">**--locatie**: Hallo web-app-locatie.</span><span class="sxs-lookup"><span data-stu-id="496b0-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="496b0-149">Voorbeeld toouse deze cmdlet:</span><span class="sxs-lookup"><span data-stu-id="496b0-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="496b0-150">Verwijderen van een bestaande app</span><span class="sxs-lookup"><span data-stu-id="496b0-150">Delete an existing app</span></span>
<span data-ttu-id="496b0-151">een bestaande app toodelete, kunt u Hallo **azure webapp verwijderen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="496b0-152">Moet u toospecify Hallo-naam van Hallo-app en de naam van resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="496b0-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="496b0-153">Lijst van bestaande apps</span><span class="sxs-lookup"><span data-stu-id="496b0-153">List existing apps</span></span>
<span data-ttu-id="496b0-154">toolist hello bestaande apps, gebruikt u Hallo **azure webapp lijst** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="496b0-155">toolist gebruiken voor alle apps in een specifieke resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="496b0-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="496b0-156">een specifieke app tooget gebruiken Hallo **azure webapp weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="496b0-157">Een bestaande app configureren</span><span class="sxs-lookup"><span data-stu-id="496b0-157">Configure an existing app</span></span>
<span data-ttu-id="496b0-158">toochange hello instellingen en configuraties voor een bestaande app gebruiken Hallo **azure webapp configuratieset** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="496b0-159">(1) voorbeeld: Wijzig de Hallo php-versie van een app</span><span class="sxs-lookup"><span data-stu-id="496b0-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="496b0-160">(2) voorbeeld: toevoegen of wijzigen van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="496b0-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="496b0-161">welke andere configuratie kan worden gewijzigd, tooknow gebruik Hallo **azure webapp-config -h ingesteld** opdracht.</span><span class="sxs-lookup"><span data-stu-id="496b0-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="496b0-162">Hallo-status van een bestaande app wijzigen</span><span class="sxs-lookup"><span data-stu-id="496b0-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="496b0-163">Een app opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="496b0-163">Restart an app</span></span>
<span data-ttu-id="496b0-164">toorestart een app, moet u Hallo en de bron groep Hallo app opgeven.</span><span class="sxs-lookup"><span data-stu-id="496b0-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="496b0-165">Een app stoppen</span><span class="sxs-lookup"><span data-stu-id="496b0-165">Stop an app</span></span>
<span data-ttu-id="496b0-166">toostop een app, moet u Hallo en de bron groep Hallo app opgeven.</span><span class="sxs-lookup"><span data-stu-id="496b0-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="496b0-167">Een app te starten</span><span class="sxs-lookup"><span data-stu-id="496b0-167">Start an app</span></span>
<span data-ttu-id="496b0-168">toostart een app, moet u Hallo en de bron groep Hallo app opgeven.</span><span class="sxs-lookup"><span data-stu-id="496b0-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="496b0-169">Publicatie van een app-profielen beheren</span><span class="sxs-lookup"><span data-stu-id="496b0-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="496b0-170">Elke app heeft een publicatieprofiel die gebruikt toopublish worden kan uw code.</span><span class="sxs-lookup"><span data-stu-id="496b0-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="496b0-171">Krijg profiel</span><span class="sxs-lookup"><span data-stu-id="496b0-171">Get Publishing Profile</span></span>
<span data-ttu-id="496b0-172">tooget hello profiel voor een app, gebruik publiceren:</span><span class="sxs-lookup"><span data-stu-id="496b0-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="496b0-173">Met deze opdracht geeft Hallo publiceren profiel gebruikersnaam en wachtwoord toohello vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="496b0-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="496b0-174">App-hostnamen beheren</span><span class="sxs-lookup"><span data-stu-id="496b0-174">Manage app hostnames</span></span>
<span data-ttu-id="496b0-175">hostnaambindings toomanage voor uw app gebruiken Hallo **azure webapp config hostnamen** opdracht</span><span class="sxs-lookup"><span data-stu-id="496b0-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="496b0-176">Hostnaambindings lijst</span><span class="sxs-lookup"><span data-stu-id="496b0-176">List hostname bindings</span></span>
<span data-ttu-id="496b0-177">tooget hello huidige hostnaam bindingen voor een app gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="496b0-178">Hostnaambindings toevoegen</span><span class="sxs-lookup"><span data-stu-id="496b0-178">Add hostname bindings</span></span>
<span data-ttu-id="496b0-179">tooadd hostnaam bindingen tooan app, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="496b0-180">Hostnaambindings verwijderen</span><span class="sxs-lookup"><span data-stu-id="496b0-180">Delete hostname bindings</span></span>
<span data-ttu-id="496b0-181">hostnaambindings toodelete, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="496b0-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="496b0-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="496b0-182">Next Steps</span></span>
* <span data-ttu-id="496b0-183">Zie toolearn over de ondersteuning van Azure Resource Manager CLI [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="496b0-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="496b0-184">toolearn over het beheren van App Service met behulp van PowerShell, Zie [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="496b0-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="496b0-185">toolearn over Azure App Service op Linux, Zie [inleiding tooApp-Service op Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="496b0-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
