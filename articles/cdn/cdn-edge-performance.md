---
title: prestaties van aaaAnalyze edge-knooppunt in Azure CDN | Microsoft Docs
description: Prestaties van edge-knooppunt in Microsoft Azure CDN analyseren. Rand prestaties Analytics biedt gedetailleerde informatie verkeer en bandbreedte gebruik voor Hallo CDN.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Prestaties van edge nod analyseren in Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Overzicht
Rand prestaties analytics biedt gedetailleerde informatie verkeer en bandbreedte gebruik voor Hallo CDN. Deze informatie kan vervolgens gebruikte toogenerate trends statistieken, waarmee u inzicht in hoe uw assets in de cache en geleverde tooyour clients worden toogain zijn. Hierdoor kunnen op zijn beurt tooform u een strategie voor hoe toooptimize Hallo levering van inhoud en toodetermine die welke problemen moet worden aangepakt toobetter hefboomwerking Hallo CDN. Als gevolg hiervan niet alleen worden kunnen tooimprove levering van prestaties, maar u ziet ook kunnen tooreduce worden uw CDN-kosten.

> [!NOTE]
> Alle rapporten gebruiken UTC/GMT-notatie bij het opgeven van een datum/tijd.
> 
> 

## <a name="reports-and-log-collection"></a>Rapporten en logboekgegevens verzameld
De activiteitsgegevens CDN moeten worden verzameld door Hallo rand prestaties Analytics module voordat deze rapporten kunt genereren. Deze verzameling gebeurt eenmaal per dag en het Hallo-activiteit die heeft plaatsgevonden tijdens de vorige dag Hallo bevat. Dit betekent dat de statistieken van het rapport een steekproef van de statistieken van de dag van de Hallo op Hallo keer is verwerkt en gaat het niet noodzakelijk vertegenwoordigen bevatten Hallo volledige set gegevens voor Hallo huidige dag. Hallo primaire functie van deze rapporten is tooassess prestaties. Ze moeten niet worden gebruikt voor factureringsdoeleinden of exacte numerieke statistieken.

> [!NOTE]
> Hallo onbewerkte gegevens waaruit rand prestaties analytische rapporten worden gegenereerd, is beschikbaar voor ten minste 90 dagen.
> 
> 

## <a name="dashboard"></a>Dashboard
Hallo rand prestaties Analytics dashboard houdt de huidige en historische CDN-verkeer via een grafiek en statistieken. Gebruik dit dashboard toodetect recente en op lange termijn trends op Hallo prestaties van CDN-verkeer voor uw account.

Dit dashboard bestaat uit:

* Een interactieve grafiek waarmee Hallo visualisatie van de belangrijkste metrische gegevens en trends.
* Een tijdlijn met een idee van de lange termijn patronen voor de belangrijkste metrische gegevens en trends.
* De belangrijkste metrische gegevens en statistische informatie over het verbetert ons netwerk CDN siteverkeer wordt gemeten door de algehele prestaties, het gebruik en efficiëntie.

### <a name="accessing-hello-edge-performance-dashboard"></a>Toegang tot Hallo rand Prestatiedashboard
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **rand leiden Analytics** doel.  Klik op **Dashboard**.
   
    Hallo edge-knooppunt analytics dashboard wordt weergegeven.

### <a name="chart"></a>Grafiek
Hallo dashboard bevat een diagram waarin een metriek bijgehouden via Hallo in Hallo tijdlijn die wordt weergegeven onder het geselecteerde periode.  Een tijdlijn die up toohello laatste twee jaar van de activiteit CDN grafieken wordt direct onder Hallo grafiek weergegeven.

#### <a name="using-hello-chart"></a>Hallo-diagram
* Standaard worden de Hallo cache efficiëntie tarief voor de afgelopen 30 dagen Hallo diagram.
* Deze grafiek is gegenereerd met gegevens die dagelijks wordt gesorteerd.
* Muiswijzer op een dag op Hallo lijngrafiek geeft een waarde voor datum en Hallo van Hallo metrische gegevens op die datum.
* Klik op markeren Weekends tootoggle een overlay lichte grijze verticale staven die tijdens het weekend naar Hallo diagram vertegenwoordigen. Dit type overlay is handig voor het identificeren van patronen in het netwerkverkeer via tijdens het weekend.
* Klik op de weergave één jaar geleden tootoggle een overlay Hallo vorige jaar voor de activiteit via Hallo dezelfde periode naar Hallo-diagram. Dit type vergelijking biedt inzicht in de lange termijn CDN gebruikspatronen. Hallo upper-rechterhoek van Hallo grafiek bevat een legenda die Hallo kleurcode voor elke regel grafiek aangeeft.

#### <a name="updating-hello-chart"></a>Hallo grafiek bijwerken
* Tijdsbereik: Voer een van de volgende Hallo:
  * Selecteer de gewenste regio Hallo in Hallo tijdlijn. Hallo-grafiek wordt bijgewerkt met gegevens die overeenkomt met toohello geselecteerde periode.
  * Dubbelklik op Hallo grafiek toodisplay alle beschikbare historische gegevens up tooa maximaal twee jaar.
* Metrische gegevens: Klik op Hallo grafiek pictogram wordt weergegeven de volgende toohello gewenst metriek. Hallo grafiek en Hallo tijdlijn wordt vernieuwd op basis van gegevens voor de bijbehorende metriek Hallo.

### <a name="key-metrics-and-statistics"></a>De belangrijkste metrische gegevens en statistieken
#### <a name="efficiency-metrics"></a>Efficiëntie metrische gegevens
Hallo-doel van deze metrische gegevens is toosee of cache-effectiviteit kan worden verbeterd. de belangrijkste voordelen Hallo afgeleid van cache-effectiviteit zijn:

* Minder belasting op de bronserver Hallo wat tot leiden kan:
  * Betere prestaties voor web-server.
  * Lagere operationele kosten.
* Gegevens levering versnelling verbeterd omdat meer aanvragen rechtstreeks vanuit Hallo CDN kunnen worden geleverd.

| Veld | Beschrijving |
| --- | --- |
| Cache-effectiviteit |Geeft Hallo percentage overgedragen gegevens die in behandeling is genomen van de cache. Deze metrische metingen wanneer er een cache versie Hallo aangevraagde inhoud is geleverd rechtstreeks vanuit Hallo CDN (randservers) toorequesters (bijvoorbeeld een webbrowser) |
| Trefferfrequentie in sjablooncache |Hiermee wordt aangegeven Hallo percentage verzoeken die zijn opgehaald uit de cache. Deze metrische metingen wanneer er een cache versie Hallo aangevraagd inhoud rechtstreeks vanuit Hallo CDN (randservers) toorequesters (bijvoorbeeld een webbrowser) is geleverd. |
| % van de externe Bytes - geen Cache-configuratie |Geeft Hallo percentage van het verkeer dat is geleverd vanuit de oorsprong servers toohello CDN (randservers) wordt niet in cache worden opgeslagen als gevolg van Hallo Bypass-Cache-functie (http-regelengine). |
| % van de externe Bytes - Cache is verlopen |Geeft Hallo percentage van het verkeer dat is geleverd vanuit de oorsprong servers toohello CDN (edge-servers) als gevolg van verouderde inhoud opnieuw te worden gevalideerd. |

#### <a name="usage-metrics"></a>Metrische gebruiksgegevens
Hallo-doel van deze metrische gegevens is tooprovide inzicht in de Hallo kostenbesparende maatregelen te volgen:

* Operationele kosten via Hallo CDN minimaliseren.
* CDN-uitgaven met cache-effectiviteit en compressie wordt verminderd.

> [!NOTE]
> Verkeer volume getallen geven aan verkeer dat is gebruikt in berekeningen van de ratio's en percentages en kan alleen een deel van het totale aantal verkeer Hallo weergeven voor klanten met hoog volume.
> 
> 

| Veld | Beschrijving |
| --- | --- |
| Ave Bytes uit |Hiermee wordt aangegeven Hallo kunt u het gemiddelde aantal bytes dat is overgedragen voor elke aanvraag die is geleverd vanuit Hallo CDN (randservers) toohello aanvrager (bijvoorbeeld een webbrowser). |
| Geen Cache-Config-Byte-snelheid |Geeft Hallo percentage verkeer die worden aangeboden via Hallo CDN (randservers) toohello aanvrager (bijvoorbeeld een webbrowser) die wordt niet in cache worden opgeslagen vanwege toohello Bypass-Cache-functie. |
| Gecomprimeerde Byte-snelheid |Geeft Hallo percentage verkeer dat wordt verzonden van Hallo CDN (randservers) toorequesters (bijvoorbeeld een webbrowser) in een gecomprimeerde indeling. |
| Verzonden bytes |Hiermee wordt aangegeven Hallo hoeveelheid gegevens, in bytes die door Hallo CDN (randservers) toohello aanvrager (bijvoorbeeld een webbrowser) zijn geleverd. |
| De bytes In |Hiermee wordt aangegeven Hallo hoeveelheid gegevens, in bytes verzonden van aanvragers (bijvoorbeeld een webbrowser) toohello CDN (randservers). |
| Extern bytes |Hiermee wordt aangegeven Hallo hoeveelheid gegevens, in bytes verzonden vanaf de CDN en klant oorsprong servers toohello CDN (randservers). |

#### <a name="performance-metrics"></a>Maatstaven voor prestaties
Hallo-doel van deze metrische gegevens is tootrack CDN prestaties voor uw-verkeer.

| Veld | Beschrijving |
| --- | --- |
| Overdrachtssnelheid |Hiermee geeft u het gemiddelde Hallo waarmee inhoud van Hallo CDN tooa aanvrager is overgedragen. |
| Duur |Geeft de gemiddelde tijd hello, in milliseconden geduurd toodeliver een asset tooa aanvrager (bijvoorbeeld een webbrowser). |
| Gecomprimeerde aanvraagsnelheid |Geeft Hallo percentage treffers geleverde van Hallo CDN (randservers) toohello aanvrager (bijvoorbeeld een webbrowser) in een gecomprimeerde indeling. |
| Frequentie van fouten 4XX |Geeft Hallo percentage treffers dat een statuscode 4xx gegenereerd. |
| Frequentie van 5xx-fouten |Geeft Hallo percentage treffers dat een 5xx-statuscode gegenereerd. |
| Treffers |Geeft het aantal aanvragen voor CDN-inhoud Hallo. |

#### <a name="secure-traffic-metrics"></a>Beveiligd verkeer metrische gegevens
Hallo-doel van deze metrische gegevens is tootrack CDN prestaties voor HTTPS-verkeer.

| Veld | Beschrijving |
| --- | --- |
| Cache-effectiviteit beveiligen |Hiermee wordt aangegeven Hallo percentage van de gegevens voor HTTPS-aanvragen die zijn overgebracht uit cache. Met deze metriek meet wanneer een versie van Hallo cache aangevraagde inhoud is geleverd rechtstreeks vanuit Hallo CDN (randservers) toorequesters (bijvoorbeeld een webbrowser) via HTTPS. |
| Overdrachtssnelheid beveiligen |Geeft het gemiddelde Hallo waarmee inhoud van Hallo CDN (randservers) toorequesters (bijvoorbeeld webservers) is overgedragen via HTTPS. |
| Gemiddelde duur van de beveiligde |Geeft de gemiddelde tijd hello, in milliseconden geduurd toodeliver een asset tooa aanvrager (bijvoorbeeld een webbrowser) via HTTPS. |
| Beveiligde treffers |Geeft het aantal HTTPS-aanvragen voor CDN-inhoud Hallo. |
| Verzonden Bytes beveiligen |Hiermee wordt aangegeven Hallo hoeveelheid HTTPS-verkeer, in bytes die door Hallo CDN (randservers) toohello aanvrager (bijvoorbeeld een webbrowser) zijn geleverd. |

