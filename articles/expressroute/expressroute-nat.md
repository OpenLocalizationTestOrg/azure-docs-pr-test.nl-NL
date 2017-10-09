---
title: vereisten voor ExpressRoute-circuits aaaNAT | Microsoft Docs
description: Deze pagina bevat gedetailleerde vereisten voor het configureren en beheren van de NAT voor ExpressRoute-circuits.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>NAT-vereisten voor ExpressRoute
tooconnect tooMicrosoft cloudservices met ExpressRoute, hebt u nodig hebt tooset en NAT's beheren. Sommige connecitiviteitsproviders bieden het instellen en beheren van NAT aan als een beheerde service. Neem contact op met uw provider connectiviteit toosee als ze deze service aanbiedt. Als dat niet het geval is, moet u voldoen toohello vereisten die hieronder worden beschreven. 

Bekijk Hallo [ExpressRoute-circuits en Routeringsdomeinen](expressroute-circuit-peerings.md) pagina tooget een overzicht van Hallo verschillende Routeringsdomeinen. toomeet hello openbare IP-adres vereisten voor openbare Azure- en Microsoft-peering, wordt aangeraden dat u NAT tussen uw netwerk en Microsoft instelt. Deze sectie bevat een gedetailleerde beschrijving van Hallo NAT-infrastructuur die u nodig hebt tooset.

## <a name="nat-requirements-for-azure-public-peering"></a>NAT-vereisten voor openbare Azure-peering
Hello Azure pad voor openbare peering kunt u tooconnect tooall services die worden gehost in Azure via de openbare IP-adressen. Deze omvatten services die worden vermeld in Hallo [Veelgestelde vragen over ExpessRoute](expressroute-faqs.md) en alle services die door ISV's in Microsoft Azure worden gehost. 

> [!IMPORTANT]
> Connectiviteit tooMicrosoft Azure services voor openbare peering wordt altijd gestart vanuit het netwerk in Hallo Microsoft-netwerk. Daarom kunnen niet sessies worden geïnitieerd worden vanuit Microsoft Azure-services tooyour netwerk via ExpressRoute. Als er is geprobeerd, verzonden pakketten toothese IP-adressen geadverteerd gebruikt Hallo internet in plaats van ExpressRoute.
> 

Verkeer dat is bestemd tooMicrosoft Azure via openbare peering moet worden omgezet toovalid die openbare IPv4-adressen voordat Hallo Microsoft-netwerk binnenkomt. Hallo afbeelding hieronder biedt een algemeen beeld van hoe Hallo NAT kan worden ingesteld toomeet Hallo bovenstaande vereiste.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>NAT IP-adresgroep en route-advertenties
U moet ervoor zorgen dat verkeer hello Azure pad voor openbare peering met geldige openbare IPv4-adres is invoert. Microsoft moet kunnen toovalidate Hallo eigendom van Hallo IPv4 NAT-adresgroep op basis van een regionale routing Internet registry (RIR) of een Internet routing registry (IRR). Een controle uitgevoerd op basis van Hallo als het getal wordt gekoppeld en Hallo IP-adressen gebruikt voor Hallo NAT bevinden. Raadpleeg toohello [routeringsvereisten voor ExpressRoute](expressroute-routing.md) pagina voor meer informatie over routeringsregisters.

Er zijn geen beperkingen voor Hallo Hallo NAT IP-voorvoegsel dat via deze peering wordt geadverteerd. U moet controleren Hallo NAT-pool en zorg ervoor dat u geen NAT-sessies tekort komt.

