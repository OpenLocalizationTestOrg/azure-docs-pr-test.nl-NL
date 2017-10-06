---
title: Azure CDN met CORS aaaUsing | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure Content Delivery Network (CDN) toowith Cross-Origin-Resource delen (CORS).
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Azure CDN gebruiken met CORS
## <a name="what-is-cors"></a>Wat is CORS?
CORS (Cross Origin Resource Sharing) is een HTTP-functie waarmee een webtoepassing die wordt uitgevoerd in een domein tooaccess resources in een ander domein. Alle moderne webbrowsers implementeren volgorde tooreduce Hallo mogelijkheid van cross-site scripting aanvallen, een beveiligingsbeperkingen bekend als [dezelfde oorsprong beleid](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Dit voorkomt dat een webpagina van aanroepen API's in een ander domein.  CORS biedt een veilige manier tooallow één oorsprong (Hallo brondomein) toocall API's in een andere bron.

## <a name="how-it-works"></a>Hoe werkt het?
Er zijn twee soorten CORS aanvragen, *eenvoudige aanvragen* en *complexe aanvragen.*

### <a name="for-simple-requests"></a>Voor eenvoudige aanvragen:

1. Hallo browser verzendt Hallo CORS-aanvraag met een extra **oorsprong** header HTTP-aanvraag. Hallo-waarde van deze header is Hallo oorsprong die behandeld Hallo bovenliggende pagina die wordt gedefinieerd als Hallo combinatie van *protocol* *domein,* en *poort.*  Wanneer een pagina uit https://www.contoso.com tooaccess gebruikersgegevens in Hallo fabrikam.com oorsprong probeert, zou Hallo aanvraagheader na toofabrikam.com worden verzonden:

   `Origin: https://www.contoso.com`

2. Hallo-server reageert met een van de volgende Hallo:

   * Een **Access Control-toestaan-oorsprong** header in zijn reactie waarmee wordt aangegeven welke bronsite is toegestaan. Bijvoorbeeld:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Een HTTP-fout 403 code als Hallo server staat niet toe dat Hallo cross-origin-aanvraag na Hallo oorsprong header controleren

   * Een **Access Control-toestaan-oorsprong** koptekst met een jokerteken waarmee alle oorsprongen:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Voor complexe aanvragen:

Een complexe aanvraag is een aanvraag CORS waarbij Hallo browser vereist toosend een *voorbereidende aanvraag* (dat wil zeggen een voorlopige test) voordat Hallo werkelijke CORS-aanvraag wordt verzonden. Hallo voorbereidende aanvraag Hallo-server om toestemming wordt gevraagd als Hallo oorspronkelijke CORS-aanvraag kan worden voortgezet en wordt een `OPTIONS` toohello aanvragen dezelfde URL.

> [!TIP]
> Voor meer informatie over de CORS-stromen en verrassingen, bekijkt hello [tooCORS handleiding voor de REST-API's](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Jokertekens of één oorsprong scenario 's
CORS op Azure CDN werkt automatisch zonder aanvullende configuratie wanneer hello **Access Control-toestaan-oorsprong** header toowildcard (*) of een enkel oorsprong is ingesteld.  Hallo CDN cache worden opgeslagen door de eerste antwoord Hallo en het gebruik van de volgende aanvragen Hallo dezelfde kop.

Als aanvragen al toohello CDN eerdere tooCORS wordt ingesteld op Hallo van uw oorsprong aangebracht zijn, moet u toopurge inhoud op uw eindpunt inhoud tooreload Hallo inhoud Hello **Access Control-toestaan-oorsprong** header.

## <a name="multiple-origin-scenarios"></a>Scenario's met meerdere oorsprong
Als u een specifieke lijst met oorsprongen toobe toegestaan voor CORS tooallow moet, ophalen dingen iets gecompliceerder. Hallo probleem treedt op wanneer Hallo CDN in de cache Hallo opgeslagen **Access Control-toestaan-oorsprong** -header voor de eerste CORS-oorsprong Hallo.  Wanneer een andere CORS-oorsprong een volgende aanvraag indient, Hallo CDN Hallo in de cache opgeslagen fungeert **Access Control-toestaan-oorsprong** koptekst, die niet overeen met.  Er zijn verschillende manieren toocorrect dit.

### <a name="azure-cdn-premium-from-verizon"></a>Azure CDN Premium van Verizon
Hallo van de beste manier tooenable dit toouse is **Azure CDN Premium van Verizon**, die beschrijft sommige geavanceerde functies. 

Je hebt te[maakt u een regel](cdn-rules-engine.md) toocheck hello **oorsprong** header op Hallo-aanvraag.  Als het een geldige oorsprong, Hallo wordt ingesteld door de regel **Access Control-toestaan-oorsprong** header met Hallo oorsprong in het Hallo-aanvraag.  Als Hallo oorsprong in Hallo opgegeven **oorsprong** header is niet toegestaan, de regel moet Hallo weglaten **Access Control-toestaan-oorsprong** header waardoor Hallo browser tooreject Hallo aanvraag. 

Er zijn twee manieren toodo dit met de Hallo regelengine.  In beide gevallen Hallo **Access Control-toestaan-oorsprong** koptekst van de bronserver Hallo-bestand volledig wordt genegeerd, Hallo CDN van regelengine beheert volledig Hallo CORS oorsprongen toegestaan.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Een reguliere expressie met alle geldige oorsprongen
In dit geval maakt u een reguliere expressie waarin alle oorsprongen Hallo gewenste tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **Azure CDN van Verizon** gebruikt [Perl compatibel reguliere expressies](http://pcre.org/) als de engine voor reguliere expressies.  U kunt een hulpprogramma zoals [reguliere expressies 101](https://regex101.com/) toovalidate uw reguliere expressie.  Let op: Hallo ' / ' teken is geldig in reguliere expressies en hoeft niet toobe escape-teken, echter escape-teken wordt beschouwd als een best practice en wordt verwacht door sommige validatiefuncties regex.
> 
> 

Indien de reguliere expressie Hallo overeenkomt, de regel Hallo vervangt **Access Control-toestaan-oorsprong** header (indien aanwezig) van de oorsprong van Hallo met Hallo oorsprong die Hallo-aanvraag heeft verzonden.  U kunt ook aanvullende CORS-kopteksten, zoals toevoegen **-besturingselement-toestaan-toegangsmethoden**.

![Voorbeeld van de regels met de reguliere expressie](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Aanvraag-header-regel voor elke oorsprong.
In plaats van reguliere expressies, kunt u in plaats daarvan een afzonderlijke maken regel voor oorsprong van elke gewenste tooallow met Hallo **aanvraag-Header jokertekens** [overeenkomen met de voorwaarde](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Als engine Hallo regels met Hallo reguliere expressie methode alleen sets Hallo CORS headers. 

![Voorbeeld van de regels zonder reguliere expressie](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> Hallo Hallo bovenstaande voorbeeld gebruik van Hallo jokerteken * vertelt Hallo regels engine toomatch HTTP en HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Azure CDN Standard
Hallo op Azure CDN Standard profielen alleen tooallow mechanisme voor meerdere oorsprongen zonder het gebruik van Hallo jokertekens oorsprong Hallo toouse is [query opslaan in cache](cdn-query-string.md).  U moet tooenable query-tekenreeks instelling voor Hallo CDN-eindpunt en een unieke queryreeks vervolgens gebruiken voor aanvragen van elk domein. Dit leidt tot Hallo CDN in cache plaatsen van een afzonderlijk object voor elke unieke queryreeks. Deze aanpak is niet ideaal, echter als het zal leiden tot meerdere exemplaren van Hallo hetzelfde bestand in cache op Hallo CDN.  

