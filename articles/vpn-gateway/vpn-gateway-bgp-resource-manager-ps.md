---
title: 'Configureren van BGP op Azure VPN-Gateways: Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van BGP met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Hoe tooconfigure BGP op Azure VPN-Gateways met behulp van PowerShell
Dit artikel begeleidt u bij Hallo stappen tooenable BGP op een cross-premises Site-naar-Site (S2S) VPN-verbinding en een VNet-naar-VNet-verbinding met Hallo Resource Manager-implementatiemodel en PowerShell.

## <a name="about-bgp"></a>Over BGP
BGP is Hallo standaardprotocol voor routering gebruikte in Hallo Internet tooexchange Routering en bereikbaarheid tussen twee of meer netwerken. BGP maakt hello Azure VPN-Gateways en uw on-premises VPN-apparaten, BGP-peers of neighbors genoemd, tooexchange 'routes' die wordt beide gateways informeren over Hallo beschikbaarheid en bereikbaarheid voor degenen prefixes toogo via Hallo gateways of routers die betrokken zijn. BGP ook transitroutering tussen meerdere netwerken door routes die een BGP-gateway van één BGP-peer-tooall leert andere BGP-peers.

Zie [overzicht van BGP met Azure VPN-Gateways](vpn-gateway-bgp-overview.md) meer discussie over de voordelen van BGP- en toounderstand Hallo technische vereisten en overwegingen van het gebruik van BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Aan de slag met BGP op Azure VPN-gateways

Dit artikel begeleidt u bij Hallo stappen toodo Hallo taken te volgen:

