---
title: aaaMedia optimalisatie via hello Azure Content Delivery Network streaming
description: Optimaliseren voor de levering van smooth streaming media-bestanden
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
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Optimalisatie via hello Azure Content Delivery Network streaming media 
 
Gebruik van hoogwaardige video neemt op Hallo Internet; dit problemen voor de levering van efficiënte van grote bestanden maakt. Klanten verwachten smooth afspelen van video op aanvraag of live video activa op tal van netwerken en clients over Hallo wereld. Een snelle en efficiënte bezorgingsmechanisme voor media streaming-bestanden is essentieel tooensure een consumer smooth en uitmuntende ervaring.  

Live streaming media is uiterst moeilijk toodeliver vanwege de grote Hallo-grootten en het aantal gelijktijdige gebruikers. Lange vertragingen veroorzaken tooleave van gebruikers. Omdat live gegevensstromen tevoren kunnen niet worden opgeslagen en grote latenties niet acceptabel tooviewers, moeten video fragmenten tijdig worden geleverd. 

Hallo aanvraag patronen van streaming bieden ook enkele nieuwe uitdagingen. Wanneer een populaire live stream of een nieuwe reeks wordt vrijgegeven voor video op aanvraag, duizenden toomillions kijkers vragen om Hallo stream op Hallo hetzelfde moment. In dit geval overbelast smart aanvraag consolidatie is essentieel toonot Hallo oorsprong servers wanneer Hallo activa zijn niet opgeslagen in de cache nog.
 
Hello Azure Content Delivery Network van Akamai biedt nu een functie die zorgt voor streaming media activa efficiënt toousers over de hele Hallo wereld op grote schaal. Hallo functie vermindert latenties omdat het Hallo-belasting op Hallo oorsprong servers vermindert. Deze functie is beschikbaar met Hallo Standard van Akamai prijscategorie. 

Hello Azure Content Delivery Network van Verizon biedt mediagegevensstromen rechtstreeks in Hallo algemene webtoepassingen bezorgingstype optimalisatie.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Een eindpunt toooptimize mediastreaming in hello Azure Content Delivery Network van Akamai configureren
 
U kunt uw content delivery network (CDN) eindpunt toooptimize leveringsmethode voor grote bestanden via hello Azure-portal configureren. U kunt ook onze REST-API's gebruiken of een van de client SDK's toodo Hallo dit. Hallo volgt Hallo proces weergeven via hello Azure-portal:

1. een nieuw eindpunt, klikt u op Hallo tooadd **CDN-profiel** pagina **eindpunt**.
  
    ![Nieuwe endpoint](./media/cdn-media-streaming-optimization/01_Adding.png)

2. In Hallo **geoptimaliseerd voor** vervolgkeuzelijst, selecteer **Video op aanvraag mediastreaming** voor video-on-demand activa. Als u een combinatie van live en video-on-demand streaming doen, selecteert u **algemene mediastreaming**.

    ![Streaming geselecteerd](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Nadat u Hallo eindpunt hebt gemaakt, toepassing hello optimalisatie voor alle bestanden die aan bepaalde criteria voldoen. Hallo volgende sectie wordt beschreven dit proces. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Optimalisaties voor hello Azure Content Delivery Network van Akamai streaming media
 
Streaming optimalisatie van Akamai geschikt voor live is-Media of video-on-demand mediagegevensstromen die gebruikmaakt van afzonderlijke media fragmenten voor de levering van. Dit proces wijkt af van een enkel grote actief worden overgedragen via progressief downloaden of met behulp van de byte-bereikaanvragen. Zie voor informatie over deze stijl media leveringsmethode, [groot bestand optimalisatie](cdn-large-file-optimization.md).


Hallo algemene levering of video-on-demand media levering optimalisatie mediatypen gebruiken een CDN met back-end-optimalisaties toodeliver media activa sneller. Ze ook configuraties gebruiken voor media activa op basis van aanbevolen procedures geleerd gedurende een bepaalde periode.

### <a name="caching"></a>Caching

Als hello Azure Content Delivery Network van Akamai dat actief Hallo detecteert streaming manifest- of fragmentdeel, gebruikt deze verschillende tijdstippen in de cache verloopt uit algemene webtoepassingen levering. (Zie de volledige lijst in de volgende tabel Hallo Hallo.) Zoals altijd worden cache-control of Expires-koppen verzonden vanuit de oorsprong Hallo gehonoreerd. Als Hallo asset niet een activum media, slaat het via Hallo verlopen tijden voor de levering van algemene webtoepassingen.

Hallo korte negatieve cache tijd is nuttig voor de oorsprong offload wanneer veel gebruikers vragen een fragment dat nog niet bestaat. Een voorbeeld is een live stream waar hello-pakketten zijn niet beschikbaar vanuit de oorsprong Hallo die seconde. meer in het cachegeheugen Hello-interval helpt ook bij het aanvragen van de oorsprong Hallo offload omdat video-inhoud doorgaans niet is gewijzigd.
 

|    | Algemeen<br> Web<br>levering | Algemeen<br> media<br> streaming | Video-on-demand <br>media<br> streaming  
--- | --- | --- | ---
Opslaan in cache: positief <br> HTTP 200, 203, 300, <br> 301, 302 en 410 | 7 dagen |365 dagen | 365 dagen   
Opslaan in cache: negatieve <br> HTTP 204 305 404, <br> en 405 | Geen | 1 seconde | 1 seconde
 
### <a name="deal-with-origin-failure"></a>Omgaan met fouten in de oorsprong  

Algemene media leveren en video-on-demand media leveren ook hebben oorsprong time-out en het logboek opnieuw op basis van best practices voor typische aanvraag patronen. Bijvoorbeeld, omdat algemene media leveren voor live en video-on-demand media leveren, een kortere verbindingstime-out vanwege toohello tijdgebonden aard van wordt live streamen.

Wanneer een verbinding een optreedt time-out, pogingen Hallo CDN een aantal keren voordat een client '504 - Gateway timeout gegenereerd' fout toohello worden verzonden. 

Wanneer een bestand overeenkomt met Hallo type en willekeurige grootte voorwaarden bestandenlijst, Hallo CDN Hallo gedrag gebruikt voor streaming media. Anders gebruikt het algemene webtoepassingen levering.
   
### <a name="conditions-for-media-streaming-optimization"></a>Voorwaarden voor de optimalisatie van mediastreaming 

Hallo volgende tabel geeft een lijst van Hallo set criteria toobe tevreden voor optimalisatie van mediastreaming: 
 
Ondersteunde typen streaming | Bestandsextensies  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, key, ts, aac
Adobe harde schijven | f4m, f4x, drmmeta, bootstrap, f4f,<br>URL totaal aantal segmenten-structuur <br> (die overeenkomen met de reguliere expressie: ^(/.*)Seq(\d+)-Frag(\d+)
STREEPJE | MPD, streepjes, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
Smooth streaming | / manifest /, QualityLevels/fragmenten /
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Optimalisaties voor hello Azure Content Delivery Network van Verizon streaming media

streaming media activa biedt Hello Azure Content Delivery Network van Verizon via Hallo algemene webtoepassingen bezorgingstype optimalisatie. Enkele onderdelen op Hallo CDN dat rechtstreeks helpt bij het leveren van media-elementen standaard.

### <a name="partial-cache-sharing"></a>Gedeeltelijke cache delen

Gedeeltelijke cache delen kan Hallo CDN tooserve gedeeltelijk in cache opgeslagen inhoud toonew aanvragen. Als Hallo eerste aanvraag toohello CDN in een cache ontbreekt resulteert, wordt Hallo aanvraag toohello oorsprong verzonden. Hoewel deze onvolledige inhoud in Hallo CDN-cache wordt geladen, kunt andere aanvragen toohello CDN beginnen met deze gegevens ophalen. 

### <a name="cache-fill-wait-time"></a>Cache opvulling wachttijd

 Hallo opvulling wacht tijd cachefunctie dwingt Hallo edge server toohold daaropvolgende verzoeken voor dezelfde resource Hallo tot HTTP-antwoord headers van de bronserver Hallo binnenkomen. Als HTTP-antwoordheaders vanuit de oorsprong Hallo plaatsvinden voordat Hallo timer verloopt, worden alle aanvragen die zijn in de wachtstand plaatsen buiten Hallo groeiende cache geleverd. Op Hallo dezelfde tijdstip, hello cache met gegevens vanuit de oorsprong Hallo is gevuld. Standaard is Hallo cache opvulling wachttijd too3, 000 milliseconden ingesteld. 