> [!IMPORTANT]
> Hallo NAT IP-adresgroep geadverteerd tooMicrosoft mag geen aangekondigd toohello Internet. Dit verbreekt de connectiviteit tooother Microsoft-services.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>NAT-vereisten voor Microsoft-peering
Hallo pad voor Microsoft-peering kunt u tooMicrosoft cloud-services die worden niet ondersteund via hello Azure pad voor openbare peering verbinding te maken. Hallo-lijst met services bevat Office 365-services, zoals Exchange Online, SharePoint Online, Skype voor bedrijven en Dynamics 365. Microsoft verwacht bidirectionele verbinding toosupport op Hallo Microsoft-peering. Verkeer dat is bestemd tooMicrosoft cloudservices moet omgezet toovalid die openbare IPv4-adressen voordat Hallo Microsoft-netwerk binnenkomt. Verkeer dat is bestemd tooyour netwerk vanuit Microsoft cloud-services moet met Snat worden op uw Internet rand tooprevent [asymmetrische routering](expressroute-asymmetric-routing.md). Hallo afbeelding hieronder biedt een algemeen beeld van hoe Hallo NAT setup voor Microsoft-peering moet worden.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Verkeer van uw netwerk en is bestemd tooMicrosoft
* U moet ervoor zorgen dat verkeer Hallo Microsoft-peering met een geldig openbaar IPv4-adres binnenkomt. Microsoft moet kunnen toovalidate Hallo eigenaar van Hallo IPv4-NAT-adresgroep Hallo regionale routing internet registry (RIR) of een internet routing registry (IRR). Een controle uitgevoerd op basis van Hallo als het getal wordt gekoppeld en Hallo IP-adressen gebruikt voor Hallo NAT bevinden. Raadpleeg toohello [routeringsvereisten voor ExpressRoute](expressroute-routing.md) pagina voor meer informatie over routeringsregisters.
* IP-adressen die worden gebruikt voor Hallo installatie van de Azure openbare peering en andere ExpressRoute-circuits mogen niet worden aangekondigd tooMicrosoft via Hallo BGP-sessie. Er is geen beperking voor Hallo Hallo NAT IP-voorvoegsel dat via deze peering wordt geadverteerd.
  
  > [!IMPORTANT]
  > Hallo NAT IP-adresgroep geadverteerd tooMicrosoft mag geen aangekondigd toohello Internet. Dit verbreekt de connectiviteit tooother Microsoft-services.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Verkeer dat afkomstig is van Microsoft die bestemd zijn tooyour netwerk
* Bepaalde scenario's moet Microsoft tooinitiate connectiviteit tooservice eindpunten die worden gehost in uw netwerk. Een typisch voorbeeld van Hallo scenario is connectiviteit tooADFS servers die worden gehost in uw netwerk vanuit Office 365. In dergelijke gevallen moet u vanuit uw netwerk geschikte voorvoegsels lekken naar Hallo Microsoft-peering. 
* U moet Microsoft met snat omzetten-verkeer bij Hallo Internet rand voor service-eindpunten binnen uw netwerk tooprevent [asymmetrische routering](expressroute-asymmetric-routing.md). Aanvragen **en antwoorden** met een doel-IP die overeenkomt met een route ontvangen via ExpressRoute worden altijd verzonden via ExpressRoute. Asymmetrische routering bestaat als Hallo-aanvraag wordt ontvangen via Internet Hallo Hello antwoord verzonden via ExpressRoute. SNATing hello binnenkomende Microsoft-verkeer bij Hallo Internet rand dwingt antwoord verkeer back toohello Internet edge, het oplossen van Hallo probleem.

![Asymmetrische routering met ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Volgende stappen
* Raadpleeg de vereisten voor toohello [routering](expressroute-routing.md) en [QoS](expressroute-qos.md).
* Voor informatie over werkstromen raadpleegt u [ExpressRoute circuit provisioning workflows and circuit states](expressroute-workflows.md) (Werkstromen voor de inrichting van ExpressRoute-circuits en circuittoestanden).
* Configureer uw ExpressRoute-verbinding.
  
  * [Een ExpressRoute-circuit maken](expressroute-howto-circuit-classic.md)
  * [Routering configureren](expressroute-howto-routing-classic.md)
  * [Koppelen van een VNet tooan ExpressRoute-circuit](expressroute-howto-linkvnet-classic.md)

