---
title: 'ExpressRoute- en site-naar-site-VPN-verbindingen configureren die naast elkaar kunnen worden gebruikt: klassiek: Azure | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van ExpressRoute en Site-naar-Site VPN-verbindingen die naast elkaar kan bestaan voor het klassieke implementatiemodel Hallo.
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="05a66-103">Gelijktijdige ExpressRoute- en site-to-site-verbindingen configureren (klassiek)</span><span class="sxs-lookup"><span data-stu-id="05a66-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="05a66-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="05a66-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="05a66-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="05a66-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="05a66-106">Hallo mogelijkheid tooconfigure Site-naar-Site VPN en ExpressRoute heeft verschillende voordelen.</span><span class="sxs-lookup"><span data-stu-id="05a66-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="05a66-107">U kunt Site-naar-Site-VPN configureren als een beveiligd failoverpad voor ExressRoute of Site-naar-Site VPN-verbindingen tooconnect toosites die niet zijn verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="05a66-108">Wordt ingegaan op het Hallo stappen tooconfigure beide scenario's in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="05a66-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="05a66-109">In dit artikel is van toepassing toohello klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="05a66-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="05a66-110">Deze configuratie is niet beschikbaar in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="05a66-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="05a66-111">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="05a66-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="05a66-112">ExpressRoute-circuits moeten vooraf worden geconfigureerd voordat u Hallo onderstaande instructies volgt.</span><span class="sxs-lookup"><span data-stu-id="05a66-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="05a66-113">Zorg ervoor dat u Hallo handleidingen te hebt gevolgd[maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) en [routering configureren](expressroute-howto-routing-classic.md) voordat u Hallo hieronder stappen.</span><span class="sxs-lookup"><span data-stu-id="05a66-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="05a66-114">Limieten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="05a66-114">Limits and limitations</span></span>
* <span data-ttu-id="05a66-115">**Transitroutering wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="05a66-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="05a66-116">U kunt niet (via Azure) routeren tussen uw lokale netwerk dat is verbonden via site-naar-site-VPN en uw lokale netwerk dat is verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="05a66-117">**Punt-naar-site wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="05a66-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="05a66-118">U kunt daar geen punt-naar-site VPN-verbindingen toohello hetzelfde VNet dat is verbonden tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="05a66-119">Punt-naar-site-VPN en ExpressRoute kunnen niet worden gecombineerd voor Hallo hetzelfde VNet.</span><span class="sxs-lookup"><span data-stu-id="05a66-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="05a66-120">**Geforceerde tunneling kan niet worden ingeschakeld op Hallo Site-naar-Site VPN-gateway.**</span><span class="sxs-lookup"><span data-stu-id="05a66-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="05a66-121">U kunt alleen 'forceren' alle Internet bestemd verkeer back tooyour on-premises netwerk via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="05a66-122">**Basic SKU-gateway wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="05a66-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="05a66-123">U moet een niet - basis-SKU-gateway gebruiken voor beide Hallo [ExpressRoute-gateway](expressroute-about-virtual-network-gateways.md) en Hallo [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="05a66-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="05a66-124">**Alleen een op route gebaseerde VPN-gateway wordt ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="05a66-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="05a66-125">U moet een op route gebaseerde [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05a66-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="05a66-126">**Statische route moet worden geconfigureerd voor de VPN-gateway.**</span><span class="sxs-lookup"><span data-stu-id="05a66-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="05a66-127">Als uw lokale netwerk verbonden tooboth ExpressRoute is en een Site-naar-Site VPN, u een statische route geconfigureerd in uw lokale netwerk tooroute Hallo Site-naar-Site VPN-verbinding toohello hebben moet openbare Internet.</span><span class="sxs-lookup"><span data-stu-id="05a66-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="05a66-128">**ExpressRoute gateway moet eerst worden geconfigureerd.**</span><span class="sxs-lookup"><span data-stu-id="05a66-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="05a66-129">U moet eerst Hallo ExpressRoute-gateway maken voordat u Hallo Site-naar-Site VPN-gateway toevoegt.</span><span class="sxs-lookup"><span data-stu-id="05a66-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="05a66-130">Configuratie-ontwerpen</span><span class="sxs-lookup"><span data-stu-id="05a66-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="05a66-131">Een site-naar-site-VPN configureren als een failoverpad voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="05a66-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="05a66-132">U kunt een site-naar-site-VPN-verbinding configureren als een back-up voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="05a66-133">Dit geldt alleen toovirtual netwerken gekoppelde toohello pad Azure-persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="05a66-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="05a66-134">Er is geen op VPN gebaseerde failoveroplossing voor services die toegankelijk zijn via openbare Azure- en Microsoft-peerings.</span><span class="sxs-lookup"><span data-stu-id="05a66-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="05a66-135">Hallo ExpressRoute-circuit is altijd Hallo primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="05a66-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="05a66-136">Gegevens worden overgebracht via Site-naar-Site VPN-pad Hallo alleen als Hallo ExpressRoute-circuit is mislukt.</span><span class="sxs-lookup"><span data-stu-id="05a66-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="05a66-137">ExpressRoute-circuit is voorkeur via Site-naar-Site VPN wanneer beide routes worden dezelfde hello, gebruikt Azure Hallo langste voorvoegsel overeen toochoose Hallo route naar de bestemming hello-pakket.</span><span class="sxs-lookup"><span data-stu-id="05a66-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="05a66-139">Een Site-naar-Site VPN-tooconnect toosites niet is verbonden via ExpressRoute configureren</span><span class="sxs-lookup"><span data-stu-id="05a66-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="05a66-140">U kunt uw netwerk waarbij sommige sites verbinding rechtstreeks tooAzure via Site-naar-Site VPN en sommige sites verbinding maken via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="05a66-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="05a66-142">U kunt een virtueel netwerk niet configureren als transitrouter.</span><span class="sxs-lookup"><span data-stu-id="05a66-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="05a66-143">Hallo stappen toouse selecteren</span><span class="sxs-lookup"><span data-stu-id="05a66-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="05a66-144">Er zijn twee sets met procedures toochoose uit in de volgorde tooconfigure verbindingen die naast elkaar kunnen bestaan.</span><span class="sxs-lookup"><span data-stu-id="05a66-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="05a66-145">Hallo-configuratieprocedure u selecteert afhankelijk van of u een bestaand virtueel netwerk dat u tooconnect naar wilt, of u wilt dat toocreate een nieuw virtueel netwerk hebt.</span><span class="sxs-lookup"><span data-stu-id="05a66-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="05a66-146">Ik heb geen VNet en moet er toocreate een.</span><span class="sxs-lookup"><span data-stu-id="05a66-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="05a66-147">Als u niet al een virtueel netwerk hebt, begeleidt deze procedure u stapsgewijs door het maken van een nieuw virtueel netwerk met behulp van het klassieke implementatiemodel Hallo en het maken van nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="05a66-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="05a66-148">tooconfigure, Hallo Volg de stappen in de sectie artikel Hallo [toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen](#new).</span><span class="sxs-lookup"><span data-stu-id="05a66-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="05a66-149">Ik heb al een VNet met het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="05a66-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="05a66-150">Mogelijk hebt u al een virtueel netwerk met een bestaande site-naar-site-VPN-verbinding of ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="05a66-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="05a66-151">sectie artikel Hallo [tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet](#add) begeleidt u bij het verwijderen van Hallo-gateway en vervolgens het maken van nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="05a66-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="05a66-152">Houd er rekening mee dat wanneer u nieuwe verbindingen maakt hello, Hallo stappen moeten worden uitgevoerd in een specifieke volgorde.</span><span class="sxs-lookup"><span data-stu-id="05a66-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="05a66-153">Gebruik geen Hallo-instructies in de andere artikelen toocreate uw gateways en verbindingen.</span><span class="sxs-lookup"><span data-stu-id="05a66-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="05a66-154">In deze procedure, maken verbindingen die naast elkaar kunnen bestaan vereisen toodelete u uw gateway, en vervolgens nieuwe gateways configureren.</span><span class="sxs-lookup"><span data-stu-id="05a66-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="05a66-155">Dit betekent dat u uitvaltijd voor uw cross-premises verbindingen terwijl u verwijderen en opnieuw maken van uw gateway en verbindingen, maar u niet toomigrate hoeft van uw virtuele machines of services tooa nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="05a66-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="05a66-156">Uw virtuele machines en services nog steeds kunnen toocommunicate uit via Hallo load balancer terwijl u uw gateway configureren als ze geconfigureerde toodo dus zijn.</span><span class="sxs-lookup"><span data-stu-id="05a66-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="05a66-157"><a name="new"></a>toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen</span><span class="sxs-lookup"><span data-stu-id="05a66-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="05a66-158">Deze procedure helpt u bij het maken van een VNet en site-naar-site- en ExpressRoute-verbindingen die naast elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="05a66-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="05a66-159">U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05a66-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="05a66-160">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05a66-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="05a66-161">Houd er rekening mee dat Hallo-cmdlets die u voor deze configuratie mogelijk enigszins afwijken van wat u mogelijk bekend zijn met.</span><span class="sxs-lookup"><span data-stu-id="05a66-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="05a66-162">Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies.</span><span class="sxs-lookup"><span data-stu-id="05a66-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="05a66-163">Maak een schema voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="05a66-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="05a66-164">Zie voor meer informatie over het configuratieschema Hallo [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="05a66-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="05a66-165">Wanneer u uw schema maakt, moet dat u Hallo volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="05a66-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="05a66-166">Hallo gatewaysubnet voor het virtuele netwerk Hallo moet/27 of een korter voorvoegsel (zoals/26 of /25).</span><span class="sxs-lookup"><span data-stu-id="05a66-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="05a66-167">gateway-verbindingstype Hallo 'speciale' is.</span><span class="sxs-lookup"><span data-stu-id="05a66-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="05a66-168">Na het maken en configureren van uw XML-schemabestanden, Hallo-bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="05a66-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="05a66-169">Hiermee maakt u het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="05a66-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="05a66-170">Hallo cmdlet tooupload na het bestand en vervang Hallo waarde door uw eigen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05a66-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="05a66-171"><a name="gw"></a>Maak een ExpressRoute-gateway.</span><span class="sxs-lookup"><span data-stu-id="05a66-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="05a66-172">Ervoor toospecify worden Hallo GatewaySKU *standaard*, *HighPerformance*, of *UltraPerformance* en GatewayType Hallo *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="05a66-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="05a66-173">Hallo voorbeeld te volgen, vervangen door Hallo waarden voor uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="05a66-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="05a66-174">Koppeling Hallo ExpressRoute-gateway toohello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="05a66-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="05a66-175">Nadat deze stap is voltooid, Hallo-verbinding tussen uw on-premises netwerk en Azure via ExpressRoute, tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="05a66-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="05a66-176"><a name="vpngw"></a>Maak vervolgens uw site-naar-site-VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="05a66-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="05a66-177">Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance* en hello GatewayType *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="05a66-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="05a66-178">tooretrieve hello virtueel netwerk gatewayinstellingen, inclusief Hallo gateway-ID en Hallo openbare IP-adres gebruiken Hallo `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05a66-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="05a66-179">Maak een lokaal exemplaar van de VPN-gateway van uw site.</span><span class="sxs-lookup"><span data-stu-id="05a66-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="05a66-180">Deze opdracht wordt niet gebruikt om uw on-premises VPN-gateway te configureren.</span><span class="sxs-lookup"><span data-stu-id="05a66-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="05a66-181">In plaats daarvan kunt u Hiermee tooprovide Hallo lokale gateway-instellingen, zoals Hallo openbare IP-adres en hello op premises-adresruimte, zodat hello Azure VPN-gateway verbinding tooit maken kan.</span><span class="sxs-lookup"><span data-stu-id="05a66-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="05a66-182">Hallo lokale site voor Hallo Site-naar-Site VPN is niet gedefinieerd in Hallo netcfg.</span><span class="sxs-lookup"><span data-stu-id="05a66-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="05a66-183">In plaats daarvan moet u deze cmdlet-parameters voor lokale site toospecify hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05a66-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="05a66-184">U kunt met behulp van de portal of Hallo netcfg-bestand niet definiëren.</span><span class="sxs-lookup"><span data-stu-id="05a66-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="05a66-185">Hallo volgende voorbeeld, waarbij Hallo waarden vervangt door uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="05a66-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="05a66-186">Als uw lokale netwerk meerdere routes heeft, kunt u ze doorgeven als een matrix.</span><span class="sxs-lookup"><span data-stu-id="05a66-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="05a66-187">$MyLocalNetworkAddress = @('10.1.2.0/24', '10.1.3.0/24', '10.2.1.0/24')</span><span class="sxs-lookup"><span data-stu-id="05a66-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="05a66-188">tooretrieve hello virtueel netwerk gatewayinstellingen, inclusief Hallo gateway-ID en Hallo openbare IP-adres gebruiken Hallo `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05a66-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="05a66-189">Zie Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="05a66-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="05a66-190">Configureer uw lokale VPN-apparaat tooconnect toohello nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="05a66-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="05a66-191">Hallo-informatie die u hebt opgehaald in stap 6 bij het configureren van uw VPN-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="05a66-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="05a66-192">Zie [VPN-apparaatconfiguratie](../vpn-gateway/vpn-gateway-about-vpn-devices.md) voor meer informatie over het configureren van een VPN-apparaat. </span><span class="sxs-lookup"><span data-stu-id="05a66-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="05a66-193">Koppeling Hallo Site-naar-Site VPN-gateway op de lokale gateway Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="05a66-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="05a66-194">In dit voorbeeld is connectedEntityId de lokale gateway-id. hello, kunt u vinden door te voeren `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="05a66-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="05a66-195">U kunt virtualnetworkgatewayid vinden met behulp van Hallo `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="05a66-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="05a66-196">Na deze stap Hallo verbinding tussen uw lokale netwerk en Azure via Hallo Site-naar-Site VPN-verbinding tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="05a66-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="05a66-197"><a name="add"></a>tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet</span><span class="sxs-lookup"><span data-stu-id="05a66-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="05a66-198">Als u een bestaand virtueel netwerk hebt, controleert u Hallo gateway subnetgrootte.</span><span class="sxs-lookup"><span data-stu-id="05a66-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="05a66-199">Als Hallo gatewaysubnet/28 of slechts/29 is, moet u Hallo virtuele netwerkgateway verwijderen en vergroot Hallo gateway-subnet.</span><span class="sxs-lookup"><span data-stu-id="05a66-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="05a66-200">Hallo stappen in deze sectie wordt uitgelegd hoe u toodo die.</span><span class="sxs-lookup"><span data-stu-id="05a66-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="05a66-201">Als Hallo gatewaysubnet/27 of groter en Hallo virtueel netwerk is verbonden via ExpressRoute, kunt u Hallo onderstaande stappen overslaan en doorgaan te['Stap 6: een Site-naar-Site VPN-gateway maken'](#vpngw) in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="05a66-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="05a66-202">Wanneer u Hallo bestaande gateway verwijdert, wordt uw lokale site Hallo verbinding tooyour virtuele netwerk verbroken terwijl u bezig bent met deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="05a66-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="05a66-203">U moet tooinstall Hallo meest recente versie van hello Azure Resource Manager PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05a66-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="05a66-204">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="05a66-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="05a66-205">Houd er rekening mee dat Hallo-cmdlets die u voor deze configuratie mogelijk enigszins afwijken van wat u mogelijk bekend zijn met.</span><span class="sxs-lookup"><span data-stu-id="05a66-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="05a66-206">Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies.</span><span class="sxs-lookup"><span data-stu-id="05a66-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="05a66-207">Verwijder de bestaande ExpressRoute of Site-naar-Site VPN-gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="05a66-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="05a66-208">Hallo volgende cmdlet, waarbij Hallo waarden vervangt door uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="05a66-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="05a66-209">Hallo virtueel netwerk schema exporteren.</span><span class="sxs-lookup"><span data-stu-id="05a66-209">Export hello virtual network schema.</span></span> <span data-ttu-id="05a66-210">Hallo volgende PowerShell-cmdlet, waarbij Hallo waarden vervangt door uw eigen gebruik.</span><span class="sxs-lookup"><span data-stu-id="05a66-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="05a66-211">Hallo network-configuratieschema bestand bewerken zodat Hallo gatewaysubnet/27 of een korter voorvoegsel (zoals/26 of /25).</span><span class="sxs-lookup"><span data-stu-id="05a66-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="05a66-212">Zie Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="05a66-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="05a66-213">Als u geen voldoende IP-adressen in uw virtuele netwerk tooincrease Hallo gateway subnetgrootte gelaten, moet u tooadd meer IP-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="05a66-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="05a66-214">Zie voor meer informatie over het configuratieschema Hallo [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="05a66-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="05a66-215">Als uw vorige gateway een Site-naar-Site-VPN was, moet u ook wijzigen Hallo verbindingstype te**toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="05a66-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="05a66-216">U hebt op dit moment een VNet zonder gateways.</span><span class="sxs-lookup"><span data-stu-id="05a66-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="05a66-217">toocreate nieuwe gateways en uw verbindingen is voltooid, kunt u doorgaan met [stap 4 - een ExpressRoute-gateway maken](#gw)vindt u in de voorgaande reeks stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="05a66-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05a66-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05a66-218">Next steps</span></span>
<span data-ttu-id="05a66-219">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="05a66-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

