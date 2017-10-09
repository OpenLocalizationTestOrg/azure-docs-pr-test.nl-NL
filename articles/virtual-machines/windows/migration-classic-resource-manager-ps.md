---
title: aaaMigrate tooResource Manager met PowerShell | Microsoft Docs
description: Dit artikel begeleidt u bij Hallo platform ondersteund migratie van IaaS-resources, zoals virtuele machines (VM's), virtuele netwerken (vnet's) en storage-accounts van klassieke tooAzure Resource Manager (ARM) met behulp van Azure PowerShell-opdrachten
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
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a><span data-ttu-id="02f60-103">Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="02f60-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure PowerShell</span></span>
<span data-ttu-id="02f60-104">Deze stappen ziet u hoe toouse Azure PowerShell toomigrate infrastructuur opdrachten als een dienst (IaaS) resources vanuit Hallo classic deployment model toohello Azure Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="02f60-104">These steps show you how toouse Azure PowerShell commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="02f60-105">Als u wilt, kunt u ook resources migreren door middel van Hallo [Azure-opdrachtregelinterface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span><span class="sxs-lookup"><span data-stu-id="02f60-105">If you want, you can also migrate resources by using hello [Azure Command Line Interface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).</span></span>

* <span data-ttu-id="02f60-106">Zie voor achtergrondinformatie over ondersteunde migratiescenario's [Platform ondersteund migratie van IaaS-resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f60-106">For background on supported migration scenarios, see [Platform-supported migration of IaaS resources from classic tooAzure Resource Manager](migration-classic-resource-manager-overview.md).</span></span>
* <span data-ttu-id="02f60-107">Zie voor gedetailleerde instructies en een overzicht van migratie [technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span><span class="sxs-lookup"><span data-stu-id="02f60-107">For detailed guidance and a migration walkthrough, see [Technical deep dive on platform-supported migration from classic tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).</span></span>
* [<span data-ttu-id="02f60-108">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="02f60-108">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md)

<br>
<span data-ttu-id="02f60-109">Hier volgt een stroomdiagram tooidentify Hallo volgorde waarin stappen toobe uitgevoerd tijdens een migratie moeten</span><span class="sxs-lookup"><span data-stu-id="02f60-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Schermafbeelding van de migratiestappen Hallo](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a><span data-ttu-id="02f60-111">Stap 1: Plannen voor migratie</span><span class="sxs-lookup"><span data-stu-id="02f60-111">Step 1: Plan for migration</span></span>
<span data-ttu-id="02f60-112">Hier volgen enkele aanbevolen procedures die wij adviseren kijkt u bij het evalueren van IaaS-Resourcemigratie van klassieke tooResource Manager:</span><span class="sxs-lookup"><span data-stu-id="02f60-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="02f60-113">Lees Hallo [ondersteunde en niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02f60-113">Read through hello [supported and unsupported features and configurations](migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="02f60-114">Als u virtuele machines die gebruikmaken van niet-ondersteunde configuraties of functies hebt, raden wij wachten op Hallo configuratie of onderdeel ondersteuning toobe aangekondigd.</span><span class="sxs-lookup"><span data-stu-id="02f60-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello configuration/feature support toobe announced.</span></span> <span data-ttu-id="02f60-115">U kunt ook als deze aan uw behoeften voldoet, verwijdert u deze functie of verlaten die configuratie tooenable migratie.</span><span class="sxs-lookup"><span data-stu-id="02f60-115">Alternatively, if it suits your needs, remove that feature or move out of that configuration tooenable migration.</span></span>
* <span data-ttu-id="02f60-116">Als u scripts die uw infrastructuur en toepassingen vandaag implementeert geautomatiseerde, kunt u toocreate instellingen voor een vergelijkbaar met behulp van deze scripts voor de migratie.</span><span class="sxs-lookup"><span data-stu-id="02f60-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="02f60-117">U kunt ook voorbeeld omgevingen instellen met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="02f60-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02f60-118">Toepassingsgateways worden momenteel niet ondersteund voor migratie van klassiek tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="02f60-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="02f60-119">Hallo gateway toomigrate een klassiek virtueel netwerk met een toepassingsgateway verwijderen voordat u een netwerk voorbereiden bewerking toomove Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="02f60-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="02f60-120">Nadat u Hallo migratie hebt voltooid, sluit u Hallo gateway in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02f60-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span>
>
><span data-ttu-id="02f60-121">ExpressRoute-gateways die verbinding maken met tooExpressRoute circuits in een ander abonnement kunnen niet automatisch worden gemigreerd.</span><span class="sxs-lookup"><span data-stu-id="02f60-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="02f60-122">In dergelijke gevallen Hallo ExpressRoute-gateway verwijderen, Migreer het virtuele netwerk Hallo en maak Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="02f60-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="02f60-123">Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02f60-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="02f60-124">Stap 2: Installeer de meest recente versie van Azure PowerShell Hallo</span><span class="sxs-lookup"><span data-stu-id="02f60-124">Step 2: Install hello latest version of Azure PowerShell</span></span>
<span data-ttu-id="02f60-125">Er zijn twee manieren tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) of [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="02f60-125">There are two main options tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) or [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="02f60-126">WebPI ontvangt maandelijkse updates.</span><span class="sxs-lookup"><span data-stu-id="02f60-126">WebPI receives monthly updates.</span></span> <span data-ttu-id="02f60-127">PowerShell Gallery ontvangt updates doorlopend.</span><span class="sxs-lookup"><span data-stu-id="02f60-127">PowerShell Gallery receives updates on a continuous basis.</span></span> <span data-ttu-id="02f60-128">In dit artikel is gebaseerd op Azure PowerShell versie 2.1.0.</span><span class="sxs-lookup"><span data-stu-id="02f60-128">This article is based on Azure PowerShell version 2.1.0.</span></span>

<span data-ttu-id="02f60-129">Zie voor installatie-instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02f60-129">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a><span data-ttu-id="02f60-130">Stap 3: Zorg ervoor dat u een beheerder zijn voor het Hallo-abonnement in Azure-portal</span><span class="sxs-lookup"><span data-stu-id="02f60-130">Step 3: Ensure that you are an administrator for hello subscription in Azure portal</span></span>
<span data-ttu-id="02f60-131">tooperform deze migratie kan u moet worden toegevoegd als medebeheerder voor Hallo-abonnement in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02f60-131">tooperform this migration, you must be added as a co-administrator for hello subscription in hello [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="02f60-132">Meld u aan bij Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02f60-132">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="02f60-133">Selecteer op de Hub-menu Hallo **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="02f60-133">On hello Hub menu, select **Subscription**.</span></span> <span data-ttu-id="02f60-134">Als u deze niet ziet, selecteert u **meer services**.</span><span class="sxs-lookup"><span data-stu-id="02f60-134">If you don't see it, select **More services**.</span></span>
3. <span data-ttu-id="02f60-135">Vermelding in het juiste abonnement Hallo vinden en vervolgens bekijkt hello **mijn rol** veld.</span><span class="sxs-lookup"><span data-stu-id="02f60-135">Find hello appropriate subscription entry, then look at hello **MY ROLE** field.</span></span> <span data-ttu-id="02f60-136">Voor een medebeheerder Hallo-waarde moet _accountbeheerder_.</span><span class="sxs-lookup"><span data-stu-id="02f60-136">For a co-administrator, hello value should be _Account admin_.</span></span>

<span data-ttu-id="02f60-137">Als u niet kunt tooadd een CO-beheerder bent, klikt u vervolgens contact op met een servicebeheerder of medebeheerder Hallo abonnement tooget zelf toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="02f60-137">If you are not able tooadd a co-administrator, then contact a service administrator or co-administrator for hello subscription tooget yourself added.</span></span>   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a><span data-ttu-id="02f60-138">Stap 4: Stel uw abonnement en aanmelden voor migratie</span><span class="sxs-lookup"><span data-stu-id="02f60-138">Step 4: Set your subscription and sign up for migration</span></span>
<span data-ttu-id="02f60-139">Eerst een PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="02f60-139">First, start a PowerShell prompt.</span></span> <span data-ttu-id="02f60-140">Voor de migratie, moet u tooset van uw omgeving voor zowel klassieke en het Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02f60-140">For migration, you need tooset up your environment for both classic and Resource Manager.</span></span>

<span data-ttu-id="02f60-141">Meld u aan tooyour-account voor Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="02f60-141">Sign in tooyour account for hello Resource Manager model.</span></span>

```powershell
    Login-AzureRmAccount
```

<span data-ttu-id="02f60-142">Hallo beschikbare abonnementen ophalen met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="02f60-142">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

<span data-ttu-id="02f60-143">Stel uw Azure-abonnement voor Hallo huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="02f60-143">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="02f60-144">In dit voorbeeld sets Hallo standaardnaam van het abonnement te**mijn Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="02f60-144">This example sets hello default subscription name too**My Azure Subscription**.</span></span> <span data-ttu-id="02f60-145">De naam van het abonnement voor Hallo-voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="02f60-145">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> <span data-ttu-id="02f60-146">Registratie is een eenmalige stap, maar u moet dit doen eenmaal voordat u de migratie.</span><span class="sxs-lookup"><span data-stu-id="02f60-146">Registration is a one-time step, but you must do it once before attempting migration.</span></span> <span data-ttu-id="02f60-147">Zonder te registreren ziet u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="02f60-147">Without registering, you see hello following error message:</span></span>
>
> <span data-ttu-id="02f60-148">*BadRequest: Abonnement is niet geregistreerd voor migratie.*</span><span class="sxs-lookup"><span data-stu-id="02f60-148">*BadRequest : Subscription is not registered for migration.*</span></span>
>
>

<span data-ttu-id="02f60-149">Registreren bij de Hallo migratie resourceprovider met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="02f60-149">Register with hello migration resource provider by using hello following command:</span></span>

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="02f60-150">Wacht vijf minuten voor Hallo registratie toofinish.</span><span class="sxs-lookup"><span data-stu-id="02f60-150">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="02f60-151">U kunt de status van de Hallo van Hallo goedkeuring controleren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="02f60-151">You can check hello status of hello approval by using hello following command:</span></span>

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

<span data-ttu-id="02f60-152">Zorg ervoor dat RegistrationState `Registered` voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="02f60-152">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

<span data-ttu-id="02f60-153">Nu tooyour-account voor het klassieke model Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="02f60-153">Now sign in tooyour account for hello classic model.</span></span>

```powershell
    Add-AzureAccount
```

<span data-ttu-id="02f60-154">Hallo beschikbare abonnementen ophalen met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="02f60-154">Get hello available subscriptions by using hello following command:</span></span>

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

<span data-ttu-id="02f60-155">Stel uw Azure-abonnement voor Hallo huidige sessie.</span><span class="sxs-lookup"><span data-stu-id="02f60-155">Set your Azure subscription for hello current session.</span></span> <span data-ttu-id="02f60-156">In dit voorbeeld wordt een standaardabonnement hello te**mijn Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="02f60-156">This example sets hello default subscription too**My Azure Subscription**.</span></span> <span data-ttu-id="02f60-157">De naam van het abonnement voor Hallo-voorbeeld vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="02f60-157">Replace hello example subscription name with your own.</span></span>

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="02f60-158">Stap 5: Controleer of er voldoende virtuele Machine van Azure Resource Manager kernen in hello Azure-regio van uw huidige implementatie of VNET</span><span class="sxs-lookup"><span data-stu-id="02f60-158">Step 5: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="02f60-159">U kunt Hallo volgende PowerShell-opdracht toocheck Hallo Huidig aantal kernen dat u in Azure Resource Manager hebt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02f60-159">You can use hello following PowerShell command toocheck hello current number of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="02f60-160">toolearn meer informatie over quota core, Zie [limieten en hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="02f60-160">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).</span></span>

<span data-ttu-id="02f60-161">In dit voorbeeld controleert op Hallo beschikbaarheid in Hallo **VS-West** regio.</span><span class="sxs-lookup"><span data-stu-id="02f60-161">This example checks hello availability in hello **West US** region.</span></span> <span data-ttu-id="02f60-162">Hallo voorbeeld regionaam vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="02f60-162">Replace hello example region name with your own.</span></span>

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a><span data-ttu-id="02f60-163">Stap 6: Uitvoeren opdrachten toomigrate uw IaaS-resources</span><span class="sxs-lookup"><span data-stu-id="02f60-163">Step 6: Run commands toomigrate your IaaS resources</span></span>
> [!NOTE]
> <span data-ttu-id="02f60-164">Alle Hallo bewerkingen hier beschreven zijn idempotent.</span><span class="sxs-lookup"><span data-stu-id="02f60-164">All hello operations described here are idempotent.</span></span> <span data-ttu-id="02f60-165">Als er een probleem dan een niet-ondersteunde functie of een configuratiefout, raden wij aan dat u opnieuw Hallo proberen voorbereiden, afgebroken of doorgevoerd, bewerking.</span><span class="sxs-lookup"><span data-stu-id="02f60-165">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="02f60-166">Hallo platform probeert vervolgens Hallo actie opnieuw.</span><span class="sxs-lookup"><span data-stu-id="02f60-166">hello platform then tries hello action again.</span></span>
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a><span data-ttu-id="02f60-167">Stap 6.1: Optie 1 - migreren van virtuele machines in een cloudservice (niet in een virtueel netwerk)</span><span class="sxs-lookup"><span data-stu-id="02f60-167">Step 6.1: Option 1 - Migrate virtual machines in a cloud service (not in a virtual network)</span></span>
<span data-ttu-id="02f60-168">Haal de lijst Hallo van cloud-services met behulp van de volgende opdracht Hallo en kies Hallo cloudservice die u wilt toomigrate.</span><span class="sxs-lookup"><span data-stu-id="02f60-168">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="02f60-169">Als Hallo virtuele machines in de cloudservice Hallo in een virtueel netwerk zijn of als ze web-of werkrollen hebben, retourneert Hallo opdracht een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02f60-169">If hello VMs in hello cloud service are in a virtual network or if they have web or worker roles, hello command returns an error message.</span></span>

```powershell
    Get-AzureService | ft Servicename
```

<span data-ttu-id="02f60-170">De naam van de Hallo implementatie voor cloudservice Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="02f60-170">Get hello deployment name for hello cloud service.</span></span> <span data-ttu-id="02f60-171">In dit voorbeeld is de naam van Hallo service **mijn Service**.</span><span class="sxs-lookup"><span data-stu-id="02f60-171">In this example, hello service name is **My Service**.</span></span> <span data-ttu-id="02f60-172">Servicenaam Hallo-voorbeeld vervangen door uw eigen servicenaam.</span><span class="sxs-lookup"><span data-stu-id="02f60-172">Replace hello example service name with your own service name.</span></span>

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

<span data-ttu-id="02f60-173">Bereid Hallo virtuele machines in de cloudservice Hallo voor migratie.</span><span class="sxs-lookup"><span data-stu-id="02f60-173">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="02f60-174">U hebt twee opties toochoose uit.</span><span class="sxs-lookup"><span data-stu-id="02f60-174">You have two options toochoose from.</span></span>

* <span data-ttu-id="02f60-175">**Optie 1. Migreer het Hallo VMs tooa platform gemaakte virtuele netwerk**</span><span class="sxs-lookup"><span data-stu-id="02f60-175">**Option 1. Migrate hello VMs tooa platform-created virtual network**</span></span>

    <span data-ttu-id="02f60-176">Eerst valideren als u met behulp van de volgende opdrachten Hallo Hallo-cloudservice kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="02f60-176">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    <span data-ttu-id="02f60-177">Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="02f60-177">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="02f60-178">Als validatie gelukt is, dan kunt u op toohello **voorbereiden** stap:</span><span class="sxs-lookup"><span data-stu-id="02f60-178">If validation is successful, then you can move on toohello **Prepare** step:</span></span>

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* <span data-ttu-id="02f60-179">**Optie 2. Migreren van tooan bestaand virtueel netwerk in Hallo Resource Manager-implementatiemodel**</span><span class="sxs-lookup"><span data-stu-id="02f60-179">**Option 2. Migrate tooan existing virtual network in hello Resource Manager deployment model**</span></span>

    <span data-ttu-id="02f60-180">In dit voorbeeld sets Hallo Resourcegroepnaam te**myResourceGroup**, virtuele-netwerknaam te Hallo**myVirtualNetwork** en subnetnaam te Hallo**mySubNet**.</span><span class="sxs-lookup"><span data-stu-id="02f60-180">This example sets hello resource group name too**myResourceGroup**, hello virtual network name too**myVirtualNetwork** and hello subnet name too**mySubNet**.</span></span> <span data-ttu-id="02f60-181">Hallo-namen in Hallo voorbeeld vervangen door Hallo namen van uw eigen resources.</span><span class="sxs-lookup"><span data-stu-id="02f60-181">Replace hello names in hello example with hello names of your own resources.</span></span>

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    <span data-ttu-id="02f60-182">Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="02f60-182">First, validate if you can migrate hello virtual network using hello following command:</span></span>

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    <span data-ttu-id="02f60-183">Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="02f60-183">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="02f60-184">Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met Hallo voorbereidingsstap te volgen:</span><span class="sxs-lookup"><span data-stu-id="02f60-184">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

<span data-ttu-id="02f60-185">Nadat Hallo Prepare-bewerking is geslaagd met een van de voorgaande opties hello, een query migratiestatus Hallo Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="02f60-185">After hello Prepare operation succeeds with either of hello preceding options, query hello migration state of hello VMs.</span></span> <span data-ttu-id="02f60-186">Zorg ervoor dat ze Hallo `Prepared` status.</span><span class="sxs-lookup"><span data-stu-id="02f60-186">Ensure that they are in hello `Prepared` state.</span></span>

<span data-ttu-id="02f60-187">In dit voorbeeld sets Hallo VM-naam te**myVM**.</span><span class="sxs-lookup"><span data-stu-id="02f60-187">This example sets hello VM name too**myVM**.</span></span> <span data-ttu-id="02f60-188">Voorbeeldnaam Hallo vervangen door de naam van uw eigen VM.</span><span class="sxs-lookup"><span data-stu-id="02f60-188">Replace hello example name with your own VM name.</span></span>

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

<span data-ttu-id="02f60-189">Controleer de configuratie voor resources voorbereid met behulp van PowerShell of Azure-portal Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="02f60-189">Check hello configuration for hello prepared resources by using either PowerShell or hello Azure portal.</span></span> <span data-ttu-id="02f60-190">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-190">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

<span data-ttu-id="02f60-191">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="02f60-191">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="02f60-192">Stap 6.1: Optie 2: migreren van virtuele machines in een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="02f60-192">Step 6.1: Option 2 - Migrate virtual machines in a virtual network</span></span>

<span data-ttu-id="02f60-193">toomigrate virtuele machines in een virtueel netwerk die u migreert Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="02f60-193">toomigrate virtual machines in a virtual network, you migrate hello virtual network.</span></span> <span data-ttu-id="02f60-194">Hallo virtuele machines migreren automatisch met het virtuele netwerk Hallo.</span><span class="sxs-lookup"><span data-stu-id="02f60-194">hello virtual machines automatically migrate with hello virtual network.</span></span> <span data-ttu-id="02f60-195">Pick Hallo virtueel netwerk dat u wilt dat toomigrate.</span><span class="sxs-lookup"><span data-stu-id="02f60-195">Pick hello virtual network that you want toomigrate.</span></span>
> [!NOTE]
> <span data-ttu-id="02f60-196">[Migreren van één klassieke virtuele machine](migrate-single-classic-to-resource-manager.md) door het maken van een nieuwe Resource Manager-virtuele machine met beheerd schijven met Hallo VHD (besturingssysteem en data)-bestanden van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="02f60-196">[Migrate single classic virtual machine](migrate-single-classic-to-resource-manager.md) by creating a new Resource Manager virtual machine with Managed Disks using hello VHD (OS and data) files of hello virtual machine.</span></span>
<br>

> [!NOTE]
> <span data-ttu-id="02f60-197">Hallo virtuele-netwerknaam kan afwijken van wat wordt weergegeven in Hallo nieuwe Portal.</span><span class="sxs-lookup"><span data-stu-id="02f60-197">hello virtual network name might be different from what is shown in hello new Portal.</span></span> <span data-ttu-id="02f60-198">Hallo nieuwe Azure Portal wordt weergegeven naam als Hallo `[vnet-name]` maar Hallo werkelijke virtuele-netwerknaam is van het type `Group [resource-group-name] [vnet-name]`.</span><span class="sxs-lookup"><span data-stu-id="02f60-198">hello new Azure Portal displays hello name as `[vnet-name]` but hello actual virtual network name is of type `Group [resource-group-name] [vnet-name]`.</span></span> <span data-ttu-id="02f60-199">Voordat u migreert, lookup Hallo werkelijke virtuele-netwerknaam met Hallo opdracht `Get-AzureVnetSite | Select -Property Name` of weergeven in Hallo oude Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="02f60-199">Before migrating, lookup hello actual virtual network name using hello command `Get-AzureVnetSite | Select -Property Name` or view it in hello old Azure Portal.</span></span> 

<span data-ttu-id="02f60-200">In dit voorbeeld sets Hallo virtuele-netwerknaam te**myVnet**.</span><span class="sxs-lookup"><span data-stu-id="02f60-200">This example sets hello virtual network name too**myVnet**.</span></span> <span data-ttu-id="02f60-201">Hallo voorbeeld van de virtuele-netwerknaam vervangen door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="02f60-201">Replace hello example virtual network name with your own.</span></span>

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> <span data-ttu-id="02f60-202">Als het virtuele netwerk Hallo bevat of werkrollen of VM's met niet-ondersteunde configuraties, krijgt u een validatiefoutbericht.</span><span class="sxs-lookup"><span data-stu-id="02f60-202">If hello virtual network contains web or worker roles, or VMs with unsupported configurations, you get a validation error message.</span></span>
>
>

<span data-ttu-id="02f60-203">Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:</span><span class="sxs-lookup"><span data-stu-id="02f60-203">First, validate if you can migrate hello virtual network by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

<span data-ttu-id="02f60-204">Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren.</span><span class="sxs-lookup"><span data-stu-id="02f60-204">hello preceding command displays any warnings and errors that block migration.</span></span> <span data-ttu-id="02f60-205">Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met Hallo voorbereidingsstap te volgen:</span><span class="sxs-lookup"><span data-stu-id="02f60-205">If validation is successful, then you can proceed with hello following Prepare step:</span></span>

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

<span data-ttu-id="02f60-206">Controleer de configuratie voor virtuele machines voorbereid met behulp van Azure PowerShell of Azure-portal Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="02f60-206">Check hello configuration for hello prepared virtual machines by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="02f60-207">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-207">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

<span data-ttu-id="02f60-208">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="02f60-208">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a><span data-ttu-id="02f60-209">Stap 6.2 migreren, een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="02f60-209">Step 6.2 Migrate a storage account</span></span>
<span data-ttu-id="02f60-210">Zodra u klaar bent met het migreren van Hallo virtuele machines, wordt u aangeraden dat u migreert Hallo storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="02f60-210">Once you're done migrating hello virtual machines, we recommend you migrate hello storage accounts.</span></span>

<span data-ttu-id="02f60-211">Voordat u Hallo storage-account migreert, uitvoeren voorafgaand aan de vereiste controles in:</span><span class="sxs-lookup"><span data-stu-id="02f60-211">Before you migrate hello storage account, please perform preceding prerequisite checks:</span></span>

* <span data-ttu-id="02f60-212">**Klassieke virtuele machines waarvan schijven zijn opgeslagen in het opslagaccount Hallo migreren**</span><span class="sxs-lookup"><span data-stu-id="02f60-212">**Migrate classic virtual machines whose disks are stored in hello storage account**</span></span>

    <span data-ttu-id="02f60-213">Voorafgaand aan de opdracht retourneert eigenschappen RoleName en DiskName van alle Hallo klassieke VM-schijven in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="02f60-213">Preceding command returns RoleName and DiskName properties of all hello classic VM disks in hello storage account.</span></span> <span data-ttu-id="02f60-214">RoleName is Hallo-naam van Hallo virtuele machine toowhich die een schijf is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="02f60-214">RoleName is hello name of hello virtual machine toowhich a disk is attached.</span></span> <span data-ttu-id="02f60-215">Als de voorgaande opdracht retourneert schijven Verzeker u ervan dat virtuele machines toowhich deze schijven zijn gekoppeld worden gemigreerd voordat u migreert Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="02f60-215">If preceding command returns disks then ensure that virtual machines toowhich these disks are attached are migrated before migrating hello storage account.</span></span>
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* <span data-ttu-id="02f60-216">**Niet-gekoppelde klassieke VM schijven die zijn opgeslagen in Hallo storage-account verwijderen**</span><span class="sxs-lookup"><span data-stu-id="02f60-216">**Delete unattached classic VM disks stored in hello storage account**</span></span>

    <span data-ttu-id="02f60-217">Zoeken naar niet-gekoppelde schijven in de klassieke VM in Hallo opslag rekening met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-217">Find unattached classic VM disks in hello storage account using following command:</span></span>

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    <span data-ttu-id="02f60-218">Als de bovenstaande opdracht retourneert schijven Verwijder deze schijven met volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-218">If above command returns disks then delete these disks using following command:</span></span>

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* <span data-ttu-id="02f60-219">**VM-installatiekopieën verwijderen opgeslagen in het opslagaccount Hallo**</span><span class="sxs-lookup"><span data-stu-id="02f60-219">**Delete VM images stored in hello storage account**</span></span>

    <span data-ttu-id="02f60-220">Opdracht vóór retourneert alle Hallo VM-installatiekopieën met besturingssysteemschijf opgeslagen in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="02f60-220">Preceding command returns all hello VM images with OS disk stored in hello storage account.</span></span>
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     <span data-ttu-id="02f60-221">Voorafgaand aan de opdracht retourneert alle Hallo VM-installatiekopieën met gegevensschijven in Hallo storage-account is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="02f60-221">Preceding command returns all hello VM images with data disks stored in hello storage account.</span></span>
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    <span data-ttu-id="02f60-222">Verwijder alle Hallo VM-installatiekopieën geretourneerd door de bovenstaande opdrachten met behulp van de voorgaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-222">Delete all hello VM images returned by above commands using preceding command:</span></span>
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

<span data-ttu-id="02f60-223">Elk opslagaccount voor migratie met behulp van de volgende opdracht Hallo valideren.</span><span class="sxs-lookup"><span data-stu-id="02f60-223">Validate each storage account for migration by using hello following command.</span></span> <span data-ttu-id="02f60-224">In dit voorbeeld Hallo opslagaccountnaam is **myStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="02f60-224">In this example, hello storage account name is **myStorageAccount**.</span></span> <span data-ttu-id="02f60-225">Voorbeeldnaam Hallo vervangen door Hallo-naam van uw eigen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="02f60-225">Replace hello example name with hello name of your own storage account.</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

<span data-ttu-id="02f60-226">Volgende stap is tooPrepare Hallo storage-account voor migratie</span><span class="sxs-lookup"><span data-stu-id="02f60-226">Next step is tooPrepare hello storage account for migration</span></span>

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

<span data-ttu-id="02f60-227">Controleer de configuratie van Hallo voor Hallo voorbereid storage-account met behulp van Azure PowerShell of hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="02f60-227">Check hello configuration for hello prepared storage account by using either Azure PowerShell or hello Azure portal.</span></span> <span data-ttu-id="02f60-228">Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="02f60-228">If you are not ready for migration and you want toogo back toohello old state, use hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

<span data-ttu-id="02f60-229">Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="02f60-229">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command:</span></span>

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a><span data-ttu-id="02f60-230">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02f60-230">Next steps</span></span>
* [<span data-ttu-id="02f60-231">Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund</span><span class="sxs-lookup"><span data-stu-id="02f60-231">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-232">Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02f60-232">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-233">Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen</span><span class="sxs-lookup"><span data-stu-id="02f60-233">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-234">CLI toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="02f60-234">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-235">Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02f60-235">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-236">Bekijk de meest voorkomende migratiefouten</span><span class="sxs-lookup"><span data-stu-id="02f60-236">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="02f60-237">Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02f60-237">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
