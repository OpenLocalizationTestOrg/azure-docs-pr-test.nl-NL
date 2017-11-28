---
title: 'Planning en ontwerp voor cross-premises verbindingen: Azure VPN-Gateway | Microsoft Docs'
description: Meer informatie over VPN-Gateway planning en ontwerp voor cross-premises en hybride VNet-naar-VNet-verbindingen
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="b9292-103">Planning en ontwerp voor VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b9292-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="b9292-104">Plannen en ontwerpen van uw cross-premises en VNet-naar-VNet-configuraties kunnen zijn eenvoudige of complexe, afhankelijk van de behoeften van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="b9292-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="b9292-105">Dit artikel begeleidt u bij basic plannings- en ontwerpoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="b9292-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="b9292-106"><a name="planning"></a>Plannen</span><span class="sxs-lookup"><span data-stu-id="b9292-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="b9292-107"><a name="compare"></a>Opties voor cross-premises-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="b9292-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="b9292-108">Als u uw lokale sites veilige verbinding met een virtueel netwerk wilt, hebt u drie verschillende manieren om dit te doen: Site-naar-Site, punt-naar-Site en ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b9292-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="b9292-109">Vergelijk de verschillende cross-premises-verbindingen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b9292-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="b9292-110">Welke optie die u kiest kan afhankelijk zijn van verschillende overwegingen, zoals:</span><span class="sxs-lookup"><span data-stu-id="b9292-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="b9292-111">Wat voor doorvoer heeft uw oplossing nodig?</span><span class="sxs-lookup"><span data-stu-id="b9292-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="b9292-112">Wilt u communiceren via het openbare internet met een beveiligd VPN, of via een particuliere verbinding?</span><span class="sxs-lookup"><span data-stu-id="b9292-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="b9292-113">Hebt u de beschikking over een openbaar IP-adres?</span><span class="sxs-lookup"><span data-stu-id="b9292-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="b9292-114">Bent u van plan om een VPN-apparaat te gebruiken?</span><span class="sxs-lookup"><span data-stu-id="b9292-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="b9292-115">Zo ja, is het compatibel?</span><span class="sxs-lookup"><span data-stu-id="b9292-115">If so, is it compatible?</span></span>
* <span data-ttu-id="b9292-116">Verbindt u slechts enkele computers met elkaar, of u wilt een persistente verbinding voor uw site?</span><span class="sxs-lookup"><span data-stu-id="b9292-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="b9292-117">Welk type VPN-gateway is vereist voor de oplossing die u wilt maken?</span><span class="sxs-lookup"><span data-stu-id="b9292-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="b9292-118">Welke gateway SKU moet u gebruiken?</span><span class="sxs-lookup"><span data-stu-id="b9292-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="b9292-119"><a name="planningtable"></a>Tabel plannen</span><span class="sxs-lookup"><span data-stu-id="b9292-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="b9292-120">De volgende tabel kunt u de beste connectiviteitsoptie voor uw oplossing bepalen.</span><span class="sxs-lookup"><span data-stu-id="b9292-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="b9292-121"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="b9292-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="b9292-122"><a name="wf"></a>Werkstroom</span><span class="sxs-lookup"><span data-stu-id="b9292-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="b9292-123">De volgende lijst geeft een overzicht van de algemene werkstroom voor cloud-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="b9292-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="b9292-124">Ontwerpen en plannen van de topologie van uw netwerkverbinding en vermeld de-adresruimtes voor alle netwerken die u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="b9292-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="b9292-125">Maak een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b9292-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="b9292-126">Een VPN-gateway voor het virtuele netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="b9292-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="b9292-127">Maken en verbindingen met on-premises netwerken of andere virtuele netwerken configureren (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="b9292-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="b9292-128">Maak en configureer een punt-naar-Site-verbinding voor uw Azure VPN-gateway (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="b9292-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="b9292-129"><a name="design"></a>Ontwerp</span><span class="sxs-lookup"><span data-stu-id="b9292-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="b9292-130"><a name="topologies"></a>Topologieën voor verbinding</span><span class="sxs-lookup"><span data-stu-id="b9292-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="b9292-131">Starten door te kijken naar de diagrammen in de [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b9292-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="b9292-132">Het artikel bevat basic diagrammen, het implementatiemodel voor elke topologie en de beschikbare implementatiehulpmiddelen die u kunt gebruiken voor het implementeren van uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="b9292-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="b9292-133"><a name="designbasics"></a>Basisprincipes van ontwerp</span><span class="sxs-lookup"><span data-stu-id="b9292-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="b9292-134">De volgende secties worden de basisprincipes van VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="b9292-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="b9292-135"><a name="servicelimits"></a>Limieten voor netwerken services</span><span class="sxs-lookup"><span data-stu-id="b9292-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="b9292-136">Blader door de tabellen om weer te geven [netwerken services limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b9292-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="b9292-137">Uw ontwerp mogelijk van invloed op de grenzen die worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="b9292-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="b9292-138"><a name="subnets"></a>Over subnetten</span><span class="sxs-lookup"><span data-stu-id="b9292-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="b9292-139">Als u verbindingen maakt, moet u rekening houden met subnet bereiken.</span><span class="sxs-lookup"><span data-stu-id="b9292-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="b9292-140">U kunt geen overlappende subnet-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="b9292-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="b9292-141">Een overlappend subnet is als een virtueel netwerk of on-premises locatie bevat dezelfde adresruimte met de andere locatie.</span><span class="sxs-lookup"><span data-stu-id="b9292-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="b9292-142">Dit betekent dat u uw netwerk engineers voor uw lokale on-premises netwerken moet reserveren een bereik moet worden gebruikt voor uw Azure-IP-adressering ruimte/subnetten.</span><span class="sxs-lookup"><span data-stu-id="b9292-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="b9292-143">U moet een adresruimte die niet wordt gebruikt op de lokale on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="b9292-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="b9292-144">Vermijden overlappende subnetten is ook belangrijk wanneer u met VNet-naar-VNet-verbindingen werkt.</span><span class="sxs-lookup"><span data-stu-id="b9292-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="b9292-145">Als uw subnetten overlappen en een IP-adres in zowel de verzendende en de bestemming VNets bestaat, mislukt de VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b9292-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="b9292-146">Azure kan niet de gegevens routeren naar het andere VNet omdat het doeladres deel uitmaakt van de verzendende VNet.</span><span class="sxs-lookup"><span data-stu-id="b9292-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="b9292-147">VPN-Gateways vereist een specifiek subnet met de naam van een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="b9292-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="b9292-148">Voor een goede werking moeten alle gatewaysubnetten de naam GatewaySubnet krijgen.</span><span class="sxs-lookup"><span data-stu-id="b9292-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="b9292-149">Zorg ervoor dat niet als de naam van een andere naam voor uw gatewaysubnet en virtuele machines of iets anders in het gatewaysubnet niet implementeren.</span><span class="sxs-lookup"><span data-stu-id="b9292-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="b9292-150">Zie [Gatewaysubnetten](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="b9292-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="b9292-151"><a name="local"></a>Over lokale netwerkgateways</span><span class="sxs-lookup"><span data-stu-id="b9292-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="b9292-152">De lokale netwerkgateway verwijst doorgaans naar uw on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="b9292-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="b9292-153">In het klassieke implementatiemodel, de lokale netwerkgateway aangeduid als een lokale netwerksite.</span><span class="sxs-lookup"><span data-stu-id="b9292-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="b9292-154">Wanneer u een lokale netwerkgateway configureert, u een naam geven, geeft het openbare IP-adres van de on-premises VPN-apparaat en de adresvoorvoegsels die zich in de on-premises locatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="b9292-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="b9292-155">Azure kijkt naar de bestemmingsadressen voor netwerkverkeer, raadpleegt de configuratie die u hebt opgegeven voor de lokale netwerkgateway en routeert pakketten dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="b9292-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="b9292-156">U kunt de adresvoorvoegsels zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b9292-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="b9292-157">Zie voor meer informatie [lokale netwerkgateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="b9292-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="b9292-158"><a name="gwtype"></a>Over gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="b9292-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="b9292-159">Als u het juiste Gatewaytype voor uw topologie is essentieel.</span><span class="sxs-lookup"><span data-stu-id="b9292-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="b9292-160">Als u het verkeerde type selecteert, werkt uw gateway niet goed.</span><span class="sxs-lookup"><span data-stu-id="b9292-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="b9292-161">Het Gatewaytype bepaalt hoe de gateway zelf is verbonden. Het is een vereiste configuratie-instelling voor het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b9292-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="b9292-162">De gatewaytypen zijn:</span><span class="sxs-lookup"><span data-stu-id="b9292-162">The gateway types are:</span></span>

* <span data-ttu-id="b9292-163">VPN</span><span class="sxs-lookup"><span data-stu-id="b9292-163">Vpn</span></span>
* <span data-ttu-id="b9292-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9292-164">ExpressRoute</span></span>

#### <span data-ttu-id="b9292-165"><a name="connectiontype"></a>Over verbindingstypen</span><span class="sxs-lookup"><span data-stu-id="b9292-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="b9292-166">Elke configuratie vereist een specifiek verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="b9292-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="b9292-167">De verbindingstypen zijn:</span><span class="sxs-lookup"><span data-stu-id="b9292-167">The connection types are:</span></span>

* <span data-ttu-id="b9292-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="b9292-168">IPsec</span></span>
* <span data-ttu-id="b9292-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="b9292-169">Vnet2Vnet</span></span>
* <span data-ttu-id="b9292-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b9292-170">ExpressRoute</span></span>
* <span data-ttu-id="b9292-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="b9292-171">VPNClient</span></span>

#### <span data-ttu-id="b9292-172"><a name="vpntype"></a>Over VPN-typen</span><span class="sxs-lookup"><span data-stu-id="b9292-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="b9292-173">Elke configuratie vereist een specifiek VPN-type.</span><span class="sxs-lookup"><span data-stu-id="b9292-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="b9292-174">Als u twee configuraties combineert - u maakt bijvoorbeeld een site-naar-site-verbinding en een punt-naar-site-verbinding met hetzelfde VNet - dan moet u een VPN-type gebruiken dat voldoet aan de vereisten van beide verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b9292-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="b9292-175">De volgende tabellen tonen de VPN-type, zoals deze wordt toegewezen aan de configuratie van elke verbinding.</span><span class="sxs-lookup"><span data-stu-id="b9292-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="b9292-176">Zorg ervoor dat het VPN-type voor uw gateway overeenkomt met de configuratie die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="b9292-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="b9292-177"><a name="devices"></a>VPN-apparaten voor Site-naar-Site-verbindingen</span><span class="sxs-lookup"><span data-stu-id="b9292-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="b9292-178">Configureren van een Site-naar-Site-verbinding, ongeacht implementatiemodel, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b9292-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="b9292-179">Een VPN-apparaat dat compatibel is met Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="b9292-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="b9292-180">Een openbare IPv4-adres die zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="b9292-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="b9292-181">U moet uw VPN-apparaat configureren ervaring hebben of dat er iemand die het apparaat voor u configureren kunt.</span><span class="sxs-lookup"><span data-stu-id="b9292-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="b9292-182"><a name="forcedtunnel"></a>Houd rekening met het geforceerd tunnel routering</span><span class="sxs-lookup"><span data-stu-id="b9292-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="b9292-183">U kunt voor de meeste configuraties configureren geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="b9292-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="b9292-184">Geforceerde tunneling kunt u omleiding of 'force' alle internetverkeer terug naar uw on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle.</span><span class="sxs-lookup"><span data-stu-id="b9292-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="b9292-185">Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b9292-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="b9292-186">Zonder geforceerde tunneling wordt internetverkeer van uw virtuele machines in Azure altijd passeren van Azure netwerkinfrastructuur rechtstreeks uit met het Internet, zonder de optie kunt u controleren of het verkeer controleren.</span><span class="sxs-lookup"><span data-stu-id="b9292-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="b9292-187">Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tot vrijgeven van informatie of andere typen schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="b9292-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="b9292-188">Een geforceerde tunneling verbinding kan worden geconfigureerd in beide implementatiemodellen en met behulp van verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b9292-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="b9292-189">Zie voor meer informatie [geforceerde tunneling configureren](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="b9292-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="b9292-190">**Geforceerde tunneling diagram**</span><span class="sxs-lookup"><span data-stu-id="b9292-190">**Forced tunneling diagram**</span></span>

![Azure VPN-Gateway geforceerde tunneling diagram](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="b9292-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b9292-192">Next steps</span></span>

<span data-ttu-id="b9292-193">Zie de [Veelgestelde vragen over het VPN-Gateway](vpn-gateway-vpn-faq.md) en [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikelen voor meer informatie om u te helpen uw ontwerp.</span><span class="sxs-lookup"><span data-stu-id="b9292-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="b9292-194">Zie voor meer informatie over specifieke gatewayinstellingen [over VPN-Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b9292-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>