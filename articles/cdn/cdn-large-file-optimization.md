---
title: optimalisatie van aaaLarge bestand downloaden via hello Azure Content Delivery Network
description: Optimalisatie van downloads van grote bestanden beschreven in de diepte
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
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 2646979bfb38e997037bcff5b1cdda34e22c394a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="large-file-download-optimization-via-hello-azure-content-delivery-network"></a>Optimalisatie van grote bestanden downloaden via hello Azure Content Delivery Network

Grootte van inhoud aangeboden via Internet Hallo blijven toogrow vanwege tooenhanced functionaliteit, verbeterde afbeeldingen en uitgebreide media-inhoud. Deze groei wordt aangedreven door vele factoren: breedband binnendringen, grotere goedkope opslagapparaten, wijdverbreid toename van hoogwaardige video- en Internet verbonden apparaten (IoT). Een snelle en efficiënte bezorgingsmechanisme voor grote bestanden is essentieel tooensure een consumer smooth en uitmuntende ervaring.

De bezorging van grote bestanden heeft enkele uitdagingen. Eerst kan Hallo gemiddelde tijd toodownload een groot bestand worden belangrijke omdat toepassingen mogelijk alle gegevens niet opeenvolgend downloaden. In sommige gevallen mogelijk toepassingen Hallo laatste deel van een bestand voordat u het eerste deel Hallo downloaden. Wanneer een kleine hoeveelheid een bestand wordt aangevraagd of een gebruiker een download wordt onderbroken, mislukken Hallo downloaden. Hallo downloaden kan ook worden uitgesteld totdat na Hallo content delivery network (CDN) Hallo hele bestand opgehaald uit het Hallo-bronserver. 

Ten tweede bepaalt Hallo latentie tussen de computer van een gebruiker en Hallo Hallo snelheid waarmee ze inhoud kunnen weergeven. Bovendien problemen met het netwerk opstoppingen en capaciteit ook van invloed op de doorvoer. Aanvullende mogelijkheden voor pakket verlies toooccur, waardoor kwaliteit maken groter afstanden tussen servers en gebruikers Hallo verminderde kwaliteit veroorzaakt door een beperkte doorvoer en verhoogde pakketverlies Hallo wachttijd voor een bestand downloaden toofinish verhogen. 

Ten slotte veel grote bestanden niet in hun geheel worden geleverd. Gebruikers kunnen downloaden halverwege annuleren of alleen Hallo eerste enkele minuten een lange MP4-video bekijken. Daarom wilt software en media levering bedrijven toodeliver enige Hallo gedeelte van een bestand dat aangevraagd. Efficiënte distributie Hallo aangevraagd delen minder Hallo uitgaande verkeer van de bronserver Hallo. Efficiënte distributie ook minder Hallo geheugen en i/o-belasting op de bronserver Hallo. 

Hello Azure Content Delivery Network van Akamai biedt nu een functie die voorziet in grote bestanden efficiënt toousers over de hele Hallo wereld op grote schaal. Hallo functie vermindert latenties omdat het Hallo-belasting op Hallo oorsprong servers vermindert. Deze functie is beschikbaar met Hallo Standard van Akamai prijscategorie.

## <a name="configure-a-cdn-endpoint-toooptimize-delivery-of-large-files"></a>Een CDN-eindpunt toooptimize de bezorging van grote bestanden configureren

U kunt uw toooptimize levering van CDN-eindpunt voor grote bestanden via hello Azure-portal configureren. U kunt ook onze REST-API's gebruiken of een van de client SDK's toodo Hallo dit. Hallo ziet volgende stappen Hallo proces via hello Azure-portal.

1. een nieuw eindpunt, klikt u op Hallo tooadd **CDN-profiel** pagina **eindpunt**.

    ![Nieuwe endpoint](./media/cdn-large-file-optimization/01_Adding.png)  
 
2. In Hallo **geoptimaliseerd voor** vervolgkeuzelijst, selecteer **downloaden van grote bestanden**.

    ![Optimalisatie van grote bestanden geselecteerd](./media/cdn-large-file-optimization/02_Creating.png)


Nadat u Hallo CDN-eindpunt hebt gemaakt, toepassing hello groot bestand optimalisaties voor alle bestanden die aan bepaalde criteria voldoen. Hallo volgende sectie wordt beschreven dit proces.

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-akamai"></a>Voor het leveren van grote bestanden Hello Azure Content Delivery Network van Akamai optimaliseren

Hallo groot bestand optimalisatie type functie ingeschakeld netwerk optimalisaties en configuraties toodeliver grote bestanden sneller en meer responsively. Algemene webtoepassingen levering met Akamai bestanden alleen hieronder 1,8 GB cache en het tunnel (geen cache) kunt too150 GB-bestanden. Optimalisatie van grote bestanden in de cache opgeslagen bestanden up too150 GB.

Optimalisatie van grote bestanden is van kracht wanneer bepaalde voorwaarden wordt voldaan. Voorwaarden omvatten de werking van de bronserver Hallo en Hallo grootten en typen Hallo-bestanden die worden aangevraagd. Voordat we naar meer informatie over deze onderwerpen sturen, moet u begrijpen hoe Hallo optimalisatie werkt. 

### <a name="object-chunking"></a>Object-verdeling in segmenten 

Hello Azure Content Delivery Network van Akamai maakt gebruik van een techniek die genoemd object verdeling in segmenten. Wanneer een groot bestand wordt aangevraagd, haalt Hallo CDN kleinere delen van Hallo bestand vanuit de oorsprong Hallo. Nadat het Hallo CDN edge/POP-server een volledige of bereik aan bytes bestand-aanvraag ontvangt, controleert deze of bestandstype hello wordt ondersteund voor deze optimalisatie. Controleert ook of Hallo bestandstype Hallo bestand grootte voldoet. Als het Hallo-bestand is groter dan 10 MB, Hallo CDN edge-server aanvragen Hallo bestand vanuit de oorsprong Hallo in segmenten van 2 MB. 

Nadat het Hallo-chunk bij Hallo CDN rand aankomt, heeft deze in de cache opgeslagen en onmiddellijk geleverd toohello gebruiker. Hallo CDN vervolgens prefetches Hallo volgende chunk parallel. Deze prefetch zorgt ervoor dat Hallo inhoud blijft één segment tevoren Hallo gebruiker, waardoor latentie. Dit proces gaat door totdat de hele Hallo bestand wordt gedownload (indien nodig), zijn alle bytereeksen beschikbaar (indien nodig), of als de client Hallo Hallo verbinding verbreekt. 

Zie voor meer informatie over Hallo bereik aan bytes aanvraag [RFC 7233](https://tools.ietf.org/html/rfc7233).

Hallo CDN plaatst alle segmenten als ze worden ontvangen. Hallo hele bestand heeft geen toobe in de cache op Hallo CDN-cache. De volgende aanvragen voor het bestand of byte adresbereiken Hallo zijn vanaf Hallo CDN cache bereikbaar. Als niet alle chunks met Hallo op Hallo CDN in cache zijn opgeslagen, is prefetch gebruikte toorequest segmenten vanuit Hallo oorsprong. Deze optimalisatie is afhankelijk van de mogelijkheid Hallo van Hallo oorsprong server toosupport byte-bereikaanvragen. _Als de bronserver Hallo biedt geen ondersteuning voor byte-bereikaanvragen, deze optimalisatie niet effectief._ 

### <a name="caching"></a>Caching
Optimalisatie van grote bestanden maakt gebruik van verschillende standaardtijden opslaan in cache verloopt uit algemene webtoepassingen levering. Het onderscheidt positieve caching en negatieve cache-opslag op basis van HTTP-antwoordcodes. Als de bronserver Hallo Hiermee geeft u een verlooptijd via een cache-control of expires-header in antwoord Hallo, respecteert Hallo CDN die waarde. Wanneer Hallo oorsprong niet opgeeft en Hallo bestand overeenkomt met Hallo type en de grootte van voorwaarden voor dit type optimalisatie, Hallo CDN Hallo standaardwaarden gebruikt voor optimalisatie van grote bestanden. Anders gebruikt Hallo CDN standaardinstellingen voor de levering van algemene webtoepassingen.


|    | Algemene webtoepassingen | Optimalisatie van grote bestanden 
--- | --- | --- 
Opslaan in cache: positief <br> HTTP 200, 203, 300, <br> 301, 302 en 410 | 7 dagen |1 dag  
Opslaan in cache: negatieve <br> HTTP 204 305 404, <br> en 405 | Geen | 1 seconde 

### <a name="deal-with-origin-failure"></a>Omgaan met fouten in de oorsprong

Hallo oorsprong lezen-timeout lengte neemt van twee seconden voor algemene webtoepassingen levering tootwo minuten voor het Hallo-optimalisatie van grote bestandstype. Deze toename is verantwoordelijk voor Hallo groter bestand grootten tooavoid een voortijdige time-out voor verbinding.

Wanneer een verbinding een optreedt time-out, pogingen Hallo CDN een aantal keren voordat een client '504 - Gateway timeout gegenereerd' fout toohello worden verzonden. 

### <a name="conditions-for-large-file-optimization"></a>Voorwaarden voor de optimalisatie van grote bestanden

Hallo volgende tabel geeft een lijst van Hallo set criteria toobe tevreden voor optimalisatie van grote bestanden:

Voorwaarde | Waarden 
--- | --- 
Ondersteunde bestandstypen | 3g, 2, 3gp, AVP, avi, bz2, dmg, exe, f4v, flv <br> GZ, hdp, iso, jxr, m4v, mkv, mov, mp4, <br> MPEG, mpg, mts, pkg, qt, DB, swf, tar, <br> tgz, wdp, webm, webp, wma, wmv, zip  
Minimale bestandsgrootte | 10 MB 
Maximale bestandsgrootte | 150 GB 
De kenmerken van een oorsprong | Byte-bereikaanvragen moet ondersteunen 

## <a name="optimize-for-delivery-of-large-files-with-hello-azure-content-delivery-network-from-verizon"></a>Voor het leveren van grote bestanden Hello Azure Content Delivery Network van Verizon optimaliseren

Hello Azure Content Delivery Network van Verizon biedt grote bestanden zonder een limiet op de bestandsgrootte. Aanvullende functies zijn ingeschakeld door standaard toomake levering van grote bestanden sneller.

### <a name="complete-cache-fill"></a>Volledige cache opvulling

Hallo standaard volledige opvulling cachefunctie kunt Hallo CDN toopull een bestand in cache Hallo als een eerste aanvraag is afgebroken of verbroken. 

Volledige cache opvulling is vooral handig voor grote activa. Normaal gesproken downloaden gebruikers niet van toofinish start. Ze gebruiken progressief downloaden. standaardgedrag Hallo Hallo edge server tooinitiate een ophaalbewerkingen van Hallo asset van de bronserver Hallo afgedwongen. Hallo asset is daarna in lokale cache Hallo rand van de server. Nadat de volledige object Hallo Hallo cache is, Hallo edge-server wordt voldaan aan bereik aan bytes aanvragen toohello CDN voor in de cache Hallo-object.

Hallo standaardgedrag kan worden uitgeschakeld via Hallo regels-Engine in Hallo Verizon Premium-laag.

### <a name="peer-cache-fill-hot-filing"></a>Peer-cache hot indiening vullen

Hallo peer-cache opvulling hot indiening standaardfunctie maakt gebruik van een geavanceerde eigen algoritme. Aanvullende edge cache servers op basis van bandbreedte wordt gebruikt en aggregatie vraagt metrische gegevens toofulfill clientaanvragen voor grote, maximaal populaire objecten. Deze functie wordt voorkomen dat een situatie waarin grote aantallen extra aanvragen bronserver tooa van de gebruiker worden verzonden. 

### <a name="conditions-for-large-file-optimization"></a>Voorwaarden voor de optimalisatie van grote bestanden

Hallo optimalisatiefuncties voor Verizon zijn standaard ingeschakeld. Er zijn geen limieten op de maximale grootte. 

## <a name="additional-considerations"></a>Aanvullende overwegingen

Houd rekening met Hallo aanvullende aspecten voor dit type optimalisatie te volgen.
 
### <a name="azure-content-delivery-network-from-akamai"></a>Azure Content Delivery Network van Akamai

- Hallo verdeling in segmenten proces genereert extra aanvragen toohello-bronserver. Hallo totale is hoeveelheid gegevens die worden geleverd vanuit de oorsprong Hallo echter veel kleiner. Chunking resulteert in betere cache in kenmerken op Hallo CDN.

- Omdat kleinere delen van Hallo-bestand worden afgeleverd worden bij de oorsprong Hallo geheugen en i/o-belasting gereduceerd.

- Voor segmenten in de cache opgeslagen op Hallo CDN, zijn er geen aanvullende aanvragen toohello oorsprong totdat Hallo inhoud verloopt of deze uit de cache Hallo onbeschikbaar wordt gemaakt.

- Gebruikers kunnen aanbrengen bereik toohello CDN aanvragen en ze worden behandeld als een normale bestand. Optimalisatie geldt alleen als het is een ongeldig bestandstype en Hallo bytebereik tussen 10 MB en 150 GB ligt. Als de gemiddelde bestandsgrootte Hallo aangevraagd kleiner is dan 10 MB, kunt u in plaats daarvan toouse algemene webtoepassingen levering.

### <a name="azure-content-delivery-network-from-verizon"></a>Azure Content Delivery Network van Verizon

Hallo algemene webtoepassingen bezorgingstype optimalisatie kan grote bestanden bieden.
