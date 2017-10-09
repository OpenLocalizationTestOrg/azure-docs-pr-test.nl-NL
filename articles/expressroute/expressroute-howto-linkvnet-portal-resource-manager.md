---
title: 'Koppelen van een virtueel netwerk tooan ExpressRoute-circuit: Azure portal | Microsoft Docs'
description: Dit document bevat een overzicht van hoe toolink virtuele (vnet's) tooExpressRoute circuits netwerken.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="2e915-103">Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="2e915-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e915-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2e915-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="2e915-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e915-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="2e915-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="2e915-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="2e915-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2e915-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="2e915-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="2e915-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="2e915-109">In dit artikel helpt u bij virtuele netwerken (vnet's) tooAzure ExpressRoute-circuits koppelen met Hallo Resource Manager-implementatiemodel en hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2e915-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="2e915-110">Virtuele netwerken kunnen zijn in Hallo hetzelfde abonnement, of dat ze deel kunnen uitmaken van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="2e915-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2e915-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2e915-111">Before you begin</span></span>
* <span data-ttu-id="2e915-112">Bekijk Hallo [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="2e915-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="2e915-113">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="2e915-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="2e915-114">Hallo-instructies te volgen[maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat Hallo-circuit inschakelen door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="2e915-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="2e915-115">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2e915-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="2e915-116">Zie Hallo [Configure routing](expressroute-howto-routing-portal-resource-manager.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="2e915-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="2e915-117">Zorg ervoor dat persoonlijke Azure-peering is geconfigureerd en actief Hallo BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2e915-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="2e915-118">Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="2e915-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="2e915-119">Hallo-instructies te volgen[maken van een virtuele netwerkgateway voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2e915-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="2e915-120">Hallo GatewayType 'ExpressRoute' niet VPN maakt gebruik van een virtuele netwerkgateway voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e915-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="2e915-121">U kunt een koppeling van too10 virtuele netwerken tooa standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="2e915-122">Alle virtuele netwerken moet Hallo dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="2e915-123">U kunt een virtueel netwerk buiten de geopolitieke regio Hallo Hallo ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken tooyour ExpressRoute-circuit als u premium-invoegtoepassing voor ExpressRoute Hallo ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2e915-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="2e915-124">Controleer de Hallo [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over Hallo premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2e915-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="2e915-125">U kunt [Bekijk een video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) voordat begin toobetter begrijpen Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="2e915-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="2e915-126">Verbinding maken met een virtueel netwerk in Hallo hetzelfde abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="2e915-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="2e915-127">toocreate een verbinding</span><span class="sxs-lookup"><span data-stu-id="2e915-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="2e915-128">BGP-configuratie-informatie wordt niet weergegeven als Hallo laag 3-provider uw peerings geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2e915-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="2e915-129">Als uw circuit ingericht status heeft is, moet u kunnen toocreate verbindingen.</span><span class="sxs-lookup"><span data-stu-id="2e915-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="2e915-130">Zorg ervoor dat uw ExpressRoute-circuit en de persoonlijke Azure-peering correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2e915-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="2e915-131">Volg de instructies in Hallo [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en [Configure routing](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2e915-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="2e915-132">Uw ExpressRoute-circuit moet eruitzien als Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="2e915-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![ExpressRoute-circuit-schermafbeelding](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="2e915-134">U kunt nu starten inrichten van een verbinding toolink uw virtuele netwerk gateway tooyour ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="2e915-135">Klik op **verbinding** > **toevoegen** tooopen hello **verbinding toevoegen** blade en configureer vervolgens Hallo waarden.</span><span class="sxs-lookup"><span data-stu-id="2e915-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Schermafbeelding van de verbinding toevoegen](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="2e915-137">Nadat de verbinding is geconfigureerd, ziet uw verbindingsobject Hallo-informatie voor Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e915-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Schermafbeelding van de verbinding-object](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="2e915-139">toodelete een verbinding</span><span class="sxs-lookup"><span data-stu-id="2e915-139">toodelete a connection</span></span>
<span data-ttu-id="2e915-140">U kunt een verbinding verwijderen door het selecteren van Hallo **verwijderen** pictogram op de blade Hallo voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e915-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="2e915-141">Verbinding maken met een virtueel netwerk in een ander abonnement tooa circuit</span><span class="sxs-lookup"><span data-stu-id="2e915-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="2e915-142">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="2e915-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="2e915-143">Hallo afbeelding hieronder ziet een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="2e915-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="2e915-145">Elk van de kleinere clouds binnen grote cloud Hallo Hallo is gebruikte toorepresent abonnementen die deel uitmaken van toodifferent afdelingen binnen een organisatie.</span><span class="sxs-lookup"><span data-stu-id="2e915-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="2e915-146">Elk van de afdelingen binnen de organisatie Hallo Hallo hun eigen abonnement kunt gebruiken voor het implementeren van hun services, maar ze kunnen een enkel ExpressRoute-circuit tooconnect back tooyour on-premises netwerk delen.</span><span class="sxs-lookup"><span data-stu-id="2e915-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="2e915-147">Één afdeling (in dit voorbeeld: IT) eigenaar kunnen Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="2e915-148">Andere abonnementen binnen de organisatie Hallo kunnen Hallo ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2e915-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e915-149">Verbindingen en bandbreedte kosten voor speciale Hallo circuit zijn toegepaste toohello ExpressRoute-circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="2e915-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="2e915-150">Alle virtuele netwerken Hallo delen dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="2e915-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="2e915-151">Beheer - circuit eigenaars en circuit gebruikers</span><span class="sxs-lookup"><span data-stu-id="2e915-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="2e915-152">Hallo 'circuiteigenaar' is een geautoriseerde gebruiker Power Hallo ExpressRoute-circuit resource.</span><span class="sxs-lookup"><span data-stu-id="2e915-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="2e915-153">Hallo circuiteigenaar kunt autorisaties die kunnen worden ingewisseld door 'circuit gebruikers' maken.</span><span class="sxs-lookup"><span data-stu-id="2e915-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="2e915-154">Circuit gebruikers kunnen eigenaren van het virtuele netwerk gateways die niet binnen hetzelfde abonnement Hallo zoals Hallo ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="2e915-155">Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="2e915-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="2e915-156">Hallo circuiteigenaar heeft Hallo power toomodify en trek autorisaties op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="2e915-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="2e915-157">Intrekken van een vergunning resulteert in alle koppeling verbindingen wordt verwijderd uit het Hallo-abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="2e915-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="2e915-158">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="2e915-158">Circuit owner operations</span></span>

<span data-ttu-id="2e915-159">**een verbindingsverificatie toocreate**</span><span class="sxs-lookup"><span data-stu-id="2e915-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="2e915-160">Hallo circuiteigenaar maakt een autorisatie.</span><span class="sxs-lookup"><span data-stu-id="2e915-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="2e915-161">Dit resulteert in Hallo maken van een autorisatiesleutel die kan worden gebruikt door een gebruiker circuit tooconnect hun virtuele netwerk gateways toohello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="2e915-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="2e915-162">Een vergunning is geldig voor slechts één verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e915-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="2e915-163">Klik op Hallo ExpressRoute blade **autorisaties** en typ vervolgens een **naam** voor Hallo autorisatie en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2e915-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![autorisaties](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="2e915-165">Zodra het Hallo-configuratie is opgeslagen, kopiëren Hallo **Resource-ID** en Hallo **Autorisatiesleutel**.</span><span class="sxs-lookup"><span data-stu-id="2e915-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Autorisatiesleutel](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="2e915-167">**een verbindingsverificatie toodelete**</span><span class="sxs-lookup"><span data-stu-id="2e915-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="2e915-168">U kunt een verbinding verwijderen door het selecteren van Hallo **verwijderen** pictogram op de blade Hallo voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e915-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="2e915-169">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="2e915-169">Circuit user operations</span></span>

<span data-ttu-id="2e915-170">Hallo circuit gebruiker moet Hallo resource-ID en een autorisatiesleutel van Hallo circuiteigenaar.</span><span class="sxs-lookup"><span data-stu-id="2e915-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="2e915-171">**een verbindingsverificatie tooredeem**</span><span class="sxs-lookup"><span data-stu-id="2e915-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="2e915-172">Klik op Hallo **+ nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="2e915-172">Click hello **+New** button.</span></span>

    ![Klik op nieuwe](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="2e915-174">Zoeken naar **'Verbinding'** in Hallo Marketplace, te selecteren en op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2e915-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Zoekactie voor verbinding](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="2e915-176">Zorg ervoor dat Hallo **verbindingstype** te is ingesteld 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="2e915-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="2e915-177">Vul Hallo details en klik vervolgens op **OK** in de blade grondbeginselen Hallo.</span><span class="sxs-lookup"><span data-stu-id="2e915-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Blade Grondbeginselen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="2e915-179">In Hallo **instellingen** blade, selecteer Hallo **virtuele netwerkgateway** en controleer Hallo **inwisselen autorisatie** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2e915-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="2e915-180">Voer Hallo **autorisatiesleutel** en Hallo **circuit URI Peer** en geef een naam op Hallo-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e915-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="2e915-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e915-181">Click **OK**.</span></span>

    ![Blade Instellingen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="2e915-183">Lees de informatie Hallo in Hallo **samenvatting** blade en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e915-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="2e915-184">**een verbindingsverificatie toorelease**</span><span class="sxs-lookup"><span data-stu-id="2e915-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="2e915-185">U kunt een vergunning vrijgeven door Hallo-verbinding die is gekoppeld aan Hallo ExpressRoute-circuit toohello virtueel netwerk te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2e915-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e915-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e915-186">Next steps</span></span>
<span data-ttu-id="2e915-187">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="2e915-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
