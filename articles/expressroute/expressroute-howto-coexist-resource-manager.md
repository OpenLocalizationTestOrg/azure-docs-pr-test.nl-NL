---
title: 'ExpressRoute- en site-naar-site-VPN-verbindingen configureren die naast elkaar kunnen worden gebruikt: klassiek: Resource Manager: Azure | Microsoft Docs'
description: Dit artikel begeleidt u bij het configureren van ExpressRoute- en site-naar-site-VPN-verbindingen die naast elkaar kunnen worden gebruikt in het Resource Manager-implementatiemodel.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="77f57-103">Gelijktijdige ExpressRoute- en site-to-site-verbindingen configureren</span><span class="sxs-lookup"><span data-stu-id="77f57-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77f57-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="77f57-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="77f57-105">PowerShell - Klassiek</span><span class="sxs-lookup"><span data-stu-id="77f57-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="77f57-106">Configuratie van gelijktijdige site-naar-site-VPN- en ExpressRoute-verbindingen heeft verschillende voordelen.</span><span class="sxs-lookup"><span data-stu-id="77f57-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="77f57-107">U kunt een Site-naar-Site-VPN configureren als een beveiligd failoverpad voor ExressRoute of Site-naar-Site VPN-verbindingen tooconnect toosites die niet zijn verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77f57-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="77f57-108">We hebben betrekking op Hallo stappen tooconfigure beide scenario's in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="77f57-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="77f57-109">In dit artikel is van toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77f57-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="77f57-110">Deze configuratie is niet beschikbaar in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="77f57-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77f57-111">ExpressRoute-circuits moeten vooraf worden geconfigureerd voordat u Hallo onderstaande instructies volgt.</span><span class="sxs-lookup"><span data-stu-id="77f57-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="77f57-112">Zorg ervoor dat u Hallo handleidingen te hebt gevolgd[maken van een ExpressRoute-circuit](expressroute-howto-circuit-arm.md) en [routering configureren](expressroute-howto-routing-arm.md) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="77f57-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="77f57-113">Limieten en beperkingen</span><span class="sxs-lookup"><span data-stu-id="77f57-113">Limits and limitations</span></span>
* <span data-ttu-id="77f57-114">**Transitroutering wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="77f57-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="77f57-115">U kunt niet (via Azure) routeren tussen uw lokale netwerk dat is verbonden via site-naar-site-VPN en uw lokale netwerk dat is verbonden via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77f57-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="77f57-116">**Basic SKU-gateway wordt niet ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="77f57-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="77f57-117">U moet een niet - basis-SKU-gateway gebruiken voor beide Hallo [ExpressRoute-gateway](expressroute-about-virtual-network-gateways.md) en Hallo [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="77f57-118">**Alleen een op route gebaseerde VPN-gateway wordt ondersteund.**</span><span class="sxs-lookup"><span data-stu-id="77f57-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="77f57-119">U moet een op route gebaseerde [VPN-gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77f57-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="77f57-120">**Statische route moet worden geconfigureerd voor de VPN-gateway.**</span><span class="sxs-lookup"><span data-stu-id="77f57-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="77f57-121">Als uw lokale netwerk verbonden tooboth ExpressRoute is en een Site-naar-Site VPN, u een statische route geconfigureerd in uw lokale netwerk tooroute Hallo Site-naar-Site VPN-verbinding toohello hebben moet openbare Internet.</span><span class="sxs-lookup"><span data-stu-id="77f57-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="77f57-122">**ExpressRoute-gateway moet als eerste worden geconfigureerd en tooa circuit gekoppeld.**</span><span class="sxs-lookup"><span data-stu-id="77f57-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="77f57-123">U moet Hallo ExpressRoute-gateway maken en een koppeling tooa circuit voordat u Hallo Site-naar-Site VPN-gateway toevoegt.</span><span class="sxs-lookup"><span data-stu-id="77f57-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="77f57-124">Configuratie-ontwerpen</span><span class="sxs-lookup"><span data-stu-id="77f57-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="77f57-125">Een site-naar-site-VPN configureren als een failoverpad voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="77f57-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="77f57-126">U kunt een site-naar-site-VPN-verbinding configureren als een back-up voor ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77f57-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="77f57-127">Dit geldt alleen toovirtual netwerken gekoppelde toohello pad Azure-persoonlijke peering.</span><span class="sxs-lookup"><span data-stu-id="77f57-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="77f57-128">Er is geen op VPN gebaseerde failoveroplossing voor services die toegankelijk zijn via openbare Azure- en Microsoft-peerings.</span><span class="sxs-lookup"><span data-stu-id="77f57-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="77f57-129">Hallo ExpressRoute-circuit is altijd Hallo primaire koppeling.</span><span class="sxs-lookup"><span data-stu-id="77f57-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="77f57-130">Gegevens loopt via de Site-naar-Site VPN-pad Hallo alleen als Hallo ExpressRoute-circuit is mislukt.</span><span class="sxs-lookup"><span data-stu-id="77f57-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="77f57-131">ExpressRoute-circuit is voorkeur via Site-naar-Site VPN wanneer beide routes worden dezelfde hello, gebruikt Azure Hallo langste voorvoegsel overeen toochoose Hallo route naar de bestemming hello-pakket.</span><span class="sxs-lookup"><span data-stu-id="77f57-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="77f57-133">Een Site-naar-Site VPN-tooconnect toosites niet is verbonden via ExpressRoute configureren</span><span class="sxs-lookup"><span data-stu-id="77f57-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="77f57-134">U kunt uw netwerk waarbij sommige sites verbinding rechtstreeks tooAzure via Site-naar-Site VPN en sommige sites verbinding maken via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77f57-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Naast elkaar gebruiken](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="77f57-136">U kunt een virtueel netwerk niet configureren als transitrouter.</span><span class="sxs-lookup"><span data-stu-id="77f57-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="77f57-137">Hallo stappen toouse selecteren</span><span class="sxs-lookup"><span data-stu-id="77f57-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="77f57-138">Er zijn twee sets met procedures toochoose uit.</span><span class="sxs-lookup"><span data-stu-id="77f57-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="77f57-139">Hallo-configuratieprocedure u selecteert, is afhankelijk van of u een bestaand virtueel netwerk dat u tooconnect naar wilt, of u wilt dat toocreate een nieuw virtueel netwerk hebt.</span><span class="sxs-lookup"><span data-stu-id="77f57-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="77f57-140">Ik heb geen VNet en moet er toocreate een.</span><span class="sxs-lookup"><span data-stu-id="77f57-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="77f57-141">Als u nog geen virtueel netwerk hebt, begeleidt deze procedure u bij het maken van een nieuw virtueel netwerk met behulp van de Resource Manager-implementatie, en bij het maken van nieuwe ExpressRoute- en site-naar-site-VPN-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="77f57-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="77f57-142">een virtueel netwerk tooconfigure Hallo stappen in [toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen](#new).</span><span class="sxs-lookup"><span data-stu-id="77f57-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="77f57-143">Ik heb al een VNet van het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="77f57-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="77f57-144">Mogelijk hebt u al een virtueel netwerk met een bestaande site-naar-site-VPN-verbinding of ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="77f57-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="77f57-145">Hallo [tooconfigure naast elkaar bestaande verbindingen voor een bestaand VNet](#add) sectie leidt u door het verwijderen van Hallo-gateway en vervolgens nieuwe ExpressRoute- en Site-naar-Site VPN-verbindingen te maken.</span><span class="sxs-lookup"><span data-stu-id="77f57-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="77f57-146">Hallo maken van nieuwe verbindingen, Hallo stappen moeten worden uitgevoerd in een bepaalde volgorde.</span><span class="sxs-lookup"><span data-stu-id="77f57-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="77f57-147">Gebruik geen Hallo-instructies in de andere artikelen toocreate uw gateways en verbindingen.</span><span class="sxs-lookup"><span data-stu-id="77f57-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="77f57-148">In deze procedure, maken verbindingen die naast elkaar kunnen bestaan vereist toodelete u uw gateway en vervolgens nieuwe gateways configureren.</span><span class="sxs-lookup"><span data-stu-id="77f57-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="77f57-149">Hebt u uitvaltijd voor uw cross-premises verbindingen terwijl u verwijderen en opnieuw maken van uw gateway en verbindingen, maar u niet toomigrate hoeft van uw virtuele machines of services tooa nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="77f57-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="77f57-150">Uw virtuele machines en services nog steeds kunnen toocommunicate uit via Hallo load balancer terwijl u uw gateway configureren als ze geconfigureerde toodo dus zijn.</span><span class="sxs-lookup"><span data-stu-id="77f57-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="77f57-151"><a name="new"></a>toocreate een nieuw virtueel netwerk en naast elkaar bestaande verbindingen</span><span class="sxs-lookup"><span data-stu-id="77f57-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="77f57-152">Deze procedure begeleidt u bij het maken van een VNet en van site-naar-site- en ExpressRoute-verbindingen die naast elkaar kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77f57-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="77f57-153">Installeer de nieuwste versie Hallo Hallo Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="77f57-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="77f57-154">Zie voor meer informatie over het installeren van de cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77f57-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="77f57-155">Hallo-cmdlets die u voor deze configuratie gebruikt is mogelijk enigszins afwijken van wat u mogelijk bekend zijn.</span><span class="sxs-lookup"><span data-stu-id="77f57-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="77f57-156">Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies.</span><span class="sxs-lookup"><span data-stu-id="77f57-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="77f57-157">Meld u in tooyour-account en Hallo-omgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="77f57-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="77f57-158">Maak een virtueel netwerk met een gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="77f57-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="77f57-159">Zie voor meer informatie over de configuratie van een virtueel netwerk Hallo [Azure Virtual Network-configuratie](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="77f57-160">Hallo Gatewaysubnet moet/27 of een korter voorvoegsel (zoals/26 of /25).</span><span class="sxs-lookup"><span data-stu-id="77f57-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="77f57-161">Maak een nieuw VNet.</span><span class="sxs-lookup"><span data-stu-id="77f57-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="77f57-162">Voeg subnetten toe.</span><span class="sxs-lookup"><span data-stu-id="77f57-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="77f57-163">Hallo-VNet-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="77f57-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="77f57-164"><a name="gw"></a>Maak een ExpressRoute-gateway.</span><span class="sxs-lookup"><span data-stu-id="77f57-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="77f57-165">Zie voor meer informatie over ExpressRoute-gatewayconfiguratie Hallo [ExpressRoute-gatewayconfiguratie](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="77f57-166">Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="77f57-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="77f57-167">Koppeling Hallo ExpressRoute-gateway toohello ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="77f57-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="77f57-168">Nadat deze stap is voltooid, Hallo-verbinding tussen uw on-premises netwerk en Azure via ExpressRoute, tot stand is gebracht.</span><span class="sxs-lookup"><span data-stu-id="77f57-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="77f57-169">Zie voor meer informatie over de koppelingsbewerking Hallo [VNets koppelen tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="77f57-170"><a name="vpngw"></a>Maak vervolgens uw site-naar-site-VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="77f57-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="77f57-171">Zie voor meer informatie over de configuratie van VPN-gateway Hallo [een VNet met een Site-naar-Site-verbinding configureren](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="77f57-172">Hallo GatewaySKU moet *standaard*, *HighPerformance*, of *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="77f57-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="77f57-173">Hallo VpnType moet *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="77f57-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="77f57-174">Azure VPN-gateway biedt ondersteuning voor BGP-routeringsprotocol.</span><span class="sxs-lookup"><span data-stu-id="77f57-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="77f57-175">U kunt ASN (AS-nummer) opgeven voor dit virtuele netwerk door Hallo - Asn switch toe te voegen in de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="77f57-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="77f57-176">Deze parameter niet opgeeft wordt standaard tooAS nummer 65515.</span><span class="sxs-lookup"><span data-stu-id="77f57-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="77f57-177">U kunt zoeken Hallo BGP-peer-IP en Hallo als getal die gebruikmaakt van Azure voor Hallo VPN-gateway in $azureVpn.BgpSettings.BgpPeeringAddress en $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="77f57-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="77f57-178">Zie [BGP configureren](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) voor Azure VPN-gateway voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="77f57-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="77f57-179">Maak een lokaal exemplaar van de VPN-gateway van uw site.</span><span class="sxs-lookup"><span data-stu-id="77f57-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="77f57-180">Deze opdracht wordt niet gebruikt om uw on-premises VPN-gateway te configureren.</span><span class="sxs-lookup"><span data-stu-id="77f57-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="77f57-181">In plaats daarvan kunt u Hiermee tooprovide Hallo lokale gateway-instellingen, zoals Hallo openbare IP-adres en hello op premises-adresruimte, zodat hello Azure VPN-gateway verbinding tooit maken kan.</span><span class="sxs-lookup"><span data-stu-id="77f57-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="77f57-182">Als uw lokale VPN-apparaat alleen statische routering ondersteunt, kunt u Hallo statische routes in de volgende manieren Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="77f57-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="77f57-183">Als uw lokale VPN-apparaat Hallo BGP ondersteunt en u wilt dat dynamische routering tooenable, moet u tooknow Hallo BGP peering IP-adres en Hallo als number die uw lokale VPN-apparaat gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77f57-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="77f57-184">Configureer uw lokale VPN-apparaat tooconnect toohello nieuwe Azure VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="77f57-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="77f57-185">Zie [VPN-apparaatconfiguratie](../vpn-gateway/vpn-gateway-about-vpn-devices.md) voor meer informatie over het configureren van een VPN-apparaat. </span><span class="sxs-lookup"><span data-stu-id="77f57-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="77f57-186">Koppeling Hallo Site-naar-Site VPN-gateway op de lokale gateway Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="77f57-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="77f57-187"><a name="add"></a>naast elkaar bestaande verbindingen tooconfigure voor een bestaand VNet</span><span class="sxs-lookup"><span data-stu-id="77f57-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="77f57-188">Als u een bestaand virtueel netwerk hebt, controleert u Hallo gateway subnetgrootte.</span><span class="sxs-lookup"><span data-stu-id="77f57-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="77f57-189">Als Hallo gatewaysubnet/28 of slechts/29 is, moet u Hallo virtuele netwerkgateway verwijderen en vergroot Hallo gateway-subnet.</span><span class="sxs-lookup"><span data-stu-id="77f57-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="77f57-190">Hallo stappen in deze sectie laten zien hoe u toodo die.</span><span class="sxs-lookup"><span data-stu-id="77f57-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="77f57-191">Als Hallo gatewaysubnet/27 of groter en Hallo virtueel netwerk is verbonden via ExpressRoute, kunt u Hallo onderstaande stappen overslaan en doorgaan te['Stap 6: een Site-naar-Site VPN-gateway maken'](#vpngw) in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="77f57-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="77f57-192">Wanneer u Hallo bestaande gateway verwijdert, wordt uw lokale site Hallo verbinding tooyour virtuele netwerk verbroken terwijl u bezig bent met deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="77f57-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="77f57-193">U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="77f57-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="77f57-194">Zie voor meer informatie over het installeren van cmdlets [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77f57-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="77f57-195">Hallo-cmdlets die u voor deze configuratie gebruikt is mogelijk enigszins afwijken van wat u mogelijk bekend zijn.</span><span class="sxs-lookup"><span data-stu-id="77f57-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="77f57-196">Ervoor toouse Hallo cmdlets worden opgegeven in deze instructies.</span><span class="sxs-lookup"><span data-stu-id="77f57-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="77f57-197">Verwijder de bestaande ExpressRoute of Site-naar-Site VPN-gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="77f57-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="77f57-198">Verwijder het gatewaysubnet.</span><span class="sxs-lookup"><span data-stu-id="77f57-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="77f57-199">Voeg een gatewaysubnet toe van /27 of hoger.</span><span class="sxs-lookup"><span data-stu-id="77f57-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="77f57-200">Als u geen voldoende IP-adressen in uw virtuele netwerk tooincrease Hallo gateway subnetgrootte gelaten, moet u tooadd meer IP-adresruimte.</span><span class="sxs-lookup"><span data-stu-id="77f57-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="77f57-201">Hallo-VNet-configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="77f57-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="77f57-202">U hebt op dit moment een VNet zonder gateways.</span><span class="sxs-lookup"><span data-stu-id="77f57-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="77f57-203">toocreate nieuwe gateways en uw verbindingen is voltooid, kunt u doorgaan met [stap 4 - een ExpressRoute-gateway maken](#gw)vindt u in de voorgaande reeks stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="77f57-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="77f57-204">tooadd punt-naar-site-configuratie toohello VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="77f57-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="77f57-205">U kunt stappen Hallo hieronder tooadd punt-naar-Site configuratie tooyour VPN-gateway in de instellingen voor een naast elkaar bestaan.</span><span class="sxs-lookup"><span data-stu-id="77f57-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="77f57-206">Voeg een VPN-clientadresgroep toe.</span><span class="sxs-lookup"><span data-stu-id="77f57-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="77f57-207">Upload Hallo VPN-hoofdmap certificaat tooAzure voor uw VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="77f57-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="77f57-208">In dit voorbeeld wordt ervan uitgegaan dat Hallo-basiscertificaat is opgeslagen in de lokale computer Hallo waarin Hallo volgende PowerShell-cmdlets worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="77f57-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="77f57-209">Zie [Een punt-naar-site-verbinding configureren](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) voor meer informatie over punt-naar-site-VPN.</span><span class="sxs-lookup"><span data-stu-id="77f57-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77f57-210">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77f57-210">Next steps</span></span>
<span data-ttu-id="77f57-211">Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="77f57-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
