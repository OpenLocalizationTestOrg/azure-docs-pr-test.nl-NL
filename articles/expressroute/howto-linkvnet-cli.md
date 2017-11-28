---
title: 'Een virtueel netwerk koppelen aan een ExpressRoute-circuit: CLI: Azure | Microsoft Docs'
description: Dit document bevat een overzicht van hoe u virtuele netwerken (vnet's) koppelen aan ExpressRoute-circuits met behulp van het implementatiemodel van Resource Manager en de CLI.
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
ms.openlocfilehash: 0ea696e796ec3a943bc028f56da417978b728b82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit-using-cli"></a><span data-ttu-id="1c1d2-103">Een virtueel netwerk verbinden met een ExpressRoute-circuit met CLI</span><span class="sxs-lookup"><span data-stu-id="1c1d2-103">Connect a virtual network to an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="1c1d2-104">In dit artikel helpt u bij virtuele netwerken (vnet's) koppelen aan Azure ExpressRoute-circuits met CLI.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-104">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="1c1d2-105">Als u wilt koppelen met Azure CLI, moeten de virtuele netwerken worden gemaakt met het implementatiemodel van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-105">To link using Azure CLI, the virtual networks must be created using the Resource Manager deployment model.</span></span> <span data-ttu-id="1c1d2-106">Ze kunnen zijn in het hetzelfde abonnement of deel uitmaken van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-106">They can either be in the same subscription, or part of another subscription.</span></span> <span data-ttu-id="1c1d2-107">Als u gebruiken van een andere methode wilt voor uw VNet verbinding met een ExpressRoute-circuit, kunt u een artikel uit de volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-107">If you want to use a different method to connect your VNet to an ExpressRoute circuit, you can select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c1d2-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1c1d2-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="1c1d2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c1d2-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="1c1d2-110">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="1c1d2-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="1c1d2-111">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="1c1d2-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="1c1d2-112">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="1c1d2-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="1c1d2-113">Configuratievereisten</span><span class="sxs-lookup"><span data-stu-id="1c1d2-113">Configuration prerequisites</span></span>

* <span data-ttu-id="1c1d2-114">U moet de meest recente versie van de opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-114">You need the latest version of the command-line interface (CLI).</span></span> <span data-ttu-id="1c1d2-115">Zie voor meer informatie [2.0 voor Azure CLI installeren](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="1c1d2-116">U moet controleren de [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-116">You need to review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="1c1d2-117">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="1c1d2-118">Volg de instructies voor [maken van een ExpressRoute-circuit](howto-circuit-cli.md) en laat het circuit inschakelen door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-118">Follow the instructions to [create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="1c1d2-119">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="1c1d2-120">Zie de [routering configureren](howto-routing-cli.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-120">See the [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="1c1d2-121">Zorg ervoor dat de persoonlijke Azure-peering is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="1c1d2-122">De BGP-peer tussen uw netwerk en Microsoft moet, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-122">The BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="1c1d2-123">Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="1c1d2-124">Volg de instructies voor [configureren van een virtuele netwerkgateway voor ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-124">Follow the instructions to [Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="1c1d2-125">Zorg ervoor dat u `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-125">Be sure to use `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="1c1d2-126">U kunt maximaal 10 virtuele netwerken koppelen aan een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-126">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="1c1d2-127">Alle virtuele netwerken moet in dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-127">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="1c1d2-128">Als u de invoegtoepassing ExpressRoute premium inschakelt, kunt u een virtueel netwerk buiten de geopolitieke regio van het ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken aan uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-128">If you enable the ExpressRoute premium add-on, you can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="1c1d2-129">Zie voor meer informatie over de premium-invoegtoepassing, de [Veelgestelde vragen over](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-129">For more information about the premium add-on, see the [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="1c1d2-130">Een virtueel netwerk in hetzelfde abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="1c1d2-130">Connect a virtual network in the same subscription to a circuit</span></span>

<span data-ttu-id="1c1d2-131">U kunt een virtuele netwerkgateway aan een ExpressRoute-circuit verbinding maken met behulp van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-131">You can connect a virtual network gateway to an ExpressRoute circuit by using the example.</span></span> <span data-ttu-id="1c1d2-132">Zorg ervoor dat de virtuele netwerkgateway wordt gemaakt en gereed is voor het koppelen voordat u de opdracht uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-132">Make sure that the virtual network gateway is created and is ready for linking before you run the command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="1c1d2-133">Een virtueel netwerk in een ander abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="1c1d2-133">Connect a virtual network in a different subscription to a circuit</span></span>

<span data-ttu-id="1c1d2-134">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="1c1d2-135">De onderstaande afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-135">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="1c1d2-136">Elk van de kleinere clouds binnen de grote cloud wordt gebruikt voor abonnementen die bij verschillende afdelingen binnen een organisatie horen te vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-136">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="1c1d2-137">Elk van de afdelingen binnen de organisatie kan hun eigen abonnement gebruiken voor het implementeren van hun services--, maar één ExpressRoute-circuit terugverbinding maken met uw on-premises netwerk kunnen delen.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-137">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="1c1d2-138">Één afdeling (in dit voorbeeld: IT) kunt eigenaar van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-138">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="1c1d2-139">Andere abonnementen binnen de organisatie kunnen het ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-139">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="1c1d2-140">Verbindingen en bandbreedte kosten voor het specifieke circuit wordt toegepast op de eigenaar van het ExpressRoute-Circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-140">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="1c1d2-141">Alle virtuele netwerken delen de dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-141">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="1c1d2-143">Beheer - Circuit eigenaars en Circuit gebruikers</span><span class="sxs-lookup"><span data-stu-id="1c1d2-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="1c1d2-144">De eigenaar van het Circuit is een geautoriseerde gebruiker Power van de bron van ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-144">The 'Circuit Owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="1c1d2-145">De eigenaar van het Circuit kunt autorisaties die kunnen worden ingewisseld door 'Circuit gebruikers' maken.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-145">The Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="1c1d2-146">Circuit gebruikers kunnen eigenaren van virtuele netwerkgateways die zich niet binnen hetzelfde abonnement als het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-146">Circuit Users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="1c1d2-147">Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="1c1d2-148">De eigenaar van het Circuit bevoegd is om te wijzigen en machtigingen intrekt op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-148">The Circuit Owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="1c1d2-149">Wanneer een vergunning wordt ingetrokken, worden alle koppeling verbindingen verwijderd uit het abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-149">When an authorization is revoked, all link connections are deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="1c1d2-150">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="1c1d2-150">Circuit Owner operations</span></span>

<span data-ttu-id="1c1d2-151">**Maken van een autorisatieregels**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-151">**To create an authorization**</span></span>

<span data-ttu-id="1c1d2-152">De eigenaar van het Circuit maakt een autorisatie, die een autorisatiesleutel die kan worden gebruikt door een gebruiker Circuit hun virtuele netwerkgateways aan ExpressRoute-circuit verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-152">The Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="1c1d2-153">Een vergunning is geldig voor slechts één verbinding.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="1c1d2-154">Het volgende voorbeeld ziet u het maken van een vergunning:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-154">The following example shows how to create an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="1c1d2-155">Het antwoord bevat de autorisatiesleutel en status:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-155">The response contains the authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="1c1d2-156">**Machtigingen controleren**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-156">**To review authorizations**</span></span>

<span data-ttu-id="1c1d2-157">De eigenaar van het Circuit Neem alle machtigingen die zijn uitgegeven voor een bepaalde circuit door te voeren in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-157">The Circuit Owner can review all authorizations that are issued on a particular circuit by running the following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="1c1d2-158">**Autorisaties toevoegen**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-158">**To add authorizations**</span></span>

<span data-ttu-id="1c1d2-159">De eigenaar van het Circuit kunt autorisaties toevoegen met behulp van het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-159">The Circuit Owner can add authorizations by using the following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="1c1d2-160">**Autorisaties verwijderen**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-160">**To delete authorizations**</span></span>

<span data-ttu-id="1c1d2-161">De eigenaar van het Circuit kunt intrekken/delete autorisaties voor de gebruiker door te voeren in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-161">The Circuit Owner can revoke/delete authorizations to the user by running the following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="1c1d2-162">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="1c1d2-162">Circuit User operations</span></span>

<span data-ttu-id="1c1d2-163">De Circuit-gebruiker moet de peer-ID en een autorisatiesleutel van de eigenaar van het Circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-163">The Circuit User needs the peer ID and an authorization key from the Circuit Owner.</span></span> <span data-ttu-id="1c1d2-164">De autorisatiesleutel is een GUID.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-164">The authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="1c1d2-165">**Voor een verbindingsverificatie inwisselen**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="1c1d2-166">De Circuit-gebruiker kan het volgende voorbeeld als u wilt gebruikmaken van een koppeling autorisatie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1c1d2-166">The Circuit User can run the following example to redeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="1c1d2-167">**Een verbindingsverificatie vrijgeven**</span><span class="sxs-lookup"><span data-stu-id="1c1d2-167">**To release a connection authorization**</span></span>

<span data-ttu-id="1c1d2-168">U kunt een vergunning vrijgeven door het verwijderen van de verbinding die is gekoppeld aan het virtuele netwerk in het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="1c1d2-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c1d2-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c1d2-169">Next steps</span></span>

<span data-ttu-id="1c1d2-170">Voor meer informatie over ExpressRoute raadpleegt u de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="1c1d2-170">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>