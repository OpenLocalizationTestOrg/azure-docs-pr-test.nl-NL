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
# <a name="about-vpn-gateway-configuration-settings"></a>Over configuratie-instellingen voor VPN-Gateway

Een VPN-gateway is een type van de virtuele netwerkgateway die versleuteld verkeer tussen uw virtuele netwerk en uw on-premises locatie via een openbare verbinding verzonden. U kunt ook een VPN-gateway toosend verkeer tussen virtuele netwerken via hello Azure-backbone gebruiken.

Er is een VPN-gatewayverbinding afhankelijk van configuratie van de Hallo van meerdere resources, die elk configureerbare instellingen bevat. Hallo-secties in dit artikel worden besproken Hallo bronnen en instellingen die betrekking tooa VPN-gateway voor een virtueel netwerk gemaakt in Resource Manager-implementatiemodel hebben. U vindt beschrijvingen en diagrammen topologie voor elke verbinding oplossing in Hallo [over VPN-Gateway](vpn-gateway-about-vpngateways.md) artikel.

## <a name="gwtype"></a>Gatewaytypen

Elk virtueel netwerk kan slechts één virtuele netwerkgateway van elk type hebben. Wanneer u een virtuele netwerkgateway maakt, moet u ervoor zorgen dat het Gatewaytype Hallo voor uw configuratie klopt.

beschikbare waarden voor - GatewayType Hallo zijn:

* VPN
* ExpressRoute

Een VPN-gateway vereist Hallo `-GatewayType` *Vpn*.

Voorbeeld:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>Gateway-SKU's

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Hallo-gateway SKU configureren

#### <a name="azure-portal"></a>Azure Portal

Als u hello Azure portal toocreate een virtuele netwerkgateway van Resource Manager gebruikt, selecteert u Hallo gateway-SKU via Hallo vervolgkeuzelijst. Hallo-opties u krijgt overeenkomen toohello Gatewaytype en VPN-type dat u selecteert.

#### <a name="powershell"></a>PowerShell

Hallo volgende PowerShell-voorbeeld geeft Hallo `-GatewaySku` als VpnGw1.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Wijzig de grootte van (wijzigen) een gateway-SKU

Als u uw gateway-SKU tooa tooupgrade wilt krachtiger SKU, kunt u Hallo `Resize-AzureRmVirtualNetworkGateway` PowerShell-cmdlet. U kunt ook downgraden Hallo gateway SKU-grootte die met deze cmdlet.

Hallo volgende PowerShell-voorbeeld ziet u dat toovpngw2 een gateway-SKU wordt gewijzigd.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Verbindingstypen

Elke configuratie vereist Hallo Resource Manager-implementatiemodel, het type van een specifieke virtuele-netwerkgateway verbinding. Hallo beschikbare Resource Manager PowerShell-waarden voor `-ConnectionType` zijn:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

Hallo PowerShell-voorbeeld te volgen, maken we een S2S-verbinding waarvoor Hallo verbindingstype *IPsec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>VPN-typen

Wanneer u de virtuele netwerkgateway Hallo voor de configuratie van een VPN-gateway maakt, moet u een VPN-type. Hallo VPN-type dat u kiest, hangt Hallo verbinding topologie dat u wilt dat toocreate. Bijvoorbeeld, vereist een P2S-verbinding een RouteBased VPN-type. Een VPN-type kan ook afhankelijk van Hallo-hardware die u gebruikt. S2S-configuraties vereisen een VPN-apparaat. Sommige VPN-apparaten ondersteunen alleen een bepaalde VPN-type.

Hallo VPN-type dat u selecteert moet voldoen aan alle vereisten voor Hallo verbinding voor de oplossing Hallo gewenste toocreate. Bijvoorbeeld als u wilt dat toocreate een S2S VPN-gatewayverbinding en een P2S-VPN-gatewayverbinding voor Hallo hetzelfde virtuele netwerk, gebruikt u VPN-type *RouteBased* omdat P2S een RouteBased VPN-type vereist. U moet tevens tooverify dat uw VPN-apparaat een RouteBased VPN-verbinding ondersteund. 

Wanneer een virtuele netwerkgateway is gemaakt, kunt u Hallo VPN-type niet wijzigen. U hebt toodelete Hallo virtuele netwerkgateway en maak een nieuwe. Er zijn twee VPN-typen:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hallo volgende PowerShell-voorbeeld geeft Hallo `-VpnType` als *RouteBased*. Wanneer u een gateway maakt, moet u ervoor zorgen dat Hallo - VpnType juist is voor uw configuratie.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Vereisten voor de gateway

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Gatewaysubnet

Voordat u een VPN-gateway maakt, moet u een gatewaysubnet maken. gatewaysubnet Hallo Hallo IP-adressen bevat die Hallo-gateway van het virtuele netwerk virtuele machines en services gebruik. Wanneer u uw virtuele netwerkgateway maakt, gateway virtuele machines zijn geïmplementeerd toohello gatewaysubnet en geconfigureerd met instellingen voor VPN-gateway Hallo vereist. U moet nooit alles anders (bijvoorbeeld extra virtuele machines) toohello gatewaysubnet implementeren. Hallo gatewaysubnet moet de naam 'GatewaySubnet' toowork goed. Naamgeving Hallo gatewaysubnet 'GatewaySubnet' kunt weet Azure dat dit Hallo subnet toodeploy Hallo virtuele netwerkgateway virtuele machines en services.

Wanneer u Hallo gatewaysubnet maakt, geeft u het aantal IP-adressen die subnet Hallo Hallo bevat. Hallo IP-adressen in het gatewaysubnet Hallo zijn toegewezen toohello gateway-VM's en gatewayservices. Sommige configuraties moeten meer IP-adressen dan andere. Bekijkt hello instructies voor het Hallo-configuratie dat u wilt dat toocreate en controleren die Hallo gatewaysubnet gewenste toocreate voldoet aan deze vereisten. Bovendien kunt u ervoor dat het gatewaysubnet bevat onvoldoende IP-adressen tooaccommodate mogelijke toekomstige aanvullende configuraties toomake. U kunt een gatewaysubnet slechts/29 maken, wordt aangeraden dat u een gatewaysubnet van/28 of groter maakt (/ 28, / 27, /26 enz.). Als u de functionaliteit toevoegen in Hallo toekomstige, u geen tootear hebben uw gateway en vervolgens verwijderen en opnieuw Hallo gateway subnet tooallow voor meer IP-adressen.

Hallo ziet volgende Resource Manager PowerShell-voorbeeld u een gatewaysubnet met de naam GatewaySubnet. U kunt zien Hallo CIDR-notatie een/27, geeft dit biedt voldoende IP-adressen voor de meeste configuraties die momenteel aanwezig zijn.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Lokale netwerkgateways

Bij het maken van de configuratie van een VPN-gateway, vertegenwoordigt de lokale netwerkgateway Hallo vaak uw on-premises locatie. In het klassieke implementatiemodel hello is de lokale netwerkgateway Hallo waarnaar wordt verwezen tooas een lokale Site. 

U Hallo lokale netwerkgateway een naam geven, Hallo openbare IP-adres van Hallo on-premises VPN-apparaat en Hallo adresvoorvoegsels die op Hallo on-premises locatie bevinden zich opgeven. Azure bekijkt hello bestemmingsadressen voor netwerkverkeer, raadpleegt Hallo-configuratie die u hebt opgegeven voor uw lokale netwerkgateway en routeert pakketten dienovereenkomstig. U wordt ook lokale netwerkgateways voor VNet-naar-VNet-configuraties die gebruikmaken van een VPN-gatewayverbinding.

Hallo volgende PowerShell-voorbeeld maakt een nieuwe lokale netwerkgateway:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Soms moet u de gateway-instellingen voor toomodify Hallo lokale netwerk. Bijvoorbeeld, wanneer u toevoegen of wijzigen van Hallo-adresbereik, of als Hallo IP-adres van Hallo VPN-apparaat is gewijzigd. U kunt deze instellingen in de klassieke portal Hallo op Hallo lokale netwerken pagina wijzigen voor een klassiek VNet. Zie voor Resource Manager [lokale gateway netwerkinstellingen wijzigen met behulp van PowerShell](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>REST-API's en PowerShell-cmdlets

Zie voor aanvullende technische bronnen en syntaxis van de specifieke vereisten voor het met de REST-API's, PowerShell-cmdlets of Azure CLI voor VPN-Gateway configuraties Hallo pagina's te volgen:

| **Klassiek** | **Resource Manager** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| Niet ondersteund | [Azure-CLI](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over beschikbare verbinding configuraties [over VPN-Gateway](vpn-gateway-about-vpngateways.md).