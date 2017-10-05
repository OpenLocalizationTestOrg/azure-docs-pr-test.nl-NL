---
title: Migreren naar Resource Manager met PowerShell | Microsoft Docs
description: Dit artikel helpt bij de migratie platform ondersteund van IaaS-resources, zoals virtuele machines (VM's), virtuele netwerken (vnet's) en storage-accounts van klassiek naar Azure Resource Manager (ARM) met behulp van Azure PowerShell-opdrachten
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 489e6cc6bd3c5b36635f5f7e398d08fed681d2e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="ee771-103">Migreren IaaS-middelen van klassiek naar Azure Resource Manager met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee771-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="ee771-104">Deze stappen ziet u hoe u Azure PowerShell-opdrachten voor het migreren van infrastructuur als een dienst (IaaS) resources van het klassieke implementatiemodel naar het Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ee771-104">These steps show you how to use Azure PowerShell commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ee771-105">Als u wilt, kunt u ook resources migreren met behulp van de [Azure-opdrachtregelinterface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee771-105">If you want, you can also migrate resources by using the [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="ee771-106">Zie voor achtergrondinformatie over ondersteunde migratiescenario's [Platform ondersteund migratie van IaaS-middelen van klassiek naar Azure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee771-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic to Azure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="ee771-107">Zie voor gedetailleerde instructies en een overzicht van migratie [technische deep dive op platform ondersteund migratie van klassiek naar Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="ee771-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic to Azure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="ee771-108">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="ee771-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="ee771-109">Hier volgt een stroomdiagram voor het identificeren van de volgorde waarin stappen moeten worden uitgevoerd tijdens een migratie</span><span class="sxs-lookup"><span data-stu-id="ee771-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Schermafbeelding van de migratiestappen](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="ee771-111">Stap 1: Plannen voor migratie</span><span class="sxs-lookup"><span data-stu-id="ee771-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="ee771-112">Hier volgen enkele aanbevolen procedures die wij adviseren kijkt u bij het evalueren van IaaS Resourcemigratie van klassiek naar Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="ee771-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="ee771-113">Lees de [ondersteunde en niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee771-113">Read through the [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="ee771-114">Als u virtuele machines die gebruikmaken van niet-ondersteunde configuraties of functies hebt, raden wij u voor ondersteuning van de configuratie of onderdeel worden aangekondigd.</span><span class="sxs-lookup"><span data-stu-id="ee771-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the configuration/feature support to be announced.</span></span> <span data-ttu-id="ee771-115">Ook als deze aan uw behoeften voldoet, verwijdert u deze functie of dat de configuratie om in te schakelen migratie verlaten.</span><span class="sxs-lookup"><span data-stu-id="ee771-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration to enable migration.</span></span>
* <span data-ttu-id="ee771-116">Als u scripts die uw infrastructuur en toepassingen vandaag implementeert geautomatiseerde, kunt u een vergelijkbare test-instellingen te maken met behulp van deze scripts voor de migratie.</span><span class="sxs-lookup"><span data-stu-id="ee771-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="ee771-117">U kunt ook de voorbeeld-omgevingen instellen met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee771-118">Toepassingsgateways worden momenteel niet ondersteund voor migratie van klassiek naar Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee771-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="ee771-119">Verwijder de gateway voordat u een voorbereidingsbewerking voor het verplaatsen van het netwerk voor het migreren van een klassiek virtueel netwerk met een Application gateway.</span><span class="sxs-lookup"><span data-stu-id="ee771-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="ee771-120">Nadat u de migratie hebt voltooid, sluit u de gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee771-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="ee771-121">ExpressRoute-gateways die verbinding maken met ExpressRoute-circuits in een ander abonnement kunnen niet automatisch worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="ee771-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="ee771-122">In dergelijke gevallen verwijderen van de ExpressRoute-gateway, migreren van het virtuele netwerk en de gateway opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="ee771-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="ee771-123">Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken van het klassieke naar het Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ee771-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="ee771-124">Stap 2: Installeer de nieuwste versie van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee771-124">Step 2: Install the latest version of Azure PowerShell</span></span>
<span data-ttu-id="ee771-125">Er zijn twee manieren Azure PowerShell te installeren: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) of [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="ee771-125">There are two main options to install Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="ee771-126">WebPI ontvangt maandelijkse updates.</span><span class="sxs-lookup"><span data-stu-id="ee771-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="ee771-127">PowerShell Gallery ontvangt updates doorlopend.</span><span class="sxs-lookup"><span data-stu-id="ee771-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="ee771-128">In dit artikel is gebaseerd op Azure PowerShell versie 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="ee771-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="ee771-129">Zie voor installatie-instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee771-129">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-the-subscription-in-azure-portal"></a><span data-ttu-id="ee771-130">Stap 3: Zorg ervoor dat u een beheerder zijn voor het abonnement in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ee771-130">Step 3: Ensure that you are an administrator for the subscription in Azure portal</span></span>
<span data-ttu-id="ee771-131">Om deze te migreren, moet u toegevoegd als medebeheerder voor het abonnement op de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee771-131">To perform this migration, you must be added as a co-administrator for the subscription in the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="ee771-132">Meld u aan bij de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee771-132">Sign into the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ee771-133">Selecteer in het menu Hub **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ee771-133">On the Hub menu, select **Subscription**.</span></span> <span data-ttu-id="ee771-134">Als u deze niet ziet, selecteert u **meer services**.</span><span class="sxs-lookup"><span data-stu-id="ee771-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="ee771-135">De abonnementvermelding in het juiste vinden en bekijk de **mijn rol** veld.</span><span class="sxs-lookup"><span data-stu-id="ee771-135">Find the appropriate subscription entry, then look at the **MY ROLE** field.</span></span> <span data-ttu-id="ee771-136">Voor een medebeheerder de waarde moet _accountbeheerder_.</span><span class="sxs-lookup"><span data-stu-id="ee771-136">For a co-administrator, the value should be _Account admin_.</span></span>

<span data-ttu-id="ee771-137">Als u niet kunt toevoegen van een CO-beheerder bent, klikt u vervolgens contact op met een servicebeheerder of CO-beheerder voor het abonnement om uzelf toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ee771-137">If you are not able to add a co-administrator, then contact a service administrator or co-administrator for the subscription to get yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="ee771-138">Stap 4: Stel uw abonnement en aanmelden voor migratie</span><span class="sxs-lookup"><span data-stu-id="ee771-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="ee771-139">Eerst een PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="ee771-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="ee771-140">Voor de migratie, moet u uw omgeving voor zowel klassieke instellen en Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee771-140">For migration, you need to set up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="ee771-141">Aanmelden bij uw account voor het Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="ee771-141">Sign in to your account for the Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="ee771-142">De beschikbare abonnementen ophalen met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-142">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="ee771-143">Stel uw Azure-abonnement voor de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="ee771-143">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="ee771-144">In het volgende voorbeeld wordt de standaardnaam voor het abonnement op **mijn Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ee771-144">This example sets the default subscription name to **My Azure Subscription**.</span></span> <span data-ttu-id="ee771-145">De naam van het abonnement voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ee771-145">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="ee771-146">Registratie is een eenmalige stap, maar u moet dit doen eenmaal voordat u de migratie.</span><span class="sxs-lookup"><span data-stu-id="ee771-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="ee771-147">Zonder te registreren ziet u het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ee771-147">Without registering, you see the following error message:</span></span>
>
> <span data-ttu-id="ee771-148">*BadRequest: Abonnement is niet geregistreerd voor migratie.*</span><span class="sxs-lookup"><span data-stu-id="ee771-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="ee771-149">Registreren bij de resourceprovider voor migratie met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-149">Register with the migration resource provider by using the following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="ee771-150">Wacht vijf minuten om de registratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ee771-150">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="ee771-151">U kunt de status van de goedkeuring controleren met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-151">You can check the status of the approval by using the following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="ee771-152">Zorg ervoor dat RegistrationState `Registered` voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="ee771-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="ee771-153">Nu aanmelden bij uw account voor het klassieke model.</span><span class="sxs-lookup"><span data-stu-id="ee771-153">Now sign in to your account for the classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="ee771-154">De beschikbare abonnementen ophalen met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-154">Get the available subscriptions by using the following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="ee771-155">Stel uw Azure-abonnement voor de huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="ee771-155">Set your Azure subscription for the current session.</span></span> <span data-ttu-id="ee771-156">In dit voorbeeld wordt het standaardabonnement ingesteld op **mijn Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ee771-156">This example sets the default subscription to **My Azure Subscription**.</span></span> <span data-ttu-id="ee771-157">De naam van het abonnement voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ee771-157">Replace the example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="ee771-158">Stap 5: Controleer of er voldoende kernen virtuele Machine van Azure Resource Manager in Azure-regio van uw huidige implementatie of VNET</span><span class="sxs-lookup"><span data-stu-id="ee771-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="ee771-159">U kunt de volgende PowerShell-opdracht gebruiken om te controleren van het huidige aantal kernen dat u in Azure Resource Manager hebt.</span><span class="sxs-lookup"><span data-stu-id="ee771-159">You can use the following PowerShell command to check the current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="ee771-160">Zie voor meer informatie over quota core, [limieten en de Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="ee771-160">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="ee771-161">In dit voorbeeld controleert de beschikbaarheid de **VS-West** regio.</span><span class="sxs-lookup"><span data-stu-id="ee771-161">This example checks the availability in the **West US** region.</span></span> <span data-ttu-id="ee771-162">De regionaam voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ee771-162">Replace the example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-to-migrate-your-iaas-resources"></a><span data-ttu-id="ee771-163">Stap 6: Voer de opdrachten voor het migreren van uw IaaS-resources</span><span class="sxs-lookup"><span data-stu-id="ee771-163">Step 6: Run commands to migrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="ee771-164">Alle bewerkingen die hier wordt beschreven, zijn de idempotent.</span><span class="sxs-lookup"><span data-stu-id="ee771-164">All the operations described here are idempotent.</span></span> <span data-ttu-id="ee771-165">Als er een probleem dan een niet-ondersteunde functie of een configuratiefout, raden wij aan dat u opnieuw de voorbereiden proberen afgebroken of doorgevoerd, bewerking.</span><span class="sxs-lookup"><span data-stu-id="ee771-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="ee771-166">Het platform worden vervolgens de actie opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="ee771-166">The platform then tries the action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="ee771-167">Stap 6.1: Optie 1 - migreren van virtuele machines in een cloudservice (niet in een virtueel netwerk)</span><span class="sxs-lookup"><span data-stu-id="ee771-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="ee771-168">Haal de lijst van cloudservices met behulp van de volgende opdracht uit en kies vervolgens de cloudservice die u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="ee771-168">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="ee771-169">Als de virtuele machines in de cloudservice zich in een virtueel netwerk of als ze web-of werkrollen hebben, de opdracht wordt een foutbericht geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ee771-169">If the VMs in the cloud service are in a virtual network or if they have web or worker roles, the command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="ee771-170">De implementatienaam van de voor de cloudservice worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ee771-170">Get the deployment name for the cloud service.</span></span> <span data-ttu-id="ee771-171">In dit voorbeeld wordt de servicenaam is **mijn Service**.</span><span class="sxs-lookup"><span data-stu-id="ee771-171">In this example, the service name is **My Service**.</span></span> <span data-ttu-id="ee771-172">De servicenaam voorbeeld vervangen door uw eigen servicenaam.</span><span class="sxs-lookup"><span data-stu-id="ee771-172">Replace the example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="ee771-173">Bereid de virtuele machines in de cloudservice voor migratie.</span><span class="sxs-lookup"><span data-stu-id="ee771-173">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="ee771-174">U hebben kunt kiezen uit twee opties.</span><span class="sxs-lookup"><span data-stu-id="ee771-174">You have two options to choose from.</span></span>

* <span data-ttu-id="ee771-175">**Optie 1. De virtuele machines migreren naar een virtueel netwerk met platform gemaakt**</span><span class="sxs-lookup"><span data-stu-id="ee771-175">**Option 1. Migrate the VMs to a platform-created virtual network**</span></span>

    <span data-ttu-id="ee771-176">Eerst valideren als u de cloudservice met de volgende opdrachten kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="ee771-176">First, validate if you can migrate the cloud service using the following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="ee771-177">De voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ee771-177">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ee771-178">Als validatie gelukt is, dan kunt u aan bij de **voorbereiden** stap:</span><span class="sxs-lookup"><span data-stu-id="ee771-178">If validation is successful, then you can move on to the **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="ee771-179">**Optie 2. Migreren naar een bestaand virtueel netwerk in het Resource Manager-implementatiemodel**</span><span class="sxs-lookup"><span data-stu-id="ee771-179">**Option 2. Migrate to an existing virtual network in the Resource Manager deployment model**</span></span>

    <span data-ttu-id="ee771-180">Dit voorbeeld wordt de naam van de resourcegroep op **myResourceGroup**, de naam van het virtuele netwerk naar **myVirtualNetwork** en de subnetnaam van het wilt **mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="ee771-180">This example sets the resource group name to **myResourceGroup**, the virtual network name to **myVirtualNetwork** and the subnet name to **mySubNet**.</span></span> <span data-ttu-id="ee771-181">De namen in het voorbeeld vervangen door de namen van uw eigen resources.</span><span class="sxs-lookup"><span data-stu-id="ee771-181">Replace the names in the example with the names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="ee771-182">Eerst valideren als u het virtuele netwerk met de volgende opdracht kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="ee771-182">First, validate if you can migrate the virtual network using the following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="ee771-183">De voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ee771-183">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ee771-184">Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met de volgende voorbereidingsstap:</span><span class="sxs-lookup"><span data-stu-id="ee771-184">If validation is successful, then you can proceed with the following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="ee771-185">Nadat de Prepare-bewerking is geslaagd met een van de voorgaande opties, query uitvoeren op de migratiestatus van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ee771-185">After the Prepare operation succeeds with either of the preceding options, query the migration state of the VMs.</span></span> <span data-ttu-id="ee771-186">Zorg ervoor dat ze in de `Prepared` staat.</span><span class="sxs-lookup"><span data-stu-id="ee771-186">Ensure that they are in the `Prepared` state.</span></span>

<span data-ttu-id="ee771-187">Dit voorbeeld wordt de naam van de VM op **myVM**.</span><span class="sxs-lookup"><span data-stu-id="ee771-187">This example sets the VM name to **myVM**.</span></span> <span data-ttu-id="ee771-188">De naam in dit voorbeeld vervangen door de naam van uw eigen VM.</span><span class="sxs-lookup"><span data-stu-id="ee771-188">Replace the example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="ee771-189">Controleer de configuratie voor de voorbereide resources met behulp van PowerShell of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-189">Check the configuration for the prepared resources by using either PowerShell or the Azure portal.</span></span> <span data-ttu-id="ee771-190">Als u niet klaar voor de migratie bent en u wilt terugkeren naar de oude status, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-190">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="ee771-191">Als de voorbereide configuratie er goed uitziet, kunt u verder gaan en het doorvoeren van de resources met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-191">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="ee771-192">Stap 6.1: Optie 2: migreren van virtuele machines in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="ee771-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="ee771-193">Als u wilt migreren van virtuele machines in een virtueel netwerk, moet u het virtuele netwerk migreren.</span><span class="sxs-lookup"><span data-stu-id="ee771-193">To migrate virtual machines in a virtual network, you migrate the virtual network.</span></span> <span data-ttu-id="ee771-194">De virtuele machines migreren automatisch met het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="ee771-194">The virtual machines automatically migrate with the virtual network.</span></span> <span data-ttu-id="ee771-195">Kies het virtuele netwerk dat u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="ee771-195">Pick the virtual network that you want to migrate.</span></span>
> [!NOTE]
> <span data-ttu-id="ee771-196">[Migreren van één klassieke virtuele machine](migrate-single-classic-to-resource-manager.md) door het maken van een nieuwe Resource Manager-virtuele machine met beheerd schijven met behulp van de VHD (besturingssysteem en data)-bestanden van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ee771-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using the VHD (OS and data) files of the virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="ee771-197">Naam van het virtuele netwerk kan afwijken van wat wordt weergegeven in de nieuwe Portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-197">The virtual network name might be different from what is shown in the new Portal.</span></span> <span data-ttu-id="ee771-198">De nieuwe Azure-Portal geeft de naam op als `[vnet-name]` , maar de daadwerkelijke virtuele-netwerknaam is van het type `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="ee771-198">The new Azure Portal displays the name as `[vnet-name]` but the actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="ee771-199">Voordat u migreert, zoeken de naam van het werkelijke virtueel netwerk met de opdracht `Get-AzureVnetSite | Select -Property Name` of weergeven in de oude Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-199">Before migrating, lookup the actual virtual network name using the command `Get-AzureVnetSite | Select -Property Name` or view it in the old Azure Portal.</span></span> 

<span data-ttu-id="ee771-200">Dit voorbeeld wordt de naam van het virtuele netwerk op **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="ee771-200">This example sets the virtual network name to **myVnet**.</span></span> <span data-ttu-id="ee771-201">De naam van het virtuele netwerk voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="ee771-201">Replace the example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="ee771-202">Als het virtuele netwerk of werkrollen of VM's met niet-ondersteunde configuraties bevat, krijgt u een validatiefoutbericht.</span><span class="sxs-lookup"><span data-stu-id="ee771-202">If the virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="ee771-203">Eerst valideren als u het virtuele netwerk migreren kunt met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-203">First, validate if you can migrate the virtual network by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="ee771-204">De voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="ee771-204">The preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="ee771-205">Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met de volgende voorbereidingsstap:</span><span class="sxs-lookup"><span data-stu-id="ee771-205">If validation is successful, then you can proceed with the following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="ee771-206">Controleer de configuratie voor de voorbereide virtuele machines met behulp van Azure PowerShell of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-206">Check the configuration for the prepared virtual machines by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="ee771-207">Als u niet klaar voor de migratie bent en u wilt terugkeren naar de oude status, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-207">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="ee771-208">Als de voorbereide configuratie er goed uitziet, kunt u verder gaan en het doorvoeren van de resources met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-208">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="ee771-209">Stap 6.2 migreren, een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="ee771-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="ee771-210">Zodra u bent met klaar de virtuele machines migreert, wordt aangeraden migreren van de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="ee771-210">Once you're done migrating the virtual machines, we recommend you migrate the storage accounts.</span></span>

<span data-ttu-id="ee771-211">Voordat u het opslagaccount migreert, uitvoeren voorafgaand aan de vereiste controles in:</span><span class="sxs-lookup"><span data-stu-id="ee771-211">Before you migrate the storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="ee771-212">**Klassieke virtuele machines waarvan schijven zijn opgeslagen in het opslagaccount migreren**</span><span class="sxs-lookup"><span data-stu-id="ee771-212">**Migrate classic virtual machines whose disks are stored in the storage account**</span></span>

    <span data-ttu-id="ee771-213">Voorafgaand aan de opdracht RoleName eigenschappen en geretourneerd DiskName van alle klassieke VM-schijven in de storage-account.</span><span class="sxs-lookup"><span data-stu-id="ee771-213">Preceding command returns RoleName and DiskName properties of all the classic VM disks in the storage account.</span></span> <span data-ttu-id="ee771-214">RoleName is de naam van de virtuele machine waaraan een schijf is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ee771-214">RoleName is the name of the virtual machine to which a disk is attached.</span></span> <span data-ttu-id="ee771-215">Als de voorgaande opdracht retourneert schijven vervolgens ervoor te zorgen dat virtuele machines die deze schijven zijn gekoppeld worden gemigreerd vóór de migratie van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ee771-215">If preceding command returns disks then ensure that virtual machines to which these disks are attached are migrated before migrating the storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="ee771-216">**Niet-gekoppelde klassieke VM schijven die zijn opgeslagen in het opslagaccount verwijderd**</span><span class="sxs-lookup"><span data-stu-id="ee771-216">**Delete unattached classic VM disks stored in the storage account**</span></span>

    <span data-ttu-id="ee771-217">Zoeken naar niet-gekoppelde schijven in de klassieke VM in de opslagruimte rekening met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-217">Find unattached classic VM disks in the storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="ee771-218">Als de bovenstaande opdracht retourneert schijven Verwijder deze schijven met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="ee771-219">**VM-installatiekopieën verwijderen opgeslagen in de storage-account**</span><span class="sxs-lookup"><span data-stu-id="ee771-219">**Delete VM images stored in the storage account**</span></span>

    <span data-ttu-id="ee771-220">Opdracht vóór retourneert alle VM-installatiekopieën met besturingssysteemschijf opgeslagen in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ee771-220">Preceding command returns all the VM images with OS disk stored in the storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="ee771-221">Opdracht vóór retourneert alle VM-installatiekopieën met gegevensschijven opgeslagen in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ee771-221">Preceding command returns all the VM images with data disks stored in the storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="ee771-222">Verwijder alle VM-installatiekopieën die worden geretourneerd door de bovenstaande opdrachten met behulp van de voorgaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-222">Delete all the VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="ee771-223">Elk opslagaccount voor de migratie valideren met behulp van de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="ee771-223">Validate each storage account for migration by using the following command.</span></span> <span data-ttu-id="ee771-224">In dit voorbeeld wordt de naam van het opslagaccount is **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="ee771-224">In this example, the storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="ee771-225">De naam in dit voorbeeld vervangen door de naam van uw eigen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ee771-225">Replace the example name with the name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="ee771-226">Volgende stap is het opslagaccount voorbereiden voor migratie</span><span class="sxs-lookup"><span data-stu-id="ee771-226">Next step is to Prepare the storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="ee771-227">Controleer de configuratie voor de voorbereide storage-account met behulp van Azure PowerShell of de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ee771-227">Check the configuration for the prepared storage account by using either Azure PowerShell or the Azure portal.</span></span> <span data-ttu-id="ee771-228">Als u niet klaar voor de migratie bent en u wilt terugkeren naar de oude status, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-228">If you are not ready for migration and you want to go back to the old state, use the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="ee771-229">Als de voorbereide configuratie er goed uitziet, kunt u verder gaan en het doorvoeren van de resources met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ee771-229">If the prepared configuration looks good, you can move forward and commit the resources by using the following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="ee771-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee771-230">Next steps</span></span>
* [<span data-ttu-id="ee771-231">Overzicht van de migratie van IaaS resources van klassieke in Azure Resource Manager-platform ondersteund</span><span class="sxs-lookup"><span data-stu-id="ee771-231">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-232">Technische deep dive op platform ondersteund migratie van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee771-232">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-233">Planning voor de migratie van IaaS-resources van het klassieke implementatiemodel naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee771-233">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-234">CLI gebruiken voor het migreren van IaaS-middelen van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee771-234">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-235">Community-hulpprogramma's voor hulp bij de migratie van IaaS-middelen van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee771-235">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-236">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="ee771-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ee771-237">Lees de veelgestelde vragen over IaaS Resourcemigratie van klassiek naar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee771-237">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
