---
title: 'Locaties en connectiviteitsproviders: Azure ExpressRoute | Microsoft Docs'
description: In dit artikel bevat een gedetailleerd overzicht van de locaties waar services worden aangeboden en hoe tooconnect tooAzure regio's. Gesorteerd op locatie.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: 838d52701d177aa7f13e845b7bde66d07b5efed6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Partners en peeringlocaties voor ExpressRoute

> [!div class="op_single_selector"]
> * [Locaties per provider](expressroute-locations.md)
> * [Providers per locatie](expressroute-locations-providers.md)


Hallo-tabellen in dit artikel vindt informatie over ExpressRoute-connectiviteitsproviders, geografische dekking van ExpressRoute, Microsoft cloud-services die via ExpressRoute en een ExpressRoute-SI (SIs) worden ondersteund.

## <a name="partners"></a>ExpressRoute-connectiviteitsproviders
ExpressRoute wordt ondersteund in alle Azure-regio's en -locaties. Hallo volgende kaart bevat een lijst van Azure-regio's en een ExpressRoute-locaties. ExpressRoute-locaties zijn toothose waarop Microsoft met verschillende serviceproviders samenwerkt.

![Locatiekaart][0]

U hebt toegang tot tooAzure services in alle regio's binnen een geopolitieke regio als u tooat minimaal één ExpressRoute-locatie binnen de geopolitieke regio Hallo verbonden. 

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Azure-regio's tooExpressRoute locaties binnen een geopolitieke regio
Hallo volgende tabel geeft een overzicht van Azure-regio's tooExpressRoute locaties binnen een geopolitieke regio.

| **Geopolitieke regio** | **Azure-regio's** | **ExpressRoute-locaties** |
| --- | --- | --- |
| **Noord-Amerika** |VS - oost, VS - west, VS - oost 2, VS - west 2, VS - midden, Zuid-centraal VS, Noord-centraal VS, West-centraal VS, Canada Centraal, Canada Oost |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, New York, San Antonio, Seattle, Silicon Valley, Washington DC, Montreal, Quebec City, Toronto |
| **Zuid-Amerika** |Brazilië - zuid |Sao Paulo |
| **Europa** |Noord-Europa, West-Europa, Verenigd Koninkrijk - west, Verenigd Koninkrijk - zuid |Amsterdam, Dublin, Londen, Newport (Wales), Parijs |
| **Azië** |Oost-Azië, Zuidoost-Azië |Hongkong, Singapore |
| **Japan** |Japan - west, Japan - oost |Osaka, Tokio |
| **Australië** |Australië - zuidoost, Australië - oost |Melbourne, Sydney |
| **India** |India - west, India - midden, India - zuid |Chennai, Mumbai |
| **Zuid-Korea** |Korea Centraal, Korea Zuid |Busan, Seoul |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Regio's en geopolitieke grenzen voor nationale clouds
Hallo in de volgende tabel bevat informatie over regio's en geopolitieke grenzen voor nationale clouds.

| **Geopolitieke regio** | **Azure-regio's** | **ExpressRoute-locaties** |
| --- | --- | --- |
| **Cloud van de Amerikaanse overheid** |VS (overheid) - Iowa , VS (overheid) - Virginia, US DoD - centraal, US DoD - oost  |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **China** |China Noord, China Oost |Beijing, Shanghai |
| **Duitsland** |Duitsland Centraal, Duitsland Oost |Berlijn, Frankfurt |

Connectiviteit tussen de geopolitieke regio's wordt niet ondersteund op Hallo standaard ExpressRoute-SKU. U moet tooenable hello ExpressRoute premium-invoegtoepassing toosupport globale connectiviteit. Connectiviteit toonational cloudomgevingen wordt niet ondersteund. U kunt met uw connectiviteitsprovider samenwerken als de noodzaak daartoe zich voordoet.

## <a name="locations"></a>Locaties van connectiviteitsproviders

