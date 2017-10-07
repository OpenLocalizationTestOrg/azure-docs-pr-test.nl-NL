---
title: aaaAzure CDN regels engine functies | Microsoft Docs
description: Documentatie bij Azure CDN regels overeen motor en onderdelen.
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Functies in de engine Azure CDN-regels
Dit onderwerp vindt u gedetailleerde beschrijvingen van de beschikbare functies Hallo voor Azure Content Delivery Network (CDN) [regelengine](cdn-rules-engine.md).

Hallo derde onderdeel van een regel is Hallo-functie. Een functie definieert Hallo type actie die wordt toegepast toohello type aanvraag geïdentificeerd door een set voorwaarden van de overeenkomst.

## <a name="access"></a>Toegang

Deze functies zijn ontworpen toocontrol toegang toocontent.


Naam | Doel
-----|--------
Toegang weigeren | Hiermee bepaalt u of alle aanvragen zijn afgewezen met een 403-verboden-antwoord.
Token Auth | Hiermee wordt bepaald of verificatie op basis van tokens toegepaste tooa aanvraag.
Token Auth DOS-Code | Hallo-type van het antwoord dat tooa gebruiker moet worden geretourneerd wanneer een aanvraag wordt geweigerd vanwege tooToken gebaseerde verificatie bepaalt.
Token Auth hoofdlettergevoeligheid niet van belang URL | Hiermee wordt bepaald of URL vergelijkingen aangebracht door verificatie op basis van tokens hoofdlettergevoelig zijn.
Token Auth-Parameter | Hiermee wordt bepaald of Hallo verificatie op basis van tokens querytekenreeksparameter moet worden gewijzigd.

### <a name="deny-access"></a>Toegang weigeren
**Doel**: Hiermee bepaalt u of alle aanvragen zijn afgewezen met een 403-verboden-antwoord.

Waarde | Resultaat
------|-------
Ingeschakeld| Zorgt ervoor dat alle aanvragen die voldoen aan Hallo overeenkomende criteria toobe geweigerd met een 403-verboden-antwoord.
Uitgeschakeld| Hallo standaardgedrag herstelt. Hallo standaardgedrag is tooallow Hallo oorsprong toodetermine Hallo servertype antwoord dat wordt geretourneerd.

**Standaardgedrag**: uitgeschakeld

> [!TIP]
   > Een mogelijke gebruik voor deze functie is tooassociate deze met een aanvraag-Header voorwaarde tooblock toegang tooHTTP verwijzende sites die gebruikmaken van inline koppelingen tooyour inhoud overeenkomen.

### <a name="token-auth"></a>Token Auth
**Doel:** Hiermee wordt bepaald of verificatie op basis van tokens toegepaste tooa aanvraag.

Als verificatie op basis van het Token is ingeschakeld, wordt alleen aanvragen die een gecodeerde token bieden en te voldoen toohello vereisten die zijn opgegeven in die worden uitgevoerd.

Hallo-versleutelingssleutel die wordt gebruikt tooencrypt en ontsleutelen token waarden wordt bepaald door de primaire sleutel en de sleutel van de back-up-opties op de pagina Token Auth. Houd er rekening mee dat versleutelingssleutels platform-specifieke.

Waarde | Resultaat
------|---------
Ingeschakeld | Beveiligt Hallo aangevraagde inhoud met verificatie op basis van tokens. Alleen aanvragen van clients die voorzien van een geldig token en voldoen aan de vereisten gehonoreerd. FTP-transacties zijn uitgesloten van verificatie op basis van tokens.
Uitgeschakeld| Hallo standaardgedrag herstelt. standaardgedrag Hallo tooallow is uw toodetermine van de configuratie van verificatie op basis van tokens of een aanvraag worden beveiligd.

**Standaardgedrag:** uitgeschakeld.

###<a name="token-auth-denial-code"></a>Token Auth DOS-Code
**Doel:** bepaalt Hallo type antwoord dat wordt geretourneerd tooa gebruiker wanneer een aanvraag wordt geweigerd vanwege tooToken gebaseerde verificatie.

Hallo beschikbaar reactiecodes worden hieronder vermeld.

Antwoordcode|De naam van de reactie|Beschrijving
----------------|-----------|--------
301|Permanent verplaatst|Deze statuscode leidt onbevoegde gebruikers toohello URL die is opgegeven in de locatie-header.
302|Gevonden|Deze statuscode leidt onbevoegde gebruikers toohello URL die is opgegeven in de locatie-header. Deze statuscode is Hallo-industrienorm van de uitvoering van een omleiding.
307|Tijdelijke omleiding|Deze statuscode leidt onbevoegde gebruikers toohello URL die is opgegeven in de locatie-header.
401|Niet geautoriseerd|Deze statuscode combineren met de reactie WWW-Authenticate-header kunt u tooprompt een gebruiker voor verificatie.
403|Is niet toegestaan|Dit is Hallo standaard 403 verboden statusbericht dat een onbevoegde gebruiker ziet wanneer tooaccess probeert van beveiligde inhoud.
404|Bestand is niet gevonden|Deze statuscode geeft aan dat Hallo HTTP-client kunnen toocommunicate met Hallo-server is, maar Hallo aangevraagde inhoud is niet gevonden.

#### <a name="url-redirection"></a>URL-omleiding

Deze functie ondersteunt URL omleiding tooa gebruiker gedefinieerde URL wanneer het geconfigureerde tooreturn 3xx statuscode. Deze door de gebruiker gedefinieerde URL kan worden opgegeven door Hallo volgende stappen uit te voeren:

1. Selecteer een antwoordcode 3xx voor Hallo Token autorisatiecode DOS-functie.
2. Selecteer 'Locatie' in de optie optionele Header-naam.
3. De optionele waarde voor Header optie toohello gewenst URL ingesteld.

Als een URL is niet gedefinieerd voor een statuscode 3xx, vervolgens hello standaard antwoordpagina voor een 3xx statuscode geretourneerd toohello gebruiker.

URL-doorverwijzing is alleen van toepassing voor 3xx responscodes.

De optie optioneel Header-waarde ondersteunt alfanumerieke tekens, aanhalingstekens en spaties.

#### <a name="authentication"></a>Authentication

Deze functie ondersteunt Hallo mogelijkheid tooinclude de WWW-verificatie header wanneer reageert tooan ongeautoriseerde aanvraag voor inhoud die is beveiligd door verificatie op basis van tokens. Als de WWW-Authenticate-header is te 'basic' in de configuratie ingesteld, wordt voor accountreferenties Hallo onbevoegde gebruikers gevraagd.

Hallo hierboven configuratie kan worden bereikt door Hallo volgende stappen uit te voeren:

1. Selecteer '401' als Hallo antwoordcode voor Hallo Token autorisatiecode DOS-functie.
2. Selecteer 'WWW ' verificatie van de optionele naam van de Header-optie.
3. Stelt u de optie optioneel headerwaarde te 'basic'.

De WWW-Authenticate-header is alleen van toepassing op 401 responscodes.

### <a name="token-auth-ignore-url-case"></a>Token Auth hoofdlettergevoeligheid niet van belang URL
**Doel:** bepaalt u of URL vergelijkingen aangebracht door verificatie op basis van tokens hoofdlettergevoelig zijn.

Deze functie van invloed op Hallo-parameters zijn:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Geldige waarden zijn:

Waarde|Resultaat
---|----
Ingeschakeld|Zorgt ervoor dat de edge-server tooignore geval bij het vergelijken van URL's voor de parameters voor verificatie op basis van tokens.
Uitgeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is voor de URL vergelijkingen voor tokenverificatie toobe hoofdlettergevoelig.

**Standaardgedrag:** uitgeschakeld.
 
### <a name="token-auth-parameter"></a>Token Auth-Parameter
**Doel:** bepaalt of Hallo verificatie op basis van tokens querytekenreeksparameter moet worden gewijzigd.

Belangrijke informatie:

- De optie waarde definieert Hallo parameternaam van querytekenreeks waarmee een token worden opgegeven.
- De optie waarde te kan niet worden ingesteld 'ec_token'.
- Zorg ervoor dat Hallo naam zijn gedefinieerd in de optie waarde 
- geldige URL-tekens bevat.

Waarde|Resultaat
----|----
Ingeschakeld|De optie waarde definieert Hallo parameternaam van querytekenreeks waarmee tokens moeten worden gedefinieerd.
Uitgeschakeld|Een token kan worden opgegeven als een niet-gedefinieerde querytekenreeksparameter in Hallo aanvraag-URL.

**Standaardgedrag:** uitgeschakeld. Een token kan worden opgegeven als een niet-gedefinieerde querytekenreeksparameter in Hallo aanvraag-URL.

## <a name="caching"></a>Caching

Deze functies zijn ontworpen toocustomize wanneer en hoe de inhoud in cache wordt opgeslagen.

