---
title: 'Een virtueel netwerk koppelen aan een ExpressRoute-circuit: Azure portal | Microsoft Docs'
description: Dit document bevat een overzicht van het virtuele netwerken (vnet's) koppelen aan ExpressRoute-circuits.
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
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="a2e94-103">Een virtueel netwerk verbinden met een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="a2e94-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2e94-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2e94-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="a2e94-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2e94-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="a2e94-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="a2e94-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="a2e94-107">Video - Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a2e94-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="a2e94-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a2e94-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="a2e94-109">In dit artikel helpt u bij virtuele netwerken (vnet's) koppelen aan Azure ExpressRoute-circuits met behulp van het implementatiemodel van Resource Manager en de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a2e94-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="a2e94-110">Virtuele netwerken in hetzelfde abonnement kunnen zijn of deel uitmaken van een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2e94-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a2e94-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a2e94-111">Before you begin</span></span>
* <span data-ttu-id="a2e94-112">Controleer de [vereisten](expressroute-prerequisites.md), [routeringsvereisten](expressroute-routing.md), en [werkstromen](expressroute-workflows.md) voordat u begint met de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a2e94-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="a2e94-113">U moet een actief ExpressRoute-circuit hebben.</span><span class="sxs-lookup"><span data-stu-id="a2e94-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="a2e94-114">Volg de instructies voor [maken van een ExpressRoute-circuit](expressroute-howto-circuit-portal-resource-manager.md) en laat het circuit inschakelen door de connectiviteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="a2e94-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="a2e94-115">Zorg ervoor dat u persoonlijke Azure-peering voor uw circuit is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2e94-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="a2e94-116">Zie de [Configure routing](expressroute-howto-routing-portal-resource-manager.md) artikel voor routering instructies.</span><span class="sxs-lookup"><span data-stu-id="a2e94-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="a2e94-117">Zorg ervoor dat de persoonlijke Azure-peering is geconfigureerd en van de BGP-peering tussen uw netwerk en Microsoft is, zodat u kunt end-to-end-connectiviteit inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="a2e94-118">Zorg ervoor dat u hebt een virtueel netwerk en een virtuele netwerkgateway gemaakt en volledig is ingericht.</span><span class="sxs-lookup"><span data-stu-id="a2e94-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="a2e94-119">Volg de instructies voor [maken van een virtuele netwerkgateway voor ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a2e94-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="a2e94-120">Het GatewayType 'ExpressRoute' niet VPN maakt gebruik van een virtuele netwerkgateway voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a2e94-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="a2e94-121">U kunt maximaal 10 virtuele netwerken koppelen aan een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="a2e94-122">Alle virtuele netwerken moet in dezelfde geopolitieke regio bij gebruik van een standaard ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="a2e94-123">U kunt een virtueel netwerk buiten de geopolitieke regio van het ExpressRoute-circuit koppelen of verbinding maken met een groter aantal virtuele netwerken aan uw ExpressRoute-circuit als u de invoegtoepassing ExpressRoute premium ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a2e94-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="a2e94-124">Controleer de [Veelgestelde vragen over](expressroute-faqs.md) voor meer informatie over de premium-invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a2e94-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="a2e94-125">U kunt [Bekijk een video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) voordat u begint met de stappen beter te begrijpen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="a2e94-126">Een virtueel netwerk in hetzelfde abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="a2e94-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="a2e94-127">Een verbinding te maken</span><span class="sxs-lookup"><span data-stu-id="a2e94-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="a2e94-128">BGP-configuratie-informatie wordt niet weergegeven als de layer 3-provider uw peerings geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2e94-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="a2e94-129">Als uw circuit ingericht status heeft is, moet u mogelijk zijn om verbindingen te maken.</span><span class="sxs-lookup"><span data-stu-id="a2e94-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="a2e94-130">Zorg ervoor dat uw ExpressRoute-circuit en de persoonlijke Azure-peering correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2e94-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="a2e94-131">Volg de instructies in [maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en [Configure routing](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a2e94-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="a2e94-132">Uw ExpressRoute-circuit moet eruitzien als in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="a2e94-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![ExpressRoute-circuit-schermafbeelding](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="a2e94-134">U kunt nu starten voor het inrichten van een verbinding voor het koppelen van uw virtuele netwerkgateway aan uw ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="a2e94-135">Klik op **verbinding** > **toevoegen** openen de **verbinding toevoegen** blade en configureer vervolgens de waarden.</span><span class="sxs-lookup"><span data-stu-id="a2e94-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Schermafbeelding van de verbinding toevoegen](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="a2e94-137">Nadat de verbinding is geconfigureerd, kan uw verbindingsobject gegevens voor de verbinding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a2e94-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Schermafbeelding van de verbinding-object](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="a2e94-139">Een verbinding verwijderen</span><span class="sxs-lookup"><span data-stu-id="a2e94-139">To delete a connection</span></span>
<span data-ttu-id="a2e94-140">U kunt een verbinding verwijderen door het selecteren van de **verwijderen** pictogram op de blade voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a2e94-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="a2e94-141">Een virtueel netwerk in een ander abonnement verbinden met een circuit</span><span class="sxs-lookup"><span data-stu-id="a2e94-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="a2e94-142">U kunt een ExpressRoute-circuit delen tussen meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="a2e94-143">De onderstaande afbeelding ziet u een eenvoudige schematische van hoe delen werkt voor ExpressRoute-circuits voor meerdere abonnementen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Abonnementoverschrijdende connectiviteit](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="a2e94-145">Elk van de kleinere clouds binnen de grote cloud wordt gebruikt voor abonnementen die bij verschillende afdelingen binnen een organisatie horen te vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="a2e94-146">Elk van de afdelingen binnen de organisatie kan hun eigen abonnement gebruiken voor het implementeren van hun services, maar één ExpressRoute-circuit terugverbinding maken met uw on-premises netwerk kunnen delen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="a2e94-147">Één afdeling (in dit voorbeeld: IT) kunt eigenaar van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="a2e94-148">Andere abonnementen binnen de organisatie kunnen het ExpressRoute-circuit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a2e94-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a2e94-149">Verbindingen en bandbreedte kosten voor het specifieke circuit wordt toegepast op de eigenaar van het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="a2e94-150">Alle virtuele netwerken delen de dezelfde bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="a2e94-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="a2e94-151">Beheer - circuit eigenaars en circuit gebruikers</span><span class="sxs-lookup"><span data-stu-id="a2e94-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="a2e94-152">De circuiteigenaar is een geautoriseerde gebruiker Power van de bron van ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="a2e94-153">De circuiteigenaar van het kunt autorisaties die kunnen worden ingewisseld door 'circuit gebruikers' maken.</span><span class="sxs-lookup"><span data-stu-id="a2e94-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="a2e94-154">Circuit gebruikers kunnen eigenaren van virtuele netwerkgateways die zich niet binnen hetzelfde abonnement als het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="a2e94-155">Circuit gebruikers kunnen inwisselen autorisaties (één autorisatie per virtueel netwerk).</span><span class="sxs-lookup"><span data-stu-id="a2e94-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="a2e94-156">De circuiteigenaar van het bevoegd is om te wijzigen en machtigingen intrekt op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="a2e94-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="a2e94-157">Intrekken van een vergunning resulteert in alle koppeling verbindingen wordt verwijderd uit het abonnement waarvoor de toegang is ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="a2e94-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="a2e94-158">Circuit eigenaar bewerkingen</span><span class="sxs-lookup"><span data-stu-id="a2e94-158">Circuit owner operations</span></span>

<span data-ttu-id="a2e94-159">**Maken van een verbinding-autorisatieregels**</span><span class="sxs-lookup"><span data-stu-id="a2e94-159">**To create a connection authorization**</span></span>

<span data-ttu-id="a2e94-160">De circuiteigenaar van het maakt een autorisatie.</span><span class="sxs-lookup"><span data-stu-id="a2e94-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="a2e94-161">Dit resulteert in het maken van een autorisatiesleutel die kan worden gebruikt door een gebruiker circuit verbinding maken hun virtuele netwerkgateways aan ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="a2e94-162">Een vergunning is geldig voor slechts één verbinding.</span><span class="sxs-lookup"><span data-stu-id="a2e94-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="a2e94-163">Klik op de blade ExpressRoute **autorisaties** en typ vervolgens een **naam** voor autorisatie en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2e94-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![autorisaties](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="a2e94-165">Zodra de configuratie is opgeslagen, kopieert u de **Resource-ID** en de **Autorisatiesleutel**.</span><span class="sxs-lookup"><span data-stu-id="a2e94-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Autorisatiesleutel](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="a2e94-167">**De autorisatie van een verbinding verwijderen**</span><span class="sxs-lookup"><span data-stu-id="a2e94-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="a2e94-168">U kunt een verbinding verwijderen door het selecteren van de **verwijderen** pictogram op de blade voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a2e94-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="a2e94-169">Bewerkingen voor circuit-gebruikers</span><span class="sxs-lookup"><span data-stu-id="a2e94-169">Circuit user operations</span></span>

<span data-ttu-id="a2e94-170">De circuit-gebruiker moet de resource-ID en een autorisatiesleutel van de circuiteigenaar van het.</span><span class="sxs-lookup"><span data-stu-id="a2e94-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="a2e94-171">**Voor een verbindingsverificatie inwisselen**</span><span class="sxs-lookup"><span data-stu-id="a2e94-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="a2e94-172">Klik op de **+ nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="a2e94-172">Click the **+New** button.</span></span>

    ![Klik op nieuwe](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="a2e94-174">Zoeken naar **'Verbinding'** in de Marketplace te selecteren en op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a2e94-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Zoekactie voor verbinding](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="a2e94-176">Zorg ervoor dat de **verbindingstype** is ingesteld op 'ExpressRoute'.</span><span class="sxs-lookup"><span data-stu-id="a2e94-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="a2e94-177">Vul de details en klik vervolgens op **OK** in de blade grondbeginselen.</span><span class="sxs-lookup"><span data-stu-id="a2e94-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Blade Grondbeginselen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="a2e94-179">In de **instellingen** blade, selecteer de **virtuele netwerkgateway** en controleer de **inwisselen autorisatie** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="a2e94-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="a2e94-180">Voer de **autorisatiesleutel** en de **circuit URI Peer** en geef een naam op voor de verbinding.</span><span class="sxs-lookup"><span data-stu-id="a2e94-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="a2e94-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2e94-181">Click **OK**.</span></span>

    ![Blade Instellingen](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="a2e94-183">Lees de informatie in de **samenvatting** blade en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2e94-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="a2e94-184">**Een verbindingsverificatie vrijgeven**</span><span class="sxs-lookup"><span data-stu-id="a2e94-184">**To release a connection authorization**</span></span>

<span data-ttu-id="a2e94-185">U kunt een vergunning vrijgeven door het verwijderen van de verbinding die is gekoppeld aan het virtuele netwerk in het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a2e94-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2e94-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2e94-186">Next steps</span></span>
<span data-ttu-id="a2e94-187">Voor meer informatie over ExpressRoute raadpleegt u de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a2e94-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
