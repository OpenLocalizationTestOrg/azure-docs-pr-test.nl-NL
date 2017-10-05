---
title: 'Een virtueel netwerk koppelen aan een ExpressRoute-circuit: PowerShell: klassieke: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe u virtuele netwerken (vnet's) koppelen aan ExpressRoute-circuits met behulp van het klassieke implementatiemodel en PowerShell.
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
ms.openlocfilehash: 8df8a4c6ff0897c821e13248e0494b17e1a4992d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="77258-103">Een virtueel netwerk verbinden met een ExpressRoute-circuit met behulp van PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="77258-103">Connect a virtual network to an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77258-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="77258-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="77258-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77258-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="77258-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="77258-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="77258-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="77258-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="77258-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="77258-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="77258-109">In dit artikel helpt u virtuele netwerken (vnet's) koppelen aan Azure ExpressRoute-circuits met behulp van het klassieke implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77258-109">This article will help you link virtual networks (VNets) to Azure ExpressRoute circuits by using the classic deployment model and PowerShell.</span></span> <span data-ttu-id="77258-110">Virtuele netwerken in hetzelfde abonnement kunnen zijn of deel kunnen uitmaken van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="77258-110">Virtual networks can either be in the same subscription or can be part of another subscription.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="77258-111">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="77258-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a><span data-ttu-id="77258-112">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="77258-112">Configuration prerequisites</span></span>
1. <span data-ttu-id="77258-113">U moet de meest recente versie van de Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="77258-113">You need the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="77258-114">U kunt de meest recente PowerShell-modules downloaden van de PowerShell-sectie van de [pagina Azure Downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="77258-114">You can download the latest PowerShell modules from the PowerShell section of the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="77258-115">Volg de instructies in [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor stapsgewijze instructies voor het configureren van uw computer voor het gebruik van de Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="77258-115">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>
2. <span data-ttu-id="77258-116">U moet controleren de [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="77258-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
3. <span data-ttu-id="77258-117">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="77258-117">You must have an active ExpressRoute circuit.</span></span>
   * <span data-ttu-id="77258-118">Volg de instructies voor [maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en vraag uw connectiviteitsprovider het circuit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="77258-118">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have your connectivity provider enable the circuit.</span></span>
   * <span data-ttu-id="77258-119">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="77258-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="77258-120">Zie de [Configure routing](expressroute-howto-routing-classic.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="77258-120">See the [Configure routing](expressroute-howto-routing-classic.md) article for routing instructions.</span></span>
   * <span data-ttu-id="77258-121">Zorg ervoor dat de persoonlijke Azure-peering is geconfigureerd en van de BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="77258-121">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
   * <span data-ttu-id="77258-122">U hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="77258-122">You must have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="77258-123">Volg de instructies voor [een virtueel netwerk configureren voor ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="77258-123">Follow the instructions to [configure a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

<span data-ttu-id="77258-124">U kunt maximaal 10 virtuele netwerken koppelen aan een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="77258-124">You can link up to 10 virtual networks to an ExpressRoute circuit.</span></span> <span data-ttu-id="77258-125">Alle virtuele netwerken moeten zich in dezelfde geopolitieke regio.</span><span class="sxs-lookup"><span data-stu-id="77258-125">All virtual networks must be in the same geopolitical region.</span></span> <span data-ttu-id="77258-126">U kunt een groter aantal virtuele netwerken aan uw ExpressRoute-circuit of koppeling virtuele netwerken die zich in andere geopolitieke regio's als u de invoegtoepassing ExpressRoute premium ingeschakeld koppelen.</span><span class="sxs-lookup"><span data-stu-id="77258-126">You can link a larger number of virtual networks to your ExpressRoute circuit, or link virtual networks that are in other geopolitical regions if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="77258-127">Controleer de [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over de premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="77258-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="77258-128">Een virtueel netwerk in hetzelfde abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="77258-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="77258-129">U kunt een virtueel netwerk koppelen aan een ExpressRoute-circuit met de volgende cmdlet.</span><span class="sxs-lookup"><span data-stu-id="77258-129">You can link a virtual network to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="77258-130">Zorg ervoor dat de virtuele netwerkgateway wordt gemaakt en gereed is voor het koppelen voordat u de cmdlet uitvoert.</span><span class="sxs-lookup"><span data-stu-id="77258-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet.</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="77258-131">Een virtueel netwerk in een ander abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="77258-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="77258-132">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="77258-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="77258-133">De volgende afbeelding ziet een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="77258-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="77258-134">Elk van de kleinere clouds binnen de grote cloud wordt gebruikt voor abonnementen die bij verschillende afdelingen binnen een organisatie horen te vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="77258-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="77258-135">Elk van de afdelingen binnen de organisatie kan hun eigen abonnement gebruiken voor het implementeren van hun services--, maar de afdelingen één ExpressRoute-circuit terugverbinding maken met uw on-premises netwerk kan delen.</span><span class="sxs-lookup"><span data-stu-id="77258-135">Each of the departments within the organization can use their own subscription for deploying their services--but the departments can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="77258-136">Één afdeling (in dit voorbeeld: IT) kunt eigenaar van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="77258-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="77258-137">Andere abonnementen binnen de organisatie kunnen het ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77258-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="77258-138">Verbindingen en bandbreedte kosten voor het specifieke circuit wordt toegepast op de eigenaar van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="77258-138">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="77258-139">Alle virtuele netwerken delen de dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="77258-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a><span data-ttu-id="77258-141">Beheer</span><span class="sxs-lookup"><span data-stu-id="77258-141">Administration</span></span>
<span data-ttu-id="77258-142">De *circuiteigenaar* is de beheerder/CO-beheerder van het abonnement waarin het ExpressRoute-circuit is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="77258-142">The *circuit owner* is the administrator/coadministrator of the subscription in which the ExpressRoute circuit is created.</span></span> <span data-ttu-id="77258-143">De circuiteigenaar van het kan beheerders/coadministrators van andere abonnementen, aangeduid als machtigen *circuit gebruikers*, om de specifieke circuit waarvan ze eigenaar moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77258-143">The circuit owner can authorize administrators/coadministrators of other subscriptions, referred to as *circuit users*, to use the dedicated circuit that they own.</span></span> <span data-ttu-id="77258-144">Circuit gebruikers die zijn gemachtigd voor het gebruik van de organisatie ExpressRoute-circuit kunnen het virtuele netwerk in het abonnement koppelen aan het ExpressRoute-circuit nadat ze zijn gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="77258-144">Circuit users who are authorized to use the organization's ExpressRoute circuit can link the virtual network in their subscription to the ExpressRoute circuit after they are authorized.</span></span>

<span data-ttu-id="77258-145">De circuiteigenaar van het bevoegd is om te wijzigen en machtigingen intrekt op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="77258-145">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="77258-146">Intrekken van een vergunning leidt ertoe dat alle koppelingen worden verwijderd uit het abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="77258-146">Revoking an authorization will result in all links being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="77258-147">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="77258-147">Circuit owner operations</span></span>

<span data-ttu-id="77258-148">**Maken van een vergunning**</span><span class="sxs-lookup"><span data-stu-id="77258-148">**Creating an authorization**</span></span>

<span data-ttu-id="77258-149">De circuiteigenaar van het machtigt de beheerders van andere abonnementen te gebruiken van het opgegeven circuit.</span><span class="sxs-lookup"><span data-stu-id="77258-149">The circuit owner authorizes the administrators of other subscriptions to use the specified circuit.</span></span> <span data-ttu-id="77258-150">In het volgende voorbeeld kan de beheerder van het circuit (Contoso IT) de beheerder van een ander abonnement (Dev-Test) maximaal twee virtuele netwerken koppelen aan het circuit.</span><span class="sxs-lookup"><span data-stu-id="77258-150">In the following example, the administrator of the circuit (Contoso IT) enables the administrator of another subscription (Dev-Test) to link up to two virtual networks to the circuit.</span></span> <span data-ttu-id="77258-151">De Contoso-IT-beheerder maakt dit door op te geven van de Microsoft Developer-Test-ID.</span><span class="sxs-lookup"><span data-stu-id="77258-151">The Contoso IT administrator enables this by specifying the Dev-Test Microsoft ID.</span></span> <span data-ttu-id="77258-152">De cmdlet verzenden geen e-mail naar de opgegeven id van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77258-152">The cmdlet doesn't send email to the specified Microsoft ID.</span></span> <span data-ttu-id="77258-153">De circuiteigenaar van het moet expliciet melden andere eigenaar van het abonnement dat de autorisatie voltooid is.</span><span class="sxs-lookup"><span data-stu-id="77258-153">The circuit owner needs to explicitly notify the other subscription owner that the authorization is complete.</span></span>

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

<span data-ttu-id="77258-154">**Machtigingen controleren**</span><span class="sxs-lookup"><span data-stu-id="77258-154">**Reviewing authorizations**</span></span>

<span data-ttu-id="77258-155">De circuiteigenaar van het Neem alle machtigingen die zijn uitgegeven voor een bepaalde circuit door de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="77258-155">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

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


<span data-ttu-id="77258-156">**Autorisaties bijwerken**</span><span class="sxs-lookup"><span data-stu-id="77258-156">**Updating authorizations**</span></span>

<span data-ttu-id="77258-157">De circuiteigenaar van het kunt autorisaties wijzigen met behulp van de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="77258-157">The circuit owner can modify authorizations by using the following cmdlet:</span></span>

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


<span data-ttu-id="77258-158">**Autorisaties verwijderen**</span><span class="sxs-lookup"><span data-stu-id="77258-158">**Deleting authorizations**</span></span>

<span data-ttu-id="77258-159">De circuiteigenaar van het kan intrekken/delete autorisaties voor de gebruiker door de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="77258-159">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a><span data-ttu-id="77258-160">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="77258-160">Circuit user operations</span></span>

<span data-ttu-id="77258-161">**Machtigingen controleren**</span><span class="sxs-lookup"><span data-stu-id="77258-161">**Reviewing authorizations**</span></span>

<span data-ttu-id="77258-162">De circuit-gebruiker kunt autorisaties bekijken met behulp van de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="77258-162">The circuit user can review authorizations by using the following cmdlet:</span></span>

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

<span data-ttu-id="77258-163">**Wisselt autorisaties voor koppelingen**</span><span class="sxs-lookup"><span data-stu-id="77258-163">**Redeeming link authorizations**</span></span>

<span data-ttu-id="77258-164">De circuit-gebruiker kan de volgende cmdlet als u wilt gebruikmaken van een koppeling autorisatie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="77258-164">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

<span data-ttu-id="77258-165">Deze opdracht uitvoeren in het nieuwe gekoppelde abonnement voor het virtuele netwerk:</span><span class="sxs-lookup"><span data-stu-id="77258-165">Run this command in the newly linked subscription for the virtual network:</span></span>

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a><span data-ttu-id="77258-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77258-166">Next steps</span></span>
<span data-ttu-id="77258-167">Voor meer informatie over ExpressRoute raadpleegt u de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="77258-167">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

