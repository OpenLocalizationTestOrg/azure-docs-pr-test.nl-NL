---
title: 'Maken en een ExpressRoute-circuit wijzigen: PowerShell: klassieke Azure Portal | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en een ExpressRoute-circuit inrichten. Dit artikel ziet u ook hoe toocheck Hallo status, bijwerken, of verwijderen en uw circuit inrichting ervan ongedaan maakt.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="4c319-104">Maken en een ExpressRoute-circuit met behulp van PowerShell (klassiek) wijzigen</span><span class="sxs-lookup"><span data-stu-id="4c319-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c319-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4c319-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="4c319-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c319-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="4c319-107">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="4c319-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="4c319-108">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4c319-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="4c319-109">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="4c319-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="4c319-110">Dit artikel begeleidt u bij Hallo stappen toocreate een Azure ExpressRoute-circuit met PowerShell-cmdlets en Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4c319-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="4c319-111">Dit artikel leest u hoe toocheck Hallo status, bijwerken, of verwijderen en een ExpressRoute-circuit inrichting ervan ongedaan.</span><span class="sxs-lookup"><span data-stu-id="4c319-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="4c319-112">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="4c319-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="4c319-113">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4c319-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="4c319-114">Step 1.</span><span class="sxs-lookup"><span data-stu-id="4c319-114">Step 1.</span></span> <span data-ttu-id="4c319-115">Hallo-vereisten en werkstroom artikelen controleren</span><span class="sxs-lookup"><span data-stu-id="4c319-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="4c319-116">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="4c319-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="4c319-117">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="4c319-117">Step 2.</span></span> <span data-ttu-id="4c319-118">De meest recente versies Hallo van hello Azure Service Management (SM) PowerShell-modules installeren</span><span class="sxs-lookup"><span data-stu-id="4c319-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="4c319-119">Volg de instructies in Hallo [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview) voor stapsgewijze instructies voor het tooconfigure uw computer toouse hello Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="4c319-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="4c319-120">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="4c319-120">Step 3.</span></span> <span data-ttu-id="4c319-121">Meld u bij tooyour Azure-account en een abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="4c319-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="4c319-122">Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="4c319-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="4c319-123">Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="4c319-124">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="4c319-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="4c319-125">Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="4c319-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="4c319-126">Gebruik vervolgens Hallo cmdlet tooadd na uw Azure-abonnement tooPowerShell Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="4c319-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="4c319-127">Maken en een ExpressRoute-circuit inrichten</span><span class="sxs-lookup"><span data-stu-id="4c319-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="4c319-128">Step 1.</span><span class="sxs-lookup"><span data-stu-id="4c319-128">Step 1.</span></span> <span data-ttu-id="4c319-129">Hallo PowerShell-modules importeren voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c319-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="4c319-130">Als u dit nog niet hebt gedaan, moet u hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4c319-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="4c319-131">Importeren van modules Hallo Hallo locatie die ze waren geïnstalleerd tooon uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="4c319-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="4c319-132">Afhankelijk van de methode Hallo u tooinstall Hallo modules gebruikt, Hallo locatie mogelijk anders dan Hallo volgende voorbeeld wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="4c319-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="4c319-133">Hallo voorbeeld desgewenst wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4c319-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="4c319-134">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="4c319-134">Step 2.</span></span> <span data-ttu-id="4c319-135">Hallo-lijst met ondersteunde providers, locaties en bandbreedten</span><span class="sxs-lookup"><span data-stu-id="4c319-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="4c319-136">Voordat u een ExpressRoute-circuit maken, moet u Hallo lijst met ondersteunde connectiviteitsproviders, locaties en bandbreedte-opties.</span><span class="sxs-lookup"><span data-stu-id="4c319-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="4c319-137">PowerShell-cmdlet Hallo `Get-AzureDedicatedCircuitServiceProvider` retourneert deze informatie, die u in latere stappen:</span><span class="sxs-lookup"><span data-stu-id="4c319-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="4c319-138">Controleer de toosee als uw connectiviteitsprovider daar wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="4c319-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="4c319-139">Maak een notitie van de volgende informatie omdat u hebt deze later nodig bij het maken van een circuit Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="4c319-140">Naam</span><span class="sxs-lookup"><span data-stu-id="4c319-140">Name</span></span>
* <span data-ttu-id="4c319-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="4c319-141">PeeringLocations</span></span>
* <span data-ttu-id="4c319-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="4c319-142">BandwidthsOffered</span></span>

