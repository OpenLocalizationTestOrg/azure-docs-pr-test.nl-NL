---
title: 'Hoe tooconfigure routering (peering) voor een ExpressRoute-circuit: Azure: klassieke | Microsoft Docs'
description: Dit artikel begeleidt u bij Hallo stappen voor het maken en inrichten Hallo persoonlijke, openbare en Microsoft-peering van een ExpressRoute-circuit. Dit artikel leest u hoe de status van toocheck hello, bijwerken of verwijderen van peerings voor uw circuit.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="48615-104">Maken en wijzigen van de peering voor een ExpressRoute-circuit (klassiek)</span><span class="sxs-lookup"><span data-stu-id="48615-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48615-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="48615-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="48615-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48615-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="48615-107">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="48615-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="48615-108">Video - persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="48615-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="48615-109">Video - openbare peering</span><span class="sxs-lookup"><span data-stu-id="48615-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="48615-110">Video - Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="48615-111">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="48615-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="48615-112">Dit artikel begeleidt u bij Hallo stappen toocreate en beheren van routeringsconfiguratie voor een ExpressRoute-circuit met PowerShell en Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="48615-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="48615-113">Hallo stappen hieronder ziet u ook hoe toocheck Hallo status, bijwerken, of verwijder en inrichting ervan ongedaan peerings voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="48615-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="48615-114">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="48615-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="48615-115">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="48615-115">Configuration prerequisites</span></span>
* <span data-ttu-id="48615-116">U moet de meest recente versie Hallo van hello Azure Service Management (SM) PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="48615-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="48615-117">Zie voor meer informatie [aan de slag met Azure PowerShell-cmdlets](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48615-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="48615-118">Zorg ervoor dat u Hallo hebt bekeken [vereisten](expressroute-prerequisites.md) pagina hello [routeringsvereisten](expressroute-routing.md) pagina en Hallo [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="48615-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="48615-119">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="48615-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="48615-120">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en Hallo circuit inschakelen door de connectiviteitsprovider voordat u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="48615-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="48615-121">Hallo ExpressRoute-circuit moet zich in een status ingericht en zijn ingeschakeld voor u toobe kunnen toorun Hallo cmdlets die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="48615-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48615-122">Deze instructies zijn alleen van toepassing toocircuits gemaakt met serviceproviders die services voor Layer 2-connectiviteit aanbieden.</span><span class="sxs-lookup"><span data-stu-id="48615-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="48615-123">Als u gebruikmaakt van een serviceprovider die beheerde Laag-3-services aanbiedt (meestal een IPVPN, zoals MPLS), zal de connectiviteitsprovider routering voor u configureren en beheren.</span><span class="sxs-lookup"><span data-stu-id="48615-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="48615-124">U kunt een, twee of alle drie de peerings (Azure privé, Azure openbaar en Microsoft) voor een ExpressRoute-circuit configureren.</span><span class="sxs-lookup"><span data-stu-id="48615-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="48615-125">U kunt peerings configureren in elke gewenste volgorde.</span><span class="sxs-lookup"><span data-stu-id="48615-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="48615-126">Echter, moet u ervoor zorgen dat Hallo configuratie van elke peering een tegelijk te voltooien.</span><span class="sxs-lookup"><span data-stu-id="48615-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="48615-127">Meld u bij tooyour Azure-account en een abonnement selecteren</span><span class="sxs-lookup"><span data-stu-id="48615-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="48615-128">Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen.</span><span class="sxs-lookup"><span data-stu-id="48615-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="48615-129">Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="48615-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="48615-130">Controleer de abonnementen Hallo voor Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="48615-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="48615-131">Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="48615-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="48615-132">Gebruik vervolgens Hallo cmdlet tooadd na uw Azure-abonnement tooPowerShell Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="48615-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="48615-133">Persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-133">Azure private peering</span></span>
<span data-ttu-id="48615-134">Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van persoonlijke peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="48615-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="48615-135">toocreate persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="48615-136">**Importeer Hallo PowerShell-module voor ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="48615-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="48615-137">U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="48615-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="48615-138">Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="48615-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="48615-139">**Maak een ExpressRoute-circuit.**</span><span class="sxs-lookup"><span data-stu-id="48615-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="48615-140">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="48615-141">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48615-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="48615-142">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="48615-143">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="48615-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="48615-144">**Controleer Hallo ExpressRoute-circuit tooensure die deze is ingericht.**</span><span class="sxs-lookup"><span data-stu-id="48615-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="48615-145">Als Hallo ExpressRoute-circuit is ingericht en ook is ingeschakeld, moet u eerst toosee controleren.</span><span class="sxs-lookup"><span data-stu-id="48615-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="48615-146">Zie Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="48615-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="48615-147">Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat.</span><span class="sxs-lookup"><span data-stu-id="48615-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="48615-148">Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.</span><span class="sxs-lookup"><span data-stu-id="48615-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="48615-149">**Configureer persoonlijke Azure-peering voor Hallo circuit.**</span><span class="sxs-lookup"><span data-stu-id="48615-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="48615-150">Zorg ervoor dat u de volgende items voordat u met de volgende stappen Hallo verdergaat Hallo hebt:</span><span class="sxs-lookup"><span data-stu-id="48615-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="48615-151">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="48615-152">Dit mag geen deel uitmaken van een adresruimte die is gereserveerd voor virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="48615-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="48615-153">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="48615-154">Dit mag geen deel uitmaken van een adresruimte die is gereserveerd voor virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="48615-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="48615-155">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="48615-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="48615-156">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="48615-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="48615-157">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="48615-157">AS number for peering.</span></span> <span data-ttu-id="48615-158">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48615-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="48615-159">U kunt een persoonlijk AS-nummer voor deze peering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48615-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="48615-160">Zorg dat u niet 65515 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48615-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="48615-161">Een MD5-hash als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="48615-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="48615-162">**Dit is optioneel**.</span><span class="sxs-lookup"><span data-stu-id="48615-162">**This is optional**.</span></span>
     
    <span data-ttu-id="48615-163">U kunt uitvoeren Hallo cmdlet tooconfigure persoonlijke Azure-peering voor uw circuit te volgen.</span><span class="sxs-lookup"><span data-stu-id="48615-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="48615-164">Nieuwe AzureBGPPeering - AccessType persoonlijke - ServiceKey ' *** ' - PrimaryPeerSubnet '10.0.0.0/30' - SecondaryPeerSubnet '10.0.0.4/30' - PeerAsn 1234 - VlanId 100</span><span class="sxs-lookup"><span data-stu-id="48615-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="48615-165">U kunt Hallo onderstaande cmdlet gebruiken als u een MD5-hash toouse kiest.</span><span class="sxs-lookup"><span data-stu-id="48615-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="48615-166">Nieuwe AzureBGPPeering - AccessType persoonlijke - ServiceKey ' *** ' - PrimaryPeerSubnet '10.0.0.0/30' - SecondaryPeerSubnet '10.0.0.4/30' - PeerAsn 1234 - VlanId 100 - SharedKey 'A1B2C3D4'</span><span class="sxs-lookup"><span data-stu-id="48615-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="48615-167">Zorg dat u uw AS-nummer als peering-ASN opgeeft, niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="48615-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="48615-168">tooview Azure persoonlijke peering details</span><span class="sxs-lookup"><span data-stu-id="48615-168">tooview Azure private peering details</span></span>
