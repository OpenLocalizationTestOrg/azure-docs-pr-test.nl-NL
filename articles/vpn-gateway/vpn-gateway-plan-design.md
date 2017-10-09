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
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="b152f-103">Planning en ontwerp voor VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b152f-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="b152f-104">Plannen en ontwerpen van uw cross-premises en VNet-naar-VNet-configuraties kunnen zijn eenvoudige of complexe, afhankelijk van de behoeften van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="b152f-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="b152f-105">Dit artikel begeleidt u bij basic plannings- en ontwerpoverwegingen.</span><span class="sxs-lookup"><span data-stu-id="b152f-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="b152f-106"><a name="planning"></a>Plannen</span><span class="sxs-lookup"><span data-stu-id="b152f-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="b152f-107"><a name="compare"></a>Opties voor cross-premises-connectiviteit</span><span class="sxs-lookup"><span data-stu-id="b152f-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="b152f-108">Als u wilt dat tooconnect uw on-premises sites veilig tooa virtueel netwerk, hebt u drie verschillende manieren toodo dus: Site-naar-Site, punt-naar-Site en ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b152f-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="b152f-109">Vergelijk Hallo verschillende cross-premises verbindingen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b152f-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="b152f-110">Hallo-optie die u kiest kan afhankelijk zijn van verschillende overwegingen, zoals:</span><span class="sxs-lookup"><span data-stu-id="b152f-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="b152f-111">Wat voor doorvoer heeft uw oplossing nodig?</span><span class="sxs-lookup"><span data-stu-id="b152f-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="b152f-112">Wilt u toocommunicate via Hallo openbare Internet via een beveiligd VPN, of via een particuliere verbinding?</span><span class="sxs-lookup"><span data-stu-id="b152f-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="b152f-113">Hebt u een openbaar IP-adres beschikbaar toouse?</span><span class="sxs-lookup"><span data-stu-id="b152f-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="b152f-114">Bent u van plan toouse een VPN-apparaat?</span><span class="sxs-lookup"><span data-stu-id="b152f-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="b152f-115">Zo ja, is het compatibel?</span><span class="sxs-lookup"><span data-stu-id="b152f-115">If so, is it compatible?</span></span>
* <span data-ttu-id="b152f-116">Verbindt u slechts enkele computers met elkaar, of u wilt een persistente verbinding voor uw site?</span><span class="sxs-lookup"><span data-stu-id="b152f-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="b152f-117">Welk type VPN-gateway is vereist voor de oplossing Hallo gewenste toocreate?</span><span class="sxs-lookup"><span data-stu-id="b152f-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="b152f-118">Welke gateway SKU moet u gebruiken?</span><span class="sxs-lookup"><span data-stu-id="b152f-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="b152f-119"><a name="planningtable"></a>Tabel plannen</span><span class="sxs-lookup"><span data-stu-id="b152f-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="b152f-120">Hallo volgende tabel kunt u bepalen Hallo beste connectiviteitsoptie voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="b152f-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="b152f-121"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="b152f-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="b152f-122"><a name="wf"></a>Werkstroom</span><span class="sxs-lookup"><span data-stu-id="b152f-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="b152f-123">Hallo Hallo volgende overzichten van de lijst algemene werkstroom voor cloud-verbinding:</span><span class="sxs-lookup"><span data-stu-id="b152f-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="b152f-124">Ontwerp- en plan dat uw connectiviteit topologie en lijst Hallo adresruimten voor alle netwerken u wilt dat tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b152f-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="b152f-125">Maak een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b152f-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="b152f-126">Een VPN-gateway voor Hallo virtueel netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="b152f-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="b152f-127">Maak en configureer verbindingen tooon-premises netwerken of andere virtuele netwerken (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="b152f-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="b152f-128">Maak en configureer een punt-naar-Site-verbinding voor uw Azure VPN-gateway (indien nodig).</span><span class="sxs-lookup"><span data-stu-id="b152f-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="b152f-129"><a name="design"></a>Ontwerp</span><span class="sxs-lookup"><span data-stu-id="b152f-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="b152f-130"><a name="topologies"></a>Topologieën voor verbinding</span><span class="sxs-lookup"><span data-stu-id="b152f-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="b152f-131">Bekijkt hello diagrammen in Hallo [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b152f-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="b152f-132">Hallo artikel bevat basic diagrammen Hallo implementatiemodellen voor elke topologie en Hallo beschikbaar implementatiehulpprogramma's kunt u toodeploy uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="b152f-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="b152f-133"><a name="designbasics"></a>Basisprincipes van ontwerp</span><span class="sxs-lookup"><span data-stu-id="b152f-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="b152f-134">Hallo uit te voeren bespreken basisbeginselen van Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="b152f-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="b152f-135"><a name="servicelimits"></a>Limieten voor netwerken services</span><span class="sxs-lookup"><span data-stu-id="b152f-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="b152f-136">Blader door Hallo tabellen tooview [netwerken services limieten](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b152f-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="b152f-137">uw ontwerp mogelijk van invloed op Hallo-limieten die zijn vermeld.</span><span class="sxs-lookup"><span data-stu-id="b152f-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="b152f-138"><a name="subnets"></a>Over subnetten</span><span class="sxs-lookup"><span data-stu-id="b152f-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="b152f-139">Als u verbindingen maakt, moet u rekening houden met subnet bereiken.</span><span class="sxs-lookup"><span data-stu-id="b152f-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="b152f-140">U kunt geen overlappende subnet-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="b152f-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="b152f-141">Een overlappend subnet is als één virtueel netwerk of on-premises locatie bevat Hallo dezelfde adresruimte die door andere locatie Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="b152f-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="b152f-142">Dit betekent dat u moet uw netwerk engineers voor uw lokale lokale netwerken toocarve uit een bereik voor u toouse voor uw Azure-IP-adressering ruimte/subnetten.</span><span class="sxs-lookup"><span data-stu-id="b152f-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="b152f-143">U moet een adresruimte die niet wordt gebruikt op Hallo lokale on-premises netwerk.</span><span class="sxs-lookup"><span data-stu-id="b152f-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="b152f-144">Vermijden overlappende subnetten is ook belangrijk wanneer u met VNet-naar-VNet-verbindingen werkt.</span><span class="sxs-lookup"><span data-stu-id="b152f-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="b152f-145">Als uw subnetten overlappen en een IP-adres in zowel Hallo verzenden als de doelserver VNets bestaat, mislukt de VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b152f-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="b152f-146">Azure kan geen route Hallo gegevens toohello andere VNet omdat Hallo doeladres deel uitmaakt van Hallo VNet verzenden.</span><span class="sxs-lookup"><span data-stu-id="b152f-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="b152f-147">VPN-Gateways vereist een specifiek subnet met de naam van een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="b152f-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="b152f-148">Alle gatewaysubnetten moeten de naam GatewaySubnet toowork goed.</span><span class="sxs-lookup"><span data-stu-id="b152f-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="b152f-149">Zorg ervoor dat geen tooname het gatewaysubnet van een andere naam geven en virtuele machines of alles anders toohello gatewaysubnet niet implementeren.</span><span class="sxs-lookup"><span data-stu-id="b152f-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="b152f-150">Zie [Gatewaysubnetten](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="b152f-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="b152f-151"><a name="local"></a>Over lokale netwerkgateways</span><span class="sxs-lookup"><span data-stu-id="b152f-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="b152f-152">Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="b152f-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="b152f-153">In het klassieke implementatiemodel hello is de lokale netwerkgateway Hallo waarnaar wordt verwezen tooas een lokale netwerksite.</span><span class="sxs-lookup"><span data-stu-id="b152f-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="b152f-154">Wanneer u een lokale netwerkgateway configureert, u een naam geven, Hallo openbare IP-adres van Hallo on-premises VPN-apparaat en geef Hallo adresvoorvoegsels in Hallo on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="b152f-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="b152f-155">Azure bekijkt hello bestemmingsadressen voor netwerkverkeer, raadpleegt Hallo-configuratie die u hebt opgegeven voor de lokale netwerkgateway Hallo en routeert pakketten dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="b152f-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="b152f-156">U kunt Hallo adresvoorvoegsels zo nodig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b152f-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="b152f-157">Zie voor meer informatie [lokale netwerkgateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="b152f-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="b152f-158"><a name="gwtype"></a>Over gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="b152f-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="b152f-159">Het is essentieel Hallo juiste Gatewaytype voor uw topologie te selecteren.</span><span class="sxs-lookup"><span data-stu-id="b152f-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="b152f-160">Als u het verkeerde type Hallo selecteert, werkt uw gateway niet goed.</span><span class="sxs-lookup"><span data-stu-id="b152f-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="b152f-161">Hallo-Gatewaytype bepaalt hoe Hallo gateway zelf is verbonden en een vereiste configuratie-instelling voor Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b152f-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="b152f-162">Hallo gatewaytypen zijn:</span><span class="sxs-lookup"><span data-stu-id="b152f-162">hello gateway types are:</span></span>

