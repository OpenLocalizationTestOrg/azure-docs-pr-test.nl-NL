---
title: 'Overzicht van ExpressRoute: Uw lokale netwerk tooAzure uitbreiden via een particuliere verbinding | Microsoft Docs'
description: Dit technisch overzicht van ExpressRoute wordt uitgelegd hoe een ExpressRoute-verbinding werkt tooextend uw lokale netwerk tooAzure via een particuliere verbinding.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Overzicht van ExpressRoute
Microsoft Azure ExpressRoute kunt u uw on-premises netwerken in Hallo Microsoft cloud uitbreiden via een persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider. Met ExpressRoute kunt kunt u verbindingen tooMicrosoft cloudservices, zoals Microsoft Azure, Office 365 en Dynamics 365 maken.

Via een connectiviteitsprovider in een co-locatiefaciliteit is connectiviteit mogelijk vanuit een any-to-any (IP VPN) netwerk, een point-to-point Ethernet-netwerk of een virtuele overlappende verbinding. ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. ExpressRoute-verbindingen toooffer kan dit meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo. Voor meer informatie over tooconnect de tooMicrosoft van uw netwerk met behulp van ExpressRoute, Zie [ExpressRoute connectiviteitsmodellen](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Belangrijkste voordelen

* Layer 3-connectiviteit tussen uw on-premises netwerk en Microsoft Cloud Hallo via een connectiviteitsprovider. Connectiviteit is mogelijk van een any-to-any (IPVPN) netwerk, een point-to-point Ethernet-verbinding of langs een virtuele overlappende verbinding via een Ethernet-exchange.
* Connectiviteit tooMicrosoft cloud-services tussen alle regio's in Hallo geopolitieke regio.
* Globale connectiviteit tooMicrosoft-services tussen alle regio's met premium-invoegtoepassing voor ExpressRoute.
* Dynamische routering tussen uw netwerk en Microsoft via standaardprotocollen (BGP).
* Ingebouwde redundantie op elke peeringlocatie voor hogere betrouwbaarheid.
* [SLA](https://azure.microsoft.com/support/legal/sla/) voor verbindingsbedrijfstijd.
* QoS-ondersteuning voor Skype voor Bedrijven.

Zie voor meer informatie, Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Functies

### <a name="layer-3-connectivity"></a>Laag-3-connectiviteit
Microsoft maakt gebruik van branche standard dynamische routering protocol (BGP) tooexchange van routes tussen uw on-premises netwerk, uw exemplaren in Azure en Microsoft openbare adressen.  We stellen meerdere BGP-sessies met uw netwerk in voor verschillende verkeersprofielen. Meer informatie vindt u in Hallo [ExpressRoute-circuit en -Routeringsdomeinen](expressroute-circuit-peerings.md) artikel.

### <a name="redundancy"></a>Redundantie
Elk ExpressRoute-circuit bestaat uit twee verbindingen tootwo Microsoft Enterprise-randrouters (msee's) van Hallo connectiviteitsprovider / uw netwerkrand. Microsoft vereist een dubbele BGP-verbinding van Hallo connectiviteitsprovider / uw kant één tooeach MSEE. U kunt ervoor kiezen geen toodeploy redundante apparaten / Ethernet-circuits aan uw kant. Connectiviteitsproviders gebruiken redundante apparaten tooensure die uw verbindingen op een redundante manier tooMicrosoft worden doorgegeven. Een redundante laag-3-connectiviteit is geconfigureerd, is een vereiste voor onze [SLA](https://azure.microsoft.com/support/legal/sla/) toobe is ongeldig.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Connectiviteit tooMicrosoft cloudservices
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

ExpressRoute-verbindingen inschakelen toegang toohello volgende services:

* Microsoft Azure-services
* Microsoft Office 365-services
* Microsoft Dynamics 365

U kunt ook bezoeken Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md) pagina voor een gedetailleerde lijst met services die via ExpressRoute worden ondersteund.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Connectiviteit tooall regio's binnen een geopolitieke regio
U kunt verbinding maken tooMicrosoft in een van onze [peeringlocaties](expressroute-locations.md) en hebben toegang tot tooall regio's binnen de geopolitieke regio Hallo. 

Bijvoorbeeld, als u tooMicrosoft in Amsterdam via ExpressRoute verbonden, hebt u toegang tooall Microsoft cloud-services die worden gehost in Noord-Europa en West-Europa. Zie Hallo [ExpressRoute-partners en peeringlocaties](expressroute-locations.md) artikel voor een overzicht van Hallo geopolitieke regio's, bijbehorende Microsoft cloud-regio en bijbehorende ExpressRoute-peeringlocaties.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Globale connectiviteit met de Premium-invoegtoepassing voor ExpressRoute
U kunt Hallo ExpressRoute premium-invoegtoepassing voor functie tooextend connectiviteit inschakelen buiten de geopolitieke grenzen. Bijvoorbeeld, als u verbonden tooMicrosoft in Amsterdam via ExpressRoute bent, hebt u toegang tooall Microsoft-cloudservices in alle regio's wordt gehost op Hallo wereld (uitgezonderd nationale clouds). U kunt toegang tot services die zijn geïmplementeerd in Zuid-Amerika of Australië Hallo dezelfde manier als u toegang tot Hallo Noord en West-Europa regio's.

### <a name="rich-connectivity-partner-ecosystem"></a>Uitgebreid connectiviteitsecosysteem van partners
ExpressRoute heeft een voortdurend groeiend ecosysteem van connectiviteitsproviders en SI-partners. U kunt verwijzen toohello [ExpressRoute-providers en -locaties](expressroute-locations.md) artikel voor Hallo meest recente informatie.

### <a name="connectivity-toonational-clouds"></a>Connectiviteit toonational clouds
Microsoft stuurt geïsoleerde cloudomgevingen aan voor speciale geopolitieke regio's en klantsegmenten. Raadpleeg toohello [ExpressRoute-providers en -locaties](expressroute-locations.md) pagina voor een lijst van nationale clouds en providers.

### <a name="bandwidth-options"></a>Bandbreedte-opties
U kunt ExpressRoute-circuits aanschaffen voor een breed scala aan bandbreedten. Hieronder vindt u een lijst van ondersteunde bandbreedten. Ervoor toocheck worden met de connectiviteit provider toodetermine Hallo lijst met ondersteunde bandbreedten.

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>Dynamische schaling van bandbreedte
U kunt Hallo ExpressRoute circuit bandbreedte (best effort op basis van een) vergroten zonder tootear de verbindingen. 

### <a name="flexible-billing-models"></a>Flexibele factureringsmodellen
U kunt een factureringsmodel selecteren dat voor u het meest geschikt is. Kiezen tussen de hieronder vermelde Hallo-factureringsmodellen. Zie voor meer informatie, Hallo [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

* **Onbeperkt gegevensverkeer**. Hallo ExpressRoute-circuit u betaalt maandelijks een vast bedrag en alle binnenkomende en uitgaande gegevensoverdracht is verder gratis. 
* **Naar gebruik**. Hallo ExpressRoute-circuit u betaalt maandelijks een vast bedrag. Alle binnenkomende gegevensoverdracht is gratis. Uitgaande gegevensoverdracht wordt in rekening gebracht per GB aan gegevensoverdracht. De tarieven voor gegevensoverdracht verschillen per regio.
* **Premium-invoegtoepassing voor ExpressRoute**. Hallo ExpressRoute premium is een invoegtoepassing via Hallo ExpressRoute-circuit. Hallo premium-invoegtoepassing voor ExpressRoute biedt Hallo volgende mogelijkheden: 
  * Ruimere routelimieten voor openbare en Azure persoonlijke Azure-peering van 4000 routes too10, 000 routes.
  * Globale connectiviteit voor services. Een ExpressRoute-circuit dat is gemaakt in een willekeurige regio (met uitzondering van nationale clouds) hebt in elke andere regio ter wereld Hallo tooresources toegang. Zo is een virtueel netwerk, gemaakt in West-Europa, toegankelijk via een ExpressRoute-circuit dat is ingericht in Silicon Valley.
  * Verbeterde aantal VNet-koppelingen per ExpressRoute-circuit van 10 tooa hogere limiet, afhankelijk van de bandbreedte van het circuit Hallo Hallo.

## <a name="faq"></a>Veelgestelde vragen

Zie voor veelgestelde vragen over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over [ExpressRoute-connectiviteitsmodellen](expressroute-connectivity-models.md).
* Meer informatie over ExpressRoute-verbindingen en -routeringsdomeinen. Zie [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md) (ExpressRoute-circuits en -routeringsdomeinen).
* Zoek een serviceprovider Zie [ExpressRoute partners and peering locations](expressroute-locations.md) (ExpressRoute-partners en -peeringlocaties).
* Controleer of aan alle vereisten is voldaan. Zie [ExpressRoute prerequisites](expressroute-prerequisites.md) (Vereisten voor ExpressRoute).
* Raadpleeg de vereisten voor toohello [routering](expressroute-routing.md), [NAT](expressroute-nat.md), en [QoS](expressroute-qos.md).
* Configureer uw ExpressRoute-verbinding.
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-portal-resource-manager.md)
  * [Peering configureren voor een ExpressRoute-circuit](expressroute-howto-routing-portal-resource-manager.md)
  * [Verbinding maken met een virtueel netwerk tooan ExpressRoute-circuit](expressroute-howto-linkvnet-portal-resource-manager.md)
* Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.
