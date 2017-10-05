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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Overzicht van 3e partij VPN-apparaatconfiguraties
Dit artikel bevat een overzicht van de lokale VPN-apparaatconfiguraties voor het verbinden met Azure VPN-gateways. Verbinding maken met verschillende on-premises VPN-apparaten met dezelfde parameters wordt de steekproef virtuele Azure-netwerk en de VPN-gateway-installatie gebruikt.

## <a name="device-requirements"></a>Vereisten voor apparaten
Standaard IPsec/IKE-protocol suites Azure VPN-gateways gebruiken voor S2S-VPN-tunnels. Raadpleeg [over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor de parameters van gedetailleerde IPsec/IKE-protocol en de standaard cryptografische algoritmen voor Azure VPN-gateways. U kunt optioneel de exacte combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Één VPN-tunnel
De eerste topologie bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat. U kunt desgewenst BGP configureren via de VPN-tunnel.

![één tunnel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Raadpleeg [site-naar-site-verbinding configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md) voor gedetailleerde, stapsgewijze instructies. De volgende secties de parameters en een PowerShell-voorbeeldscript om u aan de slag te bieden.

### <a name="network-and-vpn-gateway-information"></a>Gegevens voor netwerk- en VPN-gateway
Deze sectie lijst van de parameters voor de bovenstaande voorbeelden.

| **Parameter**                | **Waarde**                    |
| ---                          | ---                          |
| VNet-adresvoorvoegsels        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN-gateway-IP         | Azure VPN-Gateway IP         |
| Lokale adresvoorvoegsels | 10.51.0.0/16<br>10.52.0.0/16 |
| Lokale VPN-apparaat IP    | Lokale VPN-apparaat IP    |
| * VNet BGP ASN                | 65010                        |
| * Azure BGP-peer-IP           | 10.12.255.30                 |
| * On-premises BGP ASN         | 65050                        |
| * On-premises BGP-peer-IP     | 10.52.255.254                |

* (*) Optionele parameters voor BGP alleen

### <a name="sample-powershell-script"></a>PowerShell-voorbeeldscript
[Een S2S VPN-verbinding maken met PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) gedetailleerde instructies. Deze sectie bevat een voorbeeldscript om u op weg.

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

### <a name ="policybased"></a>[Optioneel] Aangepaste IPsec/IKE-beleid met 'UsePolicyBasedTrafficSelectors' gebruiken
Als uw VPN-apparaten 'any-to-any' verkeer selectoren (op route gebaseerd/VTI-gebaseerde configuration) niet ondersteunen, moet u een aangepast IPsec/IKE-beleid maken en configureren van de optie 'UsePolicyBasedTrafficSelectors' zoals beschreven in [in dit artikel ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> U moet een IPsec/IKE-beleid maken om in te schakelen, de optie 'UsePolicyBasedTrafficSelectors' op de verbinding.

Het onderstaande voorbeeldscript maakt een IPsec/IKE-beleid met de volgende algoritmen en parameters:
* IKEv2: AES256, SHA384 DHGroup24
* IPsec: AES256, SHA1, PFS24, SA levensduur 7200 seconden & 20480000KB (20GB)

Het beleid van toepassing is en het schakelt 'UesPolicyBasedTrafficSelectors' op de verbinding.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Optioneel] BGP gebruiken voor S2S-VPN-verbinding
U kunt desgewenst BGP gebruiken op de verbinding. Zie [BGP voor VPN-gateway](vpn-gateway-bgp-resource-manager-ps.md). Er zijn twee verschillen:

De lokale adresvoorvoegsels kunnen een enkele host-adres, het lokale BGP-peer-IP-adres zijn:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

U moet instellen '-EnableBGP ' op $True bij het maken van de verbinding:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Volgende stappen
Zie [Actief/actief VPN-gateways configureren voor cross-premises en VNet-naar-VNet-verbindingen](vpn-gateway-activeactive-rm-powershell.md) voor de stappen om actief/actief on-premises en VNet-naar-VNet-verbindingen te configureren.

