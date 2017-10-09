---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: CLI: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe virtuele toolink (vnet's) tooExpressRoute circuits netwerken met behulp van Hallo Resource Manager-implementatiemodel en CLI.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="a9642-103">Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit met CLI</span><span class="sxs-lookup"><span data-stu-id="a9642-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="a9642-104">In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits met CLI koppelen.</span><span class="sxs-lookup"><span data-stu-id="a9642-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="a9642-105">met Azure CLI toolink Hallo virtuele netwerken worden gemaakt met behulp van Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a9642-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a9642-106">Ze kunnen zijn in Hallo hetzelfde abonnement of een deel van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="a9642-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="a9642-107">Als u een andere methode tooconnect toouse uw VNet tooan ExpressRoute-circuit wilt, kunt u een artikel van Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="a9642-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9642-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a9642-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="a9642-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9642-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="a9642-110">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="a9642-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="a9642-111">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a9642-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="a9642-112">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a9642-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="a9642-113">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="a9642-113">Configuration prerequisites</span></span>

* <span data-ttu-id="a9642-114">U moet de meest recente versie Hallo van Hallo-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="a9642-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="a9642-115">Zie voor meer informatie [2.0 voor Azure CLI installeren](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9642-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="a9642-116">U moet tooreview hello [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a9642-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="a9642-117">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="a9642-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="a9642-118">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](howto-circuit-cli.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="a9642-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="a9642-119">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a9642-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="a9642-120">Zie Hallo [routering configureren](howto-routing-cli.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="a9642-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="a9642-121">Zorg ervoor dat de persoonlijke Azure-peering is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a9642-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="a9642-122">Hallo BGP-peering tussen uw netwerk en Microsoft moet zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a9642-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="a9642-123">Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="a9642-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="a9642-124">Hallo-instructies te volgen[configureren van een virtuele netwerkgateway voor ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="a9642-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="a9642-125">Ervoor toouse worden `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="a9642-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="a9642-126">U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="a9642-127">Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="a9642-128">Als u premium-invoegtoepassing voor ExpressRoute Hallo inschakelt, kunt u een virtueel netwerk buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a9642-129">Zie voor meer informatie over de premium-invoegtoepassing Hallo Hallo [Veelgestelde vragen over](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a9642-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="a9642-130">Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="a9642-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="a9642-131">Met behulp van Hallo voorbeeld kunt u een virtueel netwerk gateway tooan ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="a9642-132">Zorg ervoor dat Hallo virtuele netwerkgateway wordt gemaakt en is gereed voor het koppelen voordat u Hallo-opdracht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a9642-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="a9642-133">Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="a9642-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="a9642-134">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a9642-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="a9642-135">Hallo afbeelding hieronder ziet een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a9642-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="a9642-136">Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie.</span><span class="sxs-lookup"><span data-stu-id="a9642-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="a9642-137">Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services--, maar een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk kunnen delen.</span><span class="sxs-lookup"><span data-stu-id="a9642-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="a9642-138">Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="a9642-139">Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a9642-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="a9642-140">Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-Circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="a9642-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="a9642-141">Alle virtuele netwerken Hallo delen dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="a9642-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="a9642-143">Beheer - Circuit eigenaars en Circuit gebruikers</span><span class="sxs-lookup"><span data-stu-id="a9642-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="a9642-144">Hallo 'Circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource.</span><span class="sxs-lookup"><span data-stu-id="a9642-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="a9642-145">Hallo Circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'Circuit gebruikers' maken.</span><span class="sxs-lookup"><span data-stu-id="a9642-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="a9642-146">Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="a9642-147">Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="a9642-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="a9642-148">Hallo Circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="a9642-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="a9642-149">Wanneer een vergunning wordt ingetrokken, worden alle koppeling verbindingen verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="a9642-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="a9642-150">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="a9642-150">Circuit Owner operations</span></span>

<span data-ttu-id="a9642-151">**toocreate een autorisatie**</span><span class="sxs-lookup"><span data-stu-id="a9642-151">**toocreate an authorization**</span></span>

<span data-ttu-id="a9642-152">Hallo Circuiteigenaar maakt een autorisatie, die wordt gemaakt van een autorisatiesleutel die kan worden gebruikt door een tooconnect Circuitgebruikers hun virtuele netwerk gateways toohello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a9642-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="a9642-153">Een vergunning is geldig voor slechts één verbinding.</span><span class="sxs-lookup"><span data-stu-id="a9642-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="a9642-154">Hallo volgende voorbeeld wordt getoond hoe toocreate een vergunning:</span><span class="sxs-lookup"><span data-stu-id="a9642-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="a9642-155">antwoord Hallo bevat Hallo autorisatiesleutel en de status:</span><span class="sxs-lookup"><span data-stu-id="a9642-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="a9642-156">**tooreview autorisaties**</span><span class="sxs-lookup"><span data-stu-id="a9642-156">**tooreview authorizations**</span></span>

<span data-ttu-id="a9642-157">Hallo Circuiteigenaar kunt bekijken alle autorisaties die op een bepaalde circuit zijn uitgegeven door Hallo volgt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a9642-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="a9642-158">**tooadd autorisaties**</span><span class="sxs-lookup"><span data-stu-id="a9642-158">**tooadd authorizations**</span></span>

<span data-ttu-id="a9642-159">Hallo Circuiteigenaar kunt autorisaties toevoegen met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9642-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="a9642-160">**toodelete autorisaties**</span><span class="sxs-lookup"><span data-stu-id="a9642-160">**toodelete authorizations**</span></span>

<span data-ttu-id="a9642-161">Hallo Circuiteigenaar kunt intrekken/delete autorisaties toohello gebruiker door te voeren Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="a9642-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="a9642-162">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="a9642-162">Circuit User operations</span></span>

<span data-ttu-id="a9642-163">Hallo Circuitgebruikers nodig Hallo peer-ID en een autorisatiesleutel van Hallo Circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="a9642-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="a9642-164">Hallo autorisatiesleutel is een GUID.</span><span class="sxs-lookup"><span data-stu-id="a9642-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="a9642-165">**een verbindingsverificatie tooredeem**</span><span class="sxs-lookup"><span data-stu-id="a9642-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="a9642-166">Hallo Circuitgebruikers kunt Hallo voorbeeld tooredeem na een koppeling autorisatie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a9642-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="a9642-167">**een verbindingsverificatie toorelease**</span><span class="sxs-lookup"><span data-stu-id="a9642-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="a9642-168">U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a9642-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9642-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a9642-169">Next steps</span></span>

<span data-ttu-id="a9642-170">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a9642-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
