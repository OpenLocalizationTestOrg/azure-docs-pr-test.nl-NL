---
title: 'Actieve S2S VPN-verbindingen configureren voor VPN-Gateways: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van actieve verbindingen met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Actieve S2S VPN-verbindingen met Azure VPN-Gateways configureren

Dit artikel begeleidt u bij Hallo stappen toocreate actieve cross-premises en VNet-naar-VNet-verbindingen met Hallo Resource Manager-implementatiemodel en PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Over maximaal beschikbare Cross-Premises verbindingen
hoge beschikbaarheid tooachieve voor cross-premises en VNet-naar-VNet-connectiviteit, moet u meerdere VPN-gateways implementeert en meerdere parallelle verbindingen tussen uw netwerken en Azure tot stand brengen. Zie [maximaal beschikbare Cross-Premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor een overzicht van opties voor netwerkconnectiviteit en -topologie.

Dit artikel bevat instructies Hallo tooset van een actieve cross-premises VPN-verbinding en de actieve verbinding tussen twee virtuele netwerken:

* [Deel 1 - maken en configureren van uw Azure VPN-gateway in de actieve-actieve modus](#aagateway)
* [Deel 2: actieve cross-premises verbindingen tot stand brengen](#aacrossprem)
* [Deel 3 - actief / actief-VNet-naar-VNet-verbindingen tot stand brengen](#aav2v)
* [Deel 4 - bestaande gateway tussen actieve en stand-by active-Update](#aaupdate)

U kunt deze samen toobuild een meer complexe, maximaal beschikbare netwerktopologie die voldoet aan uw behoeften kunt combineren.

> [!IMPORTANT]
> Houd er rekening mee dat Hallo actieve-actieve modus maakt gebruik van alleen Hallo SKU's te volgen: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (voor oude verouderde SKU's)
> 
> 

## <a name ="aagateway"></a>Deel 1 - maken en configureren van actieve VPN-gateways
Hallo stappen te volgen configureert in actieve modi uw Azure VPN-gateway. Hallo belangrijke verschillen tussen Hallo actieve en stand-by active-gateways:

* U moet twee IP-Gateway-configuraties toocreate met twee openbare IP-adressen
* U moet Hallo EnableActiveActiveFeature markering instellen
* Hallo gateway-SKU moet VpnGw1, VpnGw2, VpnGw3 of HighPerformance (verouderde SKU).

Hallo zijn andere eigenschappen Hallo hetzelfde als Hallo actieve actieve gateways. 

### <a name="before-you-begin"></a>Voordat u begint
* Controleer of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* U moet tooinstall hello Azure Resource Manager PowerShell-cmdlets. Zie [overzicht van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.

### <a name="step-1---create-and-configure-vnet1"></a>Stap 1: Maak en configureer VNet1
#### <a name="1-declare-your-variables"></a>1. De variabelen declareren
Voor deze oefening declareert u eerst de variabelen. Hallo onderstaand voorbeeld declareert Hallo variabelen met Hallo waarden voor deze oefening. Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie. U kunt deze variabelen gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert. Wijzig variabelen hello, en kopieert en plakt u in de PowerShell-console.

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
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
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken
Zorg ervoor dat u overschakelt tooPowerShell modus toouse Hallo Resource Manager-cmdlets. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

Open de PowerShell-console en tooyour-account koppelen. Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. TestVNet1 maken
Hallo onderstaand voorbeeld maakt een virtueel netwerk met de naam TestVNet1 en drie subnetten, één naam GatewaySubnet, een opgeroepen FrontEnd en één opgeroepen back-end. Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet. Als u een andere naam kiest, mislukt het maken van de gateway.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Stap 2: Hallo VPN-gateway voor TestVNet1 maken met de actieve-actieve modus
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Hallo openbare IP-adressen en IP-configuraties van gateway maken
Aanvraag twee openbare IP-adressen toobe toegewezen toohello gateway u voor uw VNet maakt. U zult ook definiëren Hallo subnet en IP-configuraties die nodig zijn.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Hallo VPN-gateway maken met een actief / actief-configuratie
De virtuele netwerkgateway Hallo voor TestVNet1 maken. Houd er rekening mee dat er twee GatewayIpConfig vermeldingen zijn en Hallo EnableActiveActiveFeature-vlag is ingesteld. Maken van een gateway kan even duren (45 minuten of meer toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Hallo gateway openbare IP-adressen en Hallo BGP-Peer-IP-adres verkrijgen
Zodra Hallo gateway is gemaakt, moet u tooobtain Hallo BGP-Peer-IP-adres op Hallo Azure VPN-Gateway. Dit adres is de benodigde tooconfigure hello Azure VPN-Gateway als een BGP-Peer voor uw on-premises VPN-apparaten.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Gebruik Hallo cmdlets tooshow Hallo twee openbare IP-adressen toegewezen voor uw VPN-gateway en de bijbehorende BGP-Peer-IP-adressen voor elk gatewayexemplaar te volgen:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

Hallo volgorde van Hallo openbare IP-adressen voor Hallo gatewayexemplaren en bijbehorende BGP-Peering adressen zijn Hallo Hallo dezelfde. In dit voorbeeld Hallo gateway-VM met openbare IP-adres van 40.112.190.5 10.12.255.4 gebruikt als het adres BGP-Peering en Hallo gateway met 138.91.156.129 10.12.255.5 wordt gebruikt. Deze informatie is nodig bij het instellen van uw on-premises VPN-apparaten toohello actieve gateway verbinding te maken. Hallo-gateway wordt weergegeven in Hallo diagram hieronder met alle adressen:

![actieve-actieve gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Zodra Hallo gateway is gemaakt, kunt u deze gateway tooestablish actieve cross-premises of VNet-naar-VNet-verbinding. Hallo uit te voeren doorlopen Hallo stappen toocomplete Hallo oefening.

## <a name ="aacrossprem"></a>Deel 2: een actieve cross-premises-verbinding tot stand brengen
tooestablish een cross-premises-verbinding, moet u een lokale netwerkgateway toorepresent toocreate uw on-premises VPN-apparaat en een verbinding tooconnect hello Azure VPN-gateway met de lokale netwerkgateway Hallo. In dit voorbeeld is hello Azure VPN-gateway actief / actief-actief. Als gevolg hiervan, zelfs als er slechts één on-premises VPN-apparaat (lokale netwerkgateway) en één verbindingsbron, beide exemplaren van Azure VPN-gateway tot stand brengen S2S VPN-tunnels met Hallo on-premises-apparaat.

Voordat u doorgaat, Controleer of u hebt voltooid [Part 1](#aagateway) van deze oefening.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Stap 1 - maken en configureren van de lokale netwerkgateway Hallo
#### <a name="1-declare-your-variables"></a>1. De variabelen declareren
In deze oefening blijven toobuild Hallo configuratie wordt weergegeven in het Hallo-diagram. Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Een aantal dingen toonote met betrekking tot Hallo lokale netwerk gateway parameters:

* Hallo lokale netwerkgateway kan zich in dezelfde hello of een andere locatie en resource als Hallo VPN-gateway. Dit voorbeeld ziet u ze in verschillende resourcegroepen, maar in Hallo dezelfde Azure-locatie.
* Als er slechts één on-premises VPN-apparaat zoals hierboven beschreven, worden de Hallo actieve verbinding kunt werken met of zonder BGP-protocol. In dit voorbeeld gebruikt BGP voor Hallo cross-premises-verbinding.
* Als BGP is ingeschakeld, is Hallo voorvoegsel dat u toodeclare nodig voor de lokale netwerkgateway Hallo Hallo host-adres van uw BGP-Peer-IP-adres op uw VPN-apparaat. In dit geval is een /32 prefix '10.52.255.253/32'.
* U moet verschillende ASN van BGP tussen uw on-premises netwerken en Azure VNet gebruiken als een herinnering. Als ze zijn dezelfde hello, moet u toochange uw VNet ASN als Hallo ASN toopeer in uw on-premises VPN-apparaat al worden gebruikt met andere BGP-neighbors.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. De lokale netwerkgateway Hallo voor Site5 maken
Controleer of dat u bent nog steeds verbonden tooSubscription 1 voordat u doorgaat. Hallo-resourcegroep maken als deze nog niet is gemaakt.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Stap 2: verbinding maken met de Hallo VNet-gateway en de lokale netwerkgateway
#### <a name="1-get-hello-two-gateways"></a>1. Hallo twee gateways ophalen

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Hallo TestVNet1 tooSite5 verbinding maken
In deze stap maakt u Hallo verbinding van TestVNet1 tooSite5_1 met 'EnableBGP' ingesteld te$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. VPN- en BGP-parameters voor uw on-premises VPN-apparaat
Hallo in het volgende voorbeeld bevat Hallo-parameters u in de configuratiesectie BGP Hallo op uw on-premises VPN-apparaat voor deze oefening voert:

    - Site5 ASN: 65050
    - BGP-IP-Site5: 10.52.255.253
    - Tooannounce-prefixes: (bijvoorbeeld) 10.51.0.0/16 en 10.52.0.0/16
    - Azure VNet ASN: 65010
    - Azure VNet BGP IP 1: 10.12.255.4 voor tunnel too40.112.190.5
    - Azure VNet BGP IP 2: 10.12.255.5 voor tunnel too138.91.156.129
    - Statische routes: bestemming 10.12.255.4/32, nexthop Hallo VPN-tunnel-interface too40.112.190.5 bestemming 10.12.255.5/32, nexthop Hallo VPN-tunnel-interface too138.91.156.129
    - eBGP Multihop: Zorg ervoor dat Hallo "multihop"-optie voor eBGP is ingeschakeld op uw apparaat, indien nodig

Hallo verbinding moet worden gemaakt na een paar minuten en Hallo BGP-peeringsessie wordt gestart zodra Hallo IPsec-verbinding tot stand is gebracht. In dit voorbeeld is tot nu toe geconfigureerd dat slechts één on-premises VPN-apparaat, wat resulteert in Hallo diagram hieronder weergegeven:

![Active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Stap 3: verbinding maken met twee lokale VPN-apparaten toohello actieve VPN-gateway
Als u twee VPN-apparaten op Hallo hebt dezelfde lokale netwerk, kunt u dual redundantie bereiken door de verbindende hello Azure VPN-gateway toohello tweede VPN-apparaat.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Hallo tweede lokale-netwerkgateway voor Site5 maken
Opmerking dat IP-adres van Hallo gateway adresvoorvoegsel en adres voor BGP-peering voor Hallo tweede lokale-netwerkgateway elkaar niet met Hallo vorige lokale netwerkgateway voor Hallo dezelfde overlappen mogen lokale netwerk.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Verbinding maken met de Hallo VNet gateway en Hallo tweede lokale-netwerkgateway
Hallo-verbinding van TestVNet1 tooSite5_2 maken met 'EnableBGP' ingesteld te$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. VPN- en BGP-parameters voor uw tweede on-premises VPN-apparaat
Op deze manier onderstaande lijsten Hallo parameters voert u in Hallo tweede VPN-apparaat:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Zodra het Hallo-verbinding (tunnels) worden gemaakt, hebt u twee redundante VPN-apparaten en tunnels verbinding maken met uw on-premises netwerk en Azure:

![Dual-redundantie-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Deel 3: een actieve VNet-naar-VNet-verbinding tot stand brengen
Deze sectie maakt een actief / actief-VNet-naar-VNet-verbinding met BGP. 

Hallo-instructies die hieronder worden overgenomen van Hallo hierboven beschreven stappen. U moet voltooien [Part 1](#aagateway) toocreate en configureer TestVNet1 en VPN-Gateway met BGP Hallo. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Stap 1: TestVNet2 en Hallo VPN-gateway maken
Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet2, niet met een van uw VNet-bereiken overlapt.

In dit voorbeeld behoren virtuele netwerken Hallo toohello hetzelfde abonnement. U kunt een VNet-naar-VNet-verbindingen tussen de verschillende abonnementen; instellen Raadpleeg het te[een VNet-naar-VNet-verbinding configureren](vpn-gateway-vnet-vnet-rm-ps.md) toolearn om meer details. Zorg ervoor dat u toevoegt Hallo '-EnableBgp $True ' wanneer maken Hallo verbindingen tooenable BGP.

#### <a name="1-declare-your-variables"></a>1. De variabelen declareren
Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
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
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
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

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Hallo actieve VPN-gateway voor TestVNet2 maken
Aanvraag twee openbare IP-adressen toobe toegewezen toohello gateway u voor uw VNet maakt. U zult ook definiëren Hallo subnet en IP-configuraties die nodig zijn.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Hallo VPN-gateway maken met Hallo als getal en Hallo 'EnableActiveActiveFeature' vlag. Houd er rekening mee dat u Hallo standaard een ASN op uw Azure VPN-gateways moet overschrijven. Hallo ASN's voor Hallo VNets verbonden moet zijn verschillende tooenable BGP en transitroutering.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
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

Na het voltooien van deze stappen Hallo verbinding maken in een paar minuten en Hallo BGP-peeringsessie zijn nadat Hallo VNet-naar-VNet-verbinding is voltooid met dubbel redundantie:

![Active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Deel 4 - bestaande gateway tussen actieve en stand-by active-Update
Hallo laatste sectie wordt beschreven hoe u een bestaande Azure VPN-gateway kunt configureren van de actieve stand-by-tooactive-actieve modus of vice versa.

> [!NOTE]
> Deze sectie bevat Hallo stappen tooresize een verouderde SKU (oude SKU) van een bestaande VPN-gateway van de standaard tooHighPerformance. Deze stappen voert geen upgrade van een oude verouderde SKU tooone Hallo nieuwe SKU's.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Een actieve stand-by-gateway tooactive-actieve gateway configureren
#### <a name="1-gateway-parameters"></a>1. Gateway-parameters
een gateway actief stand-by-converteert Hallo volgt naar een actief / actief-gateway. U moet toocreate een ander openbaar IP-adres en vervolgens een tweede Gateway IP-configuratie toevoegen. Hieronder bevat hello parameters gebruikt:

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Hallo openbare IP-adres maken, en voeg vervolgens Hallo tweede gateway IP-configuratie

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Actieve-actieve modus en update Hallo gateway inschakelen
Hallo gateway-object moet u instellen in PowerShell tootrigger Hallo feitelijke update. Hallo SKU van de virtuele netwerkgateway Hallo moet ook worden gewijzigd (formaat is gewijzigd) tooHighPerformance sinds deze eerder is gemaakt als standaard.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Deze update kan 30 too45 minuten duren.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Een actieve gateway tooactive stand-by-gateway configureren
#### <a name="1-gateway-parameters"></a>1. Gateway-parameters
Gebruik dezelfde Hallo Hallo-naam van de Hallo IP-configuratie die u wilt dat tooremove parameters zoals hierboven, opvragen.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Hallo gateway IP-configuratie verwijderen en Hallo actieve-actieve modus uitschakelen
U moet op dezelfde manier Hallo gateway object ingesteld in PowerShell tootrigger Hallo feitelijke update.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Deze update kan duren too30 met te 45 minuten.

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.
