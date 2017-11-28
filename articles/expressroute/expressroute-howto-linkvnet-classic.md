---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: PowerShell: klassieke: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo klassieke implementatiemodel en PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="25864-103">Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="25864-103">Connect a virtual network tooan ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25864-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="25864-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="25864-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25864-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="25864-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="25864-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="25864-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="25864-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="25864-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="25864-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="25864-109">In dit artikel helpt u virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen via Hallo klassieke implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25864-109">This article will help you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello classic deployment model and PowerShell.</span></span> <span data-ttu-id="25864-110">Virtuele netwerken kunnen hetzelfde abonnement Hallo of zijn kan deel uitmaken van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="25864-110">Virtual networks can either be in hello same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="25864-111">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="25864-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="25864-112">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="25864-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="25864-113">Moet u de meest recente versie Hallo van hello Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="25864-113">You need hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="25864-114">U kunt de meest recente PowerShell-modules Hallo downloaden van Hallo PowerShell sectie Hallo [pagina Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="25864-114">You can download hello latest PowerShell modules from hello PowerShell section of hello [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="25864-115">Volg de instructies in Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor stapsgewijze instructies voor het tooconfigure uw computer toouse hello Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="25864-115">Follow hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>
2. <span data-ttu-id="25864-116">U moet tooreview hello [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="25864-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="25864-117">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="25864-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="25864-118">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en vraag uw connectiviteitsprovider Hallo circuit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25864-118">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable hello circuit.</span></span>
   * <span data-ttu-id="25864-119">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="25864-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="25864-120">Zie Hallo [Configure routing](expressroute-howto-routing-classic.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="25864-120">See hello [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="25864-121">Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25864-121">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="25864-122">U hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="25864-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="25864-123">Hallo-instructies te volgen[een virtueel netwerk configureren voor ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="25864-123">Follow hello instructions too[configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="25864-124">U kunt een koppeling van too10 virtuele netwerken tooan ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="25864-124">You can link up too10 virtual networks tooan ExpressRoute circuit.</span></span> <span data-ttu-id="25864-125">Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio.</span><span class="sxs-lookup"><span data-stu-id="25864-125">All virtual networks must be in hello same geopolitical region.</span></span> <span data-ttu-id="25864-126">U kunt een groter aantal virtuele netwerken tooyour ExpressRoute-circuit koppelen of koppelen van virtuele netwerken die zich in andere geopolitieke regio's als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="25864-126">You can link a larger number of virtual networks tooyour ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="25864-127">Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="25864-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="25864-128">Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="25864-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="25864-129">U kunt een virtueel netwerk tooan ExpressRoute-circuit met behulp van de volgende cmdlet Hallo koppelen.</span><span class="sxs-lookup"><span data-stu-id="25864-129">You can link a virtual network tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="25864-130">Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u het Hallo-cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="25864-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="25864-131">Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="25864-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="25864-132">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="25864-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="25864-133">Hallo volgende afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="25864-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="25864-134">Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie.</span><span class="sxs-lookup"><span data-stu-id="25864-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="25864-135">Alle Hallo afdelingen binnen Hallo organisatie kan hun eigen abonnement gebruiken voor het implementeren van hun services-- maar Hallo afdelingen een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kan delen.</span><span class="sxs-lookup"><span data-stu-id="25864-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but hello departments can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="25864-136">Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="25864-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="25864-137">Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25864-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="25864-138">Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="25864-138">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="25864-139">Alle virtuele netwerken Hallo delen dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="25864-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="25864-141">Beheer</span><span class="sxs-lookup"><span data-stu-id="25864-141">Administration</span></span>
<span data-ttu-id="25864-142">Hallo *circuiteigenaar* is Hallo beheerder/CO-beheerder van het Hallo-abonnement in welke Hallo ExpressRoute circuit is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25864-142">hello *circuit owner* is hello administrator/coadministrator of hello subscription in which hello ExpressRoute circuit is created.</span></span> <span data-ttu-id="25864-143">Hallo circuiteigenaar kan machtigen beheerders/coadministrators van andere abonnementen, waarnaar wordt verwezen tooas *circuit gebruikers*, toouse Hallo dedicated circuit waarvan ze eigenaar.</span><span class="sxs-lookup"><span data-stu-id="25864-143">hello circuit owner can authorize administrators/coadministrators of other subscriptions, referred tooas *circuit users*, toouse hello dedicated circuit that they own.</span></span> <span data-ttu-id="25864-144">Circuit-gebruikers die geautoriseerd toouse Hallo organisatie ExpressRoute-circuit kan zijn koppelen Hallo virtuele netwerk in hun abonnement toohello ExpressRoute-circuit nadat ze zijn gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="25864-144">Circuit users who are authorized toouse hello organization's ExpressRoute circuit can link hello virtual network in their subscription toohello ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="25864-145">Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="25864-145">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="25864-146">Intrekken van een vergunning leidt ertoe dat alle koppelingen worden verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="25864-146">Revoking an authorization will result in all links being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="25864-147">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="25864-147">Circuit owner operations</span></span>

<span data-ttu-id="25864-148">**Maken van een vergunning**</span><span class="sxs-lookup"><span data-stu-id="25864-148">**Creating an authorization**</span></span>

<span data-ttu-id="25864-149">Hallo circuiteigenaar machtigt Hallo beheerders van andere abonnementen toouse Hallo opgegeven circuit.</span><span class="sxs-lookup"><span data-stu-id="25864-149">hello circuit owner authorizes hello administrators of other subscriptions toouse hello specified circuit.</span></span> <span data-ttu-id="25864-150">Hallo beheerder van Hallo circuit (Contoso IT) kunt Hallo voorbeeld te volgen, Hallo beheerder van een ander abonnement (Dev-Test) toolink up tootwo virtuele netwerken toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="25864-150">In hello following example, hello administrator of hello circuit (Contoso IT) enables hello administrator of another subscription (Dev-Test) toolink up tootwo virtual networks toohello circuit.</span></span> <span data-ttu-id="25864-151">Hallo Contoso IT-beheerder maakt dit door op te geven Hallo Microsoft Dev-Test-ID.</span><span class="sxs-lookup"><span data-stu-id="25864-151">hello Contoso IT administrator enables this by specifying hello Dev-Test Microsoft ID.</span></span> <span data-ttu-id="25864-152">Hallo-cmdlet verzenden niet e toohello opgegeven Microsoft-ID.</span><span class="sxs-lookup"><span data-stu-id="25864-152">hello cmdlet doesn't send email toohello specified Microsoft ID.</span></span> <span data-ttu-id="25864-153">Hallo circuiteigenaar moet tooexplicitly melden Hallo andere eigenaar van het abonnement dat Hallo autorisatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="25864-153">hello circuit owner needs tooexplicitly notify hello other subscription owner that hello authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="25864-154">**Machtigingen controleren**</span><span class="sxs-lookup"><span data-stu-id="25864-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="25864-155">Hallo circuiteigenaar kunt alle machtigingen die zijn uitgegeven voor een bepaalde circuit door het uitvoeren van de volgende cmdlet Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="25864-155">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


<span data-ttu-id="25864-156">**Autorisaties bijwerken**</span><span class="sxs-lookup"><span data-stu-id="25864-156">**Updating authorizations**</span></span>

<span data-ttu-id="25864-157">Hallo circuiteigenaar kunt autorisaties wijzigen met behulp van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="25864-157">hello circuit owner can modify authorizations by using hello following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="25864-158">**Autorisaties verwijderen**</span><span class="sxs-lookup"><span data-stu-id="25864-158">**Deleting authorizations**</span></span>

<span data-ttu-id="25864-159">Hallo circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door het uitvoeren van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="25864-159">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="25864-160">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="25864-160">Circuit user operations</span></span>

<span data-ttu-id="25864-161">**Machtigingen controleren**</span><span class="sxs-lookup"><span data-stu-id="25864-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="25864-162">Hallo circuitgebruikers kunt autorisaties bekijken met behulp van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="25864-162">hello circuit user can review authorizations by using hello following cmdlet:</span></span>

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

<span data-ttu-id="25864-163">**Wisselt autorisaties voor koppelingen**</span><span class="sxs-lookup"><span data-stu-id="25864-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="25864-164">Hallo circuitgebruikers kunt Hallo cmdlet tooredeem na een koppeling autorisatie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="25864-164">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="25864-165">Deze opdracht uitvoeren in het abonnement voor het virtuele netwerk Hallo Hallo zojuist gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="25864-165">Run this command in hello newly linked subscription for hello virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="25864-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25864-166">Next steps</span></span>
<span data-ttu-id="25864-167">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="25864-167">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

