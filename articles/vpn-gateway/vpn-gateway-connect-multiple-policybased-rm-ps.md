---
title: 'Verbinding maken met Azure VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van Azure op route gebaseerde VPN-gateway toomultiple op beleid gebaseerde VPN-apparaten met Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>Verbinding maken met Azure VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten met behulp van PowerShell

In dit artikel helpt u bij het configureren van een Azure op route gebaseerde VPN-gateway tooconnect toomultiple on-premises op beleid gebaseerde VPN-apparaten gebruik te maken van aangepaste IPsec/IKE-beleidsregels voor S2S-VPN-verbindingen.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>Over op beleid gebaseerd en op route gebaseerde VPN-gateways

Beleid - *versus* op route gebaseerde VPN-apparaten in hoe Hallo IPsec verkeer selectoren zijn ingesteld op een verbinding verschillen:

* **Op basis van beleid** VPN-apparaten gebruiken Hallo combinaties van voorvoegsels van beide netwerken toodefine hoe verkeer wordt versleuteld/ontsleuteld via IPsec-tunnels. Dit wordt gewoonlijk samengesteld op de firewallapparaten wordt uitgevoerd met het filteren van netwerkpakketten. IPSec-tunnel versleuteling en ontsleuteling toegevoegd toohello pakketfilters en verwerkingsengine.
* **Op route gebaseerde** VPN-apparaten gebruiken any-to-any (jokertekens) verkeer selectoren en laat routering/doorsturen tabellen direct verkeer toodifferent IPSec-tunnels. Dit wordt gewoonlijk samengesteld op router platforms waarbij elke IPsec-tunnel is gemodelleerd als een netwerkinterface of VTI (virtuele tunnelinterface).

Hallo markeren volgende diagrammen Hallo twee modellen:

### <a name="policy-based-vpn-example"></a>Op beleid gebaseerde VPN-voorbeeld
![op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Op route gebaseerde VPN-voorbeeld
![op route gebaseerd](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Azure-ondersteuning voor VPN op basis van beleid
Azure ondersteunt momenteel, beide modi van VPN-gateways: op route gebaseerde VPN-gateways en op beleid gebaseerde VPN-gateways. Ze zijn gebaseerd op verschillende interne platforms, ertoe leiden dat andere specificaties:

|                          | **Beleid gebaseerd VPN-Gateway** | **Op route gebaseerd VPN-Gateway**               |
| ---                      | ---                         | ---                                      |
| **Azure-Gateway SKU**    | Basic                       | Basic, Standard, HighPerformance         |
| **IKE-versie**          | IKEv1                       | IKEv2                                    |
| **Max. S2S-verbindingen** | **1**                       | Basic-/ Standard: 10<br> HighPerformance: 30 |
|                          |                             |                                          |

Hallo aangepaste IPsec/IKE-beleid, kunt u nu Azure op route gebaseerde VPN-gateways toouse verkeer op basis van het voorvoegsel selectoren met optie configureren '**PolicyBasedTrafficSelectors**', tooconnect tooon-premises op beleid gebaseerde VPN-apparaten. Op deze manier kunt u tooconnect van een virtuele Azure-netwerk en VPN-gateway toomultiple on-premises VPN-/ firewall-apparaten op basis van beleid, Hallo één verbindingslimiet verwijderen uit Hallo huidige Azure op beleid gebaseerde VPN-gateways.

> [!IMPORTANT]
> 1. tooenable deze connectiviteit uw on-premises op beleid gebaseerde VPN-apparaten moeten ondersteunen **IKEv2** tooconnect toohello Azure op route gebaseerde VPN-gateways. Raadpleeg de specificaties van uw VPN-apparaat.
> 2. Hallo on-premises netwerken verbinding maken via VPN-apparaten op basis van beleid met deze methode kunnen alleen verbinding maken met toohello virtuele Azure-netwerk; **ze tooother on-premises netwerken kunnen niet doorvoer of virtuele netwerken via dezelfde Azure VPN-gateway Hallo**.
> 3. de configuratieoptie Hallo maakt deel uit van aangepaste IPsec/IKE-verbindingsbeleid Hallo. Als u Hallo verkeer op basis van beleid selector-optie inschakelt, moet u de volledige beleid Hallo (IPsec/IKE-algoritmen voor versleuteling en integriteit, kracht en SA-levensduur) opgeven.

Hallo volgende diagram ziet waarom transitroutering via Azure VPN-gateway werkt niet met op beleid gebaseerde Hallo-optie:

![doorvoer op basis van beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Zoals u in het diagram hello, heeft hello Azure VPN-gateway verkeer selectoren van Hallo virtueel netwerk tooeach van Hallo-voorvoegsels voor lokale netwerk, maar niet de voorvoegsels van Hallo-cross-verbinding. Kan elk communiceren tooVNet1 respectievelijk maar kan geen verbinding maken via hello Azure VPN-gateway tooeach andere bijvoorbeeld lokale site 2, 3, en site 4. Hallo diagram ziet u Hallo verkeer selectoren die niet beschikbaar in hello Azure VPN-gateway in deze configuratie cross-verbinding.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Op beleid gebaseerde verkeer selectoren configureren op een verbinding

Hallo instructies in dit artikel volgen Hallo dezelfde voorbeeld zoals beschreven in [configureren IPsec/IKE-beleid voor S2S of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish een S2S VPN-verbinding. Dit wordt weergegeven in het volgende diagram Hallo:

![s2s-beleid](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Hallo werkstroom tooenable deze connectiviteit:
1. Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway voor uw cross-premises-verbinding maken
2. Een IPsec/IKE-beleid maken
3. Hallo-beleid toepassen wanneer u een S2S- of VNet-naar-VNet-verbinding maakt en **inschakelen Hallo verkeer op basis van beleid selectoren** op Hallo-verbinding
4. Als al Hallo verbinding is gemaakt, kunt u toepassen of Hallo beleid tooan bestaande verbinding bijwerken

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Op beleid gebaseerde verkeer selectoren op een verbinding inschakelen

Zorg ervoor dat u hebt voltooid [deel 3 van Hallo configureren IPsec/IKE-beleid artikel](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor deze sectie. Hallo wordt na Hallo dezelfde parameters en stappen:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Stap 1: Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. De variabelen declareren & tooyour abonnement verbinding
Voor deze oefening eerst we onze variabelen declareren. Ervoor tooreplace Hallo waarden door uw eigen worden wanneer u configureert voor productie.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
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
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
toouse hello Resource Manager-cmdlets, zorg ervoor dat u overschakelt naar tooPowerShell modus. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

Open de PowerShell-console en tooyour-account koppelen. Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken
Hallo volgende voorbeeld maakt Hallo virtueel netwerk TestVNet1 met drie subnetten en Hallo VPN-gateway. Bij het vervangen van waarden, is het belangrijk dat u altijd de naam het gatewaysubnet bijzonder GatewaySubnet. Als u een andere naam kiest, mislukt het maken van de gateway.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid

#### <a name="1-create-an-ipsecike-policy"></a>1. Een IPsec/IKE-beleid maken

> [!IMPORTANT]
> U moet een beleid voor IPsec/IKE in volgorde tooenable 'UsePolicyBasedTrafficSelectors' optie op Hallo verbinding toocreate.

Hallo volgende voorbeeld wordt een IPsec/IKE-beleid met deze algoritmen en parameters:
* IKEv2: AES256, SHA384 DHGroup24
* IPsec: AES256, SHA256, PFS24, SA levensduur 3600 seconden & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Hallo S2S VPN-verbinding maken met op beleid gebaseerde verkeer selectoren en IPsec/IKE-beleid
Een S2S VPN-verbinding maken en toepassen van Hallo IPsec/IKE-beleid in de vorige stap Hallo hebt gemaakt. Houd rekening met de extra parameter Hallo '-UsePolicyBasedTrafficSelectors $True ' waarmee verkeer op basis van beleid selectoren op Hallo-verbinding.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Na het voltooien van Hallo stappen wordt Hallo S2S VPN-verbinding gebruik Hallo IPsec/IKE-beleid is gedefinieerd, en schakel verkeer op basis van beleid selectoren op Hallo verbinding. U kunt dezelfde tooadd meer verbindingen tooadditional on-premises op beleid gebaseerde VPN-apparaten van stappen Hallo herhalen Hallo dezelfde Azure VPN-gateway.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Selectoren verkeer op basis van beleid voor een verbinding bijwerken
de laatste sectie Hallo ziet u hoe tooupdate Hallo verkeer op basis van beleid Selector optie voor een bestaande S2S VPN-verbinding.

### <a name="1-get-hello-connection"></a>1. Hallo-verbinding ophalen
Hallo verbindingsbron ophalen.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Hallo-verkeer op basis van beleid Selector optie controleren
Hallo geeft volgende regel aan of Hallo verkeer op basis van beleid selectoren worden gebruikt voor Hallo verbinding:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Als Hallo regel retourneert '**True**', vervolgens selectoren verkeer op basis van beleid worden geconfigureerd op Hallo verbinding; anders wordt '**False**. "

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Hallo-verkeer op basis van beleid selectoren op een verbinding bijwerken
Zodra u Hallo verbindingsbron hebt verkregen, kunt u in- of uitschakelen van Hallo-optie.

#### <a name="disable-usepolicybasedtrafficselectors"></a>UsePolicyBasedTrafficSelectors uitschakelen
Hello volgende voorbeeld wordt uitgeschakeld Hallo verkeer op basis van beleid Selector optie, maar blijft Hallo ongewijzigd IPsec/IKE-beleid:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>UsePolicyBasedTrafficSelectors inschakelen
Hallo volgende voorbeeld wordt Hallo verkeer op basis van beleid Selector-optie ingeschakeld, maar blijft Hallo ongewijzigd IPsec/IKE-beleid:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.

Bekijk ook [configureren IPsec/IKE-beleid voor S2S-VPN- of VNet-naar-VNet-verbindingen](vpn-gateway-ipsecikepolicy-rm-powershell.md) voor meer informatie over aangepaste IPsec/IKE-beleidsregels.