<span data-ttu-id="4c319-143">U bent nu klaar toocreate een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="4c319-144">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="4c319-144">Step 3.</span></span> <span data-ttu-id="4c319-145">Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="4c319-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="4c319-146">Hallo volgende voorbeeld ziet u hoe toocreate een 200 Mbps-ExpressRoute-circuit via Equinix in Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="4c319-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="4c319-147">Als u een andere provider en andere instellingen gebruikt, vervangt u die informatie door wanneer u uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="4c319-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c319-148">Uw ExpressRoute-circuit worden gefactureerd vanaf Hallo moment dat die de sleutel van een service wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="4c319-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="4c319-149">Zorg ervoor dat u deze bewerking niet uitvoeren wanneer de connectiviteitsprovider Hallo gereed tooprovision Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="4c319-150">Hallo Hier volgt een voorbeeld van de aanvraag voor een nieuwe servicesleutel:</span><span class="sxs-lookup"><span data-stu-id="4c319-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="4c319-151">Of als u een ExpressRoute-circuit met premium-invoegtoepassing voor Hallo toocreate wilt, gebruik Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="4c319-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="4c319-152">Raadpleeg toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="4c319-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="4c319-153">Hallo-antwoord bevat de servicesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c319-153">hello response will contain hello service key.</span></span> <span data-ttu-id="4c319-154">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="4c319-155">Stap 4.</span><span class="sxs-lookup"><span data-stu-id="4c319-155">Step 4.</span></span> <span data-ttu-id="4c319-156">Lijst van alle Hallo ExpressRoute-circuits</span><span class="sxs-lookup"><span data-stu-id="4c319-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="4c319-157">U kunt uitvoeren Hallo `Get-AzureDedicatedCircuit` opdracht tooget een lijst met alle Hallo ExpressRoute-circuits die u hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4c319-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="4c319-158">antwoord Hallo zijn iets dergelijks toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="4c319-159">U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4c319-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="4c319-160">Hallo aanroepen zonder parameters maken een lijst met alle Hallo circuits.</span><span class="sxs-lookup"><span data-stu-id="4c319-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="4c319-161">De sleutel van uw service wordt weergegeven in Hallo *ServiceKey* veld.</span><span class="sxs-lookup"><span data-stu-id="4c319-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="4c319-162">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="4c319-163">Stap 5.</span><span class="sxs-lookup"><span data-stu-id="4c319-163">Step 5.</span></span> <span data-ttu-id="4c319-164">Sleutel tooyour Hallo-connectiviteit serviceprovider voor het inrichten van verzenden</span><span class="sxs-lookup"><span data-stu-id="4c319-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="4c319-165">*ServiceProviderProvisioningState* bevat informatie over de huidige status van de Hallo van inrichting Hallo serviceprovider zijde.</span><span class="sxs-lookup"><span data-stu-id="4c319-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="4c319-166">*Status* Hallo status biedt op Hallo Microsoft aan clientzijde.</span><span class="sxs-lookup"><span data-stu-id="4c319-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="4c319-167">Zie voor meer informatie over het circuit inrichtingstatuswaarden hello [werkstromen](expressroute-workflows.md#expressroute-circuit-provisioning-states) artikel.</span><span class="sxs-lookup"><span data-stu-id="4c319-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="4c319-168">Bij het maken van nieuwe ExpressRoute-circuit liggen Hallo circuit Hallo status te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="4c319-169">Hallo circuit gaat toohello status wanneer Hallo connectiviteitsprovider in Hallo-proces voor het inschakelen van deze voor u te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="4c319-170">Een ExpressRoute-circuit moet zijn Hallo status voor u toobe kunnen toouse na het:</span><span class="sxs-lookup"><span data-stu-id="4c319-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="4c319-171">Stap 6.</span><span class="sxs-lookup"><span data-stu-id="4c319-171">Step 6.</span></span> <span data-ttu-id="4c319-172">Hallo-status en Hallo-status van de Hallo circuit sleutel regelmatig te controleren</span><span class="sxs-lookup"><span data-stu-id="4c319-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="4c319-173">Dit laat u weten wanneer uw provider uw circuit is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4c319-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="4c319-174">Nadat het Hallo-circuit is geconfigureerd, *ServiceProviderProvisioningState* weergegeven als *ingericht* zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="4c319-175">Stap 7.</span><span class="sxs-lookup"><span data-stu-id="4c319-175">Step 7.</span></span> <span data-ttu-id="4c319-176">Maken van uw configuratie van de routering</span><span class="sxs-lookup"><span data-stu-id="4c319-176">Create your routing configuration</span></span>
<span data-ttu-id="4c319-177">Raadpleeg toohello [routeringsconfiguratie voor ExpressRoute-circuit (maken en wijzigen van circuit peerings)](expressroute-howto-routing-classic.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="4c319-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c319-178">Deze instructies zijn alleen van toepassing toocircuits die zijn gemaakt met serviceproviders die services op laag 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="4c319-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="4c319-179">Als u een serviceprovider die beheerde laag-3-services (meestal een IP VPN, zoals MPLS), uw connectiviteitsprovider configureren en beheren van routering voor u.</span><span class="sxs-lookup"><span data-stu-id="4c319-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="4c319-180">Stap 8.</span><span class="sxs-lookup"><span data-stu-id="4c319-180">Step 8.</span></span> <span data-ttu-id="4c319-181">Koppelen van een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4c319-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="4c319-182">Koppel vervolgens een virtueel netwerk tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="4c319-183">Raadpleeg te[koppelen ExpressRoute-circuits toovirtual netwerken](expressroute-howto-linkvnet-classic.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="4c319-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="4c319-184">Als u een virtueel netwerk met het klassieke implementatiemodel Hallo voor ExpressRoute toocreate moet, Zie [een virtueel netwerk maken voor ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="4c319-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="4c319-185">Hallo-status van een ExpressRoute-circuit ophalen</span><span class="sxs-lookup"><span data-stu-id="4c319-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="4c319-186">U kunt deze informatie op elk gewenst moment ophalen met behulp van Hallo `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4c319-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="4c319-187">Hallo aanroepen zonder parameters maken een lijst met alle Hallo circuits.</span><span class="sxs-lookup"><span data-stu-id="4c319-187">Making hello call without any parameters lists all hello circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="4c319-188">U kunt de informatie op een specifieke ExpressRoute-circuit opvragen door Hallo servicesleutel doorgeven als een aanroep van de parameter toohello.</span><span class="sxs-lookup"><span data-stu-id="4c319-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="4c319-189">U kunt gedetailleerde beschrijvingen van alle Hallo parameters krijgen door het uitvoeren van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="4c319-190">Wijzigen van een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4c319-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="4c319-191">U kunt bepaalde eigenschappen van een ExpressRoute-circuit wijzigen zonder enige impact op connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="4c319-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="4c319-192">U kunt doen Hallo zonder uitvaltijd te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="4c319-193">In- of uitschakelen van een ExpressRoute premium-invoegtoepassing voor ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="4c319-194">Hallo-bandbreedte verhoging van uw ExpressRoute-circuit mits capaciteit beschikbaar op Hallo-poort.</span><span class="sxs-lookup"><span data-stu-id="4c319-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="4c319-195">Houd er rekening mee dat Hallo bandbreedte van een circuit downgraden wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4c319-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="4c319-196">Hallo softwarelicentiecontrole plan van gegevens Datalimiet tooUnlimited gegevens wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4c319-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="4c319-197">Houd er rekening mee dat veranderende Hallo softwarelicentiecontrole plan van onbeperkt tooMetered die gegevens worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4c319-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="4c319-198">U kunt inschakelen en uitschakelen *klassieke bewerkingen toestaan*.</span><span class="sxs-lookup"><span data-stu-id="4c319-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="4c319-199">Raadpleeg toohello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor meer informatie over limieten en beperkingen.</span><span class="sxs-lookup"><span data-stu-id="4c319-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="4c319-200">tooenable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="4c319-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="4c319-201">U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit inschakelen met behulp van de volgende PowerShell-cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="4c319-202">Het circuit hebt nu Hallo ExpressRoute premium-invoegtoepassing voor functies die worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4c319-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="4c319-203">Houd er rekening mee dat we facturering voor Hallo premium-invoegtoepassing mogelijkheid start zodra Hallo-opdracht met succes is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4c319-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="4c319-204">toodisable hello ExpressRoute premium-invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="4c319-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4c319-205">Deze bewerking kan mislukken als u resources die groter zijn dan wat voor Hallo standaard circuit is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="4c319-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="4c319-206">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="4c319-206">Considerations</span></span>

* <span data-ttu-id="4c319-207">U moet ervoor zorgen dat het aantal virtuele netwerken gekoppelde toohello circuit Hallo minder dan 10 voordat u van premium toostandard downgraden.</span><span class="sxs-lookup"><span data-stu-id="4c319-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="4c319-208">Als u dit doet, uw aanvraag bijwerken mislukt en u zult gefactureerd Hallo Premietarieven.</span><span class="sxs-lookup"><span data-stu-id="4c319-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="4c319-209">U moet alle virtuele netwerken in andere geopolitieke regio's ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="4c319-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="4c319-210">Als u dit doet, uw aanvraag bijwerken mislukt en u zult gefactureerd Hallo Premietarieven.</span><span class="sxs-lookup"><span data-stu-id="4c319-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="4c319-211">De routetabel moet minder dan 4000 routes voor persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="4c319-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="4c319-212">Uw tabel route is groter dan 4000 routes, Hallo BGP-sessie wordt als totdat Hallo aantal geadverteerde voorvoegsels daaronder 4.000 won't worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4c319-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="4c319-213">Premium-invoegtoepassing voor Hallo uitschakelen</span><span class="sxs-lookup"><span data-stu-id="4c319-213">Disable hello premium add-on</span></span>
<span data-ttu-id="4c319-214">U kunt Hallo ExpressRoute premium-invoegtoepassing voor uw bestaande circuit uitschakelen met behulp van de volgende PowerShell-cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="4c319-215">bandbreedte tooupdate hello ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4c319-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="4c319-216">Controleer de Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) voor ondersteunde bandbreedte-opties voor uw provider.</span><span class="sxs-lookup"><span data-stu-id="4c319-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="4c319-217">U kunt de grootte die groter is dan Hallo grootte van uw bestaande circuit zolang Hallo fysieke poort (waarop uw circuit is gemaakt) kunnen verzamelen.</span><span class="sxs-lookup"><span data-stu-id="4c319-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c319-218">Mogelijk hebt u toorecreate hello ExpressRoute-circuit als er onvoldoende capaciteit op de bestaande poort Hallo.</span><span class="sxs-lookup"><span data-stu-id="4c319-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="4c319-219">U kunt Hallo circuit niet upgraden als er geen extra capaciteit beschikbaar is op die locatie.</span><span class="sxs-lookup"><span data-stu-id="4c319-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="4c319-220">U kunt Hallo bandbreedte van een ExpressRoute-circuit zonder onderbreking niet reduceren.</span><span class="sxs-lookup"><span data-stu-id="4c319-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="4c319-221">Downgraden bandbreedte, moet u toodeprovision hello ExpressRoute-circuit en vervolgens opnieuw inrichten van nieuwe ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="4c319-222">Een circuit vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="4c319-222">Resize a circuit</span></span>

<span data-ttu-id="4c319-223">Nadat u welke grootte die u nodig hebt besluit, kunt u uw circuit Hallo opdracht tooresize volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4c319-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="4c319-224">Uw circuit wordt zijn grote Hallo Microsoft zijde.</span><span class="sxs-lookup"><span data-stu-id="4c319-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="4c319-225">U moet contact opnemen met uw connectiviteit provider tooupdate-configuraties van hun kant toomatch deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="4c319-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="4c319-226">Opmerking dat we start u facturering voor Hallo bandbreedte optie vanaf dit punt op bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="4c319-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="4c319-227">Als u de volgende fout bij het verhogen van de bandbreedte van het circuit Hallo Hallo ziet, betekent dit er is onvoldoende bandbreedte links op Hallo van de fysieke poort waarop uw bestaande circuit is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c319-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="4c319-228">U hebt toodelete dit circuit en een nieuwe circuit Hallo grootte die u moet maken.</span><span class="sxs-lookup"><span data-stu-id="4c319-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="4c319-229">Opheffen van inrichting en een ExpressRoute-circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c319-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="4c319-230">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="4c319-230">Considerations</span></span>

* <span data-ttu-id="4c319-231">U moet alle virtuele netwerken vanuit Hallo ExpressRoute-circuit voor deze bewerking toosucceed ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="4c319-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="4c319-232">Controleer toosee als er geen virtuele netwerken die zijn gekoppeld toohello circuit als deze bewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4c319-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="4c319-233">Als Hallo ExpressRoute-circuit serviceprovider Inrichtingsstatus **inrichten** of **ingericht** moet u werken met uw serviceprovider toodeprovision Hallo circuit op hun kant.</span><span class="sxs-lookup"><span data-stu-id="4c319-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="4c319-234">We gaan tooreserve resources en kosten in rekening brengen totdat Hallo serviceprovider inrichting Hallo circuit is voltooid en een melding van ons.</span><span class="sxs-lookup"><span data-stu-id="4c319-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="4c319-235">Als serviceprovider Hallo heeft gemaakt Hallo circuit (Hallo serviceprovider Inrichtingsstatus te is ingesteld**niet ingericht**) kunt u Hallo circuit verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4c319-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="4c319-236">Hiermee stopt u facturering voor Hallo circuit.</span><span class="sxs-lookup"><span data-stu-id="4c319-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="4c319-237">Een circuit verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c319-237">Delete a circuit</span></span>

<span data-ttu-id="4c319-238">U kunt uw ExpressRoute-circuit verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="4c319-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="4c319-239">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c319-239">Next steps</span></span>
<span data-ttu-id="4c319-240">Nadat u het circuit hebt gemaakt, moet u Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c319-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="4c319-241">Maken en aanpassen van routering voor ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4c319-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="4c319-242">Koppelen van uw virtuele netwerk tooyour ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="4c319-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