<span data-ttu-id="48615-169">U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen</span><span class="sxs-lookup"><span data-stu-id="48615-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="48615-170">tooupdate Azure configuratie van persoonlijke peering</span><span class="sxs-lookup"><span data-stu-id="48615-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="48615-171">U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="48615-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="48615-172">In onderstaande Hallo voorbeeld, wordt Hallo VLAN-ID van het circuit Hallo van 100 too500 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="48615-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="48615-173">toodelete persoonlijke Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-173">toodelete Azure private peering</span></span>
<span data-ttu-id="48615-174">U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="48615-175">U moet ervoor zorgen dat alle virtuele netwerken losgekoppeld van Hallo ExpressRoute-circuit zijn voordat u deze cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="48615-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="48615-176">Openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-176">Azure public peering</span></span>
<span data-ttu-id="48615-177">Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van hello Azure configuratie van openbare peering voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="48615-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="48615-178">toocreate openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="48615-179">**Importeer Hallo PowerShell-module voor ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="48615-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="48615-180">U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="48615-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="48615-181">Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="48615-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="48615-182">**Een ExpressRoute-circuit maken**</span><span class="sxs-lookup"><span data-stu-id="48615-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="48615-183">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="48615-184">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable openbare peering voor u Azure aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48615-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="48615-185">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="48615-186">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="48615-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="48615-187">**Deze is voorzien van ExpressRoute-circuit tooensure controleren**</span><span class="sxs-lookup"><span data-stu-id="48615-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="48615-188">Als Hallo ExpressRoute-circuit is ingericht en ook is ingeschakeld, moet u eerst toosee controleren.</span><span class="sxs-lookup"><span data-stu-id="48615-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="48615-189">Zie Hallo voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="48615-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="48615-190">Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat.</span><span class="sxs-lookup"><span data-stu-id="48615-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="48615-191">Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.</span><span class="sxs-lookup"><span data-stu-id="48615-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="48615-192">**Configureer openbare Azure-peering voor Hallo circuit**</span><span class="sxs-lookup"><span data-stu-id="48615-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="48615-193">Zorg ervoor dat u de volgende informatie voordat u verder Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="48615-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="48615-194">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="48615-195">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="48615-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="48615-196">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="48615-197">Dit moet een geldig openbaar IPv4-voorvoegsel zijn.</span><span class="sxs-lookup"><span data-stu-id="48615-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="48615-198">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="48615-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="48615-199">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="48615-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="48615-200">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="48615-200">AS number for peering.</span></span> <span data-ttu-id="48615-201">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48615-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="48615-202">Een MD5-hash als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="48615-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="48615-203">**Dit is optioneel**.</span><span class="sxs-lookup"><span data-stu-id="48615-203">**This is optional**.</span></span>
     
    <span data-ttu-id="48615-204">Kunt u de volgende cmdlet tooconfigure openbare Azure-peering voor uw circuit Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="48615-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="48615-205">Nieuwe AzureBGPPeering - AccessType openbare - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - PeerAsn 1234 - VlanId 200</span><span class="sxs-lookup"><span data-stu-id="48615-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="48615-206">U kunt Hallo onderstaande cmdlet gebruiken als u een MD5-hash toouse kiezen</span><span class="sxs-lookup"><span data-stu-id="48615-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="48615-207">Nieuwe AzureBGPPeering - AccessType openbare - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - PeerAsn 1234 - VlanId 200 - SharedKey 'A1B2C3D4'</span><span class="sxs-lookup"><span data-stu-id="48615-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="48615-208">Zorg dat u uw AS-nummer als peering-ASN opgeeft en niet als klant-ASN.</span><span class="sxs-lookup"><span data-stu-id="48615-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="48615-209">tooview Azure openbare peering details</span><span class="sxs-lookup"><span data-stu-id="48615-209">tooview Azure public peering details</span></span>
