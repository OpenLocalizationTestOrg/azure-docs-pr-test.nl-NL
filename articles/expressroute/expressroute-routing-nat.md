---
title: NAT voor Azure ExpressRoute | Microsoft Docs
description: Deze pagina bevat gedetailleerde vereisten voor het configureren en beheren van routering voor ExpressRoute-circuits.
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>NAT voor ExpressRoute

tooconnect tooMicrosoft cloudservices met ExpressRoute, hebt u nodig hebt tooset en routing beheert. Sommige connectiviteitsproviders bieden het instellen en beheren van routering aan als een beheerde service. Neem contact op met uw provider connectiviteit toosee als ze deze service aanbiedt. Zo niet, moet u toohello volgens de vereisten voldoen. 

Raadpleeg toohello [Circuits en Routeringsdomeinen](expressroute-circuit-peerings.md) artikel voor een beschrijving van het Hallo routering sessies die toobe moeten instellen in de toofacilitate verbinding.

> [!NOTE]
> Microsoft biedt geen ondersteuning voor routerredundantieprotocollen (zoals HSRP, VRRP) voor de configuratie van hoge beschikbaarheid. We zijn afhankelijk van twee redundante BGP-sessies per peering voor maximale beschikbaarheid.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>IP-adressen die worden gebruikt voor peerings

U moet enkele blokken van IP-adres tooreserve adressen tooconfigure routering tussen uw netwerk en routers van Microsoft Enterprise-rand (msee's). Deze sectie bevat een lijst met vereisten en beschrijft Hallo regels met betrekking tot hoe deze IP-adressen moeten worden aangeschaft en gebruikt.

### <a name="ip-addresses-used-for-azure-private-peering"></a>IP-adressen die worden gebruikt voor persoonlijke Azure-peering

U kunt privé IP-adressen of openbare IP-adressen tooconfigure hello peerings gebruiken. Hallo adresbereik dat wordt gebruikt voor het configureren van routes mogen elkaar niet overlappen met adres adresbereiken gebruikt toocreate virtuele netwerken in Azure. 

* U moet een /29-subnet of twee /30-subnetten voor routeringsinterfaces reserveren.
* Hallo subnetten voor routering kunnen privé IP-adressen of openbare IP-adressen worden.
* Hallo subnetten moeten niet in conflict met gereserveerd door de klant voor gebruik in de Microsoft-cloud Hallo HALLO hallo-bereik.
* Als een /29-subnet wordt gebruikt, wordt dit verdeeld in twee /30-subnetten. 
  * Hallo eerst/30-subnet wordt gebruikt voor de primaire koppeling Hallo en tweede /30 Hallo subnet wordt gebruikt voor de secundaire koppeling Hallo.
  * Voor elk Hallo /30 subnetten, moet u het eerste IP-adres Hallo van Hallo /30 subnet op uw router. Microsoft gebruikt het tweede IP-adres Hallo van Hallo /30 subnet tooset van een BGP-sessie.
  * U moet beide BGP-sessies instellen onze [beschikbaarheids-SLA](https://azure.microsoft.com/support/legal/sla/) toobe is ongeldig.  

#### <a name="example-for-private-peering"></a>Voorbeeld voor persoonlijke peering

Als u toouse a.b.c.d/29 tooset up Hallo peering kiest, wordt dit verdeeld in twee/30-subnetten. In Hallo onderstaand voorbeeld kijken we hoe Hallo a.b.c.d/29 subnet wordt gebruikt. 

a.b.c.d/29 wordt gesplitst tooa.b.c.d/30 en a.b.c.d+4/30 en tooMicrosoft via Hallo inrichting-API's doorgegeven. U gaat a.b.c.d+1 gebruiken als Hallo VRF IP voor Hallo primaire PE en Microsoft gaat a.b.c.d+2 gebruiken als de VRF IP voor Hallo Hallo primaire MSEE. U gaat a.b.c.d+5 gebruiken als hello VRF IP voor hello secundaire PE en Microsoft gaat a.b.c.d+6 gebruiken als de VRF IP voor Hallo Hallo secundaire MSEE.

U kunt een aanvraag waarin u 192.168.100.128/29 tooset up persoonlijke peering selecteren. 192.168.100.128/29 bevat adressen van 192.168.100.128 too192.168.100.135, waaronder:

* 192.168.100.128/30 wordt toolink1, waarbij de provider 192.168.100.129 gebruikt en Microsoft 192.168.100.130 toegewezen.
* 192.168.100.132/30 wordt toolink2, waarbij provider 192.168.100.133 gebruikt en Microsoft 192.168.100.134 toegewezen.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>IP-adressen die worden gebruikt voor openbare Azure-peering en Microsoft-peering

Openbare IP-adressen waarvan u eigenaar moet u gebruiken voor het instellen van Hallo BGP-sessies. Microsoft moet kunnen tooverify Hallo eigendom van Hallo IP-adressen via Routing Internet Registries en Internet Routing Registries. 

* Moet u een uniek/29-subnet of twee/30-subnetten tooset up Hallo BGP-peering voor elke peering per ExpressRoute-circuit (als u meer dan één hebt). 
* Als een /29-subnet wordt gebruikt, wordt dit verdeeld in twee /30-subnetten. 
  * Hallo eerst/30-subnet wordt gebruikt voor de primaire koppeling Hallo en tweede /30 Hallo subnet wordt gebruikt voor de secundaire koppeling Hallo.
  * Voor elk Hallo /30 subnetten, moet u het eerste IP-adres Hallo van Hallo /30 subnet op uw router. Microsoft gebruikt het tweede IP-adres Hallo van Hallo /30 subnet tooset van een BGP-sessie.
  * U moet beide BGP-sessies instellen onze [beschikbaarheids-SLA](https://azure.microsoft.com/support/legal/sla/) toobe is ongeldig.

## <a name="public-ip-address-requirement"></a>Vereiste openbaar IP-adres

### <a name="private-peering"></a>Persoonlijke peering

U kunt toouse openbaar of particulier IPv4-adressen voor persoonlijke peering. We bieden end-to-end-isolatie van uw verkeer, zodat het overlappen van adressen met andere klanten niet mogelijk is in het geval van persoonlijke peering. Deze adressen zijn niet aangekondigd tooInternet. 

### <a name="public-peering"></a>Openbare peering

Hello Azure pad voor openbare peering kunt u tooconnect tooall services die worden gehost in Azure via de openbare IP-adressen. Deze omvatten services die worden vermeld in Hallo [Veelgestelde vragen over ExpessRoute](expressroute-faqs.md) en alle services die door ISV's in Microsoft Azure worden gehost. Connectiviteit tooMicrosoft Azure services voor openbare peering wordt altijd gestart vanuit het netwerk in Hallo Microsoft-netwerk. U moet de openbare IP-adressen voor Hallo verkeer die bestemd zijn tooMicrosoft netwerk gebruiken.

### <a name="microsoft-peering"></a>Microsoft-peering

Hallo pad voor Microsoft-peering kunt u tooMicrosoft cloud-services die worden niet ondersteund via hello Azure pad voor openbare peering verbinding te maken. Hallo-lijst met services bevat Office 365-services, zoals Exchange Online, SharePoint Online, Skype voor bedrijven en Dynamics 365. Microsoft ondersteunt bidirectionele connectiviteit op Hallo Microsoft-peering. Verkeer dat is bestemd tooMicrosoft cloudservices moeten geldige openbare IPv4-adressen gebruiken voordat Hallo Microsoft-netwerk binnenkomt.

Zorg ervoor dat uw IP-adres en AS-nummer zijn geregistreerde tooyou in een Hallo registers hieronder vermeld.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Openbare IP-adres adressen aangekondigd tooMicrosoft via ExpressRoute mag geen aangekondigd toohello Internet. Dit kan verbreekt de connectiviteit tooother Microsoft-services. Openbare IP-adressen die worden gebruikt door servers in uw netwerk en communiceren met O365-eindpunten in Microsoft, kunnen echter wel worden geadverteerd via ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Dynamische route-uitwisseling

Routeringsuitwisseling vindt plaats via het eBGP-protocol. EBGP-sessies worden tot stand gebracht tussen Hallo msee's en uw routers. Verificatie van BGP-sessies is niet vereist. Indien nodig kan een MD5-hash worden geconfigureerd. Zie Hallo [Configure routing](expressroute-howto-routing-classic.md) en [Circuit provisioning workflows en statussen circuit](expressroute-workflows.md) voor informatie over het configureren van BGP-sessies.

## <a name="autonomous-system-numbers"></a>Autonome systeemnummers

Microsoft gebruikt AS 12076 voor persoonlijke Azure-peering, openbare Azure-peering en Microsoft-peering. We hebben ASN's gereserveerde van 65515 too65520 voor intern gebruik. Zowel 16- als 32-bits AS-getallen worden ondersteund.

Er zijn geen vereisten met betrekking tot gegevensoverdrachtsymmetrie. Hallo inkomende en uitgaande paden lopen mogelijk langs verschillende routerparen. Identieke routes moeten worden geadverteerd van beide zijden van meerdere circuitparen waarvan u eigenaar bent. Route metrische gegevens zijn niet vereist toobe identiek zijn.

## <a name="route-aggregation-and-prefix-limits"></a>Limieten voor route-aggregatie en voorvoegsel

We ondersteuning voor maximaal too4000 voorvoegsels aangekondigd toous via Hallo persoonlijke Azure-peering. Dit kan worden verhoogd van too10, 000 voorvoegsels als Hallo premium-invoegtoepassing voor ExpressRoute is ingeschakeld. We accepteren van too200 voorvoegsels per BGP-sessie voor openbare Azure- en Microsoft-peering. 

Hallo BGP-sessie wordt verwijderd als het aantal voorvoegsels Hallo Hallo overschrijdt. Standaardroutes op Hallo persoonlijke peeringkoppeling alleen geaccepteerd. Provider moet standaardroute en privé IP-adressen (RFC 1918) uit Hallo openbare Azure paden en Microsoft-peering filteren. 

## <a name="transit-routing-and-cross-region-routing"></a>Transitroutering en regio-overschrijdende routering

ExpressRoute kan niet worden geconfigureerd als transitrouter. Hebt u toorely op uw connectiviteitsprovider voor transitrouteringsservices.

## <a name="advertising-default-routes"></a>Standaardroutes adverteren

Standaardroutes zijn alleen toegestaan voor persoonlijke Azure-peeringsessies. In dat geval wordt er al het verkeer van Hallo gekoppelde virtuele netwerken tooyour netwerk routeren. Wanneer standaardroutes worden geadverteerd naar persoonlijke peering leidt tot Hallo internetpad vanuit Azure geblokkeerd. U moet zijn afhankelijk van uw bedrijfsfunctionaliteit tooroute verkeer van en toohello internet voor services die worden gehost in Azure. 

 tooenable connectiviteit tooother Azure services en infrastructuurservices, moet u ervoor zorgen dat een van de volgende items Hallo is geïmplementeerd:

* Openbare Azure-peering is ingeschakeld tooroute verkeer toopublic eindpunten
* Gebruiker gedefinieerde routering tooallow verbinding met internet wordt gebruikt voor elk subnet vereisen internetverbinding.

> [!NOTE]
> Wanneer standaardroutes worden geadverteerd, wordt de activering van Windows- en andere VM-licenties verbroken. Volg de instructies [hier](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork voorkomen.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Ondersteuning voor BGP-community's (Preview)

Deze sectie bevat een overzicht van hoe BGP-community's worden gebruikt met ExpressRoute. Microsoft adverteert routes in Hallo openbare en Microsoft-peering paden met routes zijn gemarkeerd met de juiste Communitywaarden. Hallo reden hiervoor en meer informatie over community waarden worden hieronder beschreven Hallo. Microsoft, echter niet van toepassing een community met tags tooroutes waarden tooMicrosoft aangekondigd.

Als u tooMicrosoft zijn verbonden via ExpressRoute op een locatie binnen een geopolitieke regio, hebt u toegang tooall Microsoft-cloudservices in alle regio's binnen de geopolitieke grenzen Hallo. 

Als u tooMicrosoft in Amsterdam via ExpressRoute verbonden, hebt u bijvoorbeeld toegang tooall Microsoft cloud-services die worden gehost in Noord-Europa en West-Europa. 

Raadpleeg toohello [ExpressRoute-partners en peeringlocaties](expressroute-locations.md) pagina voor een gedetailleerde lijst met geopolitieke regio's, bijbehorende Azure-regio's en bijbehorende ExpressRoute-peeringlocaties.

U kunt meer dan één ExpressRoute-circuit per geopolitieke regio aanschaffen. Hebben van meer verbindingen biedt aanzienlijke voordelen wat betreft hoge beschikbaarheid vanwege toogeo redundantie. In gevallen waarin u meerdere ExpressRoute-circuits hebt, ontvangt u van Microsoft op Hallo openbare peering en Microsoft-peering paden Hallo dezelfde set voorvoegsels zijn geadverteerd. Dat betekent dat er vanuit uw netwerk meerdere paden zijn naar Microsoft. Dit kan veroorzaken suboptimale routering beslissingen toobe die zijn aangebracht in uw netwerk. Als gevolg hiervan kunnen optreden suboptimale connectiviteit ervaringen toodifferent services. 

Microsoft voorvoegsels die worden geadverteerd via openbare peering en Microsoft-peering met de juiste BGP-Communitywaarden die aangeeft Hallo regio Hallo voorvoegsels worden gehost in. U kunt vertrouwen op Hallo community waarden toomake juiste routering beslissingen toooffer [optimale routering toocustomers](expressroute-optimize-routing.md).

| **Geopolitieke regio** | **Microsoft Azure-regio** | **BGP-communitywaarde** |
| --- | --- | --- |
| **Noord-Amerika** | | |
| VS - oost |12076:51004 | |
| VS - oost 2 |12076:51005 | |
| VS - west |12076:51006 | |
| VS - west 2 |12076:51026 | |
| West-centraal VS |12076:51027 | |
| Noord-centraal VS |12076:51007 | |
| Zuid-centraal VS |12076:51008 | |
| VS - midden |12076:51009 | |
| Canada - midden |12076:51020 | |
| Canada - oost |12076:51021 | |
| **Zuid-Amerika** | | |
| Brazilië - zuid |12076:51014 | |
| **Europa** | | |
| Noord-Europa |12076:51003 | |
| West-Europa |12076:51002 | |
| **Azië en Stille Oceaan** | | |
| Oost-Azië |12076:51010 | |
| Zuidoost-Azië |12076:51011 | |
| **Japan** | | |
| Japan - oost |12076:51012 | |
| Japan - west |12076:51013 | |
| **Australië** | | |
| Australië - oost |12076:51015 | |
| Australië - zuidoost |12076:51016 | |
| **India** | | |
| India - zuid |12076:51019 | |
| India - west |12076:51018 | |
| India - midden |12076:51017 | |

Alle routes die worden geadverteerd vanuit Microsoft worden, gemarkeerd met de juiste communitywaarde Hallo. 

> [!IMPORTANT]
> Globale voorvoegsels worden gemarkeerd met een juiste communitywaarde en worden alleen geadverteerd wanneer de Premium-invoegtoepassing voor ExpressRoute is ingeschakeld.
> 
> 

Bovendien toohello hoger, Microsoft ook voorvoegsels op basis van Hallo service waartoe ze behoren. Dit geldt alleen toohello Microsoft-peering. Hallo in de volgende tabel bevat een toewijzing van de service tooBGP community-waarde.

| **Service** | **BGP-communitywaarde** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype voor Bedrijven** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Andere Office 365-services** |12076:5100 |

> [!NOTE]
> BGP-Communitywaarden die u op Hallo routes aangekondigd tooMicrosoft instelt worden niet door door Microsoft.
> 
> 

## <a name="next-steps"></a>Volgende stappen

* Configureer uw ExpressRoute-verbinding.
  
  * [Maken van een ExpressRoute-circuit voor het klassieke implementatiemodel Hallo](expressroute-howto-circuit-classic.md) of [maken en een ExpressRoute-circuit met Azure Resource Manager wijzigen](expressroute-howto-circuit-arm.md)
  * [Routering configureren voor het klassieke implementatiemodel Hallo](expressroute-howto-routing-classic.md) of [routering configureren voor Hallo Resource Manager-implementatiemodel](expressroute-howto-routing-arm.md)
  * [Koppelen van een klassiek VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md) of [koppelen van een Resource Manager VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-arm.md)

