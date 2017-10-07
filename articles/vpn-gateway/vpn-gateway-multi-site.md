---
title: 'Verbinding maken met een virtueel netwerk toomultiple sites met behulp van VPN-Gateway en PowerShell: klassieke | Microsoft Docs'
description: In dit artikel begeleidt u stapsgewijs door meerdere lokale on-premises sites tooa virtueel netwerk met behulp van een VPN-Gateway voor het klassieke implementatiemodel Hallo verbinding te maken.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Toevoegen van een Site-naar-Site-verbinding tooa VNet met een bestaande VPN-gatewayverbinding (klassiek)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klassiek)](vpn-gateway-multi-site.md)
>
>

Dit artikel begeleidt u bij het gebruik van PowerShell tooadd Site-naar-Site (S2S)-verbindingen tooa VPN-gateway met een bestaande verbinding. Dit type verbinding is vaak waarnaar wordt verwezen tooas een 'multi-site'-configuratie. Hallo stappen in dit artikel van toepassing toovirtual netwerken die zijn gemaakt met Hallo klassieke implementatiemodel (ook wel bekend als Service Management). Deze stappen zijn niet van toepassing tooExpressRoute/Site-naar-Site naast elkaar bestaande verbinding configuraties.

### <a name="deployment-models-and-methods"></a>Implementatiemodellen en -methoden

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Deze tabel wordt bijgewerkt als er nieuwe artikelen en aanvullende hulpprogramma's beschikbaar zijn voor deze configuratie. Wanneer een artikel beschikbaar is, koppelen we rechtstreeks tooit uit deze tabel.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Over het aansluiten van

U kunt meerdere on-premises sites tooa één virtueel netwerk verbinden. Dit is vooral aantrekkelijke voor het bouwen van oplossingen voor hybride cloud. Maken van een gateway met multi-site-verbinding tooyour virtuele Azure-netwerk is vergelijkbaar toocreating andere Site-naar-Site-verbindingen. In feite kunt u een bestaande Azure VPN-gateway, zolang het Hallo-gateway is dynamische (op route gebaseerd).

Als u al een statische gateway verbonden tooyour virtueel netwerk hebt, kunt u Hallo gateway type toodynamic wijzigen zonder toorebuild Hallo virtueel netwerk in volgorde tooaccommodate meerdere locaties. Voordat u Hallo routeringstype wijzigt, zorg dat uw on-premises VPN-gateway ondersteuning biedt voor op route gebaseerde VPN-configuraties.

![Multi-site-diagram](./media/vpn-gateway-multi-site/multisite.png "meerdere locaties")

## <a name="points-tooconsider"></a>Punten tooconsider

**U kunt toouse Hallo portal toomake wijzigingen toothis virtueel netwerk niet.** U moet toomake wijzigingen toohello netwerk-configuratiebestand in plaats van met Hallo-portal. Als u wijzigingen in Hallo-portal aanbrengt, worden ze uw documentatie over de meerdere site-instellingen voor dit virtuele netwerk hebt overschreven.

U moet vertrouwd Hallo netwerk-configuratiebestand gebruiken door Hallo tijd inschrijvingen Hallo multi-site procedure. Echter, als er meerdere personen op uw netwerkconfiguratie werkt, moet u ervoor dat iedereen op de hoogte van deze beperking toomake. Dit betekent niet dat u de portal Hallo helemaal niet gebruiken. U kunt deze gebruiken voor alle andere behalve configuratie wijzigingen toothis bepaald virtueel netwerk maken.

## <a name="before-you-begin"></a>Voordat u begint

Voordat u begint met de configuratie, Controleer of u de volgende Hallo:

* Compatibele VPN-hardware voor elke lokale locatie. Controleer [over VPN-apparaten voor verbinding met het virtuele netwerk](vpn-gateway-about-vpn-devices.md) tooverify als Hallo-apparaat dat u wilt dat toouse iets waarvan bekend toobe compatibel is.
* Een extern gericht openbaar IPv4-IP-adres voor elke VPN-apparaat. Hallo IP-adres kan zich niet achter een NAT bevinden. Dit is vereiste.
* U moet tooinstall Hallo meest recente versie van hello Azure PowerShell-cmdlets. Zorg ervoor dat u Hallo Service Management (SM) versie in toevoeging toohello Resource Manager-versie installeert. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.
* Iemand die wordt getoond hoe u goed configureren van uw VPN-hardware. Hebt u toohave een sterke begrijpt hoe tooconfigure uw VPN-apparaat of werk met iemand die biedt.
* Hallo IP-adresbereiken dat u toouse voor het virtuele netwerk wilt (als u dit nog niet hebt gemaakt).
* Hallo IP-adresbereiken voor elk Hallo lokale netwerksites die u een verbinding met maken hebt. U moet toomake ervoor dat Hallo IP-voor elk van de lokale netwerksites Hallo adresbereiken dat u wilt dat tooconnect toodo niet overlappen. Anders weigert Hallo portal of REST-API Hallo Hallo-configuratie die u wilt uploaden.<br>Bijvoorbeeld, als er twee lokale netwerksites dat beide Hallo IP-adresbereik 10.2.3.0/24 bevatten en u een pakket met een doeladres 10.2.3.3 hebt, wouldn't Azure weten welke site die u wilt dat toosend Hallo pakket toobecause Hallo-adresbereiken zijn overlappende. problemen met tooprevent routing, Azure is niet toegestaan tooupload een configuratiebestand met overlappende bereiken.

## <a name="1-create-a-site-to-site-vpn"></a>1. Een Site-naar-Site VPN-verbinding maken
Als u al een Site-naar-Site VPN met een gateway voor dynamische routering geweldig! U kunt verdergaan te[Hallo virtueel netwerk configuratie-instellingen exporteren](#export). Als dat niet Hallo te volgen:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Als u al een virtueel netwerk van de Site-naar-Site hebt, maar een statische routering (op beleid gebaseerd)-gateway heeft:
1. Wijzig uw gateway type toodynamic routering. Een VPN voor meerdere locaties is een (ook wel bekend als op route gebaseerd) gateway voor dynamische routering vereist. toochange uw gateway typt, maar u zult toofirst verwijderen Hallo bestaande gateway nodig en vervolgens een nieuwe maken. Zie voor instructies [hoe toochange routering VPN-type voor uw gateway Hallo](vpn-gateway-configure-vpn-gateway-mp.md).  
2. De nieuwe gateway configureren en uw VPN-tunnel maken. Zie voor instructies [een VPN-Gateway configureren in de klassieke Azure-Portal Hallo](vpn-gateway-configure-vpn-gateway-mp.md). Wijzig eerst uw gateway type toodynamic routering.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Als u geen Site-naar-Site virtueel netwerk hebt:
1. Uw Site-naar-Site virtueel netwerk maken met deze instructies: [een virtueel netwerk maken met een Site-naar-Site VPN-verbinding in de klassieke Azure-Portal Hallo](vpn-gateway-site-to-site-create.md).  
2. Configureren van een gateway voor dynamische routering met behulp van deze instructies: [configureren van een VPN-Gateway](vpn-gateway-configure-vpn-gateway-mp.md). Ervoor tooselect worden **dynamische routering** voor uw Gatewaytype.

## <a name="export"></a>2. Hallo netwerk configuratiebestand exporteren
Exporteer het bestand met de Azure-netwerk door het uitvoeren van de volgende opdracht Hallo. U kunt Hallo-locatie van Hallo tooexport tooa verschillende bestandslocatie indien nodig wijzigen.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Open Hallo netwerk-configuratiebestand
Configuratiebestand van het Hallo-netwerk dat u hebt gedownload in de laatste stap Hallo openen. Een xml-editor die u wilt gebruiken. Hallo-bestand ziet er vergelijkbare toohello volgende:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Verwijzingen naar meerdere toevoegen
Wanneer u toevoegen of verwijderen van de referentie-informatie voor site, zult u configuratiewijzigingen aanbrengt toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Een nieuwe lokale siteverwijzing toevoegen activeert Azure toocreate een nieuwe tunnel. In onderstaande Hallo voorbeeld is Hallo netwerkconfiguratie voor een enkele site-verbinding. Hallo-bestand opslaan nadat u uw wijzigingen hebt aangebracht.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd aanvullende verwijzingen naar websites (een configuratie met meerdere sites maken), toevoegen gewoon 'LocalNetworkSiteRef' extra regels, zoals weergegeven in Hallo voorbeeld hieronder:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Importbestand Hallo netwerk configuratie
Hallo netwerk-configuratiebestand importeren. Als u dit bestand met de Hallo wijzigingen importeert, worden nieuwe tunnels Hallo wordt toegevoegd. Hallo-tunnels gebruikt Hallo dynamische gateway die u eerder hebt gemaakt. U kunt ofwel Hallo klassieke portal of PowerShell tooimport Hallo-bestand.

## <a name="6-download-keys"></a>6. Downloaden van sleutels
Als uw nieuwe tunnels zijn toegevoegd, moet u Hallo PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Hallo IPsec/IKE vooraf gedeelde sleutels gebruiken voor elke tunnel.

Bijvoorbeeld:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

Als u liever, kunt u ook hello gebruiken *ophalen Virtual Network Gateway gedeelde sleutel* REST-API tooget Hallo vooraf gedeelde sleutels.

## <a name="7-verify-your-connections"></a>7. Controleer uw verbindingen
Controleer de status van Hallo tunnel voor meerdere locaties. Na het downloaden van Hallo sleutels voor elke tunnel, moet u tooverify verbindingen. Gebruik 'Get-AzureVnetConnection' tooget een lijst van het virtuele netwerk tunnels, zoals getoond in Hallo in het volgende voorbeeld. VNet1 is de naam Hallo Hallo VNet.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Voorbeeld geretourneerd:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over VPN-Gateways, Zie [over VPN-Gateways](vpn-gateway-about-vpngateways.md).
