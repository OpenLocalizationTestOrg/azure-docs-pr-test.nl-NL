---
title: Detectie - afwijkingen aaaSmart | Microsoft Docs
description: "Application Insights voert smart analyse van uw app Telemetrie en waarschuwt u potentiële problemen. Er zijn geen instellingen, moet deze functie."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Slimme detectie - afwijkingen

[Application Insights](app-insights-overview.md) automatisch Hallo prestaties van uw webtoepassing analyseert en kunt u gewaarschuwd over mogelijke problemen. U kan worden gelezen dit omdat u een van onze Slimme detectie meldingen ontvangen.

Dit onderdeel vereist geen speciale instellingen, dan het configureren van de app voor Application Insights (op [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), of [Node.js](app-insights-nodejs.md), en in [code webpagina](app-insights-javascript.md)). Het is actief wanneer uw app genoeg telemetrie genereert.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Wanneer een melding Slimme detectie krijgt?

Application Insights gedetecteerd prestaties van uw toepassing hello piekactiviteit in een van de volgende manieren:

* **Antwoord tijd vermindering** -uw app is gestart toorequests langzamer dan gebruikt om te reageren. Hallo wijziging mogelijk is de snelle, bijvoorbeeld omdat er een regressie in uw meest recente implementatie. Of het mogelijk is de geleidelijke, mogelijk veroorzaakt door een geheugenlek. 
* **Afhankelijkheid duur vermindering** -kunt u uw app tooa REST-API aanroepen, database of andere afhankelijkheid. Hallo-afhankelijkheid reageert langzamer dan voorheen.
* **Trage prestaties patroon** -uw app wordt weergegeven toohave prestaties van een probleem dat alleen bepaalde aanvragen beïnvloedt. Bijvoorbeeld, worden pagina's trager geladen op één type browser dan andere; of de aanvragen van een bepaalde server trager zijn wordt geleverd. Op dit moment kijken onze algoritmen laadtijden voor pagina's, reactietijden van de aanvraag en reactietijden van de afhankelijkheid.  

Detectie van de smartcard moet ten minste acht dagen telemetrie bij een werkbare volume in de volgorde tooestablish een basislijn van de normale prestaties. Dus nadat uw toepassing actief is geweest gedurende die tijd, leidt eventuele belangrijke problemen tot een melding.


## <a name="does-my-app-definitely-have-a-problem"></a>Beschikt over mijn app zeker een probleem?

Nee, een melding betekent dat uw app zeker een probleem heeft niet. Het is gewoon een suggestie over iets die kunt u toolook op beter.

## <a name="how-do-i-fix-it"></a>Hoe kan ik oplossen?

Hallo meldingen bevatten diagnostische gegevens. Hier volgt een voorbeeld:


![Hier volgt een voorbeeld van Server antwoord tijd vermindering detectie](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Selectie**. Hallo-melding ziet u hoeveel gebruikers of hoeveel bewerkingen worden beïnvloed. Hierdoor kunt u een prioriteit toohello probleem toewijzen.
2. **Bereik**. Hallo probleem invloed op alle verkeer of slechts enkele's? Is beperkt it tooparticular browsers of locaties? Deze informatie kan worden verkregen vanaf Hallo-melding.
3. **Diagnose**. Diagnostische gegevens in de melding Hallo Hallo voorgesteld vaak Hallo aard van Hallo probleem. Bijvoorbeeld, als reactietijd vertraagd als aanvraagsnelheid hoog is, die stelt voor dat uw server of afhankelijkheden overbelast zijn. 

    Open de blade Performance Hallo anders in Application Insights. Daar vindt u [Profiler](app-insights-profiler.md) gegevens. Als er uitzonderingen worden veroorzaakt, kunt u ook Hallo proberen [momentopname foutopsporingsprogramma](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>E-mailmeldingen configureren

Smart detectie meldingen zijn standaard ingeschakeld en toothose die hebben verzonden [eigenaren, bijdragers en lezers toegang krijgen tot de Application Insights-resource toohello](app-insights-resources-roles-access-control.md). toochange dit, klik op **configureren** in e-mailmelding Hallo of Slimme detectie-instellingen in de Application Insights openen. 
  
  ![Detectie-instellingen van smartcard](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * U kunt Hallo **opzeggen** koppeling in Hallo Slimme detectie e toostop Hallo e-mailmeldingen ontvangen.

E-mailberichten over afwijkingen Smart detecties zijn beperkt tooone e per dag per Application Insights-resource. alleen als er ten minste één nieuwe probleem dat is gedetecteerd op die dag Hallo e-mailadres verzonden. U won't wordt herhaald van elk bericht ophalen. 

## <a name="faq"></a>Veelgestelde vragen

* *Ja, bekijkt u die mijn gegevens?*
  * Nee. Hallo-service is geheel automatisch. Alleen het ophalen van Hallo meldingen. Uw gegevens [persoonlijke](app-insights-data-retention-privacy.md).
* *U alle Hallo gegevens verzameld door Application Insights analyseren?*
  * Niet op dit moment. Op dit moment kunnen analyseren we aanvraag die de laadtijd van reactietijd, afhankelijkheid reactietijd en pagina. Analyse van aanvullende gegevens is op onze benieuwd achterstand.

* Welke typen toepassingen werkt dit voor?
  * Deze degradations worden gedetecteerd in elke toepassing die Hallo juiste telemetrie genereert. Als u Application Insights in uw web-app hebt geïnstalleerd, worden klikt u vervolgens aanvragen en afhankelijkheden automatisch bijgehouden. Maar in de back-end-services of andere apps, als u de aanroepen te ingevoegd[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) of [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), en vervolgens Slimme detectie in Hallo dezelfde werkt manier.

* *Kan ik mijn eigen afwijkingsdetectie detectieregels maken of aanpassen van bestaande regels?*

  * Nog niet, maar u kunt:
    * [Stel waarschuwingen](app-insights-alerts.md) waarmee wordt aangegeven dat wanneer een metriek een drempelwaarde overschrijdt.
    * [Exporteren van telemetrie](app-insights-export-telemetry.md) tooa [database](app-insights-code-sample-export-sql-stream-analytics.md) of [tooPowerBI](app-insights-export-power-bi.md), waar u kunt deze analyseren zelf.
* *Hoe vaak wordt Hallo analyse uitgevoerd?*

  * Dagelijks Hallo analyse voor Hallo telemetrie van Hallo vorige dag (volledige dag in UTC-tijdzone).
* *Zo biedt deze vervangen [metrische waarschuwingen](app-insights-alerts.md)?*
  * Nee.  We doorvoeren niet toodetecting elke gedrag op dat u abnormale overwegen kunt.


* *Als ik iets in clientbeveiligingssessie tooa melding niet doet, krijg een herinnering?*
  * Nee, u krijgt een bericht over elk probleem slechts één keer. Als Hallo probleem zich blijft voordoen wordt deze in Hallo die Slimme detectie feed blade worden bijgewerkt.
* *Ik Hallo e-mailbericht is verbroken. Waar vind ik Hallo meldingen in Hallo-portal*
  * In Application Insights-overzicht Hallo van uw app, klikt u op Hallo **Slimme detectie** tegel. U zult er kunnen toofind back-alle meldingen too90 dagen.

## <a name="how-can-i-improve-performance"></a>Hoe kan ik de prestaties verbeteren?
Trage en mislukte antwoorden zijn een van de grootste frustraties Hallo voor gebruikers van de website, zoals u uit uw eigen ervaring weet. Het is dus belangrijk tooaddress Hallo problemen.

### <a name="triage"></a>Selectie
Eerst maakt het uit? Als een pagina altijd trage tooload is, maar slechts 1% van de gebruikers van uw site ooit toolook op deze hebt, misschien hebt u belangrijkere zaken toothink over. Hallo daarentegen op als er slechts 1% van de gebruikers openen, maar deze uitzonderingen genereert telkens die mogelijk waard.

Hallo impact-instructie (betrokken gebruikers of % van het verkeer) gebruiken als algemene richtlijnen, maar houd er rekening mee dat niet het gehele artikel Hallo. Andere tooconfirm bewijs verzamelen.

Overweeg het Hallo-parameters van het Hallo-probleem. Als het Geografie-afhankelijk is, kunt u instellen [beschikbaarheidstests](app-insights-monitor-web-app-availability.md) met inbegrip van die regio: er simpelweg mogelijk problemen met netwerken in het desbetreffende gebied.

### <a name="diagnose-slow-page-loads"></a>Diagnose van trage pagina wordt geladen
Waar bevindt zich Hallo probleem? Hallo server trage toorespond is, is erg lang Hallo-pagina of Hallo browser heeft toodo veel werk toodisplay deze?

Hallo Browsers metrische blade geopend. Hallo gesegmenteerde weergave van de browser load tijd wordt aangegeven waar Hallo gaan. 

* Als **aanvraagtijd verzenden** is hoog is, ofwel Hallo server reageert langzaam of Hallo-aanvraag is een bericht met een grote hoeveelheden gegevens. Bekijkt hello [maatstaven voor prestaties](app-insights-web-monitor-performance.md#metrics) tooinvestigate reactietijden.
* Instellen van [bijhouden van afhankelijkheid](app-insights-asp-net-dependencies.md) toosee Hallo traagheid wordt aangegeven of vervaldatum tooexternal services of de database.
* Als **reactie ontvangen van** overwegend, wordt de pagina en de afhankelijke onderdelen - JavaScript, CSS, afbeeldingen, enzovoort (maar niet asynchroon geladen gegevens) lang zijn. Instellen van een [beschikbaarheidstest](app-insights-monitor-web-app-availability.md), en ervoor tooset Hallo optie tooload afhankelijke onderdelen. Als u bepaalde resultaten krijgt, Hallo details van een resultaat open en vouw dit toosee Hallo laden van de tijd van de verschillende bestanden.
* Hoge **Client verwerkingstijd** wordt voorgesteld scripts langzaam worden uitgevoerd. Hallo reden niet duidelijk, overweeg timing code als Hallo keren verzenden in trackMetric aanroepen.

### <a name="improve-slow-pages"></a>Langzame pagina's verbeteren
Er is een volledige van advies over het verbeteren van uw antwoorden van de server en de laadtijden voor pagina's, zodat we toorepeat won't proberen web alle hier. Hier volgen enkele tips die u waarschijnlijk al, net tooget kent u denkt:

* Langzaam laden vanwege de grote bestanden: asynchroon laden van Hallo scripts en andere onderdelen. Gebruik script bundeling. Hallo hoofdpagina opdelen in widgets die hun gegevens afzonderlijk laden. Gewone oude HTML voor lange tabellen niet verzenden: een script toorequest Hallo gegevens gebruiken als JSON of andere gecomprimeerde indeling en klik vervolgens Hallo tabel invullen. Er zijn frameworks geweldige toohelp de. (Zij ook inhouden big scripts natuurlijk.)
* Trage server afhankelijkheden: overweeg Hallo geografische locaties van de onderdelen van uw. Bijvoorbeeld, als u Azure gebruikt, controleert u of Hallo-webserver en Hallo-database in Hallo dezelfde regio. Query's meer gegevens dan ze nodig hebben ophalen? Caching of help batchverwerking zou?
* Capaciteit problemen: bekijkt hello metrische servergegevens van responstijden en het aantal aanvragen. Als de responstijden pieksnelheden niet goed met pieken in aanvraag aantallen, is het waarschijnlijk dat uw servers worden uitgerekt.


## <a name="server-response-time-degradation"></a>Antwoord tijd verslechtering van server

Hallo antwoord tijd vermindering melding vertelt u:

* Hallo reactietijd vergeleken toonormal reactietijd voor deze bewerking.
* Hoeveel gebruikers zijn beïnvloed.
* Gemiddelde responstijd en 90 percentiel reactietijd voor deze bewerking op de dag Hallo Hallo detectie-en zeven dagen voor. 
* Telling van deze bewerking aanvragen op Hallo dag van Hallo detectie en zeven dagen voor.
* Correlatie tussen vermindering in deze bewerking en degradations in de bijbehorende afhankelijkheden. 
* Koppelingen toohelp u Hallo probleem diagnosticeren.
  * Profiler traceert toohelp u weergeven waar bewerkingstijd is besteed (Hallo-koppeling is beschikbaar als Profiler trace voorbeelden voor deze bewerking tijdens de detectieperiode Hallo zijn verzameld). 
  * Prestatierapporten in metriek Explorer kunt u segmenteren en Tijdfilters bereik voor deze bewerking te analyseren.
  * Zoeken naar dit roept tooview aanroepen van specifieke eigenschappen.
  * Fout rapporteert - als > 1 dit betekenen dat er fouten zijn opgetreden in deze bewerking dat mogelijk hebben bijgedragen tooperformance vermindering tellen.

## <a name="dependency-duration-degradation"></a>Verslechtering van de duur van de afhankelijkheid

Moderne toepassingen vast meer ontwerpbenadering micro services, wat in veel gevallen tooheavy betrouwbaarheid leidt op externe services. Bijvoorbeeld, als uw toepassing, is afhankelijk van bepaalde gegevensplatform of zelfs wanneer u uw eigen bot-service dat u waarschijnlijk zal relay op sommige cognitieve serviceprovider tooenable uw toointeract bots op meer menselijke manieren en bepaalde gegevens worden opgeslagen service voor bot toopull Hallo antwoorden uit.  

Voorbeeld afhankelijkheid vermindering melding:

![Hier volgt een voorbeeld van afhankelijkheid duur vermindering detectie](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

U ziet dat het vertelt u:

* Hallo duur vergeleken toonormal reactietijd voor deze bewerking
* Hoeveel gebruikers worden beïnvloed
* Gemiddelde duur en 90 percentiel duur voor deze afhankelijkheid op Hallo dag van Hallo detectie en zeven dagen voor
* Dit is het aantal afhankelijkheid aanroepen op Hallo dag van Hallo detectie en zeven dagen voor
* Koppelingen toohelp u Hallo probleem onderzoeken
  * Prestatierapporten in Verkenner metrische gegevens voor deze afhankelijkheid
  * Zoeken naar deze afhankelijkheid roept tooview aanroepen eigenschappen
  * Rapporten van de fout - als het aantal > 1 dit betekenen dat er mislukte afhankelijkheid zijn aangeroepen tijdens de detectie Hallo periode die mogelijk hebben bijgedragen tooduration nadelig beïnvloeden. 
  * Open Analytics met query's die deze afhankelijkheid duur en het aantal berekenen  

## <a name="smart-detection-of-slow-performing-patterns"></a>Slimme detectie van trage presterende patronen 

Application Insights vindt prestatieproblemen die mogelijk alleen van invloed op een gedeelte van uw gebruikers of alleen van invloed op gebruikers in sommige gevallen. Meldingen over het laden van pagina's is bijvoorbeeld slowler op één type browser dan op andere typen browsers, of als aanvragen langzamer worden geleverd vanuit een bepaalde server. Het kan ook problemen met de combinaties van eigenschappen, detecteren, zoals trage pagina wordt geladen in een geografisch gebied voor clients met specifieke besturingssysteem.  

Afwijkingen zoals deze zijn zeer moeilijk toodetect door Hallo gegevens te bekijken, maar komen vaker dan u denkt. Vaak surface ze alleen wanneer uw klanten klagen. Die tijd is te laat: Hallo van invloed op gebruikers al tooyour concurrenten overschakelt!

Op dit moment kijken onze algoritmen laadtijden voor pagina's, reactietijden van de aanvraag op Hallo-server en reactietijden van de afhankelijkheid.  

U geen tooset zijn alle drempelwaarden of regels configureren. Machine learning en gegevensanalyse-algoritmen zijn gebruikte toodetect afwijkende patronen.

![E-mailmelding hello, klik op Hallo koppeling tooopen Hallo diagnostisch rapport in Azure](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Wanneer** toont Hallo tijd Hallo probleem is gedetecteerd.
* **Wat** wordt beschreven:

  * Hallo-probleem dat is gedetecteerd;
  * Hallo-kenmerken van Hallo ingesteld van gebeurtenissen die we gevonden Hallo probleem gedrag weergegeven.
* Hallo tabel vergelijkt Hallo slecht presterende set met Hallo gemiddelde gedrag van alle andere gebeurtenissen.

Klik Hallo koppelingen tooopen metriek Explorer en zoek op de relevante rapporten, gefilterd op Hallo tijd en eigenschappen van Hallo trage set uitvoeren.

Hallo tijd bereik en filters tooexplore telemetrie Hallo wijzigen.

## <a name="next-steps"></a>Volgende stappen
Deze diagnostische hulpprogramma's kunnen u controleren Hallo telemetrie van uw app:

* [Profiler](app-insights-profiler.md) 
* [Momentopname-foutopsporingsprogramma](app-insights-snapshot-debugger.md)
* [Analytische gegevens](app-insights-analytics-tour.md)
* [Diagnostische gegevens voor de analyse van de smartcard](app-insights-analytics-diagnostics.md)

Smart detecties zijn volledig automatisch. Maar misschien wilt u tooset van sommige waarschuwingen meer?

* [Handmatig geconfigureerde metrische waarschuwingen](app-insights-alerts.md)
* [Webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md)
