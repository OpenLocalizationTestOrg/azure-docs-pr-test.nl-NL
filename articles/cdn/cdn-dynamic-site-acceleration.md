---
title: aaaDynamic Site versnelling via Azure CDN
description: Dynamische site-versnelling diepgaand
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Dynamische Site-versnelling via Azure CDN

Met de Hallo explosie van sociale media, elektronische transacties en Hallo hyper persoonlijke web, snel toenemende percentage Hallo inhoud aangeboden tooend gebruikers gegenereerd in realtime. Gebruikers verwachten snelle, betrouwbare en gepersonaliseerde webervaringen, onafhankelijk van hun browser, locatie, apparaat of netwerk. Hallo zeer vernieuwingen waaruit deze dus ook bezighouden ervaringen trage pagina downloads en de kwaliteit Hallo Hallo consumer ervaring risico. 

Standaard CDN-mogelijkheid geldt Hallo mogelijkheid toocache bestanden dichter tooend gebruikers toospeed up levering van statische bestanden. Echter met dynamische webtoepassingen die inhoud op rand locaties opslaan in cache is niet mogelijk omdat Hallo server Hallo inhoud in het antwoord toouser gedrag genereert. Hallo-levering van deze inhoud te versnellen is complexer dan traditionele edge cache en een end-to-end-oplossing die geoptimaliseerd voor elk element in de hele gegevenspad Hallo van begin toodelivery vereist. Met Azure CDN dynamische Site Acceleration (DSA), de prestaties van webpagina's met dynamische inhoud Hallo aantoonbaar verbeterd.

Azure CDN van Akamai en Verizon biedt DSA optimalisatie via Hallo **geoptimaliseerd voor** menu tijdens het maken van het eindpunt.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Levering van CDN-eindpunt tooaccelerate van dynamische bestanden configureren

U kunt de levering van CDN-eindpunt toooptimize van dynamische bestanden via Azure portal configureren met behulp van Hallo **dynamische site-versnelling** optie onder Hallo **geoptimaliseerd voor** eigenschap selecteren tijdens Hallo-eindpunt maken. U kunt ook onze REST-API's gebruiken of een van de Hallo client SDK's toodo hetzelfde programmatisch Hallo. 

### <a name="probe-path"></a>Pad van de test
Test-pad is een functie specifieke tooDynamic versnelling Site en een geldig is vereist voor het maken van. DSA maakt gebruik van een klein *test pad* bestand op Hallo oorsprong toooptimize routering netwerkconfiguraties voor Hallo CDN geplaatst. Download en onze site voorbeeld bestand tooyour uploaden, of gebruik een bestaande asset op uw oorsprong is ongeveer 10 KB voor Hallo test pad in plaats daarvan als Hallo asset bestaat.

> [!Note]
> DSA extra kosten in rekening worden gebracht. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/cdn/) voor meer informatie.

Hallo volgende schermafbeeldingen illustreren Hallo proces via de Azure-portal.
 
![Een nieuw CDN-eindpunt toevoegen](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Afbeelding 1: Het toevoegen van een nieuw CDN-eindpunt van Hallo CDN-profiel*
 
![Het maken van een nieuw CDN-eindpunt met DSA](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Afbeelding 2: Het maken van een CDN-eindpunt met dynamische site-versnelling optimalisatie geselecteerd*

Zodra Hallo CDN-eindpunt is gemaakt, toepassing hello DSA optimalisaties voor alle bestanden die aan bepaalde criteria voldoen. Hallo volgende sectie wordt DSA optimalisatie in detail beschreven.

## <a name="dsa-optimization-using-azure-cdn"></a>DSA optimalisatie met behulp van Azure CDN

Dynamische Site-versnelling op Azure CDN wordt versneld levering van dynamische elementen Hallo volgende technieken gebruiken:

-   Route optimalisatie
-   Optimalisaties voor TCP
-   Object Prefetch (alleen Akamai)
-   Compressie mobiele afbeelding (alleen Akamai)

### <a name="route-optimization"></a>Route optimalisatie

Optimalisatie van de route is belangrijk omdat Hallo Internet een dynamische plaats is, waar verkeer en tijdelijk uitval voortdurend Hallo netwerktopologie veranderen. Hallo Border Gateway Protocol (BGP) is Hallo routeringsprotocol Hallo Internet, maar er is mogelijk sneller routes via een tussenliggende punt aanwezigheid (PoP)-servers. 

Route optimalisatie kiest Hallo optimale pad toohello oorsprong zodat een site voortdurend toegankelijk en dynamische inhoud wordt wordt geleverd tooend gebruikers via Hallo snelste en betrouwbaarste route mogelijk. 

Hallo Akamai netwerk gebruikt technieken toocollect realtime gegevens en verschillende paden via andere knooppunten in het Hallo Akamai server, evenals de standaardroute BGP Hallo van Hallo open Internet toodetermine Hallo snelste route tussen Hallo oorsprong en Hallo met elkaar vergelijken CDN-rand. Deze technieken te voorkomen dat Internet congestie punten en lang routes. 

Op deze manier Hallo Hallo Verizon netwerk gebruikt een combinatie van Anycast DNS, hoge capaciteit ondersteunen POP's en statuscontroles, toodetermine Hallo best gateways toobest routegegevens van client toohello oorsprong.
 
Als gevolg hiervan volledig dynamische en transactionele inhoud wordt geleverd sneller en betrouwbaarder tooend gebruikers, zelfs wanneer het uncacheable. 

### <a name="tcp-optimizations"></a>Optimalisaties voor TCP

Transmission Control Protocol (TCP) is standaard Hallo van Internet-protocolsuite Hallo gebruikt toodeliver informatie tussen toepassingen op een IP-netwerk.  Er zijn verschillende back standaard en weer aanvragen tooset van een TCP-verbinding, evenals limieten tooavoid netwerk congestions, waardoor het inefficiëntie op grote schaal vereist. Azure CDN van Akamai omgaat met dit probleem door te optimaliseren in drie gebieden: 

 - Trage start elimineren
 - Gebruik van permanente verbindingen
 - afstemming van TCP-pakket parameters (alleen Akamai)

#### <a name="eliminating-slow-start"></a>Trage start elimineren

*Trage start* deel uitmaakt van Hallo TCP-protocol waarmee wordt voorkomen opstoppingen in het netwerk dat door te beperken Hallo hoeveelheid gegevens die via Hallo-netwerk worden verzonden. Deze begint uitschakelen met kleine congestie venstergrootte tussen zender en ontvanger totdat Hallo maximum is bereikt of pakketverlies wordt gedetecteerd.

Azure CDN van Akamai en Verizon elimineert trage start in drie stappen:

1.  Zowel Akamai van Verizon netwerk health en bewaking toomeasure Hallo bandbreedte van de verbindingen tussen PoP randservers bandbreedte gebruiken.
2. Hallo metrische gegevens worden gedeeld tussen edge PoP-servers, zodat elke server op de hoogte van Hallo netwerkomstandigheden is en serverstatus van andere POP's omheen Hallo.  
3. Hallo CDN randservers zijn nu kunnen toomake veronderstellingen over sommige transmission-parameters, zoals welke Hallo optimale venstergrootte moet tijdens de communicatie met andere servers van de rand CDN in de buurt. Deze stap betekent Hallo initiële congestie venstergrootte kan worden verhoogd als Hallo-status van het Hallo-verbinding tussen Hallo CDN randservers hogere pakket gegevensoverdrachten staat is.  

#### <a name="leveraging-persistent-connections"></a>Gebruik van permanente verbindingen

Met behulp van een CDN minder unieke computers verbinding maken met bronserver tooyour rechtstreeks vergeleken met gebruikers tooyour oorsprong rechtstreeks verbinding maken. Azure CDN van Akamai en Verizon ook aan de groep gebruikers aanvragen samen tooestablish minder verbindingen met Hallo oorsprong.

Zoals eerder gezegd, netwerkverzoeken TCP-verbindingen verschillende heen en weer in een handshake tooestablish een nieuwe verbinding. Permanente verbindingen, ook wel bekend als ' HTTP Keep-Alive, ' bestaande TCP-verbindingen gebruiken voor HTTP-aanvragen toosave round trip meermaals en levering versnellen. 

Hallo Verizon netwerk verzendt ook periodieke keepalive-pakketten via Hallo TCP-verbinding tooprevent een open verbinding wordt afgesloten.

#### <a name="tuning-tcp-packet-parameters"></a>Afstemming van TCP-pakket parameters

Azure CDN van Akamai ook Hallo-parameters die server naar server verbindingen van toepassing verbetert de prestatie en vermindert Hallo hoeveelheid lange afstand ronde reizen vereist tooretrieve inhoud ingesloten in Hallo site met behulp van Hallo technieken te volgen:

1.  Hallo opstoppingen in het eerste venster vergroot zodat meer pakketten kunnen worden verzonden zonder te wachten op een bevestiging.
2.  Hallo initiële retransmit time-out verlagen zodat een verlies wordt gedetecteerd en herverzending sneller vindt plaats.
3.  Afnemende Hallo minimum en maximum opnieuw time-out tooreduce Hallo wachttijd voordat wordt aangenomen dat pakketten verloren zijn gegaan in verzending.

### <a name="object-prefetch-akamai-only"></a>Object Prefetch (alleen Akamai)

De meeste websites bestaan uit een HTML-pagina die verwijst naar diverse andere resources, zoals afbeeldingen en scripts. Normaal gesproken wanneer een client een webpagina aanvraagt, Hallo browser downloadt eerst Hallo HTML-object parseert en maakt vervolgens extra aanvragen toolinked assets die vereist toofully zijn Hallo pagina laden. 

*Prefetch* is een techniek tooretrieve afbeeldingen en scripts ingesloten in Hallo HTML-pagina terwijl hello HTML wordt behandeld toohello browser voordat Hallo browser zelfs deze aanvragen object maakt. 

Hello **prefetch** optie is ingeschakeld tijdens het Hallo wanneer Hallo CDN fungeert Hallo HTML basispagina toohello clientbrowser, CDN Hallo Hallo HTML-bestand wordt geparseerd en aanvullende aanvragen voor alle gekoppelde resources maken en opslaan in de cache. Wanneer hello client Hallo aanvragen voor Hallo gekoppeld activa, Hallo CDN edge-server al heeft Hallo gevraagde objecten en kan dienen ze onmiddellijk zonder een round trip toohello oorsprong. Deze optimalisatie voordelen biedt voor caching geschikte en niet-caching geschikte inhoud.

### <a name="adaptive-image-compression-akamai-only"></a>Adaptieve compressie (alleen Akamai)

Op sommige apparaten, met name mobiele die ervaren tragere netwerksnelheden van tijd tootime. In deze scenario's, is het meer nuttig voor Hallo gebruiker tooreceive kleinere afbeeldingen in hun webpagina sneller in plaats van met een lange wachttijd voor installatiekopieën van de volledige resolutie.

Deze functie automatisch bewaakt netwerk kwaliteit en JPEG-compressie standaardmethoden veiligheidsmaatregelen wanneer netwerksnelheden tragere tooimprove leveringstijd zijn.

Adaptieve compressie | Bestandsextensies  
--- | ---  
JPEG-compressie | JPG, JPEG, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Caching

Met DSA, is opslaan in cache standaard uitgeschakeld op Hallo CDN, zelfs wanneer Hallo oorsprong cache-control/verloopt kopteksten in Hallo antwoord bevat. Deze standaard is uitgeschakeld omdat DSA doorgaans voor dynamische activa dat mag niet worden opgeslagen gebruikt wordt omdat ze unieke tooeach client en cache standaard ingeschakeld op dit gedrag kunt verbreken.

Hebt u een website met een combinatie van statische en dynamische activa, is het beste tootake een hybride benadering tooget Hallo optimale prestaties. 

Als u van ADN met Premium van Verizon gebruikmaakt, kunt u opnieuw in de cache voor specifieke gevallen Hallo regels-Engine.  

Een alternatief is toouse twee CDN-eindpunten. Met dynamische activa van DSA toodeliver en een ander eindpunt met een statische optimalisatie typt, zoals algemene web-levering toodelivery caching geschikte activa. In de volgorde tooaccomplish dit alternatieve wijzigt u uw toolink webpagina-URL's rechtstreeks toohello asset op Hallo u van plan bent toouse CDN-eindpunt. 

Bijvoorbeeld: `mydynamic.azureedge.net/index.html` is een dynamische pagina en is geladen vanuit Hallo DSA-eindpunt.  Hallo html-pagina verwijst naar meerdere statische elementen zoals JavaScript-bibliotheken of installatiekopieën die worden geladen vanuit Hallo statische CDN-eindpunt, zoals `mystatic.azureedge.net/banner.jpg` en `mystatic.azureedge.net/scripts.js`. 

U vindt een voorbeeld [hier](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) op hoe web toouse domeincontrollers in een ASP.NET-toepassing tooserve inhoud via een specifieke CDN-URL.




