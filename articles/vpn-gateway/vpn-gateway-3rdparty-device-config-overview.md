---
title: aaaAbout 3e partij VPN-apparaat configuratie tooconnect tooAzure VPN-gateways | Microsoft Docs
description: Dit artikel bevat een overzicht van 3e partij VPN-apparaatconfiguraties voor het verbinden van tooAzure VPN-gateways.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="f0b7f-103">Overzicht van 3e partij VPN-apparaatconfiguraties</span><span class="sxs-lookup"><span data-stu-id="f0b7f-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="f0b7f-104">Dit artikel bevat een overzicht van de lokale VPN-apparaatconfiguraties voor het verbinden van tooAzure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="f0b7f-105">Hallo voorbeeld virtuele Azure-netwerk- en VPN-gateway setup wordt gebruikte tooconnect toodifferent on-premises VPN-apparaten met Hallo worden dezelfde parameters.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="f0b7f-106">Vereisten voor apparaten</span><span class="sxs-lookup"><span data-stu-id="f0b7f-106">Device requirements</span></span>
<span data-ttu-id="f0b7f-107">Standaard IPsec/IKE-protocol suites Azure VPN-gateways gebruiken voor S2S-VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="f0b7f-108">Raadpleeg te[over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor Hallo gedetailleerde parameters voor IPsec/IKE-protocol en standaard cryptografische algoritmen voor Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="f0b7f-109">U kunt optioneel Hallo exact dezelfde combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="f0b7f-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="f0b7f-110"><a name ="singletunnel"></a>Één VPN-tunnel</span><span class="sxs-lookup"><span data-stu-id="f0b7f-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="f0b7f-111">de eerste topologie Hallo bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="f0b7f-112">Desgewenst kunt u BGP configureren op Hallo VPN-tunnel.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![één tunnel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="f0b7f-114">Raadpleeg te[site-naar-site-verbinding configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md) voor gedetailleerde, stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="f0b7f-115">Hallo volgende secties Hallo parameters en geef een voorbeeld PowerShell script toohelp die u aan de slag.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="f0b7f-116">Gegevens voor netwerk- en VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="f0b7f-116">Network and VPN gateway information</span></span>
<span data-ttu-id="f0b7f-117">Deze sectie lijst Hallo parameters op voor het bovenstaande Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="f0b7f-118">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="f0b7f-118">**Parameter**</span></span>                | <span data-ttu-id="f0b7f-119">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="f0b7f-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="f0b7f-120">VNet-adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="f0b7f-120">VNet address prefixes</span></span>        | <span data-ttu-id="f0b7f-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f0b7f-121">10.11.0.0/16</span></span><br><span data-ttu-id="f0b7f-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f0b7f-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="f0b7f-123">Azure VPN-gateway-IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="f0b7f-124">Azure VPN-Gateway IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="f0b7f-125">Lokale adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="f0b7f-125">On-premises address prefixes</span></span> | <span data-ttu-id="f0b7f-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f0b7f-126">10.51.0.0/16</span></span><br><span data-ttu-id="f0b7f-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f0b7f-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="f0b7f-128">Lokale VPN-apparaat IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="f0b7f-129">Lokale VPN-apparaat IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="f0b7f-130">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="f0b7f-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="f0b7f-131">65010</span><span class="sxs-lookup"><span data-stu-id="f0b7f-131">65010</span></span>                        |
| <span data-ttu-id="f0b7f-132">* Azure BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="f0b7f-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="f0b7f-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="f0b7f-134">* On-premises BGP ASN</span><span class="sxs-lookup"><span data-stu-id="f0b7f-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="f0b7f-135">65050</span><span class="sxs-lookup"><span data-stu-id="f0b7f-135">65050</span></span>                        |
| <span data-ttu-id="f0b7f-136">* On-premises BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="f0b7f-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="f0b7f-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="f0b7f-137">10.52.255.254</span></span>                |

* <span data-ttu-id="f0b7f-138">(*) Optionele parameters voor BGP alleen</span><span class="sxs-lookup"><span data-stu-id="f0b7f-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="f0b7f-139">PowerShell-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="f0b7f-139">Sample PowerShell script</span></span>
<span data-ttu-id="f0b7f-140">[Een S2S VPN-verbinding maken met PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) heeft Hallo gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="f0b7f-141">Deze sectie bevat een voorbeeld script tooget die u gestart.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-141">This section provides a sample script tooget you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="f0b7f-142"><a name ="policybased"></a>[Optioneel] Aangepaste IPsec/IKE-beleid met 'UsePolicyBasedTrafficSelectors' gebruiken</span><span class="sxs-lookup"><span data-stu-id="f0b7f-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="f0b7f-143">Als uw VPN-apparaten 'any-to-any' verkeer selectoren (op route gebaseerd/VTI-gebaseerde configuration) niet ondersteunen, u moet een aangepast beleid voor IPsec/IKE toocreate en configureer de optie 'UsePolicyBasedTrafficSelectors', zoals beschreven in [in dit artikel ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f0b7f-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0b7f-144">U moet een beleid voor IPsec/IKE in volgorde tooenable 'UsePolicyBasedTrafficSelectors' optie op Hallo verbinding toocreate.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="f0b7f-145">Hallo-voorbeeldscript maakt u een beleid voor IPsec/IKE met Hallo algoritmen en parameters te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0b7f-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="f0b7f-146">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="f0b7f-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="f0b7f-147">IPsec: AES256, SHA1, PFS24, SA levensduur 7200 seconden & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="f0b7f-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="f0b7f-148">Hallo-beleid van toepassing is en het 'UesPolicyBasedTrafficSelectors' op Hallo verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="f0b7f-149"><a name ="bgp"></a>[Optioneel] BGP gebruiken voor S2S-VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="f0b7f-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="f0b7f-150">U kunt desgewenst BGP op Hallo verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="f0b7f-151">Zie [BGP voor VPN-gateway](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f0b7f-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="f0b7f-152">Er zijn twee verschillen:</span><span class="sxs-lookup"><span data-stu-id="f0b7f-152">There are two differences:</span></span>

<span data-ttu-id="f0b7f-153">Hallo lokale adresvoorvoegsels kunnen een enkele host-adres, IP-adres van Hallo lokale BGP-peer zijn:</span><span class="sxs-lookup"><span data-stu-id="f0b7f-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="f0b7f-154">U moet instellen '-EnableBGP ' te$ True bij het maken van Hallo verbinding:</span><span class="sxs-lookup"><span data-stu-id="f0b7f-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="f0b7f-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0b7f-155">Next steps</span></span>
<span data-ttu-id="f0b7f-156">Zie [actieve VPN-Gateways voor Cross-Premises en VNet-naar-VNet-verbindingen configureren](vpn-gateway-activeactive-rm-powershell.md) voor stappen tooconfigure actieve cross-premises en VNet-naar-VNet-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f0b7f-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