Naam | Doel
-----|--------
Bandbreedte-Parameters | Hiermee wordt bepaald of parameters (dat wil zeggen, ec_rate en ec_prebuf) voor bandbreedteregeling actief zijn.
Bandbreedtebeperking | Hallo bandbreedte voor Hallo respons van onze randservers bandbreedte.
De Bypass-Cache | Hiermee wordt bepaald of Hallo aanvragen van onze caching-technologie gebruikmaken kan.
Cache-Control Header behandeling | Besturingselementen Hallo generatie van Cache-Control headers door Hallo edge-server als onderdeel van de externe maximumleeftijd actief is.
Cache-sleutel queryreeks | Hiermee wordt bepaald of Hallo Cachesleutel wordt opnemen of uitsluiten van queryreeksparameters die zijn gekoppeld aan een aanvraag.
Cache-sleutel opnieuw schrijven | Herschrijft Hallo cache-sleutel die is gekoppeld aan een aanvraag.
Voltooien van de opvulling van de Cache | Hiermee bepaalt u wat er gebeurt wanneer een aanvraag resulteert in een gedeeltelijke Cachemisser op een edge-server.
Bestandstypen comprimeren | Hallo-bestandsindelingen die zal worden gecomprimeerd definieert op Hallo-server.
Standaard interne-maximumleeftijd | Hallo standaard maximumleeftijd interval voor edge server tooorigin server cache hervalidatie bepaald.
Koptekst behandeling verloopt | Besturingselementen Hallo Expires-koppen worden gegenereerd door een edge-server als Hallo externe maximumleeftijd functie actief is.
Externe maximumleeftijd | Hallo maximumleeftijd interval voor de browser tooedge server cache hervalidatie bepaald.
Interne maximumleeftijd forceren | Hallo maximumleeftijd interval voor edge server tooorigin server cache hervalidatie bepaald.
H.264-ondersteuning (http-progressief downloaden) | Hiermee wordt bepaald Hallo typen H.264 bestandsindelingen die mogelijk gebruikte toostream inhoud.
EEr No-Cache-aanvraag | Hiermee wordt bepaald of op Nee-cache-aanvragen van een HTTP-client toohello bronserver zal worden doorgestuurd.
Negeren oorsprong No-Cache | Hiermee wordt bepaald of onze CDN bepaalde geleverd van een bronserver richtlijnen worden genegeerd.
Ongeldig bereiken negeren | Hiermee wordt bepaald Hallo-antwoord dat wordt geretourneerd tooclients wanneer een aanvraag statuscode 416 aangevraagd bereik niet geldig genereert.
Interne Max-verouderd | Hiermee wordt bepaald hoe lang het verleden normale verlooptijd Hallo een activum in de cache kan worden geleverd vanuit een edge-server wanneer Hallo edge-server niet kan toorevalidate Hallo in de cache asset met de bronserver Hallo.
Gedeeltelijke Cache delen | Hiermee wordt bepaald of een aanvraag deels in cache opgeslagen inhoud kan genereren.
De inhoud in cache prevalidate | Hiermee wordt bepaald of de inhoud in cache in aanmerking komen voor vroege hervalidatie voordat de TTL verloopt.
Vernieuwen van nul bytes cachebestanden | Hiermee wordt bepaald hoe van de client van een HTTP-aanvraag voor een asset 0-byte-cache wordt verwerkt door onze randservers.
Statuscodes voor caching geschikte instellen | Definieert de set Hallo van statuscodes die tot de inhoud in cache leiden kunnen.
Verouderde Contentlevering bij fout | Bepaalt of verlopen in de cache inhoud wordt geleverd als een fout optreedt tijdens de hervalidatie van de cache of wanneer ophalen Hallo inhoud aangevraagd bij de bronserver Hallo-klant.
Verouderde tijdens Revalidate | Verbetert de prestaties doordat onze randservers tooserve verouderde client toohello aanvrager terwijl hervalidatie plaatsvindt.
Opmerking | Hallo Opmerking functie kunt een opmerking toobe binnen een regel toegevoegd.

###<a name="bandwidth-parameters"></a>Bandbreedte-Parameters
**Doel:** bepaalt of parameters (dat wil zeggen, ec_rate en ec_prebuf) voor bandbreedteregeling actief zijn.

Bandbreedte, snelheidsbeperking parameters bepalen of Hallo overdrachtssnelheid van gegevens voor de aanvraag van een client beperkt tooa aangepaste snelheid wordt.

Waarde|Resultaat
--|--
Ingeschakeld|Onze randservers kunt toohonor-aanvragen voor bandbreedteregeling.
Uitgeschakeld|Zorgt ervoor dat onze randservers tooignore-parameters voor bandbreedteregeling. Hallo aangevraagde inhoud wordt normaal gesproken worden geleverd (dat wil zeggen, zonder bandbreedtebeperking).

**Standaardgedrag:** ingeschakeld.

###<a name="bandwidth-throttling"></a>Bandbreedtebeperking
**Doel:** vertragingen Hallo bandbreedte voor Hallo respons van onze randservers.

Beide opties na Hallo moet gedefinieerde tooproperly bandbreedtebeperking instellen.

Optie|Beschrijving
--|--
KB per seconde|Stel deze optie toohello maximale bandbreedte (in Kb per seconde) die mogelijk antwoord van de Hallo gebruikte toodeliver.
Prebuf seconden|Stel deze optie toohello aantal seconden dat onze randservers tot de bandbreedteregeling bandbreedte gewacht. Hallo-doel van deze periode van de bandbreedte onbeperkt is tooprevent een mediaspeler van haperingen of problemen vanwege toobandwidth beperking buffer.

**Standaardgedrag:** uitgeschakeld.

###<a name="bypass-cache"></a>De Bypass-Cache
**Doel:** bepaalt of Hallo aanvragen van onze caching-technologie gebruikmaken kan.

Waarde|Resultaat
--|--
Ingeschakeld|Zorgt ervoor dat alle aanvragen toofall via toohello-bronserver, zelfs als het Hallo-inhoud is eerder in de cache op de edge-servers.
Uitgeschakeld|Zorgt ervoor dat randservers toocache activa volgens toohello cachebeleid is gedefinieerd in de antwoordheaders.

**Standaardgedrag:**

- **Grote HTTP:** uitgeschakeld

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Cache-Control Header behandeling
**Doel:** Hallo generatie van Cache-Control headers door Hallo edge-server bepaalt wanneer externe maximumleeftijd functie actief is.

Hallo gemakkelijkste manier tooachieve dit type configuratie is tooplace Hallo externe maximumleeftijd en Hallo Cache-Control Header behandeling functies in dezelfde instructie Hallo.

Waarde|Resultaat
--|--
Overschrijven|Zorgt ervoor dat de volgende activiteiten Hallo vindt plaats:<br/> -De header van de Cache-Control die worden gegenereerd door de bronserver Hallo overschrijft. <br/>-Voegt de header van de Cache-Control die wordt geproduceerd door Hallo externe maximumleeftijd functie toohello antwoord.
Doorgeven|Zorgt ervoor dat de header van de Cache-Control geproduceerd door Hallo externe maximumleeftijd functie nooit toohello antwoord is toegevoegd. <br/> Als de bronserver Hallo een Cache-Control-header ontstaat, worden door eindgebruikers toohello doorgegeven. <br/> Als bronserver Hallo geen een Cache-Control-header, wordt deze optie produceert kan oorzaak Hallo antwoord header toonot bevatten een Cache-Control-header.
Indien deze ontbreken toevoegen|Als een Cache-Control-header niet van de bronserver Hallo ontvangen is, voegt de header van de Cache-Control geproduceerd door Hallo externe maximumleeftijd functie met deze optie. Deze optie is nuttig om ervoor te zorgen dat alle activa een Cache-Control-header wordt toegewezen.
Verwijderen| Deze optie zorgt ervoor dat een Cache-Control-header niet opgenomen in Hallo header-reactie is. Als de header van een Cache-Control al is toegewezen, worden klikt u vervolgens het verwijderd van Hallo header-reactie.

**Standaardgedrag:** overschrijven.

###<a name="cache-key-query-string"></a>Cache-sleutel queryreeks
**Doel:** bepaalt of de cache-sleutel wordt opnemen of uitsluiten van queryreeksparameters die zijn gekoppeld aan een aanvraag.

Belangrijke informatie:

- Geef een of meer query tekenreeks parameter namen. Elke parameternaam moet worden gescheiden met een spatie.
- Deze functie bepaalt of queryreeksparameters worden opgenomen of van Hallo Cachesleutel uitgesloten. Aanvullende informatie is beschikbaar voor elk van de onderstaande opties.

Type|Beschrijving
--|--
 Opnemen|  Geeft aan dat elke opgegeven parameter in Hallo Cachesleutel moet worden opgenomen. Een unieke cache-sleutel wordt gegenereerd voor elke aanvraag met een unieke waarde voor een queryreeksparameter gedefinieerd in deze functie. 
 Alle  |Hiermee wordt aangegeven dat een unieke cache-sleutel wordt gemaakt voor elke aanvraag tooan asset die een unieke queryreeks bevat. Dit type configuratie wordt meestal niet aanbevolen omdat dit ertoe tooa klein percentage treffers in cache leiden kan. Hierdoor neemt Hallo belasting op de bronserver hello, omdat dat meer aanvragen tooserve. Deze configuratie is een duplicaat Hallo cachegedrag bekend als 'unieke-cache' op de pagina queryreeks opslaan in cache. 
 Uitsluiten | Geeft aan dat alleen Hallo opgegeven parameter (s) van Hallo Cachesleutel worden uitgesloten. Andere queryreeksparameters worden opgenomen in de cache Hallo-sleutel. 
 Sluit alle  |Hiermee wordt aangegeven dat alle queryreeksparameters van Hallo Cachesleutel worden uitgesloten. Deze configuratie is een duplicaat Hallo standaard cachegedrag, wordt ook wel 'standaard '-cache op de pagina queryreeks opslaan in cache. 

Hallo power van HTTP-Engine voor regels kunt u toocustomize Hallo manier waarin query opslaan in cache is geïmplementeerd. U kunt bijvoorbeeld opgeven dat query opslaan in cache alleen op bepaalde locaties of bestandstypen worden uitgevoerd.

