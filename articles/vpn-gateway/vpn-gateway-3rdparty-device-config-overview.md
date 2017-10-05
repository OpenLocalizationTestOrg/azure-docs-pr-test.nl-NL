---
title: Over 3e partij VPN-apparaatconfiguratie verbinding maken met Azure VPN-gateways | Microsoft Docs
description: Dit artikel bevat een overzicht van 3e partij VPN-apparaatconfiguraties voor het verbinden met Azure VPN-gateways.
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
ms.openlocfilehash: 72dab85bb882b05d72cef26bef70437695b70416
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="bfdc5-103">Overzicht van 3e partij VPN-apparaatconfiguraties</span><span class="sxs-lookup"><span data-stu-id="bfdc5-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="bfdc5-104">Dit artikel bevat een overzicht van de lokale VPN-apparaatconfiguraties voor het verbinden met Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-104">This article provides an overview of on-premises VPN device configurations for connecting to Azure VPN gateways.</span></span> <span data-ttu-id="bfdc5-105">Verbinding maken met verschillende on-premises VPN-apparaten met dezelfde parameters wordt de steekproef virtuele Azure-netwerk en de VPN-gateway-installatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-105">The sample Azure virtual network and VPN gateway setup will be used to connect to different on-premises VPN devices with the same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="bfdc5-106">Vereisten voor apparaten</span><span class="sxs-lookup"><span data-stu-id="bfdc5-106">Device requirements</span></span>
<span data-ttu-id="bfdc5-107">Standaard IPsec/IKE-protocol suites Azure VPN-gateways gebruiken voor S2S-VPN-tunnels.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="bfdc5-108">Raadpleeg [over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor de parameters van gedetailleerde IPsec/IKE-protocol en de standaard cryptografische algoritmen voor Azure VPN-gateways.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-108">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="bfdc5-109">U kunt optioneel de exacte combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="bfdc5-109">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="bfdc5-110"><a name ="singletunnel"></a>Één VPN-tunnel</span><span class="sxs-lookup"><span data-stu-id="bfdc5-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="bfdc5-111">De eerste topologie bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-111">The first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="bfdc5-112">U kunt desgewenst BGP configureren via de VPN-tunnel.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-112">You can optionally configure BGP across the VPN tunnel.</span></span>

![één tunnel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="bfdc5-114">Raadpleeg [site-naar-site-verbinding configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md) voor gedetailleerde, stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-114">Refer to [Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="bfdc5-115">De volgende secties de parameters en een PowerShell-voorbeeldscript om u aan de slag te bieden.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-115">The following sections list the parameters and provide a sample PowerShell script to help you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="bfdc5-116">Gegevens voor netwerk- en VPN-gateway</span><span class="sxs-lookup"><span data-stu-id="bfdc5-116">Network and VPN gateway information</span></span>
<span data-ttu-id="bfdc5-117">Deze sectie lijst van de parameters voor de bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-117">This section list the parameters for the examples above.</span></span>

| <span data-ttu-id="bfdc5-118">**Parameter**</span><span class="sxs-lookup"><span data-stu-id="bfdc5-118">**Parameter**</span></span>                | <span data-ttu-id="bfdc5-119">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="bfdc5-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="bfdc5-120">VNet-adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="bfdc5-120">VNet address prefixes</span></span>        | <span data-ttu-id="bfdc5-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bfdc5-121">10.11.0.0/16</span></span><br><span data-ttu-id="bfdc5-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bfdc5-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="bfdc5-123">Azure VPN-gateway-IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="bfdc5-124">Azure VPN-Gateway IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="bfdc5-125">Lokale adresvoorvoegsels</span><span class="sxs-lookup"><span data-stu-id="bfdc5-125">On-premises address prefixes</span></span> | <span data-ttu-id="bfdc5-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bfdc5-126">10.51.0.0/16</span></span><br><span data-ttu-id="bfdc5-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bfdc5-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="bfdc5-128">Lokale VPN-apparaat IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="bfdc5-129">Lokale VPN-apparaat IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="bfdc5-130">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="bfdc5-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="bfdc5-131">65010</span><span class="sxs-lookup"><span data-stu-id="bfdc5-131">65010</span></span>                        |
| <span data-ttu-id="bfdc5-132">* Azure BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="bfdc5-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="bfdc5-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="bfdc5-134">* On-premises BGP ASN</span><span class="sxs-lookup"><span data-stu-id="bfdc5-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="bfdc5-135">65050</span><span class="sxs-lookup"><span data-stu-id="bfdc5-135">65050</span></span>                        |
| <span data-ttu-id="bfdc5-136">* On-premises BGP-peer-IP</span><span class="sxs-lookup"><span data-stu-id="bfdc5-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="bfdc5-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="bfdc5-137">10.52.255.254</span></span>                |

* <span data-ttu-id="bfdc5-138">(*) Optionele parameters voor BGP alleen</span><span class="sxs-lookup"><span data-stu-id="bfdc5-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="bfdc5-139">PowerShell-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="bfdc5-139">Sample PowerShell script</span></span>
<span data-ttu-id="bfdc5-140">[Een S2S VPN-verbinding maken met PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) gedetailleerde instructies.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has the detailed instructions.</span></span> <span data-ttu-id="bfdc5-141">Deze sectie bevat een voorbeeldscript om u op weg.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-141">This section provides a sample script to get you started.</span></span>

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

# Connect to your subscription and create a new resource group

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

# Create the S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="bfdc5-142"><a name ="policybased"></a>[Optioneel] Aangepaste IPsec/IKE-beleid met 'UsePolicyBasedTrafficSelectors' gebruiken</span><span class="sxs-lookup"><span data-stu-id="bfdc5-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="bfdc5-143">Als uw VPN-apparaten 'any-to-any' verkeer selectoren (op route gebaseerd/VTI-gebaseerde configuration) niet ondersteunen, moet u een aangepast IPsec/IKE-beleid maken en configureren van de optie 'UsePolicyBasedTrafficSelectors' zoals beschreven in [in dit artikel ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bfdc5-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need to create a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfdc5-144">U moet een IPsec/IKE-beleid maken om in te schakelen, de optie 'UsePolicyBasedTrafficSelectors' op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-144">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="bfdc5-145">Het onderstaande voorbeeldscript maakt een IPsec/IKE-beleid met de volgende algoritmen en parameters:</span><span class="sxs-lookup"><span data-stu-id="bfdc5-145">The sample script below creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="bfdc5-146">IKEv2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="bfdc5-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="bfdc5-147">IPsec: AES256, SHA1, PFS24, SA levensduur 7200 seconden & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="bfdc5-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="bfdc5-148">Het beleid van toepassing is en het schakelt 'UesPolicyBasedTrafficSelectors' op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-148">It then applies the policy and enables "UesPolicyBasedTrafficSelectors" on the connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="bfdc5-149"><a name ="bgp"></a>[Optioneel] BGP gebruiken voor S2S-VPN-verbinding</span><span class="sxs-lookup"><span data-stu-id="bfdc5-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="bfdc5-150">U kunt desgewenst BGP gebruiken op de verbinding.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-150">You can optionally use BGP on the connection.</span></span> <span data-ttu-id="bfdc5-151">Zie [BGP voor VPN-gateway](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bfdc5-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="bfdc5-152">Er zijn twee verschillen:</span><span class="sxs-lookup"><span data-stu-id="bfdc5-152">There are two differences:</span></span>

<span data-ttu-id="bfdc5-153">De lokale adresvoorvoegsels kunnen een enkele host-adres, het lokale BGP-peer-IP-adres zijn:</span><span class="sxs-lookup"><span data-stu-id="bfdc5-153">The on-premises address prefixes can be a single host address, the on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="bfdc5-154">U moet instellen '-EnableBGP ' op $True bij het maken van de verbinding:</span><span class="sxs-lookup"><span data-stu-id="bfdc5-154">You must set "-EnableBGP" to $True when creating the connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="bfdc5-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfdc5-155">Next steps</span></span>
<span data-ttu-id="bfdc5-156">Zie [Actief/actief VPN-gateways configureren voor cross-premises en VNet-naar-VNet-verbindingen](vpn-gateway-activeactive-rm-powershell.md) voor de stappen om actief/actief on-premises en VNet-naar-VNet-verbindingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="bfdc5-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

