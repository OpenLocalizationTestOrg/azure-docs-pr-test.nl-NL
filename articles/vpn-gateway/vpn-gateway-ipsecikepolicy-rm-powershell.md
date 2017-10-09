---
title: 'IPsec/IKE-beleid voor S2S-VPN- of VNet-naar-VNet-verbindingen te configureren: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In dit artikel begeleidt u bij het configureren van beleid voor IPsec/IKE voor S2S of VNet-naar-VNet-verbindingen met Azure VPN-Gateways met Azure Resource Manager en PowerShell.
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Beleid voor IPsec/IKE voor S2S-VPN- of VNet-naar-VNet-verbindingen configureren

Dit artikel begeleidt u bij Hallo stappen tooconfigure IPsec/IKE-beleid voor Site-naar-Site VPN- of VNet-naar-VNet-verbindingen met Hallo Resource Manager-implementatiemodel en PowerShell.

## <a name="about"></a>Informatie over IPsec en IKE beleidsparameters voor Azure VPN-gateways
IPsec en IKE-protocol standaard ondersteunt een groot aantal cryptografische algoritmen in verschillende combinaties. Raadpleeg te[over cryptografische vereisten en Azure VPN-gateways](vpn-gateway-about-compliance-crypto.md) toosee hoe dit kan helpen waarborgen cross-premises en VNet-naar-VNet-connectiviteit voldoen aan uw vereisten voor naleving of beveiliging.

In dit artikel biedt instructies toocreate en een IPsec/IKE-beleid configureren en toepassen van de nieuwe of bestaande verbinding tooa:

* [Deel 1 - werkstroom toocreate en IPsec/IKE-beleid instellen](#workflow)
* [Deel 2 - ondersteund cryptografische algoritmen en de belangrijkste voordelen](#params)
* [Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid](#crossprem)
* [Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid](#vnet2vnet)
* [Deel 5 - beheren (maken, toevoegen, verwijderen) IPsec/IKE-beleid voor een verbinding](#managepolicy)

> [!IMPORTANT]
> 1. Houd er rekening mee dat IPsec/IKE-beleid alleen werkt op Hallo gateway-SKU's te volgen:
>    * ***VpnGw1, VpnGw2, VpnGw3*** (op route gebaseerd)
>    * ***Standaard*** en ***HighPerformance*** (op route gebaseerd)
> 2. U kunt maar ***één*** beleidscombinatie opgeven voor een bepaalde verbinding.
> 3. U moet alle algoritmen en parameters opgeven voor zowel IKE (hoofdmodus) en IPsec (snelle modus). Gedeeltelijke beleidsspecificatie is niet toegestaan.
> 4. Neem contact op met uw VPN-apparaat Leverancierspecificaties tooensure Hallo beleid op uw on-premises VPN-apparaten wordt ondersteund. S2S of VNet-naar-VNet-verbindingen kunnen niet tot stand brengen als Hallo beleid niet compatibel zijn.

## <a name ="workflow"></a>Deel 1 - werkstroom toocreate en IPsec/IKE-beleid instellen
Deze sectie geeft een overzicht van Hallo werkstroom toocreate en update IPsec/IKE-beleid op een S2S VPN- of VNet-naar-VNet-verbinding:
1. Een virtueel netwerk en een VPN-gateway maken
2. Maak een lokale netwerkgateway voor cross-premises-verbinding of een ander virtueel netwerk en de gateway voor VNet-naar-VNet-verbinding
3. Een beleid voor IPsec/IKE maken met geselecteerde algoritmen en parameters
4. Maak een verbinding (IPSec- of VNet2VNet) met Hallo IPsec/IKE-beleid
5. Toevoegen/bijwerken/verwijderen uit een IPsec/IKE-beleid voor een bestaande verbinding

Hallo-instructies in dit artikel helpt u bij het instellen en configureren van beleid voor IPsec/IKE zoals u in Hallo diagram:

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Deel 2 - ondersteund cryptografische algoritmen en kracht van

Hallo volgende tabel bevat Hallo ondersteund cryptografische algoritmen en kracht kunnen worden geconfigureerd door Hallo-klanten:

| **IPsec/IKEv2**  | **Opties**    |
| ---  | --- 
| IKEv2-versleuteling | AES256, AES192, AES128, DES3, DES  
| IKEv2-integriteit  | SHA384, SHA256, SHA1, MD5  |
| DH-groep         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, geen |
| IPsec-versleuteling | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, geen    |
| IPsec-integriteit  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| PFS-groep        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, geen 
| QM SA-levensduur   | (**Optioneel**: standaardwaarden worden gebruikt als dat niet het opgegeven)<br>Seconden (geheel getal; **min. 300** /standaard 27000 seconden)<br>KB (geheel getal; **min. 1024**/standaard 102400000 KB)   |
| Verkeersselector | UsePolicyBasedTrafficSelectors ** ($True/$False; **Optioneel**, standaard $False als u niets opgeeft)    |
|  |  |

> [!IMPORTANT]
> 1. **Als GCMAES als voor IPsec-versleutelingsalgoritme wordt gebruikt, moet u dezelfde GCMAES algoritme en de sleutellengte Hallo voor IPSec-integriteit; bijvoorbeeld, met behulp van GCMAES128 voor beide**
> 2. Levensduur voor de Hoofdmodus IKEv2 wordt vastgesteld op 28.800 seconden op Hallo Azure VPN-gateways
> 3. Instelling 'UsePolicyBasedTrafficSelectors' te$ True voor een verbinding configureert hello Azure VPN-gateway tooconnect toopolicy gebaseerde VPN-firewall on-premises. Als u PolicyBasedTrafficSelectors inschakelt, moet u uw VPN-apparaat Hallo overeenkomende verkeer selectoren gedefinieerd met behulp van alle combinaties van uw lokale netwerk (lokale netwerkgateway) voorvoegsels van voorvoegsels Hallo virtuele Azure-netwerk heeft, tooensure in plaats van any-to-any. Als uw lokale netwerkvoorvoegsels 10.1.0.0/16 en 10.2.0.0/16 zijn, en de voorvoegsels van uw virtuele netwerk 192.168.0.0/16 en 172.16.0.0/16 zijn, moet u bijvoorbeeld toospecify Hallo verkeer selectoren te volgen:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

Zie voor meer informatie over op beleid gebaseerde verkeer selectoren [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Hallo volgende Tabellijsten Hallo bijbehorende Diffie-Hellman-groepen die worden ondersteund door het aangepaste beleid Hallo:

| **Diffie-Hellman-groep**  | **DHGroup**              | **PFSGroup** | **Sleutellengte** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | 768-bits MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024-bits MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048-bits MODP  |
| 19                        | ECP256                   | ECP256       | 256-bits ECP    |
| 20                        | ECP384                   | ECP284       | 384-bits ECP    |
| 24                        | DHGroup24                | PFS24        | 2048-bits MODP  |

Raadpleeg te[RFC3526](https://tools.ietf.org/html/rfc3526) en [RFC5114](https://tools.ietf.org/html/rfc5114) voor meer informatie.

## <a name ="crossprem"></a>Deel 3: een nieuwe S2S VPN-verbinding maken met IPsec/IKE-beleid

In deze sectie leert u Hallo van een S2S VPN-verbinding maken met een IPsec/IKE-beleid. Hallo volgt Hallo verbinding maken zoals u in Hallo diagram:

![s2s-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Zie [een S2S VPN-verbinding](vpn-gateway-create-site-to-site-rm-powershell.md) voor stapsgewijze instructies gedetailleerde voor het maken van een S2S VPN-verbinding.

### <a name="before"></a>Voordat u begint

* Controleer of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* Hello Azure Resource Manager PowerShell-cmdlets installeren. Zie [overzicht van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.

### <a name="createvnet1"></a>Stap 1: Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken

#### <a name="1-declare-your-variables"></a>1. De variabelen declareren

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Verbinding maken met tooyour abonnement en een nieuwe resourcegroep maken

Zorg ervoor dat u overschakelt tooPowerShell modus toouse Hallo Resource Manager-cmdlets. Zie [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md) (Windows PowerShell gebruiken met Resource Manager) voor meer informatie.

Open de PowerShell-console en tooyour-account koppelen. Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Hallo virtueel netwerk, VPN-gateway en de lokale netwerkgateway maken

Hallo volgende voorbeeld maakt Hallo virtueel netwerk TestVNet1, met drie subnetten en Hallo VPN-gateway. Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet. Als u een andere naam kiest, mislukt het maken van de gateway.

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

### <a name="s2sconnection"></a>Stap 2: een S2S VPN-verbinding maken met een IPsec/IKE-beleid

#### <a name="1-create-an-ipsecike-policy"></a>1. Een IPsec/IKE-beleid maken

Hallo volgende voorbeeldscript maakt u een beleid voor IPsec/IKE met Hallo algoritmen en parameters te volgen:

* IKEv2: AES256, SHA384 DHGroup24
* IPsec: AES256, SHA256, PFS24, SA levensduur 7200 seconden & 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Als u GCMAES voor IPSec-authenticatie gebruikt, moet u dezelfde GCMAES algoritme en de sleutellengte voor IPSec-codering en integriteit, bijvoorbeeld Hallo:

* IKEv2: AES256, SHA384 DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, SA levensduur 7200 seconden & 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Hallo S2S VPN-verbinding maken met Hallo IPsec/IKE-beleid

Een S2S VPN-verbinding maken en toepassen van beleid voor IPsec/IKE Hallo eerder hebt gemaakt.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

U kunt optioneel toevoegen '-UsePolicyBasedTrafficSelectors $True ' toohello verbinding maken cmdlet tooenable Azure VPN-gateway tooconnect toopolicy gebaseerde VPN-apparaten on-premises, zoals hierboven is beschreven.

> [!IMPORTANT]
> Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt alleen hello Azure VPN-gateway verzenden of Hallo IPsec/IKE voorstel met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren. Controleer of uw on-premises VPN-apparaat voor verbinding Hallo gebruikt of accepteert Hallo exacte beleid combinatie, anders Hallo S2S VPN-tunnel niet tot stand brengen.


## <a name ="vnet2vnet"></a>Deel 4: een nieuwe VNet-naar-VNet-verbinding maken met IPsec/IKE-beleid

Hallo-stappen voor het maken van een VNet-naar-VNet-verbinding met een beleid voor IPsec/IKE zijn vergelijkbaar toothat van een S2S VPN-verbinding. Hallo volgende voorbeeldscripts Hallo verbinding maken zoals u in Hallo diagram:

![V2V-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Zie [Maak een VNet-naar-VNet-verbinding](vpn-gateway-vnet-vnet-rm-ps.md) voor stappen gedetailleerde voor het maken van een VNet-naar-VNet-verbinding. U moet voltooien [deel 3](#crossprem) toocreate en configureer TestVNet1 en Hallo VPN-Gateway.

### <a name="createvnet2"></a>Stap 1: Hallo tweede virtuele netwerk- en VPN-gateway maken

#### <a name="1-declare-your-variables"></a>1. De variabelen declareren

Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Hallo tweede virtuele netwerk- en VPN-gateway in Hallo nieuwe resourcegroep maken

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Stap 2: een VNet-toVNet verbinding maken met Hallo IPsec/IKE-beleid

Vergelijkbare toohello S2S VPN-verbinding een IPsec/IKE-beleid maken en toepassen van toopolicy toohello nieuwe verbinding.

#### <a name="1-create-an-ipsecike-policy"></a>1. Een IPsec/IKE-beleid maken

Hallo volgende voorbeeldscript maakt u een ander IPsec/IKE-beleid met Hallo algoritmen en parameters te volgen:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, SA levensduur 7200 seconden en 4096KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. VNet-naar-VNet-verbindingen maken met de Hallo IPsec/IKE-beleid

Een VNet-naar-VNet-verbinding maken en toepassen van Hallo IPsec/IKE-beleid die u hebt gemaakt. In dit voorbeeld beide gateways zijn in Hallo hetzelfde abonnement. Zodat het is mogelijk toocreate en configureren van beide verbindingen met dezelfde IPsec/IKE-beleid in Hallo Hallo dezelfde PowerShell-sessie.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Als een beleid voor IPsec/IKE op een verbinding is opgegeven, wordt alleen hello Azure VPN-gateway verzenden of Hallo IPsec/IKE voorstel met opgegeven cryptografische algoritmen en de belangrijkste sterkte op die bepaalde verbinding accepteren. Zorg ervoor dat Hallo IPSec-beleid voor beide verbindingen zijn Hallo dezelfde, anders de VNet-naar-VNet-verbinding niet tot stand brengen.

Hallo-verbinding is gemaakt in een paar minuten na het voltooien van deze stappen en hebt u Hallo netwerktopologie te volgen, zoals wordt weergegeven in Hallo vanaf:

![ike-IPSec-beleid](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Deel 5 - Update IPsec/IKE-beleid voor een verbinding

de laatste sectie Hallo ziet u hoe toomanage IPsec/IKE-beleid voor een bestaande S2S of VNet-naar-VNet-verbinding. Hallo oefening hieronder wordt u begeleid bij Hallo bewerkingen op een verbinding te volgen:

1. Hallo IPsec/IKE-beleid van een verbinding weergeven
2. Toevoegen of bijwerken van Hallo IPsec/IKE-beleid tooa verbinding
3. Hallo IPsec/IKE-beleid verwijderen uit een verbinding

Hallo dezelfde stappen van toepassing tooboth S2S- en VNet-naar-VNet-verbindingen.

> [!IMPORTANT]
> IPsec/IKE-beleid wordt ondersteund op *standaard* en *HighPerformance* op route gebaseerde VPN-gateways alleen. Deze werkt niet op Hallo Basic gateway-SKU of Hallo op beleid gebaseerde VPN-gateway.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Hallo IPsec/IKE-beleid van een verbinding weergeven

Hallo volgende voorbeeld ziet u hoe tooget Hallo IPsec/IKE-beleid op een verbinding is geconfigureerd. Hallo scripts blijven ook uit Hallo oefeningen hierboven.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

de laatste opdracht Hallo bevat Hallo huidige IPsec/IKE-beleid geconfigureerd op Hallo verbinding, indien deze aanwezig is. Hallo volgende voorbeelduitvoer wordt voor Hallo verbinding:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

Als er geen IPsec/IKE-beleid dat is geconfigureerd, Hallo opdracht (PS > $connection6.policy) een leeg retourtype opgehaald. Dit betekent niet dat IPsec/IKE is niet geconfigureerd op Hallo verbinding, maar er is geen aangepaste IPsec/IKE-beleid. de huidige verbinding Hallo maakt gebruik van Hallo standaardbeleid onderhandeld tussen uw on-premises VPN-apparaat en hello Azure VPN-gateway.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Toevoegen of bijwerken van een beleid voor IPsec/IKE voor een verbinding

een nieuw beleid voor stappen tooadd Hallo of update zijn van een bestaand beleid op een verbinding Hallo dezelfde: een nieuw beleid maken en toepassen van Hallo nieuwe beleid toohello verbinding.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable 'UsePolicyBasedTrafficSelectors' wanneer tooan verbinding maken met on-premises op beleid gebaseerde VPN-apparaat toevoegen Hallo '-UsePolicyBaseTrafficSelectors ' parameter toohello cmdlet, of stel deze in te$ False toodisable Hallo optie:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

U krijgt Hallo verbinding opnieuw toocheck als Hallo beleid wordt bijgewerkt.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

U ziet Hallo-uitvoer van de laatste regel hello, zoals wordt weergegeven in Hallo voorbeeld te volgen:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Een beleid voor IPsec/IKE verwijderen uit een verbinding

Wanneer u een aangepast beleid Hallo van een verbinding verwijdert, hello Azure VPN-gateway wordt teruggezet back toohello [standaardlijst met IPsec/IKE voorstellen](vpn-gateway-about-vpn-devices.md) en start een opnieuw nieuwe onderhandeling met uw on-premises VPN-apparaat.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

U kunt hetzelfde script toocheck Hallo als Hallo beleid uit Hallo-verbinding is verwijderd.

## <a name="next-steps"></a>Volgende stappen

Zie [verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie over op beleid gebaseerde verkeer selectoren.

Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Een virtuele machine maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor de stappen.