* <span data-ttu-id="b152f-163">VPN</span><span class="sxs-lookup"><span data-stu-id="b152f-163">Vpn</span></span>
* <span data-ttu-id="b152f-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b152f-164">ExpressRoute</span></span>

#### <span data-ttu-id="b152f-165"><a name="connectiontype"></a>Over verbindingstypen</span><span class="sxs-lookup"><span data-stu-id="b152f-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="b152f-166">Elke configuratie vereist een specifiek verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="b152f-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="b152f-167">Hallo verbindingstypen zijn:</span><span class="sxs-lookup"><span data-stu-id="b152f-167">hello connection types are:</span></span>

* <span data-ttu-id="b152f-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="b152f-168">IPsec</span></span>
* <span data-ttu-id="b152f-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="b152f-169">Vnet2Vnet</span></span>
* <span data-ttu-id="b152f-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b152f-170">ExpressRoute</span></span>
* <span data-ttu-id="b152f-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="b152f-171">VPNClient</span></span>

#### <span data-ttu-id="b152f-172"><a name="vpntype"></a>Over VPN-typen</span><span class="sxs-lookup"><span data-stu-id="b152f-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="b152f-173">Elke configuratie vereist een specifiek VPN-type.</span><span class="sxs-lookup"><span data-stu-id="b152f-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="b152f-174">Als u twee configuraties, zoals het maken van een Site-naar-Site-verbinding en een punt-naar-Site-verbinding toohello combineert hetzelfde VNet, moet u een VPN-type dat voldoet aan de vereisten van beide verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b152f-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="b152f-175">Hallo volgende tabellen bevatten Hallo VPN-type als de verbindingsconfiguratie tooeach wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b152f-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="b152f-176">Zorg ervoor dat Hallo VPN-type voor uw gateway komt overeen met Hallo configuratie die u toocreate wilt.</span><span class="sxs-lookup"><span data-stu-id="b152f-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="b152f-177"><a name="devices"></a>VPN-apparaten voor Site-naar-Site-verbindingen</span><span class="sxs-lookup"><span data-stu-id="b152f-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="b152f-178">tooconfigure een Site-naar-Site-verbinding, ongeacht het implementatiemodel, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="b152f-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="b152f-179">Een VPN-apparaat dat compatibel is met Azure VPN-gateways</span><span class="sxs-lookup"><span data-stu-id="b152f-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="b152f-180">Een openbare IPv4-adres die zich niet achter een NAT bevinden.</span><span class="sxs-lookup"><span data-stu-id="b152f-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="b152f-181">U moet toohave ervaring voor configuratie van uw VPN-apparaat, of iemand zijn en kunnen Hallo apparaat configureren voor u.</span><span class="sxs-lookup"><span data-stu-id="b152f-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="b152f-182"><a name="forcedtunnel"></a>Houd rekening met het geforceerd tunnel routering</span><span class="sxs-lookup"><span data-stu-id="b152f-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="b152f-183">U kunt voor de meeste configuraties configureren geforceerde tunneling.</span><span class="sxs-lookup"><span data-stu-id="b152f-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="b152f-184">Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle.</span><span class="sxs-lookup"><span data-stu-id="b152f-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="b152f-185">Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="b152f-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="b152f-186">Zonder geforceerde tunneling wordt internetverkeer van uw virtuele machines in Azure altijd passeren van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer.</span><span class="sxs-lookup"><span data-stu-id="b152f-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="b152f-187">Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.</span><span class="sxs-lookup"><span data-stu-id="b152f-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="b152f-188">Een geforceerde tunneling verbinding kan worden geconfigureerd in beide implementatiemodellen en met behulp van verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b152f-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="b152f-189">Zie voor meer informatie [geforceerde tunneling configureren](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="b152f-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="b152f-190">**Geforceerde tunneling diagram**</span><span class="sxs-lookup"><span data-stu-id="b152f-190">**Forced tunneling diagram**</span></span>

![Azure VPN-Gateway geforceerde tunneling diagram](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="b152f-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b152f-192">Next steps</span></span>

<span data-ttu-id="b152f-193">Zie Hallo [Veelgestelde vragen over het VPN-Gateway](vpn-gateway-vpn-faq.md) en [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikelen voor meer informatie toohelp u bij uw ontwerp.</span><span class="sxs-lookup"><span data-stu-id="b152f-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="b152f-194">Zie voor meer informatie over specifieke gatewayinstellingen [over VPN-Gateway-instellingen](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b152f-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>