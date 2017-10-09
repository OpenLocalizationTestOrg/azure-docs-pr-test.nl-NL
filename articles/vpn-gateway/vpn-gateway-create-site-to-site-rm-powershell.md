---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: PowerShell | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>Een VNet met een site-naar-site-VPN-verbinding maken met PowerShell

Dit artikel laat zien hoe toouse PowerShell toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw on-premises netwerk toohello VNet. Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Klassieke portal (klassiek)](vpn-gateway-site-to-site-create.md)
> 
>


Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel. Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit. Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.

![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Voordat u begint

Controleer of dat u Hallo criteria volgen voordat u begint met de configuratie hebt voldaan:

* Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze. Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.
* Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt. Dit IP-adres kan zich niet achter een NAT bevinden.
* Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan. Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie. Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.
* Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. PowerShell-cmdlets worden regelmatig bijgewerkt en normaal gesproken moet u tooupdate uw PowerShell-cmdlets tooget Hallo meest recente functionaliteit. Als u uw PowerShell-cmdlets niet bijwerkt, mislukken Hallo waarden die zijn opgegeven. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het downloaden en installeren van de PowerShell-cmdlets.

### <a name="example"></a>Voorbeeldwaarden

Hallo-voorbeelden in dit artikel gebruiken Hallo waarden te volgen. U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Verbinding maken met tooyour abonnement

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Een virtueel netwerk en een gatewaysubnet maken

Als u nog geen virtueel netwerk hebt, maakt u er een. Wanneer u een virtueel netwerk maakt, zorg dat Hallo-adresruimten die u opgeeft niet overlappen met adresruimten Hallo die u op uw on-premises netwerk hebt.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate een virtueel netwerk en een gatewaysubnet

In dit voorbeeld worden een virtueel netwerk en een gatewaysubnet gemaakt. Als u al een virtueel netwerk die u een gatewaysubnet moet Zie tooadd [tooadd een gateway subnet tooa virtueel netwerk u al hebt gemaakt](#gatewaysubnet).

Een resourcegroep maken:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Maak uw virtuele netwerk.

1. Hallo-variabelen worden ingesteld.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Hallo VNet maken.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>een virtueel netwerk voor gateway-subnet tooa tooadd die u al hebt gemaakt

1. Hallo-variabelen worden ingesteld.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Hallo gatewaysubnet maken.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Hallo configuratie instellen.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Hallo lokale netwerkgateway maken

Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie. U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding. U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat. Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk. Als uw on-premises netwerk verandert, kunt u Hallo voorvoegsels eenvoudig bijwerken.

Hallo volgende waarden gebruiken:

* Hallo *GatewayIPAddress* Hallo IP-adres van uw on-premises VPN-apparaat. Het VPN-apparaat kan zich niet achter een NAT bevinden.
* Hallo *AddressPrefix* is uw on-premises-adresruimte.

een lokale netwerkgateway met één adresvoorvoegsel tooadd:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

een lokale netwerkgateway met meerdere adresvoorvoegsels tooadd:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify IP-adresvoorvoegsels voor uw lokale netwerkgateway:<br>
Soms veranderen de voorvoegsels voor uw lokale netwerkgateway. Hallo stappen u rekening houden met toomodify uw IP-adres voorvoegsels is afhankelijk van of u een VPN-gatewayverbinding hebt gemaakt. Zie Hallo [adresvoorvoegsels voor een lokale netwerkgateway wijzigen](#modify) sectie van dit artikel.

## <a name="PublicIP"></a>4. Een openbaar IP-adres aanvragen

Een VPN Gateway moet een openbaar IP-adres hebben. U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway. Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt. VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen. U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen. Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen. de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.

Een openbaar IP-adres dat wordt toegewezen tooyour virtueel netwerk VPN-gateway aanvragen.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Hallo-gateway voor IP-adressen van de configuratie maken

Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse. Hallo voorbeeld toocreate na de configuratie van uw gateway gebruiken:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Hallo VPN-gateway maken

VPN-gateway van Hallo virtueel netwerk maken. Maken van een VPN-gateway kan duren too45 minuten of meer toocomplete.

Hallo volgende waarden gebruiken:

* Hallo *- GatewayType* voor een Site-naar-Site configuratie is *Vpn*. Hallo-Gatewaytype is altijd specifiek toohello configuratie die u implementeert. Andere gatewayconfiguraties vereisen misschien -GatewayType ExpressRoute.
* Hallo *- VpnType* kan *RouteBased* (bedoeld tooas een dynamische Gateway in sommige documentatie), of *PolicyBased* (aangeduid tooas een statische Gateway in sommige documentatie ). Voor meer informatie over VPN-gatewaytypen raadpleegt u [Over VPN Gateway](vpn-gateway-about-vpngateways.md).
* Selecteer Hallo dat u wilt dat toouse Gateway-SKU. Voor bepaalde SKU's gelden configuratiebeperkingen. Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie. Als u krijgt een fout bij het maken van VPN-gateway Hallo met betrekking tot Hallo - GatewaySku, controleert u of dat u de meest recente versie van PowerShell-cmdlets Hallo Hallo hebt geïnstalleerd.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. Uw VPN-apparaat configureren

Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist. In deze stap configureert u het VPN-apparaat. Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:

- Een gedeelde sleutel. Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding. In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel. Het is raadzaam dat u een complexere sleutel toouse genereert.
- Hallo openbare IP-adres van uw virtuele netwerkgateway. U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI. toofind hello openbare IP-adres van uw virtuele netwerkgateway met behulp van PowerShell, gebruik Hallo voorbeeld te volgen:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Hallo VPN-verbinding maken

Maak vervolgens Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw VPN-apparaat. Ervoor tooreplace Hallo waarden door uw eigen worden. Hallo gedeelde sleutel moet overeenkomen met de Hallo-waarde die u voor de configuratie van uw VPN-apparaat gebruikt. U ziet dat Hallo '-ConnectionType' voor Site-naar-Site is *IPsec*.

1. Hallo-variabelen worden ingesteld.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Hallo verbinding maken.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Na een korte tijd hello wordt de verbinding worden gemaakt.

## <a name="toverify"></a>9. Hallo VPN-verbinding controleren

Er zijn een aantal verschillende manieren tooverify uw VPN-verbinding.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa virtuele machine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>IP-adresvoorvoegsels wijzigen voor de gateway van een lokaal netwerk

Als Hallo IP-adresvoorvoegsels die u gerouteerd tooyour on-premises locatie wilt wijzigen, kunt u de lokale netwerkgateway Hallo wijzigen. Er zijn twee sets met instructies. Hallo-instructies die u kiest, is afhankelijk van of u al uw gatewayverbinding hebt gemaakt.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Hallo gateway IP-adres voor een lokale netwerkgateway wijzigen

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Volgende stappen

*  Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.
* Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