## <a name="reports"></a>Rapporten
Elk rapport in deze module bevat een grafiek en statistieken over gebruik van bandbreedte en verkeer voor verschillende soorten metrische gegevens (bijv, HTTP-statuscodes, cache statuscodes, aanvraag-URL, enz.). Deze informatie is mogelijk gebruikte toodelve dieper in hoe inhoud wordt aangeleverd tooyour clients en toofine afstemmen CDN gedrag tooimprove leveringsprestaties.

### <a name="accessing-hello-edge-performance-reports"></a>Hallo rand prestatierapporten openen
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **Analytics** tabblad en houd de muis boven Hallo **rand leiden Analytics** doel.  Klik op **HTTP Large Object**.
   
    edge-knooppunt analytics Rapporten welkomstscherm wordt weergegeven.

| Rapport | Beschrijving |
| --- | --- |
| Dagelijkse samenvatting |Hiermee kunt u de dagelijkse verkeer trends tooview gedurende een opgegeven periode. Elke staaf in deze grafiek vertegenwoordigt een bepaalde datum. Hallo-grootte van Hallo balk geeft Hallo kunt u het totaal aantal treffers die is opgetreden op die datum. |
| Samenvatting van per uur |Hiermee kunt u tooview per uur verkeer trends gedurende een opgegeven periode. Elke staaf in deze grafiek vertegenwoordigt één uur op een bepaalde datum. Hallo-grootte van Hallo balk geeft Hallo kunt u het totaal aantal treffers die is opgetreden tijdens dat uur. |
| Protocollen |Geeft Hallo uitsplitsing van verkeer tussen Hallo HTTP en HTTPS-protocollen. Een grafiek ring geeft Hallo percentage treffers dat is opgetreden voor elk type protocol. |
| HTTP-methoden |Hiermee kunt u een idee van welke HTTP-methoden zijn tooget gebruikte toorequest worden uw gegevens. Hallo meest voorkomende HTTP-aanvraagmethoden zijn meestal GET, HEAD en POST. Een grafiek ring geeft Hallo percentage treffers dat is opgetreden voor elk type HTTP-aanvraagmethode. |
| URL 's |Bevat een grafiek waarin Hallo bovenste 10 aangevraagde URL's. Een balk weergegeven voor elke URL. Hallo hoogte van Hallo balk geeft aan hoeveel treffers dat bepaalde URL is gegenereerd via Hallo tijdsspanne waarvoor Hallo-lijst. Statistieken voor Hallo top 100 aangevraagde dat URL 's direct onder deze grafiek worden weergegeven. |
| CNAME-records |Bevat een grafiek die wordt weergegeven Hallo bovenste 10 CNAMEs gebruikt toorequest activa via de tijdsspanne Hallo van een rapport. Statistieken voor Hallo top 100 aangevraagd dat cnames direct onder deze grafiek worden weergegeven. |
| Oorsprongen |Bevat een grafiek waarin Hallo top 10 CDN of klant oorsprong servers van waaruit de activa zijn aangevraagd gedurende een opgegeven periode. Statistieken voor Hallo top 100 aangevraagd CDN of klant oorsprong-servers direct onder deze grafiek worden weergegeven. Klant oorsprong servers worden geïdentificeerd door Hallo naam gedefinieerd in Hallo mapnaam optie. |
| Geo-POP 's |Geeft aan hoeveel van uw verkeer wordt gerouteerd via een bepaalde point-of-presence (POP). afkorting van drie letters Hallo vertegenwoordigt een pop-server in onze CDN-netwerk. |
| Clients |Bevat een grafiek die Hallo bovenste 10 geeft clients weer die activa aangevraagd gedurende een opgegeven periode. Voor Hallo toepassing van dit rapport worden alle aanvragen die afkomstig zijn uit Hallo dezelfde IP-adres worden beschouwd als toobe van Hallo dezelfde client. Statistieken voor top 100 clients Hallo worden direct onder deze grafiek weergegeven. Dit rapport is nuttig voor het bepalen van de download activiteit patronen voor uw eerste clients. |
| Cache-statussen |Geeft een gedetailleerde verdeling van het gedrag van de cache, die waarschijnlijk strategieën voor het verbeteren van de algehele gebruikerservaring Hallo. Aangezien de snelste prestaties Hallo afkomstig zijn van treffers in cache, kunt u gegevens levering snelheden door Minimalisatie van het aantal Cachemissers en treffers in cache verlopen optimaliseren. |
| GEEN Details |Bevat een grafiek waarin Hallo bovenste 10 URL's voor activa waarvoor inhoud versheid van cache niet is ingeschakeld gedurende een opgegeven periode. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| CONFIG_NOCACHE Details |Een grafiek waarin Hallo top 10 URL's voor de activa die niet in cache vervaldatum van de klant toohello CDN configuratie opgeslagen zijn bevat. Deze typen elementen zijn geleverd rechtstreeks vanuit het Hallo-bronserver. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| UNCACHEABLE Details |Een grafiek waarin Hallo bovenste 10 URL's voor de activa die niet kunnen worden opgeslagen vanwege toorequest headergegevens bevat. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| TCP_HIT Details |Bevat een grafiek waarin Hallo bovenste 10 URL's voor bedrijfsmiddelen die onmiddellijk uit cache worden behandeld. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| TCP_MISS Details |Bevat een grafiek die Hallo bovenste 10 URL's voor de activa die de Cachestatus van een van TCP_MISS weergeeft. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| TCP_EXPIRED_HIT Details |Bevat een grafiek waarin Hallo bovenste 10 URL's voor verouderde activa die rechtstreeks door Hallo pop-server zijn geleverd. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| TCP_EXPIRED_MISS Details |Bevat een grafiek waarin Hallo bovenste 10 URL's voor verouderde activa waarvoor een nieuwe versie opgehaald van de bronserver Hallo toobe had. Statistieken voor Hallo top 100 URL's voor deze typen van assets weergegeven voor direct onder deze grafiek. |
| TCP_CLIENT_REFRESH_MISS Details |Bevat een staafdiagram waarin Hallo bovenste 10 URL's voor activa zijn opgehaald van een bronserver vanwege tooa Nee-cache-aanvraag van het Hallo-client. Statistieken voor Hallo top 100 URL's voor deze typen aanvragen worden direct onder deze grafiek weergegeven. |
| Client-aanvraagtypen |Geeft Hallo-type van aanvragen die zijn gemaakt met de HTTP-clients (bijvoorbeeld browsers). Dit rapport bevat een grafiek ring met een idee als toohow aanvragen worden verwerkt. Informatie over bandbreedte en verkeer voor elk aanvraagtype wordt onder Hallo grafiek weergegeven. |
| Gebruikersagent |Bevat een staafdiagram weergegeven Hallo bovenste 10 gebruiker agents toorequest uw inhoud via onze CDN. Een gebruikersagent is meestal een webbrowser, Mediaspeler of de browser van een mobiele telefoon. Statistieken voor Hallo top 100-gebruikersagenten worden direct onder deze grafiek weergegeven. |
| Verwijzingen |Bevat een staafdiagram Hallo bovenste 10 verwijzingen toocontent toegankelijk is via onze CDN om weer te geven. Een verwijzende is doorgaans het Hallo-URL van de webpagina Hallo of bron die is gekoppeld aan tooyour inhoud. Hieronder Hallo grafiek vindt u gedetailleerde informatie voor Hallo top 100 verwijzingen. |
| Compressietypen |Bevat een grafiek ring uitsplitsing van aangevraagde activa of ze onze randservers zijn gecomprimeerd. Hallo percentage van de gecomprimeerde activa wordt opgedeeld per Hallo type compressie gebruikt. Hieronder Hallo grafiek vindt u gedetailleerde informatie voor elk compressietype en status. |
| Bestandstypen |Bevat een staafdiagram waarin Hallo bovenste 10 bestandstypen die zijn aangevraagd via onze CDN voor uw account. Voor Hallo toepassing van dit rapport wordt een bestandstype wordt gedefinieerd door de bestandsnaamextensie van Hallo actief en mediatype Internet (bijvoorbeeld .html \[text/html\], .htm \[text/html\], .aspx \[text/html\], enz.). Hieronder Hallo grafiek vindt u gedetailleerde informatie voor Hallo top 100-bestandstypen. |
| Unieke bestanden |Bevat een grafiek dat worden uitgezet Hallo kunt u het totale aantal unieke assets die zijn aangevraagd op een bepaalde dag gedurende een opgegeven periode. |
| Token Auth-samenvatting |Bevat een cirkeldiagram waarmee een snel overzicht op of de aangevraagde activa zijn beveiligd door verificatie op basis van tokens. Beveiligde activa worden weergegeven in het Hallo-grafiek volgens toohello resultaten van de poging tot verificatie. |
| Token Auth weigeren Details |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen die zijn geweigerd vanwege tooToken gebaseerde verificatie. |
| HTTP-reactiecodes |Bevat een verdeling van Hallo HTTP-statuscodes (bijvoorbeeld 200 OK 403 verboden, 404 niet wordt gevonden, enzovoort) die tooyour HTTP-clients zijn geleverd door onze randservers. U kunt een cirkeldiagram tooquickly vast hoe uw assets zijn opgehaald. Gedetailleerde statistische gegevens is beschikbaar voor elke antwoordcode onder Hallo-grafiek. |
| 404-fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen met een antwoordcode 404 niet gevonden. |
| 403 fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen dat heeft geresulteerd in een 403-verboden-antwoordcode. Een 403-verboden-antwoordcode treedt op wanneer een aanvraag wordt geweigerd door een customer oorsprong-server of een edge-server op onze pop-server. |
| 4XX fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen met een antwoordcode in Hallo 400 bereik. 403 uitgesloten van dit rapport zijn niet gevonden en 404 verboden-responscodes. Reactiecode 4xx treedt meestal op wanneer een aanvraag wordt geweigerd als gevolg van een fout op de client. |
| 504 fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen dat heeft geresulteerd in een 504 Gateway Timeout-antwoordcode. Een 504 Gateway Timeout-antwoordcode treedt op wanneer een time-out optreedt bij een HTTP-proxy is het toocommunicate met een andere server. In geval van onze CDN Hallo 504 Gateway Timeout reactiecode doorgaans treedt op wanneer een edge-server kan geen tooestablish communicatie met een klant-bronserver. |
| 502-fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen dat heeft geresulteerd in een 502 Ongeldige Gateway-antwoordcode. Een 502 Ongeldige Gateway-antwoordcode treedt op wanneer er een HTTP-protocol-fout optreedt tussen een server en een HTTP-proxy. In geval van onze CDN Hallo een 502 Ongeldige Gateway-antwoordcode treedt meestal op wanneer een klant-bronserver een ongeldige reactie tooan edge-server retourneert. Een antwoord is ongeldig als kan niet worden geparseerd of onvolledig is. |
| 5XX-fouten |Bevat een staafdiagram waarmee u tooview Hallo bovenste 10 aanvragen met een antwoordcode in Hallo 500 bereik.  Uitgesloten van dit rapport zijn 502 Slechte Gateway en 504 Gateway Timeout-responscodes. |

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure CDN](cdn-overview.md)
* [Realtime statistieken in Microsoft Azure CDN](cdn-real-time-stats.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
* [Geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md)

