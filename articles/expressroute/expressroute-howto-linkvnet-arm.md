---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: PowerShell: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo Resource Manager-implementatiemodel en PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="d422f-103">Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="d422f-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d422f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d422f-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="d422f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d422f-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="d422f-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="d422f-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="d422f-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="d422f-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="d422f-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="d422f-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="d422f-109">In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen via Hallo Resource Manager-implementatiemodel en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d422f-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="d422f-110">Virtuele netwerken in Hallo kunnen zijn hetzelfde abonnement of een deel van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="d422f-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="d422f-111">Dit artikel leest u hoe tooupdate een virtueel netwerk koppelen.</span><span class="sxs-lookup"><span data-stu-id="d422f-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d422f-112">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d422f-112">Before you begin</span></span>
* <span data-ttu-id="d422f-113">Installeer de nieuwste versie van de Hallo van hello Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="d422f-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="d422f-114">Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d422f-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d422f-115">Bekijk Hallo [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="d422f-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="d422f-116">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="d422f-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="d422f-117">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="d422f-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="d422f-118">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d422f-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="d422f-119">Zie Hallo [routering configureren](expressroute-howto-routing-arm.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="d422f-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="d422f-120">Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d422f-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="d422f-121">Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="d422f-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="d422f-122">Hallo-instructies te volgen[maken van een virtuele netwerkgateway voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d422f-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="d422f-123">Hallo GatewayType 'ExpressRoute' niet VPN maakt gebruik van een virtuele netwerkgateway voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d422f-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="d422f-124">U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="d422f-125">Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="d422f-126">U kunt een virtuele netwerken buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d422f-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="d422f-127">Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="d422f-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="d422f-128">Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="d422f-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="d422f-129">Met behulp van de volgende cmdlet Hallo kunt u een virtueel netwerk gateway tooan ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="d422f-130">Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u de cmdlet Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d422f-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="d422f-131">Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="d422f-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="d422f-132">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="d422f-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="d422f-133">Hallo volgende afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="d422f-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="d422f-134">Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie.</span><span class="sxs-lookup"><span data-stu-id="d422f-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="d422f-135">Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services--, maar een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kunnen delen.</span><span class="sxs-lookup"><span data-stu-id="d422f-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="d422f-136">Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="d422f-137">Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d422f-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="d422f-138">Verbindingen en bandbreedte kosten voor Hallo ExpressRoute-circuit is eigenaar van de toegepaste toohello-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d422f-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="d422f-139">Alle virtuele netwerken Hallo delen dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="d422f-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="d422f-141">Beheer - circuit eigenaars en circuit gebruikers</span><span class="sxs-lookup"><span data-stu-id="d422f-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="d422f-142">Hallo 'circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource.</span><span class="sxs-lookup"><span data-stu-id="d422f-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="d422f-143">Hallo circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'circuit gebruikers' maken.</span><span class="sxs-lookup"><span data-stu-id="d422f-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="d422f-144">Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="d422f-145">Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="d422f-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="d422f-146">Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="d422f-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="d422f-147">Intrekken van een vergunning resulteert in alle koppeling verbindingen wordt verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="d422f-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="d422f-148">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="d422f-148">Circuit owner operations</span></span>

<span data-ttu-id="d422f-149">**toocreate een autorisatie**</span><span class="sxs-lookup"><span data-stu-id="d422f-149">**toocreate an authorization**</span></span>

<span data-ttu-id="d422f-150">Hallo circuiteigenaar maakt een autorisatie.</span><span class="sxs-lookup"><span data-stu-id="d422f-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="d422f-151">Dit resulteert in Hallo maken van een autorisatiesleutel die kan worden gebruikt door een gebruiker circuit tooconnect hun virtuele netwerk gateways toohello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="d422f-152">Een vergunning is geldig voor slechts één verbinding.</span><span class="sxs-lookup"><span data-stu-id="d422f-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="d422f-153">Hallo cmdlet fragment wordt getoond hoe na een vergunning toocreate:</span><span class="sxs-lookup"><span data-stu-id="d422f-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="d422f-154">Hallo antwoord toothis bevat autorisatiesleutel hello en status:</span><span class="sxs-lookup"><span data-stu-id="d422f-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="d422f-155">**tooreview autorisaties**</span><span class="sxs-lookup"><span data-stu-id="d422f-155">**tooreview authorizations**</span></span>

<span data-ttu-id="d422f-156">Hallo circuiteigenaar kunt alle machtigingen die zijn uitgegeven voor een bepaalde circuit door het uitvoeren van de volgende cmdlet Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="d422f-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="d422f-157">**tooadd autorisaties**</span><span class="sxs-lookup"><span data-stu-id="d422f-157">**tooadd authorizations**</span></span>

<span data-ttu-id="d422f-158">Hallo circuiteigenaar kunt autorisaties toevoegen met behulp van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="d422f-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="d422f-159">**toodelete autorisaties**</span><span class="sxs-lookup"><span data-stu-id="d422f-159">**toodelete authorizations**</span></span>

<span data-ttu-id="d422f-160">Hallo circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door het uitvoeren van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="d422f-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="d422f-161">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="d422f-161">Circuit user operations</span></span>

<span data-ttu-id="d422f-162">Hallo circuit gebruiker moet Hallo peer-ID en een autorisatiesleutel van Hallo circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="d422f-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="d422f-163">Hallo autorisatiesleutel is een GUID.</span><span class="sxs-lookup"><span data-stu-id="d422f-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="d422f-164">Peer-ID kan worden gecontroleerd vanuit Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d422f-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="d422f-165">**een verbindingsverificatie tooredeem**</span><span class="sxs-lookup"><span data-stu-id="d422f-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="d422f-166">Hallo circuitgebruikers kunt Hallo cmdlet tooredeem na een koppeling autorisatie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d422f-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="d422f-167">**een verbindingsverificatie toorelease**</span><span class="sxs-lookup"><span data-stu-id="d422f-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="d422f-168">U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d422f-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="d422f-169">De verbinding van een virtueel netwerk wijzigen</span><span class="sxs-lookup"><span data-stu-id="d422f-169">Modify a virtual network connection</span></span>
<span data-ttu-id="d422f-170">U kunt bepaalde eigenschappen van een virtueel netwerkverbinding bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d422f-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="d422f-171">**tooupdate hello verbinding gewicht**</span><span class="sxs-lookup"><span data-stu-id="d422f-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="d422f-172">Het virtuele netwerk kan worden verbonden toomultiple ExpressRoute-circuits.</span><span class="sxs-lookup"><span data-stu-id="d422f-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="d422f-173">Het foutbericht Hallo dezelfde voorvoegsel van meer dan één ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="d422f-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="d422f-174">toochoose welke verbinding toosend-verkeer dat is bestemd voor dit voorvoegsel, kunt u *RoutingWeight* van een verbinding.</span><span class="sxs-lookup"><span data-stu-id="d422f-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="d422f-175">Verkeer wordt verzonden op Hallo verbinding met de hoogste Hallo *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="d422f-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="d422f-176">Hallo reeks *RoutingWeight* too32000 0 is.</span><span class="sxs-lookup"><span data-stu-id="d422f-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="d422f-177">Hallo-standaardwaarde is 0.</span><span class="sxs-lookup"><span data-stu-id="d422f-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d422f-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d422f-178">Next steps</span></span>
<span data-ttu-id="d422f-179">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d422f-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
