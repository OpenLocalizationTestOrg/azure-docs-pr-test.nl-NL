---
title: aaaWhat is Traffic Manager | Microsoft Docs
description: Dit artikel helpt u begrijpen wat Traffic Manager is en of deze Hallo rechts traffic routing keuze voor uw toepassing
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Overzicht van Traffic Manager

Microsoft Azure Traffic Manager kunt u toocontrol Hallo distributie van gebruikersverkeer voor service-eindpunten in verschillende datacenters. Service-eindpunten die worden ondersteund door Traffic Manager bevatten Azure virtuele machines, Web-Apps en cloudservices. U kunt Traffic Manager ook gebruiken met externe eindpunten die niet van Azure zijn.

Traffic Manager maakt gebruik van Hallo Domain Name System (DNS) toodirect client aanvragen toohello meest geschikte eindpunt op basis van een methode traffic routing en Hallo-status van het Hallo-eindpunten. Traffic Manager biedt een reeks [verkeersroutering methoden](traffic-manager-routing-methods.md) en [eindpunt controle-opties](traffic-manager-monitoring.md) toosuit verschillende groepen van toepassingen behoeften en automatische failover-modellen. Traffic Manager is een robuuste toofailure, met inbegrip van Hallo falen van een volledige Azure-regio.

## <a name="traffic-manager-benefits"></a>Voordelen van het Traffic Manager

Traffic Manager kan u helpen:

* **Verbeter de beschikbaarheid van bedrijfskritieke toepassingen**

    Traffic Manager biedt hoge beschikbaarheid voor uw toepassingen aan de bewaking van uw eindpunten en automatische failover te bieden wanneer een eindpunt uitvalt.

* **Reactietijd voor toepassingen met hoge prestaties te verbeteren**

    Azure kunt u cloudservices toorun of websites in datacenters zich Hallo wereld. Traffic Manager verbetert de reactietijd van toepassing door verkeer toohello eindpunt met de laagste netwerklatentie Hallo voor Hallo-client.

* **Uitvoeren van serviceonderhoud zonder uitvaltijd**

    U kunt geplande onderhoudsbewerkingen uitvoeren op uw toepassingen zonder uitvaltijd. Traffic Manager stuurt verkeer tooalternative eindpunten terwijl Hallo onderhoud uitgevoerd wordt.

* **Combineren van on-premises en cloudtoepassingen**

    Traffic Manager biedt ondersteuning voor externe, niet-Azure-eindpunten inschakelen van toobe gebruikt met hybride cloud en on-premises implementaties, met inbegrip van Hallo 'burst-naar-cloud,' 'migreren-naar-cloud,' en 'failover cloud'-scenario's.

* **Verkeer voor grote, complexe implementaties distribueren**

    Met behulp van [Traffic Manager-profielen genest](traffic-manager-nested-profiles.md), verkeersroutering methoden kunnen worden gecombineerd toocreate geavanceerde en flexibele regels toosupport Hallo moet van grotere, complexe implementaties.

## <a name="how-traffic-manager-works"></a>Hoe Traffic Manager werkt

Azure Traffic Manager kunt u toocontrol Hallo distributie van verkeer tussen de eindpunten van uw toepassing. Een eindpunt is een internetgerichte service die wordt gehost binnen of buiten Azure.

Traffic Manager biedt twee belangrijke voordelen:

1. Distributie van verkeer op basis van tooone van verschillende [verkeersroutering methoden](traffic-manager-routing-methods.md)
2. [Doorlopende bewaking van de status van endpoint](traffic-manager-monitoring.md) en automatische failover wanneer eindpunten mislukken

Wanneer een client tooconnect tooa service probeert, moet deze eerst Hallo DNS-naam van Hallo service tooan IP-adres oplossen. Hallo-client maakt vervolgens verbinding toothat IP-adres tooaccess Hallo service.

**Hallo zeer belangrijk punt toounderstand is dat het Traffic Manager op Hallo DNS-niveau werkt.**  Traffic Manager maakt gebruik van DNS-toodirect clients toospecific service-eindpunten op basis van regels Hallo van Hallo verkeersroutering methode. Clients verbinding maken met eindpunt toohello geselecteerd **rechtstreeks**. Traffic Manager is niet een proxy of gateway. Traffic Manager doorgeven tussen Hallo client- en Hallo Hallo-verkeer niet te zien.

### <a name="traffic-manager-example"></a>Traffic Manager-voorbeeld

Contoso Corp hebben een nieuwe Partnerportal ontwikkeld. Hallo-URL voor deze portal is https://partners.contoso.com/login.aspx. Hallo-toepassing wordt gehost in drie gebieden van Azure. tooimprove beschikbaarheid en prestaties van globale, gebruiken ze toodistribute Traffic Manager-client verkeer toohello dichtstbijzijnde beschikbare eindpunt.

tooachieve deze configuratie voltooid Hallo stappen te volgen:

1. Drie exemplaren van de service implementeren. Hallo DNS-namen van deze implementaties zijn 'contoso-us.cloudapp .net', 'contoso-eu.cloudapp .net' en 'contoso-asia.cloudapp .net'.
2. Een Traffic Manager-profiel met de naam 'contoso.trafficmanager.net' Maak en configureer deze toouse Hallo ''-verkeer routeren methode voor alle drie Hallo-eindpunten.
* Configureren van hun domeinnaam vanity, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net', met een DNS CNAME-record.

![Traffic Manager-DNS-configuratie][1]

> [!NOTE]
> Wanneer u een vanity-domein met Azure Traffic Manager, moet u een CNAME-toopoint uw vanity domain name tooyour Traffic Manager-domeinnaam. DNS-standaarden staan niet toe dat u een CNAME op Hallo 'top' toocreate (of hoofdmap) van een domein. U kunt geen dus een CNAME voor contoso.com (ook wel een domein, open' genoemd) maken. U kunt alleen een CNAME voor een domein onder 'contoso.com', zoals 'www.contoso.com' maken. toowork om deze beperking, wordt u aangeraden een eenvoudige HTTP-omleiding toodirect aanvragen voor 'contoso.com' tooan alternatieve naam zoals 'www.contoso.com'.

### <a name="how-clients-connect-using-traffic-manager"></a>Hoe clients verbinding maken met behulp van Traffic Manager

U doorgaat uit het vorige voorbeeld hello, wanneer een client Hallo pagina https://partners.contoso.com/login.aspx aanvraagt, Hallo-client voert hello te volgen stappen tooresolve Hallo DNS-naam en een verbinding tot stand brengen:

![Verbinding tot stand brengen met Traffic Manager][2]

1. Hallo-client verzendt een DNS-query tooits geconfigureerd recursieve DNS-service tooresolve Hallo naam 'partners.contoso.com'. DNS-domeinen is niet rechtstreeks host van een recursieve DNS-service, ook wel een lokale DNS-service wordt genoemd. In plaats daarvan Hallo client Hallo werk off-loads van Hallo contact opnemen met verschillende gezaghebbende DNS-services via Hallo Internet nodig tooresolve een DNS-naam.
2. tooresolve hello DNS-naam Hallo recursieve DNS-service vindt u de naamservers Hallo-domein 'contoso.com' Hallo. Deze vervolgens neemt contact op met de naam servers toorequest Hallo 'partners.contoso.com' DNS-record. Hallo contoso.com DNS-servers retourneren Hallo CNAME-record die toocontoso.trafficmanager.net verwijst.
3. Vervolgens vindt Hallo recursieve DNS-service u de naamservers Hallo Hallo 'trafficmanager.net' domein, die worden geleverd door hello Azure Traffic Manager-service. Vervolgens stuurt een aanvraag voor Hallo 'contoso.trafficmanager.net' DNS-record toothose DNS-servers.
4. Hallo Traffic Manager-naamservers ontvangen Hallo-aanvraag. Ze kiezen een eindpunt op basis van:

    - Hallo geconfigureerd status van elk eindpunt (uitgeschakelde eindpunten worden niet geretourneerd)
    - Hallo huidige status van elk eindpunt, zoals wordt bepaald door Hallo Traffic Manager-status wordt gecontroleerd. Zie voor meer informatie [Traffic Manager-eindpunt bewaking](traffic-manager-monitoring.md).
    - Hallo gekozen verkeersroutering methode. Zie voor meer informatie [Traffic Manager routering methoden](traffic-manager-routing-methods.md).

5. Hallo gekozen eindpunt wordt als een andere DNS CNAME-record geretourneerd. In dit geval laat het ons Stel contoso us.cloudapp.net wordt geretourneerd.
6. Vervolgens vindt Hallo recursieve DNS-service u de naamservers Hallo Hallo 'cloudapp.net' domein. Het contact opneemt met die naam servers toorequest Hallo 'contoso-us.cloudapp .net' DNS-record. Een DNS-'A'-record met Hallo IP-adres van Hallo VS gebaseerde service-eindpunt wordt geretourneerd.
7. Hallo recursieve DNS-service worden geconsolideerd Hallo resultaten en retourneert één DNS-antwoord toohello client.
8. Hallo-client ontvangt Hallo DNS-resultaten en verbindt toohello opgegeven IP-adres. Hallo-client verbinding toohello toepassing service-eindpunt rechtstreeks, niet via het Traffic Manager. Omdat het een HTTPS-eindpunt, Hallo-client voert Hallo nodig SSL/TLS-handshake en maakt vervolgens een HTTP GET-aanvraag voor Hallo ' / login.aspx' pagina.

Hallo recursieve DNS-service in de cache opgeslagen Hallo DNS-antwoorden die het ontvangt. Hallo DNS-resolver op het clientapparaat Hallo worden ook opgeslagen Hallo resultaat. Opslaan in cache kunt volgende DNS-query's toobe sneller wordt beantwoord door gegevens uit de cache hello gebruiken in plaats van query's op de naamservers van andere. Hallo-duur van het Hallo-cache wordt bepaald door Hallo 'time-to-live-eigenschap van elke DNS-record (TTL). Kortere waarden resulteren in snellere verstrijken van de cache en dus meer retourbewerkingen toohello Traffic Manager naamservers. Langer waarden betekenen dat het langer toodirect verkeer weg van een mislukte eindpunt kan duren. Traffic Manager kunt u tooconfigure Hallo TTL die wordt gebruikt in Traffic Manager-DNS-antwoorden toobe zo laag 0 seconden en zo hoog 2.147.483.647 seconden (Hallo maximumbereik compatibel zijn met [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), zodat u toochoose Hallo waarde die behoeften van uw toepassing hello beste compromis tussen.

## <a name="pricing"></a>Prijzen

Zie voor informatie over prijzen, [Traffic Manager prijzen](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>Veelgestelde vragen

Zie voor veelgestelde vragen over Traffic Manager [Traffic Manager Veelgestelde vragen](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het Traffic Manager [eindpunt bewakings- en automatische failover](traffic-manager-monitoring.md).

Meer informatie over het Traffic Manager [verkeersrouteringsmethoden](traffic-manager-routing-methods.md).

Meer informatie over een aantal Hallo andere sleutel [netwerkmogelijkheden](../networking/networking-overview.md) van Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

