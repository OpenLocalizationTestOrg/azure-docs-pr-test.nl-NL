---
title: aaaVPN gateway-instellingen voor cross-premises Azure-verbindingen | Microsoft Docs
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="bf068-103">Over configuratie-instellingen voor VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="bf068-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="bf068-104">Een VPN-gateway is een type van de virtuele netwerkgateway die versleuteld verkeer tussen uw virtuele netwerk en uw on-premises locatie via een openbare verbinding verzonden.</span><span class="sxs-lookup"><span data-stu-id="bf068-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="bf068-105">U kunt ook een VPN-gateway toosend verkeer tussen virtuele netwerken via hello Azure-backbone gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf068-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="bf068-106">Er is een VPN-gatewayverbinding afhankelijk van configuratie van de Hallo van meerdere resources, die elk configureerbare instellingen bevat.</span><span class="sxs-lookup"><span data-stu-id="bf068-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="bf068-107">Hallo-secties in dit artikel worden besproken Hallo bronnen en instellingen die betrekking tooa VPN-gateway voor een virtueel netwerk gemaakt in Resource Manager-implementatiemodel hebben.</span><span class="sxs-lookup"><span data-stu-id="bf068-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="bf068-108">U vindt beschrijvingen en diagrammen topologie voor elke verbinding oplossing in Hallo [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="bf068-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="bf068-109"><a name="gwtype"></a>Gatewaytypen</span><span class="sxs-lookup"><span data-stu-id="bf068-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="bf068-110">Elk virtueel netwerk kan slechts één virtuele netwerkgateway van elk type hebben.</span><span class="sxs-lookup"><span data-stu-id="bf068-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="bf068-111">Wanneer u een virtuele netwerkgateway maakt, moet u ervoor zorgen dat het Gatewaytype Hallo voor uw configuratie klopt.</span><span class="sxs-lookup"><span data-stu-id="bf068-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="bf068-112">beschikbare waarden voor - GatewayType Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="bf068-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="bf068-113">VPN</span><span class="sxs-lookup"><span data-stu-id="bf068-113">Vpn</span></span>
* <span data-ttu-id="bf068-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bf068-114">ExpressRoute</span></span>

<span data-ttu-id="bf068-115">Een VPN-gateway vereist Hallo `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="bf068-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="bf068-116">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="bf068-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="bf068-117"><a name="gwsku"></a>Gateway-SKU's</span><span class="sxs-lookup"><span data-stu-id="bf068-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="bf068-118">Hallo-gateway SKU configureren</span><span class="sxs-lookup"><span data-stu-id="bf068-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="bf068-119">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bf068-119">Azure portal</span></span>

<span data-ttu-id="bf068-120">Als u hello Azure portal toocreate een virtuele netwerkgateway van Resource Manager gebruikt, selecteert u Hallo gateway-SKU via Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="bf068-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="bf068-121">Hallo-opties u krijgt overeenkomen toohello Gatewaytype en VPN-type dat u selecteert.</span><span class="sxs-lookup"><span data-stu-id="bf068-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="bf068-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf068-122">PowerShell</span></span>

<span data-ttu-id="bf068-123">Hallo volgende PowerShell-voorbeeld geeft Hallo `-GatewaySku` als VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="bf068-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="bf068-124"><a name="resize"></a>Wijzig de grootte van (wijzigen) een gateway-SKU</span><span class="sxs-lookup"><span data-stu-id="bf068-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="bf068-125">Als u uw gateway-SKU tooa tooupgrade wilt krachtiger SKU, kunt u Hallo `Resize-AzureRmVirtualNetworkGateway` PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf068-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="bf068-126">U kunt ook downgraden Hallo gateway SKU-grootte die met deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf068-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="bf068-127">Hallo volgende PowerShell-voorbeeld ziet u dat toovpngw2 een gateway-SKU wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bf068-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="bf068-128"><a name="connectiontype"></a>Verbindingstypen</span><span class="sxs-lookup"><span data-stu-id="bf068-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="bf068-129">Elke configuratie vereist Hallo Resource Manager-implementatiemodel, het type van een specifieke virtuele-netwerkgateway verbinding.</span><span class="sxs-lookup"><span data-stu-id="bf068-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="bf068-130">Hallo beschikbare Resource Manager PowerShell-waarden voor `-ConnectionType` zijn:</span><span class="sxs-lookup"><span data-stu-id="bf068-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="bf068-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="bf068-131">IPsec</span></span>
* <span data-ttu-id="bf068-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="bf068-132">Vnet2Vnet</span></span>
* <span data-ttu-id="bf068-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bf068-133">ExpressRoute</span></span>
* <span data-ttu-id="bf068-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="bf068-134">VPNClient</span></span>

<span data-ttu-id="bf068-135">Hallo PowerShell-voorbeeld te volgen, maken we een S2S-verbinding waarvoor Hallo verbindingstype *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="bf068-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="bf068-136"><a name="vpntype"></a>VPN-typen</span><span class="sxs-lookup"><span data-stu-id="bf068-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="bf068-137">Wanneer u de virtuele netwerkgateway Hallo voor de configuratie van een VPN-gateway maakt, moet u een VPN-type.</span><span class="sxs-lookup"><span data-stu-id="bf068-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="bf068-138">Hallo VPN-type dat u kiest, hangt Hallo verbinding topologie dat u wilt dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="bf068-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="bf068-139">Bijvoorbeeld, vereist een P2S-verbinding een RouteBased VPN-type.</span><span class="sxs-lookup"><span data-stu-id="bf068-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="bf068-140">Een VPN-type kan ook afhankelijk van Hallo-hardware die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bf068-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="bf068-141">S2S-configuraties vereisen een VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="bf068-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="bf068-142">Sommige VPN-apparaten ondersteunen alleen een bepaalde VPN-type.</span><span class="sxs-lookup"><span data-stu-id="bf068-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="bf068-143">Hallo VPN-type dat u selecteert moet voldoen aan alle vereisten voor Hallo verbinding voor de oplossing Hallo gewenste toocreate.</span><span class="sxs-lookup"><span data-stu-id="bf068-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="bf068-144">Bijvoorbeeld als u wilt dat toocreate een S2S VPN-gatewayverbinding en een P2S-VPN-gatewayverbinding voor Hallo hetzelfde virtuele netwerk, gebruikt u VPN-type *RouteBased* omdat P2S een RouteBased VPN-type vereist.</span><span class="sxs-lookup"><span data-stu-id="bf068-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="bf068-145">U moet tevens tooverify dat uw VPN-apparaat een RouteBased VPN-verbinding ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bf068-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="bf068-146">Wanneer een virtuele netwerkgateway is gemaakt, kunt u Hallo VPN-type niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf068-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="bf068-147">U hebt toodelete Hallo virtuele netwerkgateway en maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="bf068-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="bf068-148">Er zijn twee VPN-typen:</span><span class="sxs-lookup"><span data-stu-id="bf068-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="bf068-149">Hallo volgende PowerShell-voorbeeld geeft Hallo `-VpnType` als *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="bf068-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="bf068-150">Wanneer u een gateway maakt, moet u ervoor zorgen dat Hallo - VpnType juist is voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="bf068-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="bf068-151"><a name="requirements"></a>Vereisten voor de gateway</span><span class="sxs-lookup"><span data-stu-id="bf068-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="bf068-152"><a name="gwsub"></a>Gatewaysubnet</span><span class="sxs-lookup"><span data-stu-id="bf068-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="bf068-153">Voordat u een VPN-gateway maakt, moet u een gatewaysubnet maken.</span><span class="sxs-lookup"><span data-stu-id="bf068-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="bf068-154">gatewaysubnet Hallo Hallo IP-adressen bevat die Hallo-gateway van het virtuele netwerk virtuele machines en services gebruik.</span><span class="sxs-lookup"><span data-stu-id="bf068-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="bf068-155">Wanneer u uw virtuele netwerkgateway maakt, gateway virtuele machines zijn geïmplementeerd toohello gatewaysubnet en geconfigureerd met instellingen voor VPN-gateway Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="bf068-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="bf068-156">U moet nooit alles anders (bijvoorbeeld extra virtuele machines) toohello gatewaysubnet implementeren.</span><span class="sxs-lookup"><span data-stu-id="bf068-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="bf068-157">Hallo gatewaysubnet moet de naam 'GatewaySubnet' toowork goed.</span><span class="sxs-lookup"><span data-stu-id="bf068-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="bf068-158">Naamgeving Hallo gatewaysubnet 'GatewaySubnet' kunt weet Azure dat dit Hallo subnet toodeploy Hallo virtuele netwerkgateway virtuele machines en services.</span><span class="sxs-lookup"><span data-stu-id="bf068-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="bf068-159">Wanneer u Hallo gatewaysubnet maakt, geeft u het aantal IP-adressen die subnet Hallo Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="bf068-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="bf068-160">Hallo IP-adressen in het gatewaysubnet Hallo zijn toegewezen toohello gateway-VM's en gatewayservices.</span><span class="sxs-lookup"><span data-stu-id="bf068-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="bf068-161">Sommige configuraties moeten meer IP-adressen dan andere.</span><span class="sxs-lookup"><span data-stu-id="bf068-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="bf068-162">Bekijkt hello instructies voor het Hallo-configuratie dat u wilt dat toocreate en controleren die Hallo gatewaysubnet gewenste toocreate voldoet aan deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="bf068-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="bf068-163">Bovendien kunt u ervoor dat het gatewaysubnet bevat onvoldoende IP-adressen tooaccommodate mogelijke toekomstige aanvullende configuraties toomake.</span><span class="sxs-lookup"><span data-stu-id="bf068-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="bf068-164">U kunt een gatewaysubnet slechts/29 maken, wordt aangeraden dat u een gatewaysubnet van/28 of groter maakt (/ 28, / 27, /26 enz.).</span><span class="sxs-lookup"><span data-stu-id="bf068-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="bf068-165">Als u de functionaliteit toevoegen in Hallo toekomstige, u geen tootear hebben uw gateway en vervolgens verwijderen en opnieuw Hallo gateway subnet tooallow voor meer IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="bf068-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="bf068-166">Hallo ziet volgende Resource Manager PowerShell-voorbeeld u een gatewaysubnet met de naam GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="bf068-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="bf068-167">U kunt zien Hallo CIDR-notatie een/27, geeft dit biedt voldoende IP-adressen voor de meeste configuraties die momenteel aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="bf068-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="bf068-168"><a name="lng"></a>Lokale netwerkgateways</span><span class="sxs-lookup"><span data-stu-id="bf068-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="bf068-169">Bij het maken van de configuratie van een VPN-gateway, vertegenwoordigt de lokale netwerkgateway Hallo vaak uw on-premises locatie.</span><span class="sxs-lookup"><span data-stu-id="bf068-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="bf068-170">In het klassieke implementatiemodel hello is de lokale netwerkgateway Hallo waarnaar wordt verwezen tooas een lokale Site.</span><span class="sxs-lookup"><span data-stu-id="bf068-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="bf068-171">U Hallo lokale netwerkgateway een naam geven, Hallo openbare IP-adres van Hallo on-premises VPN-apparaat en Hallo adresvoorvoegsels die op Hallo on-premises locatie bevinden zich opgeven.</span><span class="sxs-lookup"><span data-stu-id="bf068-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="bf068-172">Azure bekijkt hello bestemmingsadressen voor netwerkverkeer, raadpleegt Hallo-configuratie die u hebt opgegeven voor uw lokale netwerkgateway en routeert pakketten dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="bf068-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="bf068-173">U wordt ook lokale netwerkgateways voor VNet-naar-VNet-configuraties die gebruikmaken van een VPN-gatewayverbinding.</span><span class="sxs-lookup"><span data-stu-id="bf068-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="bf068-174">Hallo volgende PowerShell-voorbeeld maakt een nieuwe lokale netwerkgateway:</span><span class="sxs-lookup"><span data-stu-id="bf068-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="bf068-175">Soms moet u de gateway-instellingen voor toomodify Hallo lokale netwerk.</span><span class="sxs-lookup"><span data-stu-id="bf068-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="bf068-176">Bijvoorbeeld, wanneer u toevoegen of wijzigen van Hallo-adresbereik, of als Hallo IP-adres van Hallo VPN-apparaat is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="bf068-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="bf068-177">U kunt deze instellingen in de klassieke portal Hallo op Hallo lokale netwerken pagina wijzigen voor een klassiek VNet.</span><span class="sxs-lookup"><span data-stu-id="bf068-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="bf068-178">Zie voor Resource Manager [lokale gateway netwerkinstellingen wijzigen met behulp van PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="bf068-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="bf068-179"><a name="resources"></a>REST-API's en PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="bf068-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="bf068-180">Zie voor aanvullende technische bronnen en syntaxis van de specifieke vereisten voor het met de REST-API's, PowerShell-cmdlets of Azure CLI voor VPN-Gateway configuraties Hallo pagina's te volgen:</span><span class="sxs-lookup"><span data-stu-id="bf068-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="bf068-181">**Klassiek**</span><span class="sxs-lookup"><span data-stu-id="bf068-181">**Classic**</span></span> | <span data-ttu-id="bf068-182">**Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="bf068-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="bf068-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf068-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="bf068-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf068-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="bf068-185">REST API</span><span class="sxs-lookup"><span data-stu-id="bf068-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="bf068-186">REST API</span><span class="sxs-lookup"><span data-stu-id="bf068-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="bf068-187">Niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="bf068-187">Not supported</span></span> | [<span data-ttu-id="bf068-188">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="bf068-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="bf068-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf068-189">Next steps</span></span>

<span data-ttu-id="bf068-190">Zie voor meer informatie over beschikbare verbinding configuraties [over VPN-Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="bf068-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>