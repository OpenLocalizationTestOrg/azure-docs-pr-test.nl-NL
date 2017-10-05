---
title: VPN-gateway-instellingen voor cross-premises Azure-verbindingen | Microsoft Docs
description: Meer informatie over VPN-Gateway-instellingen voor gateways voor virtuele Azure-netwerk.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="88dab-103">Over configuratie-instellingen voor VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="88dab-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="88dab-104">Een VPN-gateway is een type van de virtuele netwerkgateway die versleuteld verkeer tussen uw virtuele netwerk en uw on-premises locatie via een openbare verbinding verzonden.</span><span class="sxs-lookup"><span data-stu-id="88dab-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="88dab-105">U kunt ook een VPN-gateway gebruiken om verkeer tussen virtuele netwerken via de Azure-backbone te verzenden.</span><span class="sxs-lookup"><span data-stu-id="88dab-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="88dab-106">Er is een VPN-gatewayverbinding afhankelijk van de configuratie van meerdere resources, die elk configureerbare instellingen bevat.</span><span class="sxs-lookup"><span data-stu-id="88dab-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="88dab-107">De secties in dit artikel worden de resources en de instellingen met betrekking tot een VPN-gateway voor een virtueel netwerk gemaakt in Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="88dab-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="88dab-108">U vindt beschrijvingen en diagrammen topologie voor elke oplossing verbinding in de [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="88dab-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="88dab-109"><a name="gwtype"></a>Gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="88dab-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="88dab-110">Elk virtueel netwerk kan slechts één virtuele netwerkgateway van elk type hebben.</span><span class="sxs-lookup"><span data-stu-id="88dab-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="88dab-111">Wanneer u een virtuele netwerkgateway maakt, moet u ervoor zorgen dat het Gatewaytype voor uw configuratie klopt.</span><span class="sxs-lookup"><span data-stu-id="88dab-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="88dab-112">De beschikbare waarden voor - GatewayType zijn:</span><span class="sxs-lookup"><span data-stu-id="88dab-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="88dab-113">VPN</span><span class="sxs-lookup"><span data-stu-id="88dab-113">Vpn</span></span>
* <span data-ttu-id="88dab-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="88dab-114">ExpressRoute</span></span>

<span data-ttu-id="88dab-115">Een VPN-gateway vereist de `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="88dab-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="88dab-116">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="88dab-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="88dab-117"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="88dab-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="88dab-118">De gateway-SKU configureren</span><span class="sxs-lookup"><span data-stu-id="88dab-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="88dab-119">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="88dab-119">Azure portal</span></span>

<span data-ttu-id="88dab-120">Als u de Azure-portal voor het maken van een virtuele netwerkgateway van Resource Manager gebruikt, selecteert u de gateway-SKU met behulp van de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="88dab-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="88dab-121">De opties die u krijgt correspondeert met het type van de Gateway en de VPN-type dat u selecteert.</span><span class="sxs-lookup"><span data-stu-id="88dab-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="88dab-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88dab-122">PowerShell</span></span>

<span data-ttu-id="88dab-123">Het volgende PowerShell-voorbeeld worden de `-GatewaySku` als VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="88dab-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="88dab-124"><a name="resize"></a>Wijzig de grootte van (wijzigen) een gateway-SKU</span><span class="sxs-lookup"><span data-stu-id="88dab-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="88dab-125">Als u wilt dat uw gateway-SKU bijwerken naar een krachtigere SKU, kunt u de `Resize-AzureRmVirtualNetworkGateway` PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="88dab-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="88dab-126">Ook kunt u de gateway-SKU-grootte die met deze cmdlet downgraden.</span><span class="sxs-lookup"><span data-stu-id="88dab-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="88dab-127">De volgende PowerShell-voorbeeld ziet u een gateway-SKU voor VpnGw2 wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="88dab-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="88dab-128"><a name="connectiontype"></a>Verbindingstypen</span><span class="sxs-lookup"><span data-stu-id="88dab-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="88dab-129">Elke configuratie vereist in het Resource Manager-implementatiemodel, het type van een specifieke virtuele-netwerkgateway verbinding.</span><span class="sxs-lookup"><span data-stu-id="88dab-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="88dab-130">De beschikbare Resource Manager PowerShell-waarden voor `-ConnectionType` zijn:</span><span class="sxs-lookup"><span data-stu-id="88dab-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="88dab-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="88dab-131">IPsec</span></span>
* <span data-ttu-id="88dab-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="88dab-132">Vnet2Vnet</span></span>
* <span data-ttu-id="88dab-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="88dab-133">ExpressRoute</span></span>
* <span data-ttu-id="88dab-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="88dab-134">VPNClient</span></span>

<span data-ttu-id="88dab-135">In het volgende PowerShell-voorbeeld, maken we een S2S-verbinding waarvoor het verbindingstype *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="88dab-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="88dab-136"><a name="vpntype"></a>VPN-typen</span><span class="sxs-lookup"><span data-stu-id="88dab-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="88dab-137">Wanneer u de virtuele netwerkgateway voor de configuratie van een VPN-gateway maakt, moet u een VPN-type.</span><span class="sxs-lookup"><span data-stu-id="88dab-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="88dab-138">Het VPN-type dat u kiest, is afhankelijk van de verbinding-topologie die u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="88dab-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="88dab-139">Bijvoorbeeld, vereist een P2S-verbinding een RouteBased VPN-type.</span><span class="sxs-lookup"><span data-stu-id="88dab-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="88dab-140">Een VPN-type kan ook afhankelijk van de hardware die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="88dab-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="88dab-141">S2S-configuraties vereisen een VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="88dab-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="88dab-142">Sommige VPN-apparaten ondersteunen alleen een bepaalde VPN-type.</span><span class="sxs-lookup"><span data-stu-id="88dab-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="88dab-143">Het VPN-type dat u selecteert, moet voldoen aan alle verbinding vereisten voor de oplossing die dat u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="88dab-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="88dab-144">Bijvoorbeeld, als u een S2S VPN-gatewayverbinding en een P2S-VPN-gatewayverbinding voor hetzelfde virtuele netwerk maken wilt, gebruikt u VPN-type *RouteBased* omdat P2S een RouteBased VPN-type vereist.</span><span class="sxs-lookup"><span data-stu-id="88dab-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="88dab-145">U moet ook verifiëren of uw VPN-apparaat een RouteBased VPN-verbinding ondersteund.</span><span class="sxs-lookup"><span data-stu-id="88dab-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="88dab-146">Wanneer een virtuele netwerkgateway is gemaakt, kunt u het VPN-type niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="88dab-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="88dab-147">U moet de virtuele netwerkgateway verwijderen en een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="88dab-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="88dab-148">Er zijn twee VPN-typen:</span><span class="sxs-lookup"><span data-stu-id="88dab-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="88dab-149">Het volgende PowerShell-voorbeeld worden de `-VpnType` als *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="88dab-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="88dab-150">Wanneer u een gateway maakt, moet u het juiste VPN-type voor uw configuratie kiezen.</span><span class="sxs-lookup"><span data-stu-id="88dab-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="88dab-151"><a name="requirements"></a>Vereisten voor de gateway</span><span class="sxs-lookup"><span data-stu-id="88dab-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="88dab-152"><a name="gwsub"></a>Gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="88dab-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="88dab-153">Voordat u een VPN-gateway maakt, moet u een gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="88dab-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="88dab-154">Het gatewaysubnet bevat de IP-adressen die gebruikmaken van de virtuele netwerkgateway virtuele machines en services.</span><span class="sxs-lookup"><span data-stu-id="88dab-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="88dab-155">Wanneer u uw virtuele netwerkgateway maakt, worden gateway-VM's in het gatewaysubnet is geïmplementeerd en geconfigureerd met de vereiste instellingen voor VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="88dab-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="88dab-156">U moet nooit iets anders (bijvoorbeeld extra VM's) om het gatewaysubnet te implementeren.</span><span class="sxs-lookup"><span data-stu-id="88dab-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="88dab-157">Het gatewaysubnet moet de naam 'GatewaySubnet' goed te laten werken.</span><span class="sxs-lookup"><span data-stu-id="88dab-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="88dab-158">Naamgeving van het gatewaysubnet 'GatewaySubnet', kunt weet dat deze het subnet voor het implementeren van de virtuele netwerkgateway virtuele machines en services met Azure.</span><span class="sxs-lookup"><span data-stu-id="88dab-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="88dab-159">Wanneer u het gatewaysubnet maakt, geeft u op hoeveel IP-adressen het subnet bevat.</span><span class="sxs-lookup"><span data-stu-id="88dab-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="88dab-160">De IP-adressen in het gatewaysubnet worden toegewezen aan de gateway-VM's en gatewayservices.</span><span class="sxs-lookup"><span data-stu-id="88dab-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="88dab-161">Sommige configuraties moeten meer IP-adressen dan andere.</span><span class="sxs-lookup"><span data-stu-id="88dab-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="88dab-162">Bekijk de instructies voor de configuratie die u wilt maken en te controleren of het gatewaysubnet dat u wilt maken, voldoet aan deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="88dab-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="88dab-163">Bovendien wilt u Zorg ervoor dat het gatewaysubnet bevat voldoende IP-adressen zodat mogelijke toekomstige aanvullende configuraties.</span><span class="sxs-lookup"><span data-stu-id="88dab-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="88dab-164">U kunt een gatewaysubnet slechts/29 maken, wordt aangeraden dat u een gatewaysubnet van/28 of groter maakt (/ 28, / 27, /26 enz.).</span><span class="sxs-lookup"><span data-stu-id="88dab-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="88dab-165">Op die manier als u de functionaliteit in de toekomst toevoegt u hoeft te verwijderen van uw gateway en vervolgens verwijderen en opnieuw maken van het gatewaysubnet om toe te staan voor meer IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="88dab-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="88dab-166">De volgende Resource Manager PowerShell-voorbeeld ziet een gatewaysubnet met de naam GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="88dab-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="88dab-167">U ziet dat de CIDR-notatie een/27, geeft dit biedt voldoende IP-adressen voor de meeste configuraties die momenteel aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="88dab-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="88dab-168"><a name="lng"></a>Lokale netwerkgateways</span><span class="sxs-lookup"><span data-stu-id="88dab-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="88dab-169">Wanneer u de configuratie van een VPN-gateway maakt, wordt de lokale netwerkgateway vaak uw on-premises locatie vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="88dab-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="88dab-170">In het klassieke implementatiemodel werd de lokale gateway een lokale site genoemd.</span><span class="sxs-lookup"><span data-stu-id="88dab-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="88dab-171">U geeft de lokale netwerkgateway een naam, het openbare IP-adres van de on-premises VPN-apparaat en de adresvoorvoegsels die op de on-premises locatie bevinden zich opgeven.</span><span class="sxs-lookup"><span data-stu-id="88dab-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="88dab-172">Azure kijkt naar de bestemmingsadressen voor netwerkverkeer, raadpleegt de configuratie die u voor uw lokale netwerkgateway hebt opgegeven en routeert pakketten dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="88dab-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="88dab-173">U wordt ook lokale netwerkgateways voor VNet-naar-VNet-configuraties die gebruikmaken van een VPN-gatewayverbinding.</span><span class="sxs-lookup"><span data-stu-id="88dab-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="88dab-174">Het volgende PowerShell-voorbeeld wordt een nieuwe lokale netwerkgateway:</span><span class="sxs-lookup"><span data-stu-id="88dab-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="88dab-175">Soms moet u de lokale gateway-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="88dab-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="88dab-176">Bijvoorbeeld, wanneer u toevoegen of wijzigen van het adresbereik, of als het IP-adres van de VPN-apparaat is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="88dab-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="88dab-177">U kunt deze instellingen in de klassieke portal op de pagina lokale netwerken wijzigen voor een klassiek VNet.</span><span class="sxs-lookup"><span data-stu-id="88dab-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="88dab-178">Zie voor Resource Manager [lokale gateway netwerkinstellingen wijzigen met behulp van PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="88dab-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="88dab-179"><a name="resources"></a>REST-API's en PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="88dab-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="88dab-180">Zie voor aanvullende technische bronnen en de syntaxis van de specifieke vereisten voor het met REST-API's, PowerShell-cmdlets of Azure CLI voor VPN-Gateway-configuraties, de volgende pagina's:</span><span class="sxs-lookup"><span data-stu-id="88dab-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="88dab-181">**Klassiek**</span><span class="sxs-lookup"><span data-stu-id="88dab-181">**Classic**</span></span> | <span data-ttu-id="88dab-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="88dab-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="88dab-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88dab-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="88dab-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88dab-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="88dab-185">REST API</span><span class="sxs-lookup"><span data-stu-id="88dab-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="88dab-186">REST API</span><span class="sxs-lookup"><span data-stu-id="88dab-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="88dab-187">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="88dab-187">Not supported</span></span> | [<span data-ttu-id="88dab-188">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="88dab-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="88dab-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88dab-189">Next steps</span></span>

<span data-ttu-id="88dab-190">Zie voor meer informatie over beschikbare verbinding configuraties [over VPN-Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="88dab-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>