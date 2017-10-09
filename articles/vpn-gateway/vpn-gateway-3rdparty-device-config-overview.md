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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>Overzicht van 3e partij VPN-apparaatconfiguraties
Dit artikel bevat een overzicht van de lokale VPN-apparaatconfiguraties voor het verbinden van tooAzure VPN-gateways. Hallo voorbeeld virtuele Azure-netwerk- en VPN-gateway setup wordt gebruikte tooconnect toodifferent on-premises VPN-apparaten met Hallo worden dezelfde parameters.

## <a name="device-requirements"></a>Vereisten voor apparaten
Standaard IPsec/IKE-protocol suites Azure VPN-gateways gebruiken voor S2S-VPN-tunnels. Raadpleeg te[over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor Hallo gedetailleerde parameters voor IPsec/IKE-protocol en standaard cryptografische algoritmen voor Azure VPN-gateways. U kunt optioneel Hallo exact dezelfde combinatie van cryptografische algoritmen en de belangrijkste sterkte voor een specifieke verbinding opgeven zoals beschreven in [over de vereisten voor cryptografische](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Één VPN-tunnel
de eerste topologie Hallo bestaat uit één S2S-VPN-tunnel tussen een Azure VPN-gateway en uw on-premises VPN-apparaat. Desgewenst kunt u BGP configureren op Hallo VPN-tunnel.

![één tunnel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Raadpleeg te[site-naar-site-verbinding configureren](vpn-gateway-howto-site-to-site-resource-manager-portal.md) voor gedetailleerde, stapsgewijze instructies. Hallo volgende secties Hallo parameters en geef een voorbeeld PowerShell script toohelp die u aan de slag.

### <a name="network-and-vpn-gateway-information"></a>Gegevens voor netwerk- en VPN-gateway
Deze sectie lijst Hallo parameters op voor het bovenstaande Hallo voorbeelden.

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
[Een S2S VPN-verbinding maken met PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) heeft Hallo gedetailleerde instructies. Deze sectie bevat een voorbeeld script tooget die u gestart.

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

### <a name ="policybased"></a>[Optioneel] Aangepaste IPsec/IKE-beleid met 'UsePolicyBasedTrafficSelectors' gebruiken
Als uw VPN-apparaten 'any-to-any' verkeer selectoren (op route gebaseerd/VTI-gebaseerde configuration) niet ondersteunen, u moet een aangepast beleid voor IPsec/IKE toocreate en configureer de optie 'UsePolicyBasedTrafficSelectors', zoals beschreven in [in dit artikel ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> U moet een beleid voor IPsec/IKE in volgorde tooenable 'UsePolicyBasedTrafficSelectors' optie op Hallo verbinding toocreate.

Hallo-voorbeeldscript maakt u een beleid voor IPsec/IKE met Hallo algoritmen en parameters te volgen:
* IKEv2: AES256, SHA384 DHGroup24
* IPsec: AES256, SHA1, PFS24, SA levensduur 7200 seconden & 20480000KB (20GB)

Hallo-beleid van toepassing is en het 'UesPolicyBasedTrafficSelectors' op Hallo verbinding maakt.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[Optioneel] BGP gebruiken voor S2S-VPN-verbinding
U kunt desgewenst BGP op Hallo verbinding gebruiken. Zie [BGP voor VPN-gateway](vpn-gateway-bgp-resource-manager-ps.md). Er zijn twee verschillen:

Hallo lokale adresvoorvoegsels kunnen een enkele host-adres, IP-adres van Hallo lokale BGP-peer zijn:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

U moet instellen '-EnableBGP ' te$ True bij het maken van Hallo verbinding:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Volgende stappen
Zie [actieve VPN-Gateways voor Cross-Premises en VNet-naar-VNet-verbindingen configureren](vpn-gateway-activeactive-rm-powershell.md) voor stappen tooconfigure actieve cross-premises en VNet-naar-VNet-verbindingen.