Als u tooduplicate Hallo-queryreeks cachegedrag bekend als 'no-cache' op de pagina queryreeks in cache opslaan wilt, moet u toocreate een regel met een URL-Query jokertekens overeen voorwaarde en een Bypass-Cache-functie. Hallo URL Query jokertekens overeen voorwaarde moet worden ingesteld als tooan sterretje (*).

#### <a name="sample-scenarios"></a>Voorbeeldscenario 's

Hieronder vindt u Voorbeeldgebruik voor deze functie. Een voorbeeld van een aanvraag en het Hallo-Cachesleutel default worden hieronder.

- **Voorbeeld van een aanvraag:** http://wpc.0001.&lt; Domein&gt;/800001/Origin/folder/asset.htm?sessionid=1234 en taal = nl & userid = 01
- **Standaard-cache-sleutel:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Opnemen

Configuratie van de steekproef:

- **Type:** opnemen
- **Parameter (s):** taal

Dit type configuratie genereert Hallo query tekenreeks parameter cache-sleutel te volgen:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Alle

Configuratie van de steekproef:

- **Type:** alle

Dit type configuratie genereert Hallo query tekenreeks parameter cache-sleutel te volgen:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Uitsluiten

Configuratie van de steekproef:

- **Type:** uitsluiten
- **Parameter (s):** sessionid userid

Dit type configuratie genereert Hallo query tekenreeks parameter cache-sleutel te volgen:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Sluit alle

Configuratie van de steekproef:

- **Type:** sluit alle

Dit type configuratie genereert Hallo query tekenreeks parameter cache-sleutel te volgen:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Cache-sleutel opnieuw schrijven
**Doel:** Regeneraties Hallo Cachesleutel die zijn gekoppeld aan een aanvraag.

Een cache-sleutel is Hallo relatief pad zijn dat een asset voor Hallo van caching identificeert. Onze servers, met andere woorden, controleren op de versie van een cache van een activum volgens tooits pad, zoals gedefinieerd door de cachesleutel.

Deze functie met het definiëren van beide Hallo volgend opties configureren:

Optie|Beschrijving
--|--
Oorspronkelijke pad| Hallo relatief pad toohello typen waarvan Cachesleutel herschreven aanvragen definiëren. Een relatief pad worden gedefinieerd met een base oorsprongpad selecteren en vervolgens een reguliere-expressiepatroon te definiëren.
Nieuwe pad|Definieer Hallo relatief pad zijn voor Hallo nieuwe cache-sleutel. Een relatief pad worden gedefinieerd met een base oorsprongpad selecteren en vervolgens een reguliere-expressiepatroon te definiëren. Deze relatieve pad kan dynamisch worden samengesteld door Hallo gebruik van HTTP-variabelen
**Standaardgedrag:** Cachesleutel van een aanvraag wordt bepaald door Hallo aanvraag-URI.

###<a name="complete-cache-fill"></a>Voltooien van de opvulling van de Cache
**Doel:** bepaalt wat er gebeurt wanneer een aanvraag in een gedeeltelijke Cachemisser op een edge-server resulteert.

Een gedeeltelijke Cachemisser beschrijving van status van de cache Hallo voor een asset dat nog niet volledig gedownloade tooan edge-server is. Als een asset is slechts gedeeltelijk in cache op een edge-server, klikt u vervolgens hello volgende aanvraag voor de activa doorgestuurd opnieuw toohello-bronserver.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Een gedeeltelijke Cachemisser treedt meestal op nadat een gebruiker een download annuleert of voor bedrijfsmiddelen die uitsluitend worden aangevraagd met behulp van HTTP-aanvragen voor bereik. Deze functie is vooral handig voor grote activa waar gebruikers wordt niet normaal gesproken deze downloaden bij start toofinish (bijvoorbeeld video's). Als gevolg hiervan is deze functie standaard ingeschakeld op Hallo grote HTTP-platform. Het is uitgeschakeld op alle andere platforms.

Het verdient tooleave Hallo standaardconfiguratie voor HTTP-grote Hallo-platform, omdat deze wordt Hallo belasting van uw klant oorsprong server verminderen en Hallo verkorten waarmee uw klanten uw inhoud downloaden.

Vervaldatum toohello manier in cache van welke instellingen worden bijgehouden, deze functie kan niet worden gekoppeld met de volgende voorwaarden van de overeenkomst Hallo: rand Cname, Header letterlijke aanvragen, aanvragen Header jokertekens, URL Query letterlijke, en URL-Query.

Waarde|Resultaat
--|--
Ingeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is tooforce Hallo edge server tooinitiate een ophaalbewerkingen van Hallo actief van Hallo-bronserver. Waarna Hallo asset worden weergegeven in lokale cache Hallo rand van de server.
Uitgeschakeld|Hiermee voorkomt dat een edge-server uitvoeren van een op de achtergrond ophalen voor Hallo asset. Dit betekent dat Hallo volgende aanvraag voor die asset uit die regio, een toorequest edge-server wordt op Hallo klant-bronserver.

**Standaardgedrag:** ingeschakeld.

###<a name="compress-file-types"></a>Bestandstypen comprimeren
**Doel:** Hallo-bestandsindelingen die zal worden gecomprimeerd definieert op Hallo-server.

Een bestandsindeling kan worden opgegeven met de Internet-mediatype (dat wil zeggen, Content-Type). Mediatype Internet is platformonafhankelijk metagegevens waarmee onze servers tooidentify Hallo-bestandsindeling van een bepaald actief. Hieronder vindt u een lijst met algemene typen voor Internet-media.

Internet-mediatype|Beschrijving
--|--
text/plain|Bestanden met tekst zonder opmaak
text/html| HTML-bestanden
text/css|Cascading stylesheets (CSS)
x-toepassing-javascript|Javascript
toepassing/javascript|Javascript
Belangrijke informatie:

- Geef meerdere mediatypen voor Internet door die begrenst elkaar met een spatie. 
- Deze functie worden alleen gecomprimeerd voor activa waarvan de grootte minder dan 1 MB is. Grotere activa worden niet door onze servers gecomprimeerd.
- Bepaalde typen inhoud, zoals afbeeldingen, video en audio-media-elementen (zoals JPG, MP3, MP4, enzovoort), zijn al gecomprimeerd. Aanvullende compressie op deze typen elementen zal de bestandsgrootte niet aanzienlijk afnemen. Daarom wordt aanbevolen dat u niet de mogelijkheid compressie op deze typen van activa.
- Jokertekens zoals sterretjes, worden niet ondersteund.
- Voordat u deze functie tooa regel toevoegt, zorg ervoor dat tooset de optie compressie uitgeschakeld op de pagina compressie voor Hallo platform toowhich die met deze regel wordt toegepast.

###<a name="default-internal-max-age"></a>Standaard interne-maximumleeftijd
**Doel:** bepaalt Hallo-maximumleeftijd standaardinterval voor het edge-server tooorigin server cache opnieuw te worden gevalideerd. Met andere woorden, Hallo hoeveelheid tijd dat wordt gewacht voordat een edge-server wordt gecontroleerd of een in cache asset overeenkomt met Hallo asset opgeslagen op de bronserver Hallo.

Belangrijke informatie:

- Deze actie vindt alleen plaats voor antwoorden van een bronserver die een maximumleeftijd aanduiding in de Cache-Control of Expires-header niet hebt toegewezen.
- Deze actie vindt niet plaats voor activa die niet als caching geschikte worden beschouwd.
- Deze actie heeft geen invloed op de browser tooedge server cache revalidations. Deze typen revalidations worden bepaald door de Cache-Control of Expires-koppen toohello browser, die kan worden aangepast met de functie externe maximumleeftijd wordt verzonden.
- Hallo-resultaten van deze actie hoeft niet een waarneembare effect op Hallo antwoordheaders en Hallo-inhoud vanaf randservers voor uw inhoud wordt geretourneerd, maar dit kan van invloed zijn op Hallo hoeveelheid hervalidatie verkeer dat wordt verzonden vanuit edge servers tooyour oorsprong-server.
- Deze functie door configureren:
    - Selecteren Hallo statuscode waarvoor een standaard interne-maximumleeftijd kan worden toegepast.
    - Een geheel getal opgeven en vervolgens te klikken op Hallo gewenste tijdseenheid (dat wil zeggen, seconden, minuten, uren, enzovoort). Deze waarde bepaalt Hallo standaard interne maximumleeftijd interval.

- Instelling Hallo tijdseenheid wordt te "Off" toegewezen een interne maximumleeftijd standaardinterval van 7 dagen voor aanvragen die niet zijn toegewezen aan een maximumleeftijd aanduiding in het Cache-Control of Expires-header.
- Vervaldatum toohello manier in cache van welke instellingen worden bijgehouden, deze functie kan niet worden gekoppeld met de volgende voorwaarden van de overeenkomst Hallo: 
    - Rand 
    - CNAME
    - Aanvraag-Header Literal
    - Aanvraag-Header jokertekens
    - Verzoekmethode
    - URL-Query Literal
    - URL-Query jokertekens

**Standaardwaarde:** 7 dagen

###<a name="expires-header-treatment"></a>Koptekst behandeling verloopt
**Doel:** Hallo Expires-koppen worden gegenereerd door een edge-server bepaalt wanneer de functie externe maximumleeftijd actief is.

Hallo gemakkelijkste manier tooachieve dit type configuratie is tooplace Hallo externe maximumleeftijd en Hallo verloopt Header behandeling functies in dezelfde instructie Hallo.

Waarde|Resultaat
--|--
Overschrijven|Zorgt ervoor dat de volgende activiteiten Hallo vindt plaats:<br/>-De Expires-header die worden gegenereerd door de bronserver Hallo overschrijft.<br/>-Voegt de Expires-header die wordt geproduceerd door Hallo externe maximumleeftijd functie toohello antwoord.
Doorgeven|Zorgt ervoor dat de Expires-header die wordt geproduceerd door Hallo externe maximumleeftijd functie nooit toohello antwoord is toegevoegd. <br/> Als de bronserver Hallo een Expires-header ontstaat, worden door eindgebruikers toohello doorgegeven. <br/>Als bronserver Hallo geen een Expires-header, wordt deze optie produceert kan oorzaak Hallo antwoord header toonot bevatten een Expires-header.
Indien deze ontbreken toevoegen| Als een Expires-header niet van de bronserver hello ontvangen is, voegt de Expires-header die wordt geproduceerd door Hallo externe maximumleeftijd functie met deze optie. Deze optie is nuttig om ervoor te zorgen dat alle activa een Expires-header wordt toegewezen.
Verwijderen| Zorgt ervoor dat een Expires-header is niet opgenomen in Hallo header-reactie. Als er al een Expires-header is toegewezen, worden vervolgens deze verwijderd uit Hallo header-reactie.

**Standaardgedrag:** overschrijven

###<a name="external-max-age"></a>Externe maximumleeftijd
**Doel:** bepaalt Hallo maximumleeftijd interval voor de browser tooedge server cache opnieuw te worden gevalideerd. Met andere woorden, Hallo hoeveelheid tijd die wordt doorgegeven voordat een browser kan worden gecontroleerd voor een nieuwe versie van een actief van een edge-server.

Inschakelen van deze functie genereert Cache-Control: max-na verloop van tijd en headers op onze servers rand verloopt en ze toohello HTTP-client te verzenden. Standaard wordt deze headers die zijn gemaakt met de bronserver hallo overschreven. Echter, de behandeling van Cache-Control-Header en de functies verloopt Header behandeling kunnen worden gebruikt tooalter dit gedrag.

Belangrijke informatie:

- Deze actie heeft geen invloed op de edge server tooorigin server cache revalidations. Deze typen revalidations worden bepaald door de Cache-Control/Expires-koppen ontvangen van de bronserver Hallo en kunnen worden aangepast met de standaard interne-maximumleeftijd en de onderdelen van Force interne-maximumleeftijd.
- Deze functie configureren door een geheel getal opgeven en het selecteren van Hallo gewenste tijdseenheid (dat wil zeggen, seconden, minuten, uren, enzovoort).
- Als u deze functie tooa negatieve waarde zorgt ervoor dat onze servers rand toosend een Cache-Control: no-cache en een Expires-tijd die is ingesteld in Hallo verleden met elke reactie toohello browser. Hoewel een HTTP-client wordt Hallo reactie niet in cache, wordt deze instelling geen invloed op onze randservers mogelijkheid toocache Hallo reactie van de bronserver Hallo.
- Instelling Hallo tijdseenheid te "Off" wordt deze functie uitschakelen. De Cache-Control/Expires-koppen in de cache opgeslagen met de reactie van de bronserver Hallo Hallo worden doorgegeven aan toohello browser.

**Standaardgedrag:** uitschakelen

###<a name="force-internal-max-age"></a>Interne maximumleeftijd forceren
**Doel:** bepaalt Hallo maximumleeftijd interval voor edge server tooorigin server cache opnieuw te worden gevalideerd. Met andere woorden, Hallo hoeveelheid tijd dat wordt gewacht voordat een edge-server controleren kunt of een in cache asset overeenkomt met Hallo asset opgeslagen op de bronserver Hallo.

Belangrijke informatie:

- Deze functie wordt Hallo maximumleeftijd interval is gedefinieerd in de Cache-Control of Expires-koppen gegenereerd op basis van een bronserver overschreven.
- Deze functie heeft geen invloed op de browser tooedge server cache revalidations. Deze typen revalidations worden bepaald door de Cache-Control of Expires-koppen toohello browser wordt verzonden.
- Deze functie heeft geen gevolgen heeft voor antwoord Hallo geleverd door een edge-server toohello aanvrager waarneembare. Het kan echter een effect op Hallo hoeveelheid hervalidatie verkeer dat wordt verzonden van onze randserver servers toohello oorsprong hebben.
- Deze functie door configureren:
    - Selecteren Hallo statuscode waarvoor een interne maximumleeftijd worden toegepast.
    - Een geheel getal opgeven en het selecteren Hallo gewenste tijdseenheid (dat wil zeggen, seconden, minuten, uren, enzovoort). Deze waarde bepaalt van de aanvraag Hallo maximumleeftijd interval.

- Instelling Hallo tijdseenheid te "Off" Hiermee schakelt u deze functie. Een interne maximumleeftijd interval wordt niet toorequested activa worden toegewezen. Als de oorspronkelijke Hallo-header bevat geen instructies in het cachegeheugen, vervolgens Hallo asset wordt in de cache op basis van actieve toohello-instelling in de functie standaard interne-maximumleeftijd.
- Vervaldatum toohello manier in cache van welke instellingen worden bijgehouden, deze functie kan niet worden gekoppeld met de volgende voorwaarden van de overeenkomst Hallo: 
    - Rand 
    - CNAME
    - Aanvraag-Header Literal
    - Aanvraag-Header jokertekens
    - Verzoekmethode
    - URL-Query Literal
    - URL-Query jokertekens

**Standaardgedrag:** uitschakelen

###<a name="h264-support-http-progressive-download"></a>H.264-ondersteuning (http-progressief downloaden)
**Doel:** bepaalt Hallo typen H.264 bestandsindelingen die mogelijk gebruikte toostream inhoud.

Belangrijke informatie:

- Een door spaties gescheiden set toegestane H.264 filename extensies in de optie bestandsextensies definiëren. De optie bestandsextensies overschrijft het standaardgedrag Hallo. Ondersteuning voor MP4 en F4V onderhouden door te nemen die bestandsnaamextensies als u deze optie. 
- Zorg ervoor dat tooinclude een periode bij het opgeven van elke extensie (bijvoorbeeld MP4 .f4v).

**Standaardgedrag:** MP4 en F4V media standaard HTTP progressief downloaden ondersteunt.

###<a name="honor-no-cache-request"></a>EEr Nee-cache-aanvraag
**Doel:** bepaalt of de Nee-cache-aanvragen van een HTTP-client zal worden doorgestuurd toohello-bronserver.

Een aanvraag Nee-cache treedt op wanneer Hallo HTTP-client een Cache verzendt-Control: no-cache en/of Pragma:no-cache-header in Hallo HTTP-aanvraag.

Waarde|Resultaat
--|--
Ingeschakeld|Kan toobe doorgestuurde toohello bronserver Nee-cache van een HTTP-client-aanvragen en Hallo bronserver retourneert Hallo antwoordheaders en Hallo hoofdtekst via Hallo edge-server back-toohello HTTP-client.
Uitgeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is tooprevent Nee-cache-aanvragen worden doorgestuurd toohello bronserver.

Voor alle productie-verkeer wordt ten zeerste aanbevolen tooleave deze functie in de standaardstatus uitgeschakeld. Anders oorsprong servers wordt niet worden afgeschermd van eindgebruikers die per ongeluk veel aanvragen voor Nee-cache activeren mogelijk bij het vernieuwen van webpagina's of van Hallo veel populaire mediaspelers die zijn gecodeerd toosend een Nee-cache-koptekst met elke aanvraag video. Evenwel kan deze functie nuttig tooapply toocertain niet-productieve fasering of op aanvraag voor het testen van mappen, in volgorde tooallow nieuwe inhoud toobe opgehaald uit Hallo-bronserver.

Hallo status van de cache die worden gerapporteerd voor een aanvraag die is toegestaan toobe doorgestuurd tooan bronserver vanwege toothis functie TCP_Client_Refresh_Miss is. De statussen van de Cache-rapport, die beschikbaar in rapportagemodule Hallo-Core is, bevat statistische gegevens door de status van de cache. Hiermee kunt u tootrack Hallo nummer en percentage verzoeken die de bronserver tooan vanwege toothis functie worden doorgestuurd.

**Standaardgedrag:** uitgeschakeld.

###<a name="ignore-origin-no-cache"></a>Negeren oorsprong no-cache
**Doel:** bepaalt of onze CDN negeert Hallo richtlijnen die worden geleverd vanuit een bronserver te volgen:

- Cache-Control: persoonlijke
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: Nee-cache

Belangrijke informatie:

- Deze functie configureren met het definiëren van een door spaties gescheiden lijst met statuscodes waarvoor Hallo hierboven richtlijnen worden genegeerd.
- Hallo set codes geldige status voor deze functie zijn: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, en 505.
- Deze functie uitschakelen door deze tooa lege waarde.
- Vervaldatum toohello manier in cache van welke instellingen worden bijgehouden, deze functie kan niet worden gekoppeld met de volgende voorwaarden van de overeenkomst Hallo: 
    - Rand 
    - CNAME
    - Aanvraag-Header Literal
    - Aanvraag-Header jokertekens
    - Verzoekmethode
    - URL-Query Literal
    - URL-Query jokertekens

**Standaardgedrag:** het standaardgedrag is toohonor Hallo hierboven richtlijnen.

###<a name="ignore-unsatisfiable-ranges"></a>Ongeldig bereiken negeren 
**Doel:** bepaalt Hallo-antwoord dat wordt geretourneerd tooclients wanneer een aanvraag statuscode 416 aangevraagd bereik niet geldig genereert.

Standaard wordt deze statuscode geretourneerd wanneer Hallo opgegeven bereik in bytes aanvraag kan niet worden voldaan door een edge-server en een If-Range aanvraag-header-veld is niet opgegeven.

Waarde|Resultaat
-|-
Ingeschakeld|Voorkomt dat onze randservers van reageert tooan ongeldig bytebereik aanvraag met statuscode 416 aangevraagd bereik niet geldig. In plaats daarvan onze servers leveren Hallo aangevraagde asset en een 200 OK naar Hallo client geretourneerd.
Uitgeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is toohonor de 416 statuscode aangevraagd bereik niet geldig.

**Standaardgedrag:** uitgeschakeld.

###<a name="internal-max-stale"></a>Interne Max-verouderd
**Doel:** bepaalt hoe lang afgelopen Hallo normale de verlooptijd van een activum in de cache kan worden geleverd vanuit een edge-server wanneer Hallo edge-server kan geen toorevalidate Hallo in de cache opgeslagen asset met Hallo-bronserver.

Normaal gesproken als een asset maximumleeftijd tijd is verstreken, stuurt Hallo edge-server een aanvraag voor hervalidatie toohello bronserver. Hallo bronserver zal vervolgens reageren met ofwel een 304 niet worden gewijzigd zodat Hallo edge-server een nieuwe lease op in de cache asset hello, hetzij met 200 OK om te voorzien van een bijgewerkte versie van de cache asset Hallo Hallo edge-server.

Als de Hallo edge-server kan geen tooestablish een verbinding met de bronserver Hallo tijdens een poging een dergelijke hervalidatie is, bepaalt deze functie interne Max-verouderde of en hoe lang Hallo edge-server tooserve Hallo nu verouderd asset kan doorgaan.

Houd er rekening mee dat dit tijdsinterval wordt gestart wanneer maximumleeftijd van Hallo actief is verlopen, niet het geval wanneer hello mislukte hervalidatie optreedt. Hallo maximale periode gedurende welke een asset kan worden geleverd zonder geslaagde hervalidatie is daarom Hallo hoeveelheid tijd die is opgegeven door Hallo combinatie van maximumleeftijd plus max verouderd. Bijvoorbeeld als een actief is in de cache om 9:00 uur met een maximumleeftijd van 30 minuten en een maximale-verouderde van 15 minuten en vervolgens de hervalidatie van een mislukte poging op zou 9:44 leiden tot een eindgebruiker ontvangende Hallo verlopen in de cache actief, terwijl een hervalidatie mislukte poging om 9:46 tot leiden zou Hallo-eindgebruikers ontvangen een 504 Gateway timeout gegenereerd.

Een waarde die is geconfigureerd voor deze functie wordt vervangen door Cache-Control: moet-valideren of de Cache-Control: proxy-headers heeft ontvangen van de bronserver Hallo de validatie opnieuw. Als een van deze koppen is ontvangen van de bronserver Hallo wanneer een actief is in eerste instantie in de cache opgeslagen, klikt u vervolgens in Hallo edge-server niet een verlopen in de cache asset fungeren. In dat geval als Hallo edge-server kan geen toorevalidate met Hallo oorsprong wanneer van Hallo actief maximumleeftijd interval is verstreken, retourneert Hallo edge-server een 504 Gateway timeout gegenereerd.

Belangrijke informatie:

- Deze functie door configureren:
    - Selecteren Hallo statuscode waarvoor een max-verouderde worden toegepast.
    - Een geheel getal opgeven en vervolgens te klikken op Hallo gewenste tijdseenheid (dat wil zeggen, seconden, minuten, uren, enzovoort). Deze waarde bepaalt Hallo interne max-verouderde die worden toegepast.

- Instelling Hallo tijdseenheid te "Off" wordt deze functie uitschakelen. Een element in de cache kan niet buiten de normale verlooptijd worden geleverd.
- Vervaldatum toohello manier in cache van welke instellingen worden bijgehouden, deze functie kan niet worden gekoppeld met de volgende voorwaarden van de overeenkomst Hallo: 
    - Rand 
    - CNAME
    - Aanvraag-Header Literal
    - Aanvraag-Header jokertekens
    - Verzoekmethode
    - URL-Query Literal
    - URL-Query jokertekens

**Standaardgedrag:** 2 minuten

###<a name="partial-cache-sharing"></a>Gedeeltelijke Cache delen
**Doel:** bepaalt of een aanvraag deels in cache opgeslagen inhoud kan genereren.

Deze gedeeltelijke cache mogelijk vervolgens gebruikte toofulfill nieuwe aanvragen voor de inhoud totdat Hallo aangevraagde inhoud is volledig in de cache opgeslagen.

Waarde|Resultaat
-|-
Ingeschakeld|Aanvragen deels in cache opgeslagen inhoud kunnen worden gegenereerd.
Uitgeschakeld|Aanvragen kunnen alleen een volledig in de cache genereren versie Hallo aangevraagde inhoud.

**Standaardgedrag:** uitgeschakeld.

###<a name="prevalidate-cached-content"></a>De inhoud in cache prevalidate
**Doel:** Hiermee wordt bepaald of de inhoud in cache in aanmerking komen voor vroege hervalidatie voordat de TTL verloopt.

Definieer Hallo tijdsduur voorafgaande toohello vervaldatum van Hallo van inhoud TTL waarover wordt het in aanmerking komen voor vroege hervalidatie worden aangevraagd.

Belangrijke informatie:

- "Off" selecteren als Hallo tijdseenheid is vereist op hervalidatie tootake plaats nadat de TTL Hallo opgeslagen in de cache-inhoud is verlopen. Tijd moet niet worden opgegeven en worden genegeerd.

**Standaardgedrag:** uitschakelen. Hervalidatie kan alleen plaatsvinden na Hallo in de cache inhoud TTL is verlopen.

###<a name="refresh-zero-byte-cache-files"></a>Vernieuwen van nul bytes cachebestanden
**Doel:** bepaalt hoe van de client van een HTTP-aanvraag voor een asset 0-byte-cache wordt verwerkt door onze randservers.

Geldige waarden zijn:

Waarde|Resultaat
--|--
Ingeschakeld|Zorgt ervoor dat de edge server toore ophalen Hallo asset van de bronserver Hallo.
Uitgeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is tooserve geldig cache activa op verzoek.
Deze functie is niet vereist voor de juiste caching en leveren van inhoud, maar mogelijk van pas als tijdelijke oplossing. Genereren van dynamische inhoud op servers van de oorsprong kunnen bijvoorbeeld per ongeluk resulteren in 0-byte-antwoorden toohello randservers wordt verzonden. Deze typen antwoorden zijn meestal in cache opgeslagen door onze randservers. Als u weet dat een antwoord 0 bytes nooit een geldig antwoord is 

voor dergelijke inhoud vervolgens deze functie kunt voorkomen dat deze typen elementen tooyour clients wordt geleverd.

**Standaardgedrag:** uitgeschakeld.

###<a name="set-cacheable-status-codes"></a>Statuscodes voor caching geschikte instellen
**Doel:** definieert Hallo reeks statuscodes die tot de inhoud in cache leiden kunnen.

Standaard is opslaan in cache alleen ingeschakeld voor 200 OK antwoorden.

Een door spaties gescheiden reeks Hallo gewenst statuscodes definiëren.

Belangrijke informatie:

- Neem ook de functie negeren oorsprong No-Cache inschakelen. Als deze functie niet is ingeschakeld, klikt u vervolgens 200 OK antwoorden mogelijk niet opgeslagen.
- Hallo set codes geldige status voor deze functie zijn: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, en 505.
- Deze functie kan niet worden gebruikt toodisable cache voor reacties waarbij 200 OK statuscode is gegenereerd.

**Standaardgedrag:** opslaan in cache is alleen ingeschakeld voor reacties waarbij 200 OK statuscode is gegenereerd.
###<a name="stale-content-delivery-on-error"></a>Verouderde Contentlevering bij fout
**Doel:** 

Bepaalt of verlopen in de cache inhoud wordt geleverd als een fout optreedt tijdens de hervalidatie van de cache of wanneer ophalen Hallo inhoud aangevraagd bij de bronserver Hallo-klant.

Waarde|Resultaat
-|-
Ingeschakeld|Verouderde inhoud kan toohello aanvrager geleverd als een fout tijdens een server verbinding tooan oorsprong optreedt.
Uitgeschakeld|Hallo oorsprong server-fout worden toohello aanvrager doorgestuurd.

**Standaardgedrag:** uitgeschakeld

###<a name="stale-while-revalidate"></a>Verouderde tijdens Revalidate
**Doel:** verbetert de prestaties doordat onze randservers tooserve verouderde inhoud toohello aanvrager terwijl hervalidatie plaatsvindt.

Belangrijke informatie:

- Hallo-gedrag van deze functie varieert volgens toohello geselecteerde tijdseenheid.
    - **Tijdseenheid:** geeft een tijdsduur en selecteert u een tijd-eenheid (bijvoorbeeld seconden, minuten, uren, enz.) tooallow verlopen leveren van inhoud. Dit type installatieprogramma kunnen Hallo CDN tooextend Hallo tijdsduur die dit kan worden bezorgd inhoud voordat u validatie volgens de volgende formule toohello:**TTL** + **verlopen tijdens de validatie opnieuw tijd** 
    - **Uit:** Selecteer "Off" toorequire hervalidatie voordat een aanvraag voor verouderde inhoud kan worden geleverd.
        - Geef een tijdsduur geen omdat deze niet van toepassing en worden genegeerd.

**Standaardgedrag:** uitschakelen. Hervalidatie moet plaatsvinden voordat Hallo aangevraagd inhoud kan worden geleverd.

###<a name="comment"></a>Opmerking
**Doel:** kunt een opmerking toobe binnen een regel toegevoegd.

Voor deze functie is tooprovide aanvullende informatie over het algemeen gebruik Hallo van een regel of waarom een bepaalde voorwaarde of functie overeen toohello regel is toegevoegd.

Belangrijke informatie:

- Maximaal 150 tekens mag worden opgegeven.
- Zorg ervoor dat tooonly alfanumerieke tekens bevatten.
- Deze functie heeft geen invloed op Hallo gedrag van Hallo regel. Dit is slechts een gebied waarin u gegevens voor toekomstig gebruik of die opgeven kunt helpen kan bij het oplossen van Hallo regel tooprovide bedoeld.
 
## <a name="headers"></a>Headers

Deze functies zijn ontworpen tooadd, wijzigen of verwijderen van headers uit Hallo aanvraag of antwoord.

Naam | Doel
-----|--------
Leeftijd antwoordheader | Hiermee wordt bepaald of een antwoordheader leeftijd wordt opgenomen in het Hallo-antwoord verzonden toohello aanvrager.
Fouten opsporen in Cache antwoordheaders | Hiermee wordt bepaald of een antwoord Hallo X-EC-Debug antwoordheader die informatie over het cachebeleid Hallo voor de aangevraagde asset Hallo bevat kan bevatten.
De aanvraagheader Client wijzigen | Overschreven, wordt toegevoegd of verwijderd van een koptekst van een aanvraag.
Client-antwoordheader wijzigen | Overschreven, wordt toegevoegd of verwijderd van een koptekst van een antwoord.
Stel aangepaste Header voor Client-IP | Kan Hallo IP-adres van de aanvragende client hello toobe toegevoegde toohello aanvraag als een aangepaste aanvraagheader.

###<a name="age-response-header"></a>Leeftijd antwoordheader
**Doel**: Hiermee wordt bepaald of een antwoordheader leeftijd moet worden opgenomen in Hallo antwoord verzonden toohello aanvrager.
Waarde|Resultaat
--|--
Ingeschakeld | Hallo leeftijd antwoordheader worden opgenomen in het Hallo-antwoord verzonden toohello aanvrager.
Uitgeschakeld | Hallo leeftijd antwoordheader worden uitgesloten uit Hallo-antwoord verzonden toohello aanvrager.

**Standaardgedrag**: uitgeschakeld.

###<a name="debug-cache-response-headers"></a>Fouten opsporen in Cache antwoordheaders
**Doel:** bepaalt of een antwoord antwoordheader van de X-EC-Debug die informatie over het cachebeleid Hallo voor de aangevraagde asset Hallo bevat kan bevatten.

Fouten opsporen in cacheantwoord headers worden opgenomen in het antwoord Hallo wanneer beide volgende Hallo waar zijn:

- Hallo Debug antwoord Headers cachefunctie is ingeschakeld op de gewenste Hallo-aanvraag.
- Hallo hierboven aanvraag definieert de set Hallo van foutopsporing cache antwoordheaders die wordt opgenomen in het Hallo-antwoord.

Fouten opsporen in cacheantwoord headers kunnen worden aangevraagd door Hallo header te volgen, waaronder en gewenste richtlijnen in de aanvraag Hallo Hallo:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Voorbeeld:**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Waarde|Resultaat
-|-
Ingeschakeld|Aanvragen voor foutopsporing cache antwoordheaders wordt een antwoord dat bestaat uit de header X-EC-Debug geretourneerd.
Uitgeschakeld|De antwoordheader van de X-EC-Debug zullen worden uitgesloten van antwoord Hallo.

**Standaardgedrag:** uitgeschakeld.

###<a name="modify-client-response-header"></a>Client-antwoordheader wijzigen
**Doel:** elke aanvraag bevat een set [aanvraagheaders]() die het worden beschreven. Deze functie de volgende mogelijkheden:

- Toevoegen of Hallo waarde toegewezen tooa aanvraagheader overschrijven. Als de opgegeven aanvraagheader Hallo niet bestaat, wordt vervolgens deze functie toevoegen toohello aanvraag.
- Verwijder een aanvraagheader van Hallo-aanvraag.

Aanvragen die zijn doorgestuurd tooan bronserver nieuwe Hallo-wijzigingen die door deze functie.

Een van de Hallo van de volgende activiteiten worden uitgevoerd op een aanvraag-header:

Optie|Beschrijving|Voorbeeld
-|-|-
Toevoegen|Hallo opgegeven waarde toend van Hallo bestaande aanvraag-header-waarde worden toegevoegd.|**Headerwaarde (Client) aanvraag:**Value1 <br/> **Headerwaarde (http-regelengine) aanvraag:** Value2 <br/>**Nieuwe aanvraag-header-waarde:** Value1Value2
Overschrijven|Hallo-aanvraag headerwaarde set toohello worden opgegeven.|**Headerwaarde (Client) aanvraag:**Value1 <br/>**Headerwaarde (http-regelengine) aanvraag:** Value2 <br/>**Nieuwe aanvraag-header-waarde:** Value2 <br/>
Verwijderen|Hiermee verwijdert u de opgegeven aanvraagheader Hallo.|**Headerwaarde (Client) aanvraag:**Value1 <br/> **Configuratie van de Client-aanvraagheader wijzigen:** verwijderen Hallo-aanvraagheader betrokken. <br/>**Resultaat:** Hallo opgegeven aanvraagheader niet doorgestuurd toohello-bronserver.

Belangrijke informatie:

- Zorg ervoor dat Hallo-waarde opgegeven in de optie voor een exacte overeenkomst voor de gewenste aanvraagheader Hallo is.
- Aanvraag is niet in aanmerking voor doel van de identiteit van een koptekst Hallo genomen. Voor een van de Hallo na variaties van de naam van de Cache-Control-header kan bijvoorbeeld gebruikte tooidentify het:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Zorg ervoor dat tooonly alfanumerieke tekens, streepjes of onderstrepingstekens gebruiken bij het opgeven van een header-naam.
- Verwijderen van een koptekst, kunnen er bronserver tooan door onze randservers van de worden doorgestuurd.
- Hallo volgende headers zijn gereserveerd en kunnen niet worden gewijzigd door deze functie:
    - doorgestuurd
    - host
    - via
    - Waarschuwing
    - x doorgestuurd voor
    - Alle headernamen die met 'x ec beginnen' zijn gereserveerd.

###<a name="modify-client-response-header"></a>Client-antwoordheader wijzigen
Elk antwoord bevat een reeks [antwoordheaders]() die het worden beschreven. Deze functie de volgende mogelijkheden:

- Toevoegen of Hallo waarde toegewezen tooa antwoordheader overschrijven. Als de opgegeven aanvraagheader Hallo niet bestaat, wordt vervolgens deze functie toevoegen toohello antwoord.
- Verwijder een antwoordheader van antwoord Hallo.

Standaard worden met de headerwaarden antwoord op een bronserver en op onze randservers gedefinieerd.

Een van de volgende activiteiten Hallo kan worden uitgevoerd op een antwoordheader:

Optie|Beschrijving|Voorbeeld
-|-|-
Toevoegen|Hallo opgegeven waarde toend van Hallo bestaande aanvraag-header-waarde worden toegevoegd.|**Antwoord headerwaarde (Client):**Value1 <br/> **Antwoord headerwaarde (http-regelengine):** Value2 <br/>**Nieuwe antwoord headerwaarde:** Value1Value2
Overschrijven|Hallo-aanvraag headerwaarde set toohello worden opgegeven.|**Antwoord headerwaarde (Client):**Value1 <br/>**Antwoord headerwaarde (http-regelengine):** Value2 <br/>**Nieuwe antwoord headerwaarde:** Value2 <br/>
Verwijderen|Hiermee verwijdert u de opgegeven aanvraagheader Hallo.|**Headerwaarde (Client) aanvraag:** Value1 <br/> **Aanvraag-Header voor Client-configuratie wijzigen:** verwijderen Hallo-antwoordheader betrokken. <br/>**Resultaat:** Hallo opgegeven antwoordkop niet doorgestuurd toohello aanvrager.

Belangrijke informatie:

- Zorg ervoor dat Hallo-waarde opgegeven in de optie voor een exacte overeenkomst voor de gewenste antwoordheader Hallo is. 
- Aanvraag is niet in aanmerking voor doel van de identiteit van een koptekst Hallo genomen. Voor een van de Hallo na variaties van de naam van de Cache-Control-header kan bijvoorbeeld gebruikte tooidentify het:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Verwijderen van een koptekst, kunnen er toohello aanvrager worden doorgestuurd.
- Hallo volgende headers zijn gereserveerd en kunnen niet worden gewijzigd door deze functie:
    - Accepteer codering
    - leeftijd
    - verbinding
    - codering van inhoud
    - lengte van inhoud
    - inhoud bereik
    - Datum
    - server
    - aanhangwagen
    - Transfer-encoding
    - upgrade
    - variëren
    - via
    - Waarschuwing
    - Alle headernamen die met 'x ec beginnen' zijn gereserveerd.

###<a name="set-client-ip-custom-header"></a>Stel aangepaste Header voor Client-IP
**Doel:** voegt u een aangepaste header die de aanvragende client Hallo door IP-adres toohello aanvraag identificeert.

De optie Header-naam definieert Hallo-naam van de aangepaste aanvraagheader Hallo waarin Hallo-client-IP-adres wordt opgeslagen.

Deze functie kunt een klant oorsprong server toofind client-IP-adressen via een aangepaste aanvraagheader. Als Hallo-aanvraag is geleverd vanuit cache, wordt er niet bronserver Hallo van Hallo-client-IP-adres worden geïnformeerd. Daarom is het aanbevolen dat deze functie worden gebruikt met ADN of activa dat wordt niet in cache worden opgeslagen.

Controleer of deze naam van de opgegeven header Hallo komt niet overeen met een van de volgende Hallo:

- Namen standaard aanvraag-header. Een lijst met headernamen van de standaard-kan worden gevonden in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Headernamen van de gereserveerde:
    - doorgestuurd voor
    - host
    - variëren
    - via
    - Waarschuwing
    - x doorgestuurd voor
    - Alle headernamen die met 'x ec beginnen' zijn gereserveerd.
 
## <a name="logs"></a>Logboeken

Deze functies zijn ontworpen toocustomize Hallo opgeslagen gegevens in onbewerkte logboekbestanden.

Naam | Doel
-----|--------
Aangepast logboekveld 1 | Hallo-indeling en Hallo-inhoud die wordt toegewezen toohello aangepaste logboekveld in een onbewerkte logboekbestand bepaalt.
Queryreeks logboek | Hiermee wordt bepaald of een queryreeks samen met de Hallo-URL in Logboeken worden opgeslagen.

###<a name="custom-log-field-1"></a>Aangepast logboekveld 1
**Doel:** Hallo indeling en Hallo-inhoud die wordt toegewezen toohello aangepaste logboekveld in een onbewerkte logboekbestand bepaalt.

Hallo hoofddoel achter dit aangepaste veld is tooallow toodetermine u welke headerwaarden aanvraag en -antwoord wordt opgeslagen in de logboekbestanden.

Hallo aangepaste logboekveld heet standaard 'x-ec_custom-1'. Hallo-naam van dit veld kan echter worden aangepast via de [onbewerkte logboekinstellingen pagina]().

Hallo opmaak of moet u de aanvraag- en reactieheaders toospecify is onder gedefinieerd.

Header-Type|Indeling|Voorbeelden
-|-|-
Aanvraag-Header|%{[RequestHeader]()}[ik]() | % {Accepteren codering} ik <br/> {Verwijzende site} ik <br/> % {Autorisatie} i
Antwoordkoptekst|%{[ResponseHeader]()}[o]()| % {Leeftijd} o <br/> % {Content-Type} o <br/> % {Cookie} o

Belangrijke informatie:

- Een veld van het aangepaste logboek kan bestaan uit een combinatie van header-velden en tekst zonder opmaak.
- Geldige tekens voor dit veld Hallo volgende zijn: alfanumerieke (dat wil zeggen, 0-9, a-z en A-Z), streepjes, dubbele punten, puntkomma's, enkele aanhalingstekens, komma's, punten, onderstrepingstekens, gelijk tekens, haakjes, haakjes en spaties. Hallo percentagesymbool en de accolades zijn alleen toegestaan wanneer een kopveld toospecify gebruikt.
- Hallo spelling voor elk veld van de opgegeven header moet overeenkomen met de gewenste aanvragen/reacties headernaam Hallo.
- Als u wilt toospecify wordt meerdere headers, dan aanbevolen dat u een scheidingsteken tooindicate elke koptekst. U kunt bijvoorbeeld een afkorting voor elke koptekst. Hieronder vindt u voorbeeldsyntaxis.
    - AE: % {accepteren codering} i A: % {autorisatie} i CT: % {Content-Type} o 

**Standaardwaarde:** -

###<a name="log-query-string"></a>Queryreeks logboek
**Doel:** bepaalt of een queryreeks samen met de Hallo-URL in Logboeken worden opgeslagen.

Waarde|Resultaat
-|-
Ingeschakeld|Hallo-opslag met queryreeksen kunt bij de registratie van URL's in een toegangslogboek. Als een URL een queryreeks bevat geen bevat, klikt u vervolgens heeft deze optie geen effect.
Uitgeschakeld|Hallo standaardgedrag herstelt. Hallo standaardgedrag is tooignore queryreeksen bij de registratie van URL's in een toegangslogboek.

**Standaardgedrag:** uitgeschakeld.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Oorsprong

Deze functies zijn ontworpen toocontrol hoe Hallo CDN met een bronserver communiceert.

Naam | Doel
-----|--------
Maximum aantal keepalive-aanvragen | Hiermee definieert u Hallo kunt u het maximale aantal aanvragen voor een Keep-Alive verbinding wordt gesloten.
Speciale proxy-kopteksten | Definieert de set Hallo van CDN-specifieke aanvraagheaders die van een bronserver edge server tooan moeten worden doorgestuurd.


###<a name="maximum-keep-alive-requests"></a>Maximum aantal keepalive-aanvragen
**Doel:** definieert Hallo kunt u het maximum aantal aanvragen voor een Keep-Alive verbinding wordt gesloten.

Hallo kunt u het maximum aantal aanvragen tooa lage waarde instelt, wordt sterk afgeraden en kan leiden tot verminderde prestaties.

Belangrijke informatie:

- Deze waarde als een geheel getal opgeven.
- Neem geen komma's of perioden in Hallo opgegeven waarde.

**Standaardwaarde:** 10.000 aanvragen

###<a name="proxy-special-headers"></a>Speciale proxy-kopteksten
**Doel:** definieert Hallo reeks [aanvraagheaders CDN-specifieke]() die van een bronserver edge server tooan worden doorgestuurd.

Belangrijke informatie:

- Elke aanvraag-header van het CDN-specifieke gedefinieerd in deze functie doorgestuurd tooan-bronserver.
- Voorkomen dat een aanvraagheader CDN-specifieke bronserver tooan door deze te verwijderen uit deze lijst wordt doorgestuurd.

**Standaardgedrag:** alle [CDN-specifieke aanvraagheaders]() toohello bronserver doorgestuurd.

## <a name="specialty"></a>Speciale

Deze functies bieden geavanceerde functies die alleen door ervaren gebruikers moet worden gebruikt.

Naam | Doel
-----|--------
Caching geschikte HTTP-methoden | Hiermee wordt bepaald Hallo set aanvullende HTTP-methoden die in de cache op ons netwerk kunnen worden opgeslagen.
Grootte van standaardberichthoofdtekst voor caching geschikte aanvraag | Hiermee definieert u Hallo drempelwaarde voor het bepalen of een POST-antwoord in cache.

###<a name="cacheable-http-methods"></a>Caching geschikte HTTP-methoden
**Doel:** bepaalt Hallo set aanvullende HTTP-methoden die in de cache op ons netwerk kunnen worden opgeslagen.

Belangrijke informatie:

- Deze functie wordt ervan uitgegaan dat GET antwoorden moeten altijd opslaan in de cache. Als gevolg hiervan moet Hallo ophalen van HTTP-methode niet worden opgenomen bij het instellen van deze functie.
- Deze functie ondersteunt alleen Hallo HTTP POST-methode. POST antwoord in cache opslaan door deze functie in te stellen op: POST 
- Standaard alleen aanvragen waarvan hoofdtekst kleiner dan 14 Kb is wordt in de cache opgeslagen. Gebruik de caching geschikte grootte functie van de aanvraag hoofdtekst Hallo maximale aanvraag hoofdtekst grootte instellen.

**Standaardgedrag:** wordt alleen GET-antwoord in cache worden opgeslagen.

###<a name="cacheable-request-body-size"></a>Grootte van standaardberichthoofdtekst voor caching geschikte aanvraag

**Doel:** definieert Hallo drempelwaarde voor het bepalen of een POST-antwoord in cache.

Deze drempelwaarde wordt bepaald door het opgeven van een maximale aanvraag hoofdtekst grootte. Wordt niet in cache opgeslagen dat aanvragen met een grotere aanvraagtekst.

Belangrijke informatie:

- Deze functie is alleen van toepassing wanneer POST antwoorden in aanmerking voor het opslaan in cache komen. Hallo caching geschikte HTTP-methoden functie in te schakelen POST-aanvraag in gebruik.
- Hallo aanvraagtekst voor rekening gehouden met:
    - x-1-800-www-Dell-form-urlencoded waarden
    - Een unieke Cachesleutel gezorgd
- Voor het definiëren van een grote maximale aanvraag hoofdtekst mogelijk gegevens levering van de prestaties beïnvloeden.
    - **Aanbevolen waarde:** 14 Kb
    - **Minimumwaarde:** 1 Kb

**Standaardgedrag:** 14 Kb
 
## <a name="url"></a>URL

Deze functies kunnen een aanvraag toobe omgeleid of herschreven tooa andere URL.

Naam | Doel
-----|--------
Omleidingen volgen | Hiermee wordt bepaald of aanvragen omgeleid toohello hostnaam is gedefinieerd in Hallo locatieheader geretourneerd door een klant-bronserver worden kunnen.
URL-omleiding | Aanvragen via Hallo locatieheader leidt.
Herschrijven van URL  | Herschrijft Hallo aanvraag-URL.

###<a name="follow-redirects"></a>Omleidingen volgen
**Doel:** bepaalt of aanvragen omgeleid toohello hostnaam is gedefinieerd in de locatieheader geretourneerd door een klant-bronserver worden kunnen.

Belangrijke informatie:

- Aanvragen kunnen alleen worden omgeleid tooedge CNAMEs die overeenkomen met toohello hetzelfde platform.

Waarde|Resultaat
-|-
Ingeschakeld|Aanvragen kunnen worden omgeleid.
Uitgeschakeld|Geen zal aanvragen worden omgeleid.

**Standaardgedrag:** uitgeschakeld.
###<a name="url-redirect"></a>URL-omleiding
**Doel:** aanvragen via de locatie-header wordt omgeleid.

Hallo-configuratie van deze functie moet Hallo volgend opties instellen:

Optie|Beschrijving
-|-
Code|Selecteer Hallo-antwoordcode toohello aanvrager wordt geretourneerd.
Bron & patroon| Deze instellingen geven aan een aanvraag-URI-patroon waarmee Hallo type aanvragen die kunnen worden omgeleid. Alleen aanvragen waarvan de URL voldoet aan beide Hallo volgende criteria wordt omgeleid: <br/> <br/> **Bron:** (of toegang tot inhoud genoemd) Selecteer een relatief pad zijn dat een bronserver identificeert. Dit is Hallo '/XXXX/' sectie en de naam van uw eindpunt. <br/> **Bron (patroon):** een patroon dat aanvragen worden aangeduid met het relatieve pad moet worden gedefinieerd. Dit patroon van een reguliere expressie moet een pad dat rechtstreeks wordt gestart nadat Hallo geselecteerd eerder toegang tot inhoud punt (Zie hierboven) definiëren. <br/> -Controleer of dat Hallo aanvraag URI criteria (dat wil zeggen, bron & patroon) hierboven gedefinieerde niet conflicteert met eventuele overeenkomst voorwaarden gedefinieerd voor deze functie. <br/> -Zorg ervoor dat toospecify een patroon. Met behulp van een lege waarde als Hallo-patroon wordt alleen gezocht naar aanvragen toohello-hoofdmap van de geselecteerde bronserver hello (bijv, http://cdn.mydomain.com/).
Doel| Hallo-URL opgeven toowhich Hallo hierboven aanvragen worden omgeleid. <br/> Dynamisch maken gebruik van deze URL: <br/> -Een reguliere-expressiepatroon <br/>-HTTP variabelen <br/> Vervang Hallo waarden vastgelegd in Hallo bron patroon in Hallo bestemming patroon met $ _n_  waar  _n_  identificeert een waarde door Hallo volgorde waarin deze is vastgelegd. $1 vertegenwoordigt bijvoorbeeld de eerste waarde Hallo vastgelegd in het patroon van Hallo-bron, terwijl $2 Hallo tweede waarde vertegenwoordigt. <br/> 
U wordt ten zeerste aanbevolen toouse een absolute URL. Hallo-gebruik van een relatieve URL kan Omleidings-URL's CDN tooan ongeldig pad.

**Voorbeeldscenario**

In dit voorbeeld wordt gedemonstreerd hoe tooredirect rand CNAME-URL die wordt omgezet toothis basis-URL CDN: http://marketing.azureedge.net/brochures

In aanmerking komende aanvragen worden omgeleid toothis base rand CNAME-URL: http://cdn.mydomain.com/resources

Deze URL-omleiding kan worden bereikt via Hallo volgende configuratie:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Belangrijke punten:**

- Hallo Omleidings-URL functie definieert Hallo aanvraag-URL's die wordt omgeleid. Als gevolg hiervan zijn aanvullende overeenkomst voorwaarden niet vereist. Hoewel Hallo overeen voorwaarde is gedefinieerd als "Always", vraagt alleen dat punt toohello 'brochures' map op Hallo 'marketing' klant oorsprong wordt omgeleid. 
- Alle overeenkomende aanvragen worden omgeleid toohello rand CNAME-URL die is gedefinieerd in de doel-optie. 
    - Voorbeeldscenario voor #1: 
        - Voorbeeld van een aanvraag (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf 
        - Aanvraag-URL (na omleiding): http://cdn.mydomain.com/resources/widgets.pdf  
    - Voorbeeldscenario voor #2: 
        - Voorbeeld van een aanvraag (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf 
        - Aanvraag-URL (na omleiding): voorbeeldscenario http://cdn.mydomain.com/resources/widgets.pdf
    - Voorbeeldscenario voor #3: 
        - Voorbeeld van een aanvraag (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - Aanvraag-URL (na omleiding): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- Hallo aanvragen schema (% {schema}) variabele is gebruikt in de doel-optie. Dit zorgt ervoor dat Hallo-aanvraag schema blijft ongewijzigd na omleiding.
- Hallo URL-segmenten die zijn vastgelegd van Hallo aanvraag zijn de nieuwe URL toegevoegde toohello via "$1."
 
###<a name="url-rewrite"></a>Herschrijven van URL
**Doel:** herschrijft Hallo aanvraag-URL.

Belangrijke informatie:

- Hallo-configuratie van deze functie moet Hallo volgend opties instellen:

Optie|Beschrijving
-|-
 Bron & patroon | Deze instellingen geven aan een aanvraag-URI-patroon waarmee aanvragen die kan worden herschreven Hallo type. Alleen aanvragen waarvan de URL voldoet aan beide volgende criteria Hallo herschreven: <br/>     - **Bron (of een punt voor toegang tot inhoud):** selecteert u een relatief pad zijn dat een bronserver identificeert. Dit is Hallo '/XXXX/' sectie en de naam van uw eindpunt. <br/> - **Bron (patroon):** een patroon dat aanvragen worden aangeduid met het relatieve pad moet worden gedefinieerd. Dit patroon van een reguliere expressie moet een pad dat rechtstreeks wordt gestart nadat Hallo geselecteerd eerder toegang tot inhoud punt (Zie hierboven) definiëren. <br/> Zorg ervoor dat Hallo aanvraag URI criteria (dat wil zeggen, bron & patroon) hierboven gedefinieerde niet conflicteert met Hallo overeen omstandigheden gedefinieerd voor deze functie. Zorg ervoor dat toospecify een patroon. Met behulp van een lege waarde als Hallo-patroon wordt alleen gezocht naar aanvragen toohello-hoofdmap van de geselecteerde bronserver hello (bijv, http://cdn.mydomain.com/). 
 Doel  |Hallo relatieve URL definiëren toowhich Hallo hierboven aanvragen wordt herschreven door: <br/>    1. Als u een punt voor toegang tot inhoud die een bronserver identificeert. <br/>    2. Het definiëren van een relatief pad met: <br/>        -Een reguliere-expressiepatroon <br/>        -HTTP variabelen <br/> <br/> Vervang Hallo waarden vastgelegd in Hallo bron patroon in Hallo bestemming patroon met $ _n_  waar  _n_  identificeert een waarde door Hallo volgorde waarin deze is vastgelegd. $1 vertegenwoordigt bijvoorbeeld de eerste waarde Hallo vastgelegd in het patroon van Hallo-bron, terwijl $2 Hallo tweede waarde vertegenwoordigt. 
 Deze functie kunt onze randservers toorewrite Hallo URL zonder dat u een traditionele omleiding uitvoert. Dit betekent dat aanvrager Hallo ontvangt Hallo hetzelfde antwoord code alsof Hallo herschreven URL hadden aangevraagd.

**Voorbeeldscenario 1**

In dit voorbeeld wordt gedemonstreerd hoe tooredirect rand CNAME-URL die wordt omgezet toothis basis-URL CDN: http://marketing.azureedge.net/brochures/

In aanmerking komende aanvragen worden omgeleid toothis base rand CNAME-URL: http://MyOrigin.azureedge.net/resources/

Deze URL-omleiding kan worden bereikt via Hallo volgende configuratie:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Voorbeeldscenario 2**

In dit voorbeeld wordt gedemonstreerd hoe tooredirect rand CNAME URL uit hoofdletters toolowercase reguliere expressies gebruiken.

Deze URL-omleiding kan worden bereikt via Hallo volgende configuratie:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Belangrijke punten:**

- Hallo herschrijven van URL's functie definieert Hallo URL's die herschreven aanvragen. Als gevolg hiervan zijn aanvullende overeenkomst voorwaarden niet vereist. Hoewel Hallo overeen voorwaarde is gedefinieerd als "Always", vraagt u alleen dat punt toohello 'brochures' map op Hallo 'marketing' klant oorsprong herschreven om.

- Hallo URL-segmenten die zijn vastgelegd van Hallo aanvraag zijn de nieuwe URL toegevoegde toohello via "$1."



###<a name="compatibility"></a>Compatibiliteit

Deze functie bevat die overeenkomt met de criteria waaraan moeten worden voldaan voordat het toegepast tooa aanvraag worden kan. Deze functie is niet compatibel met de volgende voorwaarden van de overeenkomst Hallo volgorde tooprevent instellen van de conflicterende vergelijkingscriterium:

- AS-nummer
- CDN-oorsprong
- IP-clientadres
- Oorsprong van de klant
- Aanvraag-schema
- URL-pad naar map
- URL-pad-uitbreiding
- URL-pad bestandsnaam
- URL-pad Literal
- URL-pad Regex
- URL-pad jokerteken
- URL-Query Literal
- URL-queryparameter
- URL-Query Regex
- URL-Query jokertekens


## <a name="next-steps"></a>Volgende stappen
* [Regels Engine verwijzing](cdn-rules-engine-reference.md)
* [Regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-conditional-expressions.md)
* [De overeenkomst motor regels](cdn-rules-engine-reference-match-conditions.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
* [Overzicht van Azure CDN](cdn-overview.md)
