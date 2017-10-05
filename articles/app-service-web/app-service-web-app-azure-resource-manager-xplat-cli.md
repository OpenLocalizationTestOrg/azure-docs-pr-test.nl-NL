---
title: Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel-hulpprogramma's voor Azure Web-App | Microsoft Docs
description: Informatie over het gebruik van de nieuwe Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel hulpmiddelen voor het beheren van uw Azure-Web-Apps.
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="1c5b5-103">Met behulp van Azure Resource Manager gebaseerde XPlat CLI voor Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1c5b5-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c5b5-104">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="1c5b5-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="1c5b5-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c5b5-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="1c5b5-106">Met de release van Microsoft Azure platformoverschrijdende opdrachtregelprogramma's versie 0.10.5 zijn nieuwe opdrachten toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-106">With the release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="1c5b5-107">Deze opdrachten krijgt de gebruiker de mogelijkheid om te gebruiken op basis van Azure Resource Manager PowerShell-opdrachten voor het beheren van App Service.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-107">These commands give the user the ability to use Azure Resource Manager-based PowerShell commands to manage App Service.</span></span>

<span data-ttu-id="1c5b5-108">Zie voor meer informatie over het beheren van resourcegroepen, [de Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-108">To learn about managing Resource Groups, see [Use the Azure CLI to manage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="1c5b5-109">Bovendien uitproberen [Azure CLI 2.0](https://github.com/Azure/azure-cli), een volgende generatie CLI in Python is geschreven voor de resource management-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for the resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="1c5b5-110">Het beheren van App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="1c5b5-111">Een App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1c5b5-111">Create an App Service Plan</span></span>
<span data-ttu-id="1c5b5-112">Gebruik voor het maken van een app service-plan de **azure appserviceplan maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-112">To create an app service plan, use the **azure appserviceplan create** command.</span></span>

<span data-ttu-id="1c5b5-113">Hieronder volgen beschrijvingen van de verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-113">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="1c5b5-114">**--resourcegroep**: resourcegroep met de nieuwe app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-114">**--resource-group**: resource group that includes the newly created app service plan.</span></span>
* <span data-ttu-id="1c5b5-115">**--naam**: naam van het app service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-115">**--name**: name of the app service plan.</span></span>
* <span data-ttu-id="1c5b5-116">**--locatie**: app service-plan locatie.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="1c5b5-117">**--sku**: de gewenste prijscategorie sku (de opties zijn: F1 (gratis).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-117">**--sku**:  the desired pricing sku (The options are: F1 (Free).</span></span> <span data-ttu-id="1c5b5-118">D1 (gedeeld).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-118">D1 (Shared).</span></span> <span data-ttu-id="1c5b5-119">B1 (Basic klein) B2 (Basic gemiddeld), en B3 (Basic grote).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="1c5b5-120">S1 (standaard klein) S2 (standaard gemiddeld), en S3 (standaard grote).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="1c5b5-121">P1 (klein Premium), P2 (Premium gemiddeld), en P3 (grote Premium).)</span><span class="sxs-lookup"><span data-stu-id="1c5b5-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="1c5b5-122">**--exemplaren**: het aantal werknemers in de app service plan (de standaardwaarde is 1).</span><span class="sxs-lookup"><span data-stu-id="1c5b5-122">**--instances**: the number of workers in the app service plan (Default value is 1).</span></span>

<span data-ttu-id="1c5b5-123">Voorbeeld van deze cmdlet gebruikt:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-123">Example to use this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="1c5b5-124">Een Linux-App Service-abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1c5b5-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="1c5b5-125">Met behulp van dezelfde **azure appserviceplan maken** opdracht met de extra parameter **--islinux waar**.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-125">Using the same **azure appserviceplan create** command, with the extra parameter **--islinux true**.</span></span> <span data-ttu-id="1c5b5-126">Noteer de beperkingen en regio's die worden beschreven in [Inleiding tot op Linux-App Service](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1c5b5-126">Note the restrictions and regions outlined in [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="1c5b5-127">Lijst met bestaande App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-127">List Existing App Service Plans</span></span>
<span data-ttu-id="1c5b5-128">U kunt de bestaande app-serviceabonnementen gebruiken **azure appserviceplan lijst** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-128">To list the existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="1c5b5-129">U kunt alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-129">To list all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="1c5b5-130">Als u een specifieke app service-abonnement, gebruikt **azure appserviceplan weergeven** opdracht:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-130">To get a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="1c5b5-131">Een bestaand App Service-Plan configureren</span><span class="sxs-lookup"><span data-stu-id="1c5b5-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="1c5b5-132">U kunt de instellingen voor een bestaand app service-abonnement wijzigen met de **azure appserviceplan config** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-132">To change the settings for an existing app service plan, use the **azure appserviceplan config** command.</span></span> <span data-ttu-id="1c5b5-133">U kunt de sku, en het aantal werknemers wijzigen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-133">You can change the sku, and the number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="1c5b5-134">Schalen van een App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="1c5b5-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="1c5b5-135">Als u wilt schalen met een bestaand App Service Plan, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-135">To scale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a><span data-ttu-id="1c5b5-136">De SKU van een App Service-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-136">Changing the SKU of an App Service Plan</span></span>
<span data-ttu-id="1c5b5-137">De sku van een bestaand App Service Plan met kunt u wijzigen:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-137">To change the sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="1c5b5-138">Verwijder een bestaande App Service-Plan</span><span class="sxs-lookup"><span data-stu-id="1c5b5-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="1c5b5-139">Als u wilt verwijderen van een bestaand app service-abonnement, moeten alle toegewezen apps worden verplaatst of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-139">To delete an existing app service plan, all assigned apps need to be moved or deleted first.</span></span> <span data-ttu-id="1c5b5-140">Klik met de **azure webapp verwijderen** opdracht kunt u het app service-abonnement verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-140">Then using the **azure webapp delete** command you can delete the app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="1c5b5-141">App Service-apps beheren</span><span class="sxs-lookup"><span data-stu-id="1c5b5-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="1c5b5-142">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="1c5b5-142">Create a web app</span></span>
<span data-ttu-id="1c5b5-143">Voor het maken van een web-app gebruikt de **azure webapp maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-143">To create a web app, use the **azure webapp create** command.</span></span>

<span data-ttu-id="1c5b5-144">Hieronder volgen beschrijvingen van de verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-144">Following are descriptions of the different parameters:</span></span>

* <span data-ttu-id="1c5b5-145">**--naam**: naam in voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-145">**--name**: name for the web app.</span></span>
* <span data-ttu-id="1c5b5-146">**--plan**: naam van de service-plan dat is gebruikt voor het hosten van de web-app.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-146">**--plan**: name for the service plan used to host the web app.</span></span>
* <span data-ttu-id="1c5b5-147">**--resourcegroep**: resourcegroep die als host fungeert voor het App service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-147">**--resource-group**: resource group that hosts the App service plan.</span></span>
* <span data-ttu-id="1c5b5-148">**--locatie**: de locatie van web-app.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-148">**--location**: the web app location.</span></span>

<span data-ttu-id="1c5b5-149">Voorbeeld van deze cmdlet gebruikt:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-149">Example to use this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="1c5b5-150">Verwijderen van een bestaande app</span><span class="sxs-lookup"><span data-stu-id="1c5b5-150">Delete an existing app</span></span>
<span data-ttu-id="1c5b5-151">Als u wilt verwijderen van een bestaande app, kunt u de **azure webapp verwijderen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-151">To delete an existing app, you can use the **azure webapp delete** command.</span></span> <span data-ttu-id="1c5b5-152">U moet de naam van de app en de naam van de resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-152">You need to specify the name of the app and the resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="1c5b5-153">Lijst van bestaande apps</span><span class="sxs-lookup"><span data-stu-id="1c5b5-153">List existing apps</span></span>
<span data-ttu-id="1c5b5-154">U kunt de bestaande apps gebruiken de **azure webapp lijst** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-154">To list the existing apps, use the **azure webapp list** command.</span></span>

<span data-ttu-id="1c5b5-155">U kunt alle apps in een specifieke resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-155">To list all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="1c5b5-156">Als u een specifieke app, gebruikt de **azure webapp weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-156">To get a specific app, use the **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="1c5b5-157">Een bestaande app configureren</span><span class="sxs-lookup"><span data-stu-id="1c5b5-157">Configure an existing app</span></span>
<span data-ttu-id="1c5b5-158">U kunt de instellingen en configuraties voor een bestaande app wijzigen met de **azure webapp configuratieset** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-158">To change the settings and configurations for an existing app, use the **azure webapp config set** command.</span></span>

<span data-ttu-id="1c5b5-159">(1) voorbeeld: Wijzig de php-versie van een app</span><span class="sxs-lookup"><span data-stu-id="1c5b5-159">Example (1): change the php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="1c5b5-160">(2) voorbeeld: toevoegen of wijzigen van app-instellingen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="1c5b5-161">Weten wat andere configuratie kan worden gewijzigd, gebruikt u de **azure webapp-config -h ingesteld** opdracht.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-161">To know what other configuration can be changed, use the **azure webapp config set -h** command.</span></span>

### <a name="change-the-state-of-an-existing-app"></a><span data-ttu-id="1c5b5-162">De status van een bestaande app wijzigen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-162">Change the state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="1c5b5-163">Een app opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="1c5b5-163">Restart an app</span></span>
<span data-ttu-id="1c5b5-164">Als u wilt een app opnieuw is opgestart, moet u de groep en de bron van de app opgeven.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-164">To restart an app, you must specify the name and resource group of the app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="1c5b5-165">Een app stoppen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-165">Stop an app</span></span>
<span data-ttu-id="1c5b5-166">Als u wilt stoppen van een app, moet u de groep en de bron van de app opgeven.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-166">To stop an app, you must specify the name and resource group of the app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="1c5b5-167">Een app te starten</span><span class="sxs-lookup"><span data-stu-id="1c5b5-167">Start an app</span></span>
<span data-ttu-id="1c5b5-168">Als u wilt een app, moet u de groep en de bron van de app opgeven.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-168">To start an app, you must specify the name and resource group of the app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="1c5b5-169">Publicatie van een app-profielen beheren</span><span class="sxs-lookup"><span data-stu-id="1c5b5-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="1c5b5-170">Elke app heeft een publicatieprofiel die kan worden gebruikt voor het publiceren van uw code.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-170">Each app has a publishing profile that can be used to publish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="1c5b5-171">Krijg profiel</span><span class="sxs-lookup"><span data-stu-id="1c5b5-171">Get Publishing Profile</span></span>
<span data-ttu-id="1c5b5-172">Als u het publicatieprofiel voor een app, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-172">To get the publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="1c5b5-173">Met deze opdracht geeft publishing profiel gebruikersnaam en wachtwoord voor de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="1c5b5-173">This command echoes the publishing profile username and password to the command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="1c5b5-174">App-hostnamen beheren</span><span class="sxs-lookup"><span data-stu-id="1c5b5-174">Manage app hostnames</span></span>
<span data-ttu-id="1c5b5-175">Voor het beheren van hostnaambindings voor uw app gebruikt de **azure webapp config hostnamen** opdracht</span><span class="sxs-lookup"><span data-stu-id="1c5b5-175">To manage hostname bindings for your app, use the **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="1c5b5-176">Hostnaambindings lijst</span><span class="sxs-lookup"><span data-stu-id="1c5b5-176">List hostname bindings</span></span>
<span data-ttu-id="1c5b5-177">Als u de huidige hostnaambindings voor een app, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-177">To get the current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="1c5b5-178">Hostnaambindings toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-178">Add hostname bindings</span></span>
<span data-ttu-id="1c5b5-179">Hostnaambindings toevoegen aan een app, als u wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-179">To add hostname bindings to an app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="1c5b5-180">Hostnaambindings verwijderen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-180">Delete hostname bindings</span></span>
<span data-ttu-id="1c5b5-181">Als u wilt verwijderen hostnaambindings, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="1c5b5-181">To delete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="1c5b5-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c5b5-182">Next Steps</span></span>
* <span data-ttu-id="1c5b5-183">Zie voor meer informatie over de ondersteuning van Azure Resource Manager CLI, [de Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="1c5b5-183">To learn about Azure Resource Manager CLI support, see [Use the Azure CLI to manage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="1c5b5-184">Zie voor meer informatie over het beheren van App Service met behulp van PowerShell, [Using Azure Resource Manager-Based PowerShell voor Azure-Web-Apps beheren.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1c5b5-184">To learn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="1c5b5-185">Zie voor meer informatie over Azure App Service op Linux, [Inleiding tot op Linux-App Service](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="1c5b5-185">To learn about Azure App Service on Linux, see [Introduction to App Service on Linux](app-service-linux-intro.md)</span></span>
