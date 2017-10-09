---
title: aaaAzure ExpressRoute-circuits en Routeringsdomeinen | Microsoft Docs
description: Deze pagina bevat een overzicht van ExpressRoute-circuits en Routeringsdomeinen Hallo.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>ExpressRoute-circuits en Routeringsdomeinen
 U moet bestellen een *ExpressRoute-circuit* tooconnect uw lokale infrastructuur tooMicrosoft via een connectiviteitsprovider. Hallo afbeelding hieronder biedt een logische representatie van de verbinding tussen uw WAN en Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>ExpressRoute-circuits
Een *ExpressRoute-circuit* vertegenwoordigt een logische verbinding tussen uw on-premises infrastructuur en Microsoft cloud-services via een connectiviteitsprovider. U kunt meerdere ExpressRoute-circuits bestellen. Elk circuit kan worden in dezelfde of verschillende regio's Hallo en verbonden tooyour premises via verschillende connectiviteitsproviders kunnen worden. 

ExpressRoute-circuits tooany fysieke entiteiten niet zijn toegewezen. Een circuit wordt uniek geïdentificeerd door een standaard die GUID worden aangeroepen als een servicesleutel (s-sleutel). Hallo servicesleutel is Hallo enige informatie uitgewisseld tussen Microsoft en Hallo connectiviteitsprovider. Hallo-s-sleutel is niet een geheim om beveiligingsredenen. Er is een 1:1-toewijzing tussen een ExpressRoute-circuit en Hallo s-sleutel.

Een ExpressRoute-circuit kan hebben van onafhankelijke peerings toothree: Azure openbare, Azure privé- en Microsoft. Elke peering is een combinatie van BGP onafhankelijke sessies van deze toch toe geconfigureerd voor maximale beschikbaarheid. Er is een 1: n (1 < = N < = 3) toewijzing tussen een ExpressRoute-circuit en routering van domeinen. Een ExpressRoute-circuit kan hebben een, twee of alle drie de peerings per ExpressRoute-circuit is ingeschakeld.

Elk circuit heeft een vaste bandbreedte (50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 10 Gbps) en is toegewezen tooa connectiviteitsprovider en een locatie. Hallo-bandbreedte die u selecteert worden verdeeld over alle Hallo peerings voor Hallo circuit. 

### <a name="quotas-limits-and-limitations"></a>Quota's, limieten en beperkingen
Standaardquota en limieten gelden voor elk ExpressRoute-circuit. Raadpleeg toohello [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md) pagina voor actuele informatie over quota.

## <a name="expressroute-routing-domains"></a>ExpressRoute-routeringsdomeinen
Een ExpressRoute-circuit heeft meerdere Routeringsdomeinen gekoppeld: Azure openbare, Azure privé- en Microsoft. Elk van de Routeringsdomeinen Hallo identiek is geconfigureerd op een combinatie van routers (in de actieve of loadsharing configuration) voor hoge beschikbaarheid. Azure-services zijn aangemerkt als *openbare Azure* en *Azure privé* toorepresent Hallo IP-adressering schema's.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Persoonlijke peering
Azure compute-services, namelijk virtuele machines (IaaS) en cloudservices (PaaS), die zijn geïmplementeerd in een virtueel netwerk kunnen worden verbonden via Hallo persoonlijke peering domein. Hallo persoonlijke peering domein wordt beschouwd als een vertrouwde uitbreiding van uw Basisnetwerk toobe in Microsoft Azure. U kunt instellen wanneer er bidirectionele connectiviteit tussen uw Basisnetwerk en de virtuele netwerken van Azure (vnet's). Deze peering, kunt u verbinding met toovirtual machines en cloudservices rechtstreeks op hun persoonlijke IP-adressen.  

U kunt meer dan één virtueel netwerk toohello persoonlijke peering domein verbinden. Bekijk Hallo [pagina met veelgestelde vragen](expressroute-faqs.md) voor meer informatie over limieten en beperkingen. U kunt ook bezoeken Hallo [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md) pagina voor actuele informatie over limieten.  Raadpleeg toohello [routering](expressroute-routing.md) pagina voor gedetailleerde informatie over de configuratie van de routering.

### <a name="public-peering"></a>Openbare peering
Services zoals Azure Storage, SQL-databases en Websites worden aangeboden op het openbare IP-adressen. U kunt privé tooservices gehost op openbare IP-adressen, met inbegrip van VIP's van uw cloud-services via Hallo openbare peering routeringsdomein verbinden. U kunt verbinding maken Hallo openbare peering domein tooyour DMZ en tooall Azure-services op hun openbare IP-adressen van uw WAN zonder tooconnect via internet Hallo. 

Connectiviteit wordt altijd gestart vanuit uw WAN tooMicrosoft Azure services. Microsoft Azure-services worden niet op uw netwerk via deze routeringsdomein kunnen tooinitiate aangesloten. Zodra openbare peering is ingeschakeld, kunt u zich kunt tooconnect tooall Azure services. We staan niet toe dat u tooselectively pick services waarvoor adverteren we de routes naar. U kunt bekijken Hallo lijst met voorvoegsels we tooyou adverteren via deze peering op Hallo [Microsoft Azure Datacenter IP-adresbereiken](http://www.microsoft.com/download/details.aspx?id=41653) pagina. Hallo pagina wordt wekelijks bijgewerkt.

U kunt aangepaste routefilters definiëren binnen uw tooconsume alleen Hallo netwerkroutes die u nodig hebt. Raadpleeg toohello [routering](expressroute-routing.md) pagina voor gedetailleerde informatie over de configuratie van de routering. 

Zie Hallo [pagina met veelgestelde vragen](expressroute-faqs.md) voor meer informatie over services die worden ondersteund via Hallo openbare peering routeringsdomein. 

### <a name="microsoft-peering"></a>Microsoft-peering
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Connectiviteit tooall andere Microsoft online services (zoals Office 365-services) worden via Hallo Microsoft-peering. We inschakelen bidirectionele connectiviteit tussen uw WAN- en Microsoft cloud-services via Hallo Microsoft peering routeringsdomein. U moet verbinding maken tooMicrosoft cloudservices alleen via het openbare IP-adressen die eigendom zijn van u of uw connectiviteitsprovider en moet u tooall Hallo gedefinieerd regels voldoen. Zie Hallo [vereisten voor ExpressRoute](expressroute-prerequisites.md) pagina voor meer informatie.

Zie Hallo [pagina met veelgestelde vragen](expressroute-faqs.md) voor meer informatie over services die worden ondersteund, kosten en configuratie-informatie. Zie Hallo [ExpressRoute-locaties](expressroute-locations.md) pagina voor informatie over het Hallo-lijst van connectiviteitsproviders met Microsoft ondersteuning.

## <a name="routing-domain-comparison"></a>Vergelijking van routering domein
Hallo in de volgende tabel vergelijkt Hallo drie Routeringsdomeinen.

|  | **Persoonlijke Peering** | **Openbare Peering** | **Microsoft-Peering** |
| --- | --- | --- | --- |
| **Max. # voorvoegsels per peering ondersteund** |4000 standaard 10.000 met ExpressRoute Premium |200 |200 |
| **IP-adresbereiken ondersteund** |Een geldig IPv4-adres binnen uw WAN. |Openbare IPv4-adressen die eigendom zijn van door u of uw connectiviteitsprovider. |Openbare IPv4-adressen die eigendom zijn van door u of uw connectiviteitsprovider. |
| **Als een aantal vereisten** |Persoonlijke en openbare AS-nummers. U moet de eigenaar Hallo openbare AS-nummer als u ervoor toouse een kiest. |Persoonlijke en openbare AS-nummers. U moet echter bewijzen dat eigendom van het openbare IP-adressen. |Persoonlijke en openbare AS-nummers. U moet echter bewijzen dat eigendom van het openbare IP-adressen. |
| **Routering Interface IP-adressen** |RFC1918 en openbare IP-adressen |Openbare IP-adressen geregistreerde tooyou in routeringsregisters. |Openbare IP-adressen geregistreerde tooyou in routeringsregisters. |
| **MD5-Hash-ondersteuning** |Ja |Ja |Ja |

U kunt tooenable een of meer van de Routeringsdomeinen Hallo als onderdeel van uw ExpressRoute-circuit. U kunt toohave alle Hallo Routeringsdomeinen plaatsen op Hallo van dezelfde VPN als u wilt dat toocombine bij één routeringsdomein. U kunt ze ook op andere Routeringsdomeinen, vergelijkbare toohello diagram plaatsen. Hallo aanbevolen configuratie is dat privépeering is verbonden rechtstreeks toohello Basisnetwerk en Hallo openbare en Microsoft-peering koppelingen zijn verbonden tooyour DMZ.

Als u toohave alle drie peeringsessies kiest, moet u drie paren van BGP-sessies (één paar voor elk type peering) hebben. Hallo BGP-sessie paren geeft u een maximaal beschikbare koppeling. Als u verbinding via layer 2-connectiviteitsproviders maakt, kunt u zich verantwoordelijk voor het configureren en beheren van routering. U kunt meer informatie aan de hand van Hallo [werkstromen](expressroute-workflows.md) voor het instellen van ExpressRoute.

## <a name="next-steps"></a>Volgende stappen
* Zoek een serviceprovider Zie [ExpressRoute-providers en -locaties service](expressroute-locations.md).
* Controleer of aan alle vereisten is voldaan. Zie [ExpressRoute prerequisites](expressroute-prerequisites.md) (Vereisten voor ExpressRoute).
* Configureer uw ExpressRoute-verbinding.
  * [Create and manage ExpressRoute circuits](expressroute-howto-circuit-portal-resource-manager.md) (ExpressRoute-circuits maken en beheren)
  * [Routering (peering) configureren voor ExpressRoute-circuits](expressroute-howto-routing-portal-resource-manager.md)