<span data-ttu-id="48615-210">U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen</span><span class="sxs-lookup"><span data-stu-id="48615-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="48615-211">configuratie van openbare peering Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="48615-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="48615-212">U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken</span><span class="sxs-lookup"><span data-stu-id="48615-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="48615-213">Hallo VLAN-ID van het circuit Hallo wordt van 200 too600 in Hallo bovenstaande voorbeeld bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="48615-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="48615-214">toodelete openbare Azure-peering</span><span class="sxs-lookup"><span data-stu-id="48615-214">toodelete Azure public peering</span></span>
<span data-ttu-id="48615-215">U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo</span><span class="sxs-lookup"><span data-stu-id="48615-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="48615-216">Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-216">Microsoft peering</span></span>
<span data-ttu-id="48615-217">Deze sectie bevat instructies over hoe toocreate, verkrijgen, bijwerken en verwijderen van configuratie Hallo Microsoft-peering gebruiken voor een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="48615-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="48615-218">toocreate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="48615-219">**Importeer Hallo PowerShell-module voor ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="48615-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="48615-220">U moet hello Azure en een ExpressRoute-modules importeren in Hallo PowerShell-sessie in de volgorde toostart met Hallo ExpressRoute-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="48615-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="48615-221">Voer Hallo volgende opdrachten tooimport hello Azure en een ExpressRoute-modules in Hallo PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="48615-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="48615-222">**Een ExpressRoute-circuit maken**</span><span class="sxs-lookup"><span data-stu-id="48615-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="48615-223">Ga als volgt Hallo instructies toocreate een [ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en laat het inrichten door de connectiviteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="48615-224">Als uw connectiviteitsprovider beheerde laag-3-services biedt, kunt u uw connectiviteit provider tooenable Azure persoonlijke peering voor u aanvragen.</span><span class="sxs-lookup"><span data-stu-id="48615-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="48615-225">In dat geval hoeft u niet toofollow instructies in de volgende secties Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="48615-226">Als uw connectiviteitsprovider routering voor u, na het maken van het circuit niet beheert volgt u onderstaande Hallo-instructies.</span><span class="sxs-lookup"><span data-stu-id="48615-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="48615-227">**Deze is voorzien van ExpressRoute-circuit tooensure controleren**</span><span class="sxs-lookup"><span data-stu-id="48615-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="48615-228">Als Hallo ExpressRoute-circuit ingericht en ingeschakeld is, moet u eerst toosee controleren.</span><span class="sxs-lookup"><span data-stu-id="48615-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="48615-229">Zorg ervoor dat Hallo circuit ingericht en ingeschakeld bevat.</span><span class="sxs-lookup"><span data-stu-id="48615-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="48615-230">Als dit niet het geval is, samen met uw provider connectiviteit tooget uw circuit toohello vereist toestand en status.</span><span class="sxs-lookup"><span data-stu-id="48615-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="48615-231">**Configureer Microsoft-peering voor Hallo circuit**</span><span class="sxs-lookup"><span data-stu-id="48615-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="48615-232">Zorg ervoor dat er Hallo volgende informatie voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="48615-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="48615-233">Een/30 subnet voor de primaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="48615-234">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="48615-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="48615-235">Een/30 subnet voor de secundaire koppeling Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="48615-236">Dit moet een geldig openbaar IPv4-voorvoegsel zijn waarvan u eigenaar bent en dat is geregistreerd in een RIR/IRR.</span><span class="sxs-lookup"><span data-stu-id="48615-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="48615-237">Een geldige VLAN-ID tooestablish deze peering.</span><span class="sxs-lookup"><span data-stu-id="48615-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="48615-238">Zorg ervoor dat er geen andere peering in Hallo circuit Hallo maakt gebruik van dezelfde VLAN-ID.</span><span class="sxs-lookup"><span data-stu-id="48615-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="48615-239">AS-nummer voor peering.</span><span class="sxs-lookup"><span data-stu-id="48615-239">AS number for peering.</span></span> <span data-ttu-id="48615-240">U kunt 2-bytes en 4-bytes AS-nummers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="48615-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="48615-241">Geadverteerde voorvoegsels: U moet een lijst verstrekken van alle voorvoegsels die u van plan bent tooadvertise via Hallo BGP-sessie.</span><span class="sxs-lookup"><span data-stu-id="48615-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="48615-242">Alleen openbare IP-adresvoorvoegsels worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="48615-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="48615-243">Als u van plan een reeks voorvoegsels toosend bent, kunt u een door komma's gescheiden lijst verzenden.</span><span class="sxs-lookup"><span data-stu-id="48615-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="48615-244">Deze voorvoegsels moeten geregistreerde tooyou in een RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="48615-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="48615-245">Klant-ASN: Als u voorvoegsels die niet zijn ingeschreven toohello peering als getal worden geadverteerd, kunt u Hallo opgeven als getal toowhich die ze zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="48615-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="48615-246">**Dit is optioneel**.</span><span class="sxs-lookup"><span data-stu-id="48615-246">**This is optional**.</span></span>
   * <span data-ttu-id="48615-247">Naam van Routeringsregister: Kunt u Hallo RIR / IRR met betrekking tot welke Hallo als number en prefixes zijn geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="48615-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="48615-248">Een MD5-hash, als u ervoor toouse een kiest.</span><span class="sxs-lookup"><span data-stu-id="48615-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="48615-249">**Dit is optioneel.**</span><span class="sxs-lookup"><span data-stu-id="48615-249">**This is optional.**</span></span>
     
    <span data-ttu-id="48615-250">Kunt u de volgende cmdlet tooconfigure Microsoft pering voor uw circuit Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="48615-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="48615-251">Nieuwe AzureBGPPeering - AccessType Microsoft - ServiceKey ' *** ' - PrimaryPeerSubnet '131.107.0.0/30' - SecondaryPeerSubnet '131.107.0.4/30' - VlanId 300 - PeerAsn 1234 - CustomerAsn. 2245 - AdvertisedPublicPrefixes '123.0.0.0/30' - RoutingRegistryName 'ARIN' - SharedKey 'A1B2C3D4'</span><span class="sxs-lookup"><span data-stu-id="48615-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="48615-252">details van tooview Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="48615-253">U kunt met behulp van de volgende cmdlet Hallo configuratiedetails ophalen.</span><span class="sxs-lookup"><span data-stu-id="48615-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="48615-254">configuratie van tooupdate Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="48615-255">U kunt elk deel van Hallo-configuratie met behulp van de volgende cmdlet Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="48615-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="48615-256">toodelete Microsoft-peering</span><span class="sxs-lookup"><span data-stu-id="48615-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="48615-257">U kunt de peeringconfiguratie verwijderen door het uitvoeren van de volgende cmdlet Hallo.</span><span class="sxs-lookup"><span data-stu-id="48615-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="48615-258">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48615-258">Next steps</span></span>
<span data-ttu-id="48615-259">Vervolgens [koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="48615-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="48615-260">Zie voor meer informatie over werkstromen [ExpressRoute-werkstromen](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="48615-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="48615-261">Voor meer informatie over circuitpeering raadpleegt u [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).</span><span class="sxs-lookup"><span data-stu-id="48615-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