Hallo volgende tabel toont connectiviteit locaties en Hallo serviceproviders voor elke locatie. Als u wilt tooview-providers en Hallo locaties waarvoor deze services kunnen bieden, Zie [locaties door serviceprovider](expressroute-locations.md#locations). 


### <a name="production-azure"></a>Productie-Azure
| **Locatie** | **Serviceproviders** |
| --- | --- |
| **Amsterdam** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, euNetworks, GÉANT, InterCloud, Internet Solutions - Cloud Connect, Interxion, KPN, Level 3 Communications, Megaport, Orange, Tata Communications, TeleCity Group, Telefonica, Telenor, Verizon, Zayo Group |
| **Atlanta** |Equinix |
| **Busan** |LG CNS |
| **Chennai** | Airtel+, Global CloudXchange (GCX), SIFY, Tata Communications |
| **Chicago** |AT&T NetBond, Comcast, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group |
| **Dallas** |Aryaka Networks, AT&T NetBond, Cologix, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group+ |
| **Denver** |CoreSite |
| **Dublin** |Colt, Interxion, Telecity Group |
| **Hongkong** |Aryaka Networks, British Telecom, China Telecom Global, Equinix, Megaport, Orange, PCCW Global Limited, Tata Communications, Verizon |
| **Las Vegas** |Level 3 Communications, Megaport |
| **Londen** |AT&T NetBond, British Telecom, Colt, Equinix, InterCloud, Internet Solutions - Cloud Connect, Interxion, Jisc, Level 3 Communications, Megaport, MTN, NTT Communications, Orange, Tata Communications, Telecity Group, Telehouse - KDDI, Telenor, Verizon, Vodafone, Zayo Group+ |
| **Los Angeles** |CoreSite, Equinix, Megaport, NTT, Zayo Group |
| **Melbourne** |AARNet, Equinix, Megaport, NEXTDC, Telstra Corporation |
| **Miami** |C3ntro+, Megaport, Neutrona Networks |
| **Montreal** |Bell Canada, Cologix |
| **Mumbai** |Airtel+, Sify, Tata Communications |
| **New York** |Coresite, Equinix, Megaport, Zayo Group |
| **Newport (Wales)** |Next Generation Data |
| **Osaka** |Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT SmartConnect, Softbank |
| **Parijs** |Colt, Interxion, Equinix, Orange |
| **Quebec** | Megaport |
| **San Antonio** |Megaport |
| **Sao Paulo** |Ascenty Data Centers+, Equinix, Level 3 Communications, Neutrona Networks, Telefonica, UOLDIVEO |
| **Seattle** |Equinix, Level 3 Communications, Megaport |
| **Seoul** |KINX, LG CNS, Sejong Telecom |
| **Silicon Valley** |Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink+, Comcast, Console, Equinix, Level 3 Communications, Megaport, Orange, Tata Communications, Verizon, Zayo Group |
| **Singapore** |Aryaka Networks, AT&T NetBond, British Telecom, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, SingTel, Tata Communications, Verizon |
| **Sydney** |AARNet, AT&T NetBond, British Telecom, Equinix, Megaport, NEXTDC, Orange, Telstra Corporation, Verizon |
| **Tokio** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, Softbank, Verizon |
| **Toronto** |AT&T NetBond, Bell Canada, Cologix, Console, Equinix, Megaport, Telus, Zayo Group |
| **Washington DC** |Aryaka Networks, AT&T NetBond, British Telecom, Comcast, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, Tata Communications, Verizon, Zayo Group |

 **+** betekent binnenkort beschikbaar

### <a name="national-cloud-environments"></a>Nationale cloudomgevingen

### <a name="us-government-cloud"></a>Cloud van de Amerikaanse overheid
| **Locatie** | **Serviceproviders** |
| --- | --- |
| **Chicago** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |
| **Dallas** |Equinix, Megaport, Verizon |
| **New York** |Equinix, Level 3 Communications+, Verizon |
| **Silicon Valley** | Equinix, Level 3 Communications |
| **Seattle** | Equinix |
| **Washington DC** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |

### <a name="china"></a>China
| **Locatie** | **Serviceproviders** |
| --- | --- |
| **Beijing** |China Telecom |
| **Shanghai** |China Telecom |

toolearn meer, Zie [ExpressRoute in China](http://www.windowsazure.cn/home/features/expressroute/)

### <a name="germany"></a>Duitsland
| **Locatie** | **Serviceproviders** |
| --- | --- |
| **Berlijn** |Colt+, e-shelter, Megaport+, T-Systems |
| **Frankfurt** |Colt, Equinix, Interxion |

## <a name="c1partners"></a>Connectiviteit via Exchange-providers
Als uw connectiviteitsprovider niet wordt vermeld in de vorige secties, kunt u alsnog verbinding maken.

* Neem contact op met uw provider connectiviteit toosee als ze verbonden tooany Hallo uitwisseling in Hallo bovenstaande tabel zijn. U kunt controleren Hallo volgende koppelingen toogather meer informatie over services die worden aangeboden door providers van exchange. Verschillende connectiviteitsproviders zijn al verbonden tooEthernet kunnen worden uitgewisseld.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [InterXion](http://www.interxion.com/)
  * [NextDC](http://www.nextdc.com/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Uw connectiviteitsprovider uitbreiden van uw netwerk toohello peering gewenste locatie hebben.
  * Vergewis u ervan dat de connectiviteitsprovider uw connectiviteit uitbreidt op een maximaal beschikbare manier, zodat er geen storingspunten zijn.
* Een ExpressRoute-circuit met Hallo exchange als uw connectiviteitsprovider tooconnect tooMicrosoft volgorde.
  * Volg de stappen in [maken van een ExpressRoute-circuit](expressroute-howto-circuit-classic.md) tooset connectiviteit.

## <a name="c1partners"></a>Connectiviteit via additionele serviceproviders
| **Locatie** | **Exchange** | **Connectiviteitsproviders** |
| --- | --- | --- |
| **Amsterdam** | Equinix, Telecity | Eurofiber , Fastweb S.p.A, Nianet |
| **Chicago** | Equinix | Lightower, Windstream |
| **Dallas** | Equinix, Megaport | C3ntro Telecom, Cox Business, Data Foundry, Transtelco |
| **Frankfurt** | Telecity | Nianet, QSC AG |
| **Hongkong** | Equinix | Macroview Telecom |
| **Londen** | Equinix, euNetworks, Telecity | Bezeq International Ltd., Epsilon, Exponential E, HSO, NexGen Networks, Tamares Telecom, Zain |
| **Los Angeles** | Equinix |Transtelco |
| **Madrid** | Level3 | Zertia |
| **Montreal** | Cologix, Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Zirro |
| **New York** |Equinix, Megaport | Altice Business, Lightower, Webair |
| **Seattle** |Equinix | Alaska Communications |
| **Silicon Valley** |Equinix | Cox Business, Windstream |
| **Singapore** |Equinix |1CLOUDSTAR, Epsilon Telecommunications Limited, LGA Telecom, United Information Highway (UIH) |
| **Slough** | Equinix | HSO|
| **Sydney** | Megaport | Macquarie Telecom Group|
| **Tokio** | Equinix | ARTERIA Networks Corporation, BroadBand Tower, Inc. |
| **Toronto** | Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Thinktel, Zirro|
| **Washington DC** |Equinix | Altice Business, Gtt Communications Inc, Epsilon, Lightower, Masergy, Windstream |

## <a name="expressroute-system-integrators"></a>ExpressRoute-SI's
Inschakelen van particuliere connectiviteit toofit die uw behoeften kunnen lastig zijn gebaseerd op Hallo van schaal van uw netwerk. U kunt werken met een van de Hallo systeemintegrators die worden vermeld in de tabel tooassist na Hallo u met onboarding tooExpressRoute.

| **Continent** | **Systeemintegratie** |
| --- | --- |
| **Azië** |Avanade Inc., OneAs1a |
| **Australië** | Ensyst, IT Consultancy, MOQdigital, Vigilant.IT |
| **Europa** |Avanade Inc., Altogee, Bright Skies GmbH, Inframon, MSG Services, New Signature, Nelite, Orange Networks, sol-tec |
| **Noord-Amerika** |Avanade Inc., Equinix Professional Services, FlexManage, Perficient, Presidio |
| **Zuid-Amerika** |Avanade Inc. |
## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over ExpressRoute hello [Veelgestelde vragen over ExpressRoute](expressroute-faqs.md).
* Controleer of aan alle vereisten is voldaan. Zie [ExpressRoute prerequisites](expressroute-prerequisites.md) (Vereisten voor ExpressRoute).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Locatiekaart"