* [Deel 1 - Enable BGP op uw Azure VPN-gateway](#enablebgp)
* [Deel 2: een cross-premises verbinding maken met BGP](#crossprembgp)
* [Deel 3 – een VNet-naar-VNet verbinding maken met BGP](#v2vbgp)

Elk deel van de instructies Hallo vormt een basisbouwsteen voor het inschakelen van BGP in uw netwerkverbinding. Als u alle drie delen hebt voltooid, build Hallo topologie zoals weergegeven in het volgende diagram Hallo:

![BGP-topologieën](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

U kunt onderdelen samen toobuild een meer complexe, Multihop, doorvoer-netwerk dat voldoet aan uw behoeften kunt combineren.

## <a name ="enablebgp"></a>Deel 1: BGP configureren op Hallo Azure VPN-Gateway
Hallo configuratiestappen instellen Hallo BGP-parameters van hello Azure VPN-gateway zoals weergegeven in het volgende diagram Hallo:

![BGP-Gateway](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Voordat u begint
* Controleer of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* Hello Azure Resource Manager PowerShell-cmdlets installeren. Zie voor meer informatie over het installeren van de PowerShell-cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Stap 1: Maak en configureer VNet1
#### <a name="1-declare-your-variables"></a>1. De variabelen declareren
Voor deze oefening eerst we onze variabelen declareren. Hallo volgende voorbeeld Hallo variabelen gedeclareerd met Hallo waarden voor deze oefening. Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie. U kunt deze variabelen gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert. Wijzig variabelen hello, en kopieert en plakt u in de PowerShell-console.

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken
toouse hello Resource Manager-cmdlets, zorg ervoor dat u overschakelt naar tooPowerShell modus. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

Open de PowerShell-console en tooyour-account koppelen. Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 maken
Hallo maakt volgende voorbeeld een virtueel netwerk met de naam TestVNet1 en drie subnetten, één naam GatewaySubnet, een opgeroepen FrontEnd en één opgeroepen back-end. Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet. Als u een andere naam kiest, mislukt het maken van de gateway.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Stap 2: Hallo VPN-Gateway voor TestVNet1 maken met de BGP-parameters
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Hallo IP-adres en subnet configuraties maken
Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt. U zult ook Hallo vereist subnet en IP-configuraties definiëren.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Hallo VPN-gateway maken met Hallo als getal
De virtuele netwerkgateway Hallo voor TestVNet1 maken. BGP is een op Route gebaseerde VPN-gateway en Hallo toevoeging parameter, - Asn tooset Hallo ASN (AS-nummer) vereist voor TestVNet1. Als Hallo ASN-parameter niet is ingesteld, wordt de ASN van 65515 toegewezen. Maken van een gateway kan even duren (30 minuten of meer toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Hello Azure BGP-Peer-IP-adres ophalen
Nadat het Hallo-gateway is gemaakt, moet u tooobtain Hallo BGP-Peer-IP-adres op Hallo Azure VPN-Gateway. Dit adres is de benodigde tooconfigure hello Azure VPN-Gateway als een BGP-Peer voor uw on-premises VPN-apparaten.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

de laatste opdracht Hallo toont Hallo bijbehorende BGP configuraties op Hallo Azure VPN-Gateway; bijvoorbeeld:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Zodra Hallo gateway is gemaakt, kunt u deze gateway tooestablish cross-premises-verbinding of een VNet-naar-VNet-verbinding met BGP. Hallo doorlopen volgende secties Hallo stappen toocomplete Hallo oefening.

## <a name ="crossprembbgp"></a>Deel 2: een cross-premises verbinding maken met BGP

tooestablish een cross-premises-verbinding, moet u een lokale netwerkgateway toorepresent toocreate uw on-premises VPN-apparaat en een verbinding tooconnect Hallo VPN-gateway met de lokale netwerkgateway Hallo. Hoewel er artikelen die u bij deze stappen helpt, wordt in dit artikel Hallo extra eigenschappen vereist toospecify Hallo BGP-configuratieparameters bevat.

![BGP voor Cross-Premises](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Controleer of u hebt uitgevoerd voordat u doorgaat, [Part 1](#enablebgp) van deze oefening.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Stap 1 - maken en configureren van de lokale netwerkgateway Hallo

#### <a name="1-declare-your-variables"></a>1. De variabelen declareren

In deze oefening blijft toobuild Hallo configuratie wordt weergegeven in het Hallo-diagram. Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Een aantal dingen toonote met betrekking tot Hallo lokale netwerk gateway parameters:

* Hallo lokale netwerkgateway kan zich in dezelfde hello of een andere locatie en resource als Hallo VPN-gateway. Dit voorbeeld ziet u ze in verschillende resourcegroepen op verschillende locaties.
* Hallo minimaal voorvoegsel moet u toodeclare voor de lokale netwerkgateway Hallo is Hallo hostadres van uw BGP-Peer-IP-adres op uw VPN-apparaat. In dit geval is een /32 voorvoegsel "10.52.255.254/32".
* U moet verschillende ASN van BGP tussen uw on-premises netwerken en Azure VNet gebruiken als een herinnering. Als ze zijn dezelfde hello, moet u toochange uw VNet ASN als Hallo ASN toopeer in uw on-premises VPN-apparaat al worden gebruikt met andere BGP-neighbors.

Voordat u doorgaat, zorg er dan voor dat u nog steeds verbonden tooSubscription 1 zijn.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. De lokale netwerkgateway Hallo voor Site5 maken

Ervoor toocreate Hallo-resourcegroep worden als deze niet gemaakt is, voordat u de lokale netwerkgateway Hallo maakt. Let op Hallo twee extra parameters voor de lokale netwerkgateway Hallo: Asn en BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Stap 2: verbinding maken met de Hallo VNet-gateway en de lokale netwerkgateway

#### <a name="1-get-hello-two-gateways"></a>1. Hallo twee gateways ophalen

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Hallo TestVNet1 tooSite5 verbinding maken

In deze stap maakt u Hallo verbinding van TestVNet1 tooSite5. U moet opgeven '-EnableBGP $True ' tooenable BGP voor deze verbinding. Zoals eerder besproken, is het mogelijk toohave BGP- en niet-BGP-verbindingen voor Hallo dezelfde Azure VPN-Gateway. Tenzij BGP is ingeschakeld in de eigenschap connection hello, wordt Azure niet BGP inschakelen voor deze verbinding Hoewel BGP-parameters zijn al geconfigureerd op beide gateways.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Hallo bevat volgende voorbeeld de parameters van Hallo die Hallo BGP-configuratiesectie aangaan op uw on-premises VPN-apparaat voor deze oefening:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Hallo-verbinding is gemaakt na een paar minuten en Hallo BGP peering sessie begint zodra Hallo IPsec-verbinding tot stand is gebracht.

## <a name ="v2vbgp"></a>Deel 3 – een VNet-naar-VNet verbinding maken met BGP

In deze sectie voegt een VNet-naar-VNet-verbinding met BGP, zoals wordt weergegeven in het volgende diagram Hallo:

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Hallo instructies te volgen blijven uit de vorige stappen Hallo. U moet voltooien [deel I](#enablebgp) toocreate en configureer TestVNet1 en VPN-Gateway met BGP Hallo. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Stap 1: TestVNet2 en Hallo VPN-gateway maken

Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet2, niet met een van uw VNet-bereiken overlapt.

In dit voorbeeld behoren virtuele netwerken Hallo toohello hetzelfde abonnement. U kunt de VNet-naar-VNet-verbindingen tussen de verschillende abonnementen instellen. Zie voor meer informatie [een VNet-naar-VNet-verbinding configureren](vpn-gateway-vnet-vnet-rm-ps.md). Zorg ervoor dat u toevoegt Hallo '-EnableBgp $True ' wanneer maken Hallo verbindingen tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. De variabelen declareren

Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. TestVNet2 in Hallo nieuwe resourcegroep maken

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Hallo VPN-gateway maken voor TestVNet2 met BGP-parameters

Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway maakt voor uw VNet en definieer Hallo vereist subnet en IP-configuraties.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Hallo VPN-gateway maken met Hallo AS-nummer. U moet Hallo standaard een ASN overschrijven op uw Azure VPN-gateways. Hallo ASN's voor Hallo VNets verbonden moet zijn verschillende tooenable BGP en transitroutering.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Stap 2: verbinding maken met de Hallo TestVNet1 en TestVNet2 gateways

In dit voorbeeld beide gateways zijn in Hallo hetzelfde abonnement. U kunt deze stap bij het Hallo voltooien dezelfde PowerShell-sessie.

#### <a name="1-get-both-gateways"></a>1. Beide gateways ophalen

Zorg ervoor dat u zich aanmeldt en verbinding maakt tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Beide verbindingen maken

In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet2 en Hallo verbinding van TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Ervoor tooenable BGP voor beide verbindingen zijn.
> 
> 

Na het voltooien van deze stappen Hallo-verbinding tot stand is gebracht na een paar minuten. Hallo BGP-peeringsessie is nadat de Hallo VNet-naar-VNet-verbinding is voltooid.

Als u alle drie de gedeelten van deze oefening hebt voltooid, hebt u vastgesteld Hallo netwerktopologie te volgen:

![BGP voor VNet-naar-VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Volgende stappen

Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.
