---
title: 'Configureer geforceerde tunneling voor Azure Site-naar-Site-verbindingen: klassieke | Microsoft Docs'
description: Hoe tooredirect of 'force' alle Internet bestemd verkeer back tooyour een on-premises locatie.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configureer geforceerde tunneling met behulp van het klassieke implementatiemodel Hallo

Geforceerde tunneling, kunt u omleiden of 'force' alle Internet bestemd verkeer back tooyour on-premises locatie via een Site-naar-Site VPN-tunnel voor inspectie en controle. Dit is een kritieke beveiligingsvereiste voor de meeste bedrijven beleidsregels. Zonder geforceerde tunneling wordt internetverkeer van uw virtuele machines in Azure altijd passeren van Azure netwerkinfrastructuur rechtstreeks uit toohello Internet, zonder Hallo optie tooallow u tooinspect of audit Hallo-verkeer. Niet-geautoriseerde toegang tot het Internet kan mogelijk leiden tooinformation openbaarmaking of andere typen schendingen van de beveiliging.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

In dit artikel begeleidt u bij het configureren geforceerde tunneling voor virtuele netwerken die zijn gemaakt met het klassieke implementatiemodel Hallo. Geforceerde tunneling kan worden geconfigureerd met behulp van PowerShell, niet via het Hallo-portal. Als u tooconfigure geforceerde tunneling Hallo Resource Manager-implementatiemodel wilt, selecteert u klassieke artikel van Hallo vervolgkeuzelijst te volgen:

> [!div class="op_single_selector"]
> * [PowerShell - Klassiek](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Resource Manager](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Vereisten en overwegingen
Geforceerde tunneling in Azure wordt geconfigureerd via het virtuele netwerk zelfgedefinieerde routes (UDR). Omleiden van verkeer tooan lokale site wordt uitgedrukt als een standaardroute toohello Azure VPN-gateway. Hallo volgende sectie vindt u Hallo beperking van het Hallo-routeringstabel en -routes voor een virtuele Azure-netwerk:

* Elk virtueel netwerksubnet heeft een ingebouwd systeem-routeringstabel. Hallo system routeringstabel heeft Hallo volgende drie groepen van routes:

  * **Lokale VNet routes:** rechtstreeks toohello bestemming virtuele machines in Hallo hetzelfde virtuele netwerk.
  * **Lokale routes:** toohello Azure VPN-gateway.
  * **Standaardroute:** rechtstreeks toohello Internet. Pakketten die bestemd zijn toohello privé IP-adressen niet wordt gedekt door de vorige twee Hallo routes worden verwijderd.
* U kunt met Hallo-release van de gebruiker gedefinieerde routes, een routering tabel tooadd een standaardroute maken en vervolgens koppelen Hallo routering tabel tooyour VNet subnetten tooenable geforceerde tunneling op deze subnetten.
* U moet tooset "standaardsite" tussen Hallo cross-premises lokale sites verbonden toohello virtueel netwerk.
* Geforceerde tunneling moet worden gekoppeld aan een VNet met een VPN-gateway voor dynamische routering (geen statische gateway genoemd).
* ExpressRoute geforceerde tunneling via dit mechanisme niet is geconfigureerd, maar in plaats daarvan wordt ingeschakeld door kondigt een standaardroute via ExpressRoute BGP Hallo peeringsessies. Zie Hallo [ExpressRoute-documentatie](https://azure.microsoft.com/documentation/services/expressroute/) voor meer informatie.

## <a name="configuration-overview"></a>Configuratie-overzicht
In de Hallo voorbeeld te volgen, tunneled Hallo Frontend subnet wordt niet geforceerd. Hallo werkbelastingen in Hallo Frontend subnet kunnen blijven tooaccept en toocustomer aanvragen rechtstreeks van Internet Hallo reageren. Hallo middelste laag en back-end subnetten worden gedwongen via een tunnel. Alle uitgaande verbindingen van deze twee subnetten toohello Internet worden geforceerd of omgeleide terug tooan lokale site via een S2S-VPN-tunnels Hallo.

Hiermee kunt u toorestrict en inspecteren van toegang tot Internet vanaf uw virtuele machines of cloudservices in Azure, maar blijft tooenable uw service met meerdere lagen architectuur die is vereist. U kunt ook geforceerde tunneling toohello volledige virtuele netwerken toepassen als er geen internetverbinding werkbelastingen in uw virtuele netwerken.

![Geforceerde tunneling](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Voordat u begint
Controleer of u Hallo volgende voordat de begin-configuratie-items.

* Een Azure-abonnement. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial/).
* Een geconfigureerde virtueel netwerk. 
* Hallo meest recente versie van hello Azure PowerShell-cmdlets. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over het installeren van Hallo PowerShell-cmdlets.

## <a name="configure-forced-tunneling"></a>Geforceerde tunneling configureren
Hallo na procedure kunt u opgeven geforceerde tunneling voor een virtueel netwerk. Hallo configuratiestappen overeen toohello VNet netwerk configuratiebestand.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

In dit voorbeeld Hallo virtueel netwerk MultiTier-VNet drie subnetten heeft: 'Frontend', 'Midtier' en 'Back-end' subnetten, met vier cross-premises verbindingen: 'DefaultSiteHQ' en drie vertakkingen. 

Hallo stappen Hallo 'DefaultSiteHQ' ingesteld als Hallo standaard site-verbinding voor geforceerde tunneling, en Hallo Midtier en back-end subnetten toouse geforceerde tunneling configureren.

1. Maak een routeringstabel. Hallo cmdlet toocreate na de routetabel gebruiken.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Een standaardrouteringstabel route toohello toevoegen. 

  Hallo wordt volgende voorbeeld een route toohello standaardrouteringstabel gemaakt in stap 1. Merk op dat alleen route ondersteund Hallo is Hallo voorvoegsel voor bestemming van '0.0.0.0/0' toohello 'VPNGateway' NextHop.

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Hallo routering tabel toohello subnetten koppelen. 

  Nadat een routeringstabel is gemaakt en een route is toegevoegd, na voorbeeld tooadd hello gebruiken of Hallo route tabel tooa VNet subnet koppelen. Hallo voorbeeld voegt Hallo route tabel 'MyRouteTable' toohello Midtier en back-end-subnetten van VNet MultiTier-VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Wijs een standaardlocatie voor geforceerde tunneling. 

  In Hallo vóór stap, Hallo cmdlet voorbeeldscripts Hallo routeringstabel gemaakt en gekoppeld Hallo route tabel tootwo hello VNet subnetten. Hallo resterende stap is tooselect een lokale site tussen Hallo meerdere site-verbindingen van het virtuele netwerk Hallo als Hallo standaardsite of -tunnel.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Aanvullende PowerShell-cmdlets
### <a name="toodelete-a-route-table"></a>een routetabel toodelete

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>een routetabel toolist

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>een route van een routetabel toodelete

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove een route van een subnet

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>toolist Hallo-routetabel die zijn gekoppeld aan een subnet

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>tooremove een standaard-site van een VNet VPN-gateway

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```