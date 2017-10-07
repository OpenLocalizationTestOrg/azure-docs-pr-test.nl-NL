---
title: 'Configureer geforceerde tunneling voor Azure Site-naar-Site-verbindingen: Resource Manager | Microsoft Docs'
description: Hoe tooredirect of 'force' alle Internet bestemd verkeer back tooyour een on-premises locatie.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configureer geforceerde tunneling met hello Azure Resource Manager-implementatiemodel

Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle. Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels. Zonder geforceerde tunneling passeert internetverkeer van uw virtuele machines in Azure altijd van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer. Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

In dit artikel begeleidt u bij het configureren geforceerde tunneling voor virtuele netwerken die zijn gemaakt met Hallo Resource Manager-implementatiemodel. Geforceerde tunneling kan worden geconfigureerd met behulp van PowerShell, niet via het Hallo-portal. Als u tooconfigure geforceerde tunneling voor het klassieke implementatiemodel hello wilt, selecteert u klassieke artikel van Hallo vervolgkeuzelijst te volgen:

> [!div class="op_single_selector"]
> * [PowerShell - Klassiek](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Over geforceerde tunneling

Hallo volgende diagram illustreert hoe geforceerde tunneling werkt. 

![Geforceerde tunneling](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Hallo Frontend-subnet wordt niet geforceerd via een tunnel Hallo bovenstaande voorbeeld. Hallo werkbelastingen in Hallo Frontend subnet kunnen blijven tooaccept en toocustomer aanvragen rechtstreeks van Internet Hallo reageren. Hallo middelste laag en back-end subnetten worden gedwongen via een tunnel. Alle uitgaande verbindingen van deze twee subnetten toohello Internet worden geforceerd of omgeleide terug tooan lokale site via een S2S-VPN-tunnels Hallo.

Hiermee kunt u toorestrict en inspecteren van toegang tot Internet vanaf uw virtuele machines of cloudservices in Azure, maar blijft tooenable uw service met meerdere lagen architectuur die is vereist. Als er geen internetverbinding werkbelastingen in uw virtuele netwerken, kunt u ook geforceerde tunneling toohello volledige virtuele netwerken toepassen.

## <a name="requirements-and-considerations"></a>Vereisten en overwegingen

Geforceerde tunneling in Azure wordt geconfigureerd via het virtuele netwerk zelfgedefinieerde routes. Omleiden van verkeer tooan lokale site wordt uitgedrukt als een standaardroute toohello Azure VPN-gateway. Zie voor meer informatie over de gebruiker gedefinieerde Routering en virtuele netwerken, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).

* Elk virtueel netwerksubnet heeft een ingebouwd systeem-routeringstabel. Hallo system routeringstabel heeft Hallo volgende drie groepen van routes:
  
  * **Lokale VNet routes:** rechtstreeks toohello bestemming virtuele machines in Hallo hetzelfde virtuele netwerk.
  * **Lokale routes:** toohello Azure VPN-gateway.
  * **Standaardroute:** rechtstreeks toohello Internet. Pakketten die bestemd zijn toohello privé IP-adressen niet wordt gedekt door de vorige twee Hallo routes worden verwijderd.
* Deze procedure maakt gebruik van de gebruiker gedefinieerde routes (UDR) toocreate een routering tabel tooadd een standaardroute en koppel deze Hallo routering tabel tooyour VNet subnetten tooenable geforceerde tunneling op deze subnetten.
* Geforceerde tunneling moet worden gekoppeld aan een VNet met een op route gebaseerde VPN-gateway. U moet tooset "standaardsite" tussen Hallo cross-premises lokale sites verbonden toohello virtueel netwerk. Bovendien Hallo lokale VPN-apparaat moet worden geconfigureerd met 0.0.0.0/0 als verkeer selectoren. 
* ExpressRoute geforceerde tunneling via dit mechanisme niet is geconfigureerd, maar in plaats daarvan wordt ingeschakeld door kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies. Zie voor meer informatie, Hallo [ExpressRoute-documentatie](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Configuratie-overzicht

Hallo na procedure kunt u een resourcegroep en een VNet maken. Vervolgens moet u een VPN-gateway maken en geforceerde tunneling configureren. In deze procedure Hallo virtueel netwerk MultiTier-VNet drie subnetten heeft: 'Frontend', 'Midtier' en 'Back-end' met vier cross-premises verbindingen: 'DefaultSiteHQ' en drie vertakkingen.

procedurestappen Hallo Hallo 'DefaultSiteHQ' niet instellen omdat Hallo standaard site-verbinding voor geforceerde tunneling en Hallo 'Midtier' en 'Back-end' subnetten toouse geforceerde tunneling configureren.

## <a name="before-you-begin"></a>Voordat u begint

Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.

### <a name="toolog-in"></a>toolog in

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>Geforceerde tunneling configureren

1. Maak een resourcegroep.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Een virtueel netwerk maken en geef de subnetten.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Hallo lokale netwerkgateways maken.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Hallo route tabel en route-regel maken.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Hallo route tabel toohello Midtier en back-end subnetten koppelen.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Hallo Gateway met een standaard-site maken. Deze stap duurt enige tijd toocomplete, soms 45 minuten of langer, omdat u momenteel maakt en Hallo gateway configureert.<br> Hallo **- GatewayDefaultSite** Hallo cmdlet-parameter waarmee Hallo gedwongen routering configuratie toowork, dus nemen voorzichtig tooconfigure deze instelling correct is. Deze parameter is beschikbaar in PowerShell 1.0 of hoger.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Tot stand brengen Hallo Site-naar-Site VPN-verbindingen.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```