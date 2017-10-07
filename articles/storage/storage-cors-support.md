---
title: Ondersteuning voor aaaCross-Origin Resource delen (CORS) | Microsoft Docs
description: Meer informatie over hoe tooenable CORS-ondersteuning voor Hallo Microsoft Azure Storage-Services.
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Cross-Origin-Resource delen (CORS) ondersteuning voor hello Azure Storage-Services
Vanaf versie 2013-08-15, ondersteuning hello Azure storage-services Cross-Origin-Resource delen (CORS) voor de services Blob, Table, wachtrij en bestand Hallo. CORS is een HTTP-functie waarmee een webtoepassing die wordt uitgevoerd in een domein tooaccess resources in een ander domein. Webbrowsers implementeren een beveiligingsbeperkingen bekend als [dezelfde oorsprong beleid](http://www.w3.org/Security/wiki/Same_Origin_Policy) dat voorkomt dat een webpagina van aanroepen API's in een ander domein; CORS biedt een veilige manier tooallow één domein (Hallo brondomein) toocall API's in een ander domein. Zie Hallo [CORS-specificatie](http://www.w3.org/TR/cors/) voor meer informatie over CORS.

U kunt instellen CORS-regels afzonderlijk voor elk Hallo storage-services door het aanroepen van [Blob-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452235.aspx), [Queue-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452232.aspx), en [tabel-Service-eigenschappeninstellen](https://msdn.microsoft.com/library/hh452240.aspx). Als u Hallo CORS-regels voor Hallo service hebt ingesteld, klikt u vervolgens een correct geverifieerde aanvraag tegen Hallo-service uit een ander domein geëvalueerde toodetermine worden of het is toegestaan op basis van toohello regels die u hebt opgegeven.

> [!NOTE]
> Houd er rekening mee dat CORS niet een verificatiemethode is. Elk verzoek ten opzichte van een opslagresource wanneer CORS is ingeschakeld moet een handtekening van de juiste verificatiegegevens, of moet worden gemaakt op basis van een openbare resource.
> 
> 

## <a name="understanding-cors-requests"></a>Understanding CORS aanvragen
Een CORS-aanvraag van een brondomein kan bestaan uit twee afzonderlijke aanvragen:

* Een voorbereidende aanvraag, die Hallo CORS beperkingen die zijn opgelegd door Hallo-service. Hallo voorbereidende aanvraag is vereist, tenzij het Hallo-aanvraagmethode is een [eenvoudige methode](http://www.w3.org/TR/cors/), wat betekent dat GET, HEAD of POST.
* Hallo werkelijke aanvraag, ten opzichte van Hallo gewenste resource.

### <a name="preflight-request"></a>Voorbereidende aanvraag
Hallo voorbereidende aanvraag voor query's Hallo CORS-beperkingen die zijn gemaakt voor de opslagservice Hallo door de eigenaar van de Hallo-account. Hallo webbrowser (of andere gebruikersagent) stuurt u een aanvraag voor opties die aanvraagheaders Hallo bevat methode en de oorsprong domein. Hallo storage-service evalueert Hallo bedoeld-bewerking op basis van een vooraf geconfigureerde reeks CORS-regels die opgeven welke domeinen, request-methoden en aanvraagheaders mag worden opgegeven voor een werkelijke aanvraag tegen een opslagresource.

CORS voor Hallo-service is ingeschakeld en er is een CORS-regel die overeenkomt met de Hallo voorbereidende aanvraag, Hallo-service reageert met de statuscode 200 (OK) als Hallo vereist Access Control-headers Hallo reactie bevat.

Als CORS is niet ingeschakeld voor Hallo service of geen CORS-regel komt overeen met de Hallo voorbereidende aanvraag, reageert Hallo-service met de statuscode 403 (verboden).

Als Hallo opties aanvraag bevat geen hello vereist CORS-headers (Hallo oorsprong en Access Control-aanvraag methode headers), reageert Hallo-service met de statuscode 400 (ongeldige aanvraag).

Houd er rekening mee dat een aanvraag voor voorbereidende wordt geëvalueerd tegen Hallo-service (Blob, wachtrijen en tabellen) en niet op Hallo aangevraagde resource. Hallo accounteigenaar, moet CORS als onderdeel van Hallo account service-eigenschappen om Hallo aanvraag toosucceed hebt ingeschakeld.

### <a name="actual-request"></a>Werkelijke aanvraag
Als voorbereidende Hallo-aanvraag is geaccepteerd en Hallo antwoord wordt geretourneerd, betekent dit dat Hallo browser zorgt ervoor dat er Hallo werkelijke aanvraag tegen Hallo storage resource. Hallo browser weigert Hallo werkelijke aanvraag onmiddellijk als hello voorbereidende aanvraag wordt afgewezen.

werkelijke Hallo-aanvraag wordt beschouwd als normale aanvraag tegen Hallo storage-service. Hallo aanwezigheid van Hallo oorsprong header geeft aan dat Hallo-aanvraag een aanvraag voor CORS is en Hallo-service controleert Hallo die overeenkomt met CORS-regels. Als een overeenkomst wordt gevonden, zijn toegevoegd toohello antwoord Hallo Access Control-kop- en back toohello client verzonden. Als een overeenkomst niet gevonden is, worden niet Hallo CORS-toegangsbeheer-headers geretourneerd.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Inschakelen van CORS voor hello Azure Storage-services
CORS-regels zijn ingesteld op Hallo serviceniveau, zodat u tooenable moet- of uitschakelen van CORS voor elke service (Blob, Queue en tabel) afzonderlijk. CORS is standaard uitgeschakeld voor elke service. tooenable CORS, moet u tooset Hallo relevante service eigenschappen versie 2013-08-15 of hoger, en voeg CORS regels toohello service-eigenschappen. Voor meer informatie over het tooenable- of uitschakelen van CORS voor een service en hoe de tooset CORS is regels, neem te verwijzen[Blob-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452235.aspx), [Queue-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452232.aspx), en [tabel instellen Service-eigenschappen](https://msdn.microsoft.com/library/hh452240.aspx).

Hier volgt een voorbeeld van een enkele CORS-regel worden opgegeven via de bewerking van een Service-eigenschappen instellen:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Elk element opgenomen in Hallo CORS-regel wordt hieronder beschreven:

* **AllowedOrigins**: Hallo-domeinen die zijn toegestaan toomake een aanvraag in voor de opslag van Hallo service via CORS. Hallo brondomein is Hallo-domein van welke Hallo aanvraag afkomstig is. Houd er rekening mee dat Hallo oorsprong moet exact hoofdlettergevoelig overeenkomt met de Hallo oorsprong Hallo gebruiker leeftijd toohello service verzendt. U kunt ook Hallo jokerteken ' *' tooallow alle oorsprong domeinen toomake aanvragen via CORS. Hallo Hallo bovenstaande voorbeeld domeinen [http://www.contoso.com](http://www.contoso.com) en [http://www.fabrikam.com](http://www.fabrikam.com) aanvragen op basis van Hallo-service met behulp van CORS kunt maken.
* **AllowedMethods**: Hallo-methoden (HTTP-aanvraag verbs) dat domein van de oorsprong Hallo mag gebruiken voor een CORS-aanvraag. Hallo bovenstaande voorbeeld worden alleen PUT en GET-aanvragen toegestaan.
* **AllowedHeaders**: Hallo aanvraagheaders dat domein van de oorsprong Hallo mogelijk op Hallo CORS aanvraag opgeven. Hallo bovenstaande voorbeeld worden alle metagegevens headers beginnen met x-ms-metagegevens, x-ms-meta-doel en de x-ms-meta-abc toegestaan. Houd er rekening mee dat Hallo jokerteken ' *' geeft aan dat een koptekst die begint met de Hallo opgegeven voorvoegsel is toegestaan.
* **ExposedHeaders**: Hallo antwoordheaders die mogelijk in Hallo antwoord toohello CORS-aanvraag verzonden en beschikbaar gesteld door Hallo browser toohello aanvraag verlener. In voorbeeld hierboven Hallo browser Hallo is gebruiksaanwijzing tooexpose een koptekst die begint met x-ms-metagegevens.
* **MaxAgeInSeconds**: Hallo maximale hoeveelheid tijd dat in een browser moet cache Hallo voorbereidende OPTIONS-verzoek.

Hello Azure storage-services ondersteuning voor het opgeven van voorvoegsels headers voor beide Hallo **AllowedHeaders** en **ExposedHeaders** elementen. tooallow een categorie-headers, kunt u een algemene voorvoegsel toothat categorie opgeven. Bijvoorbeeld, geven *x-ms-meta** als een voorvoegsels koptekst bepaalt een regel die overeenkomen met alle headers die met x-ms-metagegevens beginnen.

Hallo volgen beperkingen toepassen tooCORS regels:

* Kunt u up toofive CORS-regels per storage-service (Blob, Table en Queue).
* maximale grootte van alle CORS-regelinstellingen op verzoek hello, met uitzondering van XML-labels Hallo mag niet meer dan 2 KB.
* Hallo-lengte van een toegestane koptekst, blootgestelde koptekst of toegestane oorsprong mag niet meer dan 256 tekens.
* Toegestane headers en blootgestelde headers kunnen zijn:
  * Letterlijke waar Hallo exacte header-naam is opgegeven, zoals kopteksten **x-ms-meta-verwerkte**. Een maximum van 64 letterlijke headers worden opgegeven op Hallo-aanvraag.
  * Headers, waarbij een voorvoegsel van Hallo-header is opgegeven, zoals het voorvoegsel **x-ms-meta-data***. Een voorvoegsel geven op deze manier kunt of een header die met het opgegeven voorvoegsel Hallo begint beschrijft. Maximaal twee voorvoegsels headers worden opgegeven op Hallo-aanvraag.
* Hallo-methoden (of HTTP-woorden) opgegeven in Hallo **AllowedMethods** element moet voldoen toohello-methoden die worden ondersteund door Azure storage-service API's. Ondersteunde methoden zijn verwijderd, GET, HEAD, samenvoegen, POST, opties en PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Understanding CORS regellogica evaluatie
Wanneer een storage-service een voorbereidende of werkelijke aanvraag ontvangt, evalueert deze die op basis van Hallo CORS regels die u hebt vastgesteld voor de service via de juiste Service-eigenschappen instellen bewerking Hallo Hallo aanvraag. CORS-regels worden geëvalueerd in Hallo volgorde waarin ze zijn ingesteld in de aanvraagtekst Hallo Hallo bewerking van de Service-eigenschappen instellen.

CORS-regels worden als volgt geëvalueerd:

1. Eerst brondomein Hallo van Hallo-aanvraag wordt vergeleken met de Hallo domeinen die worden vermeld voor Hallo **AllowedOrigins** element. Als Hallo brondomein is opgenomen in de lijst Hallo of alle domeinen zijn toegestaan met Hallo jokerteken ' *', vervolgens regels evaluatie voortgezet. Als het brondomein Hallo niet opgenomen is, mislukt Hallo aanvraag.
2. Vervolgens Hallo methode (of HTTP-term) van Hallo-aanvraag wordt vergeleken met de Hallo methoden in Hallo **AllowedMethods** element. Als het Hallo-methode is opgenomen in de lijst hello, door regels evaluatie; Als dat niet het geval is, mislukt Hallo-aanvraag.
3. Hallo-aanvraag komt overeen met een regel in het domein van de oorsprong en de bijbehorende methode, die regel is geselecteerde tooprocess Hallo aanvraag als er geen verdere regels worden geëvalueerd. Voordat het Hallo-aanvraag kan worden voltooid, echter op Hallo aanvraag opgegeven headers worden gecontroleerd tegen Hallo headers die worden vermeld in Hallo **AllowedHeaders** element. Als Hallo headers verzonden hello toegestaan headers niet overeenkomen, mislukt de Hallo-aanvraag.

Aangezien Hallo regels worden verwerkt in Hallo volgorde die in de aanvraagtekst Hallo aanwezig zijn, wordt aanbevolen dat u Hallo meest beperkende regels met respecteren tooorigins eerst in de lijst hello, opgeeft zodat deze worden eerst geëvalueerd. Geef regels die minder beperkend zijn – bijvoorbeeld een regel tooallow alle oorsprongen – achter Hallo Hallo-lijst.

### <a name="example--cors-rules-evaluation"></a>Voorbeeld: CORS regels evaluatie
Hallo volgende voorbeeld ziet u een gedeeltelijke aanvraagtekst voor een bewerking tooset CORS-regels voor Hallo storage-services. Zie [Blob-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452235.aspx), [Queue-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452232.aspx), en [tabel-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452240.aspx) voor meer informatie over het samenstellen van Hallo-aanvraag.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Vervolgens kunt u overwegen Hallo CORS-aanvragen te volgen:

| Aanvraag |  |  | Antwoord |  |
| --- | --- | --- | --- | --- |
| **Methode** |**Oorsprong** |**Aanvraagheaders** |**Regel overeen** |**Resultaat** |
| **PLAATSEN** |http://www.contoso.com |x-ms-blob-content-type |Eerste regel |Geslaagd |
| **TOEVOEGEN** |http://www.contoso.com |x-ms-blob-content-type |Tweede regel |Geslaagd |
| **TOEVOEGEN** |http://www.contoso.com |x-ms-client-request-id |Tweede regel |Fout |

de eerste aanvraag Hallo overeenkomt met de eerste regel Hallo – brondomein Hallo Hallo toegestane oorsprongen overeenkomt met, Hallo-methode overeenkomt met de Hallo toegestaan methoden en Hallo header komt overeen met de Hallo headers – toegestaan en dus slaagt.

tweede Hallo-aanvraag komt niet overeen met de eerste regel Hallo omdat Hallo methode komt niet overeen met de Hallo methoden toegestaan. Komt, echter overeen met de tweede regel hello, dus deze is voltooid.

Hallo derde aanvraag komt overeen met Hallo tweede regel in het brondomein en methode, zodat er geen verdere regels worden geëvalueerd. Hallo echter *header x-ms-client-request-id* is niet toegestaan door de tweede regel hello, zodat het Hallo-aanvraag mislukt, ondanks dat Hallo semantiek van de derde regel Hallo zou hebben mag het toosucceed Hallo-feit.

> [!NOTE]
> Hoewel dit voorbeeld ziet u een minder beperkend regel voordat een meer beperkend, is in het algemeen Hallo aanbevolen procedure toolist Hallo meest beperkende regels eerst.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Begrijpen hoe Hallo Vary-kop is ingesteld
Hallo *Vary* -header is een standaard HTTP/1.1-header die bestaan uit een set van aanvraag-headervelden die adviseer Hallo browser- of -agent over Hallo criteria die zijn geselecteerd door tooprocess Hallo-Hallo serveraanvraag. Hallo *Vary* koptekst wordt hoofdzakelijk gebruikt voor caching op proxy's, browsers en CDN die ermee toodetermine hoe Hallo antwoord moet worden opgeslagen in de cache. Zie voor meer informatie, Hallo-specificatie voor Hallo [Vary-kop](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Wanneer Hallo browser of een andere gebruikersagent in de cache antwoord van een aanvraag CORS Hallo opgeslagen, Hallo brondomein in cache wordt opgeslagen als Hallo oorsprong toegestaan. Wanneer een tweede domeinproblemen Hallo dezelfde aanvraag voor een opslagresource terwijl Hallo cache actief is, gebruikersagent Hallo Hallo in de cache brondomein opgehaald. Hallo tweede domein komt niet overeen met Hallo in de cache domein, zodat het Hallo-aanvraag mislukt wanneer het anders zou slagen. In bepaalde gevallen ingesteld Azure Storage Hallo Vary-kop te**oorsprong** tooinstruct Hallo gebruiker toosend Hallo daaropvolgende CORS aanvraag toohello agentservice wanneer Hallo aanvragen domein verschilt van Hallo oorsprong in de cache opgeslagen.

Azure-opslag stelt Hallo *Vary* header te**oorsprong** voor werkelijke GET/HEAD-aanvragen in de volgende gevallen Hallo:

* Hallo-aanvraag oorsprong exact overeenkomt met de Hallo toegestaan wanneer oorsprong gedefinieerd door een regel CORS. een exacte overeenkomst toobe, Hallo CORS regel mag bevatten een jokerteken ' * ' teken.
* Er is geen regel overeenkomende Hallo aanvraag oorsprong, maar CORS is ingeschakeld voor Hallo storage-service.

In geval Hallo waar een GET/HEAD-aanvraag komt overeen met een CORS-regel waarmee alle oorsprongen Hallo antwoord geeft aan dat alle oorsprongen zijn toegestaan, Hallo agent gebruikerscache volgende aanvragen van een domein van de oorsprong wordt toestaan terwijl Hallo cache actief is.

Houd er rekening mee dat voor aanvragen met behulp van andere methoden dan GET/HEAD, Hallo storage-services wordt niet ingesteld Hallo Vary-kop, omdat antwoorden toothese methoden niet in de cache door Gebruikeragents opgeslagen zijn.

Hallo volgende tabel geeft aan hoe Azure-opslag reageert tooGET/HEAD-aanvragen op basis van Hallo eerder genoemde gevallen:

| Aanvraag | Instellingen van een account en het resultaat van evaluatie van de regels |  |  | Antwoord |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Oorsprong header aanwezig is op verzoek** |**CORS (s) is opgegeven voor deze service** |**Overeenkomende regel bestaat waarmee alle oorsprongen (*)** |**Overeenkomende regel bestaat voor de oorsprong van de exacte overeenkomst** |**Antwoord bevat Vary-kop set tooOrigin** |**Antwoord bevat de Access Control-toegestaan-oorsprong: '*'** |**Antwoord bevat Access-Control-blootgesteld-kopteksten** |
| Nee |Nee |Nee |Nee |Nee |Nee |Nee |
| Nee |Ja |Nee |Nee |Ja |Nee |Nee |
| Nee |Ja |Ja |Nee |Nee |Ja |Ja |
| Ja |Nee |Nee |Nee |Nee |Nee |Nee |
| Ja |Ja |Nee |Ja |Ja |Nee |Ja |
| Ja |Ja |Nee |Nee |Ja |Nee |Nee |
| Ja |Ja |Ja |Nee |Nee |Ja |Ja |

## <a name="billing-for-cors-requests"></a>Facturering voor CORS aanvragen
Geslaagde preflight aanvragen worden gefactureerd als u CORS voor een van de opslagservices Hallo voor uw account hebt ingeschakeld (door het aanroepen van [Blob-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452235.aspx), [Queue-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452232.aspx), of [ Tabel-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize kosten, overwegen in te stellen Hallo **MaxAgeInSeconds** -element in de CORS tooa grote waarde regels zodat hello gebruikersagent caches Hallo-aanvraag.

Mislukte voorbereidende aanvragen worden niet gefactureerd.

## <a name="next-steps"></a>Volgende stappen
[Eigenschappen van de Blob-Service instellen](https://msdn.microsoft.com/library/hh452235.aspx)

[Wachtrij-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452232.aspx)

[Tabel-Service-eigenschappen instellen](https://msdn.microsoft.com/library/hh452240.aspx)

[W3C Cross-Origin Resource Sharing specificatie](http://www.w3.org/TR/cors/)

