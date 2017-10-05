---
title: 'ExpressRoute- en site-naar-site-VPN-verbindingen configureren die naast elkaar kunnen worden gebruikt: klassiek: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het configureren van ExpressRoute- en site-naar-site-VPN-verbindingen die naast elkaar kunnen worden gebruikt in het klassieke implementatiemodel.
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
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="8afd8-103">Gelijktijdige ExpressRoute- en site-to-site-verbindingen configureren (klassiek)</span><span class="sxs-lookup"><span data-stu-id="8afd8-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8afd8-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8afd8-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="8afd8-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="8afd8-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="8afd8-106">De mogelijkheid om site-naar-site-VPN en ExpressRoute te configureren heeft verschillende voordelen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="8afd8-107">U kunt site-naar-site-VPN configureren als een beveiligd failoverpad voor ExressRoute of site-naar-site-VPN’s gebruiken om verbinding te maken met sites die niet zijn verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="8afd8-108">In dit artikel gaan we in op de stappen voor het configureren van beide scenario's.</span><span class="sxs-lookup"><span data-stu-id="8afd8-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="8afd8-109">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8afd8-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="8afd8-110">Deze configuratie is niet beschikbaar in de portal.</span><span class="sxs-lookup"><span data-stu-id="8afd8-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="8afd8-111">**Over Azure-implementatiemodellen**</span><span class="sxs-lookup"><span data-stu-id="8afd8-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="8afd8-112">ExpressRoute-circuits moeten vooraf worden geconfigureerd voordat u de onderstaande instructies volgt.</span><span class="sxs-lookup"><span data-stu-id="8afd8-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="8afd8-113">Zorg ervoor dat u de handleidingen hebt gevolgd [om een ExpressRoute-circuit te maken](expressroute-howto-circuit-classic.md) en [routering te configureren](expressroute-howto-routing-classic.md) voordat u de volgende stappen volgt.</span><span class="sxs-lookup"><span data-stu-id="8afd8-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="8afd8-114">Limieten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="8afd8-114">Limits and limitations</span></span>
* <span data-ttu-id="8afd8-115">**Transitroutering wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="8afd8-116">U kunt niet (via Azure) routeren tussen uw lokale netwerk dat is verbonden via site-naar-site-VPN en uw lokale netwerk dat is verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="8afd8-117">**Punt-naar-site wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="8afd8-118">U kunt geen punt-naar-site-VPN-verbindingen inschakelen naar het hetzelfde VNet dat is verbonden met ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="8afd8-119">Punt-naar-site-VPN en ExpressRoute kunnen niet worden gecombineerd voor hetzelfde VNet.</span><span class="sxs-lookup"><span data-stu-id="8afd8-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="8afd8-120">**Geforceerde tunneling kan niet worden ingeschakeld op de site-naar-site VPN-gateway.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="8afd8-121">U kunt alle internetverkeer alleen via ExpressRoute terug naar uw on-premises netwerk ‘forceren’.</span><span class="sxs-lookup"><span data-stu-id="8afd8-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="8afd8-122">**Basic SKU-gateway wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="8afd8-123">U moet een niet-basic SKU-gateway gebruiken voor zowel de [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) als de [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8afd8-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8afd8-124">**Alleen een op route gebaseerde VPN-gateway wordt ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="8afd8-125">U moet een op route gebaseerde [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8afd8-126">**Statische route moet worden geconfigureerd voor de VPN-gateway.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="8afd8-127">Als uw lokale netwerk is verbonden met ExpressRoute en een site-naar-site-VPN, moet u in uw lokale netwerk een statische route hebben geconfigureerd voor het routeren van de site-naar-site-VPN-verbinding met het openbare internet.</span><span class="sxs-lookup"><span data-stu-id="8afd8-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="8afd8-128">**ExpressRoute gateway moet eerst worden geconfigureerd.**</span><span class="sxs-lookup"><span data-stu-id="8afd8-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="8afd8-129">U moet eerst de ExpressRoute-gateway maken voordat u de site-naar-site-VPN-gateway kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="8afd8-130">Configuratie-ontwerpen</span><span class="sxs-lookup"><span data-stu-id="8afd8-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="8afd8-131">Een site-naar-site-VPN configureren als een failoverpad voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8afd8-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="8afd8-132">U kunt een site-naar-site-VPN-verbinding configureren als een back-up voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="8afd8-133">Dit geldt alleen voor virtuele netwerken die zijn gekoppeld aan het pad voor persoonlijke Azure-peering.</span><span class="sxs-lookup"><span data-stu-id="8afd8-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="8afd8-134">Er is geen op VPN gebaseerde failoveroplossing voor services die toegankelijk zijn via openbare Azure- en Microsoft-peerings.</span><span class="sxs-lookup"><span data-stu-id="8afd8-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="8afd8-135">Het ExpressRoute-circuit is altijd de primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="8afd8-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="8afd8-136">Gegevens worden alleen via het site-naar-site-VPN-pad geleid als het ExpressRoute-circuit niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="8afd8-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="8afd8-137">Hoewel een ExpressRoute-circuit de voorkeur heeft boven site-naar-site-VPN wanneer beide routes hetzelfde zijn, gebruikt Azure de langste voorvoegselovereenkomst om de route naar de bestemming van het pakket te kiezen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="8afd8-139">Een site-naar-site-VPN configureren om verbinding te maken met sites die niet zijn verbonden via ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8afd8-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="8afd8-140">U kunt uw netwerk zodanig configureren dat sommige sites rechtstreeks verbinding maken met Azure via site-naar-site-VPN en sommige sites verbinding maken via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="8afd8-142">U kunt een virtueel netwerk niet configureren als transitrouter.</span><span class="sxs-lookup"><span data-stu-id="8afd8-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="8afd8-143">De stappen selecteren die u gaat gebruiken</span><span class="sxs-lookup"><span data-stu-id="8afd8-143">Selecting the steps to use</span></span>
<span data-ttu-id="8afd8-144">Er zijn twee sets met procedures waaruit u kunt kiezen om verbindingen te configureren die naast elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8afd8-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="8afd8-145">Welke configuratieprocedure u selecteert, is afhankelijk van het gegeven of u een bestaand virtueel netwerk hebt waarmee u verbinding wilt maken, of of u een nieuw virtueel netwerk wilt maken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="8afd8-146">Ik heb geen VNet en moet er een maken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="8afd8-147">Als u nog geen virtueel netwerk hebt, begeleidt deze procedure u bij het maken van een nieuw virtueel netwerk met behulp van het klassieke implementatiemodel, en bij het maken van nieuwe ExpressRoute- en site-naar-site-VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8afd8-148">Volg voor de configuratie de stappen in het gedeelte [Een nieuw virtueel netwerk en naast elkaar bestaande verbindingen maken](#new) in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8afd8-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="8afd8-149">Ik heb al een VNet met het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8afd8-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="8afd8-150">Mogelijk hebt u al een virtueel netwerk met een bestaande site-naar-site-VPN-verbinding of ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="8afd8-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="8afd8-151">Het gedeelte [Naast elkaar bestaande verbindingen configureren voor een bestaand VNet](#add) in dit artikel begeleidt u bij het verwijderen van de gateway en vervolgens bij het maken van nieuwe ExpressRoute- en site-naar-site-VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8afd8-152">Houd er rekening mee dat de stappen voor het maken van de nieuwe verbindingen moeten worden uitgevoerd in een specifieke volgorde.</span><span class="sxs-lookup"><span data-stu-id="8afd8-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="8afd8-153">Gebruik geen instructies uit andere artikelen om uw gateways en verbindingen te maken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="8afd8-154">In deze procedure moet u uw gateway verwijderen en vervolgens nieuwe gateways configureren om verbindingen te maken die naast elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8afd8-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="8afd8-155">Dit betekent dat u tijdens het verwijderen en opnieuw maken van uw gateway en verbindingen rekening moet houden met uitvaltijd voor uw cross-premises verbindingen. U hoeft uw virtuele machines of services echter niet te migreren naar een nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="8afd8-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="8afd8-156">Terwijl u uw gateway configureert, kunnen uw virtuele machines en services nog steeds communiceren via de load balancer, mits ze hiervoor zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8afd8-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="8afd8-157"><a name="new"></a>Een nieuw virtueel netwerk en naast elkaar bestaande verbindingen maken</span><span class="sxs-lookup"><span data-stu-id="8afd8-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="8afd8-158">Deze procedure helpt u bij het maken van een VNet en site-naar-site- en ExpressRoute-verbindingen die naast elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8afd8-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="8afd8-159">U moet de meest recente versie van de Azure PowerShell-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="8afd8-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8afd8-160">Zie [How to install and configure Azure PowerShell](/powershell/azure/overview) (Azure PowerShell installeren en configureren) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8afd8-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8afd8-161">Houd er rekening mee dat de cmdlets die u voor deze configuratie gebruikt, mogelijk enigszins afwijken van de cmdlets waarmee u bekend bent.</span><span class="sxs-lookup"><span data-stu-id="8afd8-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8afd8-162">Zorg ervoor dat u de cmdlets gebruikt die in deze instructies worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="8afd8-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8afd8-163">Maak een schema voor het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="8afd8-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="8afd8-164">Zie [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx) voor meer informatie over het configuratieschema.</span><span class="sxs-lookup"><span data-stu-id="8afd8-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="8afd8-165">Wanneer u uw schema maakt, moet u de volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8afd8-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="8afd8-166">Het gatewaysubnet voor het virtuele netwerk moet /27 of een korter voorvoegsel (zoals /26 of /25) zijn.</span><span class="sxs-lookup"><span data-stu-id="8afd8-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="8afd8-167">Het verbindingstype van de gateway is Toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-167">The gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="8afd8-168">Upload het bestand nadat u het XML-schemabestand hebt gemaakt en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8afd8-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="8afd8-169">Hiermee maakt u het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="8afd8-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="8afd8-170">Gebruik de volgende cmdlet voor het uploaden van het bestand en vervang de waarde door uw eigen waarde.</span><span class="sxs-lookup"><span data-stu-id="8afd8-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="8afd8-171"><a name="gw"></a>Maak een ExpressRoute-gateway.</span><span class="sxs-lookup"><span data-stu-id="8afd8-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="8afd8-172">Zorg ervoor dat u de GatewaySKU opgeeft als *Standard*, *HighPerformance* of *UltraPerformance* en het GatewayType als *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8afd8-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="8afd8-173">Gebruik het volgende voorbeeld, waarbij u de waarden vervangt door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="8afd8-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="8afd8-174">Koppel de ExpressRoute-gateway aan het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="8afd8-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="8afd8-175">Nadat deze stap is voltooid, wordt de verbinding tussen uw on-premises netwerk en Azure tot stand gebracht via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8afd8-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="8afd8-176"><a name="vpngw"></a>Maak vervolgens uw site-naar-site-VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="8afd8-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8afd8-177">De GatewaySKU moet zijn ingesteld op *Standard*, *HighPerformance* of *UltraPerformance* en het GatewayType op *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8afd8-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="8afd8-178">Gebruik de cmdlet `Get-AzureVirtualNetworkGateway` om de instellingen van de gateway van het virtuele netwerk op te halen, waaronder de gateway-ID en het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8afd8-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
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
7. <span data-ttu-id="8afd8-179">Maak een lokaal exemplaar van de VPN-gateway van uw site.</span><span class="sxs-lookup"><span data-stu-id="8afd8-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="8afd8-180">Deze opdracht wordt niet gebruikt om uw on-premises VPN-gateway te configureren.</span><span class="sxs-lookup"><span data-stu-id="8afd8-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="8afd8-181">Met deze opdracht kunt u de instellingen voor de lokale gateway opgeven, zoals het openbare IP-adres en de on-premises-adresruimte, zodat de Azure VPN-gateway er verbinding mee kan maken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8afd8-182">De lokale site voor de site-naar-site-VPN-verbinding is niet gedefinieerd in de netcfg.</span><span class="sxs-lookup"><span data-stu-id="8afd8-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="8afd8-183">In plaats daarvan moet u deze cmdlet gebruiken om de parameters van de lokale site op te geven.</span><span class="sxs-lookup"><span data-stu-id="8afd8-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="8afd8-184">U kunt deze niet definiëren met de portal of het netcfg-bestand.</span><span class="sxs-lookup"><span data-stu-id="8afd8-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="8afd8-185">Gebruik het volgende voorbeeld, waarbij u de waarden vervangt door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="8afd8-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="8afd8-186">Als uw lokale netwerk meerdere routes heeft, kunt u ze doorgeven als een matrix.</span><span class="sxs-lookup"><span data-stu-id="8afd8-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="8afd8-187">$MyLocalNetworkAddress = @('10.1.2.0/24', '10.1.3.0/24', '10.2.1.0/24')</span><span class="sxs-lookup"><span data-stu-id="8afd8-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="8afd8-188">Gebruik de cmdlet `Get-AzureVirtualNetworkGateway` om de instellingen van de gateway van het virtuele netwerk op te halen, waaronder de gateway-ID en het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8afd8-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8afd8-189">Zie het volgende voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8afd8-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="8afd8-190">Configureer het lokale VPN-apparaat om verbinding te maken met de nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="8afd8-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="8afd8-191">Gebruik de informatie die u in stap 6 bij de configuratie van uw VPN-apparaat hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="8afd8-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="8afd8-192">Zie [VPN-apparaatconfiguratie](../vpn-gateway/vpn-gateway-about-vpn-devices.md) voor meer informatie over het configureren van een VPN-apparaat. </span><span class="sxs-lookup"><span data-stu-id="8afd8-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="8afd8-193">Koppel de site-naar-site-VPN-gateway in Azure aan de lokale gateway.</span><span class="sxs-lookup"><span data-stu-id="8afd8-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="8afd8-194">In dit voorbeeld is connectedEntityId de lokale gateway-ID. Deze kunt u vinden door `Get-AzureLocalNetworkGateway` uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8afd8-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="8afd8-195">U kunt virtualNetworkGatewayId vinden met behulp van de cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8afd8-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8afd8-196">Na deze stap wordt de verbinding tussen uw lokale netwerk en Azure tot stand gebracht via de site-naar-site-VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="8afd8-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="8afd8-197"><a name="add"></a>Naast elkaar bestaande verbindingen configureren voor een bestaand VNet</span><span class="sxs-lookup"><span data-stu-id="8afd8-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="8afd8-198">Als u een bestaand virtueel netwerk hebt, controleert u de grootte van het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="8afd8-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="8afd8-199">Als het gatewaysubnet /28 of /29 is, moet u eerst de gateway van het virtuele netwerk verwijderen en het gatewaysubnet vergroten.</span><span class="sxs-lookup"><span data-stu-id="8afd8-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="8afd8-200">In de stappen in dit gedeelte wordt beschreven hoe u dat doet.</span><span class="sxs-lookup"><span data-stu-id="8afd8-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="8afd8-201">Als het gatewaysubnet /27 of groter is en het virtuele netwerk is verbonden via ExpressRoute, kunt u onderstaande stappen overslaan en doorgaan met [Stap 6 - Een site-naar-site-VPN-gateway maken](#vpngw) in het vorige gedeelte.</span><span class="sxs-lookup"><span data-stu-id="8afd8-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="8afd8-202">Als u de bestaande gateway verwijdert terwijl u bezig bent met deze configuratie, wordt de verbinding tussen uw lokale site en uw virtuele netwerk verbroken.</span><span class="sxs-lookup"><span data-stu-id="8afd8-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="8afd8-203">U moet de meest recente versie van de Azure Resource Manager PowerShell-cmdlets installeren.</span><span class="sxs-lookup"><span data-stu-id="8afd8-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="8afd8-204">Zie [How to install and configure Azure PowerShell](/powershell/azure/overview) (Azure PowerShell installeren en configureren) voor meer informatie over het installeren van de PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8afd8-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8afd8-205">Houd er rekening mee dat de cmdlets die u voor deze configuratie gebruikt, mogelijk enigszins afwijken van de cmdlets waarmee u bekend bent.</span><span class="sxs-lookup"><span data-stu-id="8afd8-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8afd8-206">Zorg ervoor dat u de cmdlets gebruikt die in deze instructies worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="8afd8-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8afd8-207">Verwijder de bestaande ExpressRoute- of site-naar-site-VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="8afd8-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8afd8-208">Gebruik de volgende cmdlet, waarbij u de waarden vervangt door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="8afd8-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="8afd8-209">Exporteer het schema van het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="8afd8-209">Export the virtual network schema.</span></span> <span data-ttu-id="8afd8-210">Gebruik de volgende PowerShell-cmdlet, waarbij u de waarden vervangt door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="8afd8-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="8afd8-211">Bewerk het schema van het netwerkconfiguratiebestand zodanig dat het gatewaysubnet /27 of een kortere voorvoegsel (zoals /26 of /25) is.</span><span class="sxs-lookup"><span data-stu-id="8afd8-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="8afd8-212">Zie het volgende voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8afd8-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8afd8-213">Als u in uw virtuele netwerk niet voldoende IP-adressen over hebt om het gatewaysubnet te vergroten, moet u meer IP-adresruimte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="8afd8-214">Zie [Azure Virtual Network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx) voor meer informatie over het configuratieschema.</span><span class="sxs-lookup"><span data-stu-id="8afd8-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="8afd8-215">Als uw vorige gateway een site-naar-site-VPN was, moet u ook het verbindingstype wijzigen in **Toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="8afd8-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="8afd8-216">U hebt op dit moment een VNet zonder gateways.</span><span class="sxs-lookup"><span data-stu-id="8afd8-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="8afd8-217">Als u nieuwe gateways wilt maken en uw verbindingen wilt voltooien, kunt u doorgaan met [Stap 4 - Een ExpressRoute-gateway maken](#gw). Deze stap vindt u in de voorgaande reeks stappen.</span><span class="sxs-lookup"><span data-stu-id="8afd8-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8afd8-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8afd8-218">Next steps</span></span>
<span data-ttu-id="8afd8-219">Voor meer informatie over ExpressRoute raadpleegt u de [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="8afd8-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

