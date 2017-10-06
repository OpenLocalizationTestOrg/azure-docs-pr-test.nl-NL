---
title: aaaOverview van Azure Application Insights voor DevOps | Microsoft Docs
description: Meer informatie over hoe toouse Application Insights in een Dev Ops-omgeving.
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>Overzicht van Application Insights voor DevOps

Met [Application Insights](app-insights-overview.md), u kunt snel ontdekken hoe uw app wordt uitgevoerd en wordt gebruikt wanneer het live. Er is een probleem, kunt u informatie over het helpt bij het beoordelen van Hallo impact en Hiermee kunt u bepalen Hallo oorzaak.

Hier volgt een account van een team dat webtoepassingen ontwikkelt:

* *"Een aantal dagen geleden implementeerden we een 'secundaire' hotfix. Een brede testronde niet worden uitgevoerd, maar helaas sommige onverwachte wijziging is samengevoegd in Hallo-nettolading incompatibiliteit tussen Hallo begin- en back-ends veroorzaakt. Direct serveruitzonderingen toenam, onze waarschuwing geactiveerd en wij zijn aangebracht op de hoogte van Hallo situatie. Een paar muisklikken opgeslagen op de Application Insights-portal Hallo wij voldoende informatie van de uitzondering callstacks toonarrow omlaag Hallo probleem. We onmiddellijk teruggedraaid en Hallo schade beperkt. Application Insights heeft dit deel van Hallo devops bladeren aangebracht zeer eenvoudig en actie worden uitgevoerd."*

In dit artikel wordt een team in Fabrikam Bank die Hallo ontwikkelt Volg internetbankieren system (OBS) toosee het gebruik van Application Insights tooquickly toocustomers reageren en breng wijzigingen aan.  

Hallo-team werkt op een DevOps cyclus in de volgende illustratie Hallo:

![DevOps cyclus](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Vereisten van de feed in de achterstand van hun ontwikkeling (takenlijst). Ze werken in een korte sprints, wat vaak resulteert in een werkende software - gewoonlijk in de vorm Hallo van verbeteringen en uitbreidingen toohello bestaande toepassing. Hallo live app wordt regelmatig bijgewerkt met nieuwe functies. Hoewel het live, Hallo team wordt bewaakt om prestaties en gebruik met behulp van Application Insights Hallo. Deze gegevens APM-feeds terug naar de achterstand van hun ontwikkeling.

Hallo-team gebruik maakt van Application Insights toomonitor Hallo live webtoepassing nauw voor:

* De prestaties. Ze willen toounderstand hoe reactietijden naargelang het aantal verzoeken verschillen; hoeveel CPU-, netwerk-, schijf- en andere bronnen worden gebruikt; en waar Hallo knelpunten zijn.
* Fouten. Als er uitzonderingen zijn mislukte aanvragen, of als een prestatiemeteritem buiten de vertrouwd bereik gaat, Hallo team behoeften tooknow snel zodat ze actie kunnen ondernemen.
* Het gebruik. Wanneer er een nieuwe functie wordt uitgebracht, Hallo team wilt tooknow toowhat gebied wordt gebruikt en of gebruikers problemen ermee hebt.

Laten we zich richten op Hallo feedback deel van Hallo cyclus:

![Detecteren-selectie-onderzoeken](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Slechte beschikbaarheid detecteren
Marcela Markova is een senior ontwikkelaar op Hallo OBS team, en wordt Hallo lead op online-prestaties bewaken. Ze stelt u verschillende [beschikbaarheidstests](app-insights-monitor-web-app-availability.md):

* Een test van één URL voor de belangrijkste startpagina Hallo voor Hallo-app http://fabrikambank.com/onlinebanking/. Ze stelt criteria van HTTP-code, 200 en tekst 'Welkom!'. Als deze test mislukt, is er een ernstig probleem met het Hallo-netwerk of Hallo-servers, of misschien een probleem met de implementatie. (Of iemand Hallo Welkom is gewijzigd! bericht op de pagina Hallo zonder dat haar weten.)
* Een dieper test met meerdere stappen, die zich aanmeldt en een account van de huidige aanbieding, controle van enkele belangrijke gegevens op elke pagina opgehaald. Deze test controleert dat die Hallo koppeling toohello accountdatabase werkt. Ze gebruikt een fictieve klant-id: een aantal worden bijgehouden voor testdoeleinden.

Met deze tests is ingesteld, is het Marcela er zeker van te zijn dat team Hallo snel weten over een storing.  

Fouten worden weergegeven als rood punten op Hallo web test grafiek:

![Weergave van webtests die via Hallo voorgaande periode hebben uitgevoerd](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Maar belangrijker is, een waarschuwing over een storing toohello ontwikkelteam per e-mail is verzonden. Op die manier kunnen weten ze voordat u bijna alle klanten Hallo.

## <a name="monitor-performance"></a>Prestaties bewaken
Op de overzichtspagina Hallo in Application Insights, wordt een grafiek ziet u diverse [belangrijke metrische gegevens](app-insights-web-monitor-performance.md).

![Verschillende metrische gegevens](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Laadtijd van browserpagina is afgeleid van telemetrie die rechtstreeks van webpagina's. Serverreactietijd, aantal servers-aanvraag en aantal mislukte aanvragen zijn alle gemeten in Hallo-webserver en tooApplication Insights van daaruit verzonden.

Marcela is enigszins betrokken zijn bij Hallo server antwoord grafiek. Deze grafiek toont de gemiddelde tijd Hallo tussen wanneer Hallo-server een HTTP-aanvraag van de browser van een gebruiker ontvangt, en wanneer het Hallo-antwoord geretourneerd. Ongebruikelijke toosee een variatie in deze grafiek is niet als de belasting op Hallo systeem varieert. Maar in dit geval wordt er een correlatie tussen small verhogingen in aantal Hallo van aanvragen, en big toobe stijgt Hallo reactietijd. Dat kan duiden op Hallo systeem werkt alleen bij de grenzen.

Opent ze Hallo Servers grafieken:

![Verschillende metrische gegevens](./media/app-insights-detect-triage-diagnose/06.png)

Er lijkt toobe geen teken van bronbeperking, dus mogelijk Hallo dalen in Hallo server antwoord grafieken zojuist een samenvallen zijn.

## <a name="set-alerts-toomeet-goals"></a>Toomeet doelstellingen voor waarschuwingen instellen
Ze graag niettemin tookeep gaten op Hallo reactietijden. Als ze te hoog, wil ze tooknow over deze onmiddellijk.

Zodat ze stelt een [waarschuwing](app-insights-metrics-explorer.md), reactietijden groter is dan een typische drempelwaarde. Hiermee geeft u haar erop vertrouwen dat ze over het weten moet als reactietijden traag zijn.

![Waarschuwingen-blade toevoegen](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Waarschuwingen kunnen worden ingesteld voor een groot aantal andere metrische gegevens. U kunt bijvoorbeeld e-mailberichten ontvangen als Hallo uitzondering aantal toeneemt of Hallo beschikbaar geheugen laag gaat, of als er een piek in de aanvragen van clients.

## <a name="stay-informed-with-smart-detection-alerts"></a>Blijf op de hoogte met slim Detectiewaarschuwingen
Volgende dag, een e-mailwaarschuwingen van de Application Insights binnenkomen. Maar wanneer ze de wordt geopend, ze het Hallo-antwoord tijd waarschuwing die ze ingesteld is niet gevonden. In plaats daarvan krijgt haar is er een plotselinge toename van mislukte aanvragen - dat wil zeggen, aanvragen die codes van 500 of meer fout geretourneerd.

Mislukte aanvragen zijn waarbij gebruikers een fout - doorgaans na een uitzondering opgetreden tijdens het Hallo-code hebt gezien. Mogelijk zien ze een bericht tekst "Helaas uw gegevens nu niet bijwerken." Of op absolute gênante ergste geval een Stackdump wordt weergegeven op het scherm van de gebruiker van de hello, door de webserver Hallo.

Deze waarschuwing is een onverwachte omdat hello laatste keer dat ze hebt bekeken, Hallo van mislukte aanvragen het aantal encouragingly laag is. Een klein aantal fouten is toobe verwacht in een overbelaste server.

Het is ook een stukje onverwacht voor haar omdat ze geen tooconfigure deze waarschuwing. Application Insights bevatten Slimme detectie. Automatisch wordt aangepast tooyour-app gebruikelijke fout patroon en fouten 'wordt gebruikt voor' op een bepaalde pagina of onder hoge belasting of gekoppelde tooother metrische gegevens. Er wordt een waarschuwing Hallo gegeven alleen als er een toename wordt geleverd tooexpect hierboven wat de it.

![proactieve diagnoses e](./media/app-insights-detect-triage-diagnose/21.png)

Dit is een zeer nuttig e-mailadres. Het verhogen niet alleen een waarschuwing wordt gegeven. Het komt te veel Hallo selectie en diagnostische werk.

Er wordt weergegeven hoeveel klanten door worden getroffen, en welke webpagina's of bewerkingen. Marcela kunt bepalen of ze nodig heeft tooget Hallo hele team werkt op deze als een detailanalyse fire of of kan worden genegeerd totdat de volgende week.

Hallo e-mailbericht ziet ook dat een bepaalde uitzondering is opgetreden en - nog meer interessante - gekoppeld aan een bepaalde database voor mislukte aanroepen tooa die Hallo is mislukt is. Hier wordt uitgelegd waarom Hallo veroorzaakt plotseling komt Hoewel team Marcela van updates niet onlangs geïmplementeerd.

Marcella pingt Hallo opvulteken van Hallo database team op basis van dit e-mailbericht. Ze leert dat ze een hotfix in Hallo afgelopen halfuur; vrijgegeven en Oeps, mogelijk er is een secundaire schemawijziging...

Hallo-probleem is daarom op Hallo manier toobeing opgelost, zelfs vóór het onderzoeken van Logboeken en binnen 15 minuten ervan omzetting. Marcela klikt echter op Hallo koppeling tooopen Application Insights. Deze direct door naar een mislukte aanvraag wordt geopend en kan ze zien de mislukte aanroep in de bijbehorende lijst van afhankelijkheidsaanroepen Hallo-database.

![mislukte aanvragen](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Uitzonderingen te detecteren
Met een beetje van setup [uitzonderingen](app-insights-asp-net-exceptions.md) gemelde tooApplication Insights automatisch zijn. Ze kunnen ook worden vastgelegd expliciet door het invoegen van aanroepen te[TrackException()](app-insights-api-custom-events-metrics.md#trackexception) in Hallo code in:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


Hallo Fabrikam Bank team heeft Hallo praktijk van het verzenden van telemetrie altijd op een uitzondering ontwikkeld, tenzij er een duidelijke herstel.  

In feite hun strategie is zelfs breder is dan: verzenden van telemetrie in elk geval waar Hallo klant gefrustreerd in wat is ze wilden toodo, of het overeenkomt met tooan uitzondering in Hallo code of niet. Bijvoorbeeld, als Hallo externe tussen overschrijving system het bericht 'deze transactie kan niet worden voltooid' om een operationele reden (Er is geen fout van de klant Hallo retourneert) bijhouden vervolgens zij die gebeurtenis.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException is gebruikte tooreport uitzonderingen omdat zendt het een kopie van het Hallo-stack. TrackEvent gebruikte tooreport andere gebeurtenissen is. U kunt alle eigenschappen die mogelijk nuttig zijn bij de diagnose koppelen.

Uitzonderingen en gebeurtenissen weergegeven in Hallo [diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md) blade. U kunt inzoomen in deze toosee Hallo aanvullende eigenschappen en stack-tracering.

![Gebruik filters tooshow bepaalde typen gegevens in de diagnostische gegevens doorzoeken](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Proactief bewaken
Marcela niet alleen hoeft verder niets te wachten op waarschuwingen. Snel na elke opnieuw implementeren, ze kijken neemt [reactietijden](app-insights-web-monitor-performance.md) - beide algehele afbeelding Hallo en Hallo tabel met de traagste aanvragen, evenals de uitzondering wordt geteld.  

![Antwoord tijd grafiek en een raster van reactietijden van de server.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Ze kan gevolgen voor de prestaties van elke implementatie Hallo beoordelen doorgaans elke week Hello laatste vergelijken. Als er een plotselinge verslechtering, worden ze die gegeven met relevante Hallo-ontwikkelaars.

## <a name="triage-issues"></a>Selectie problemen
-Beoordelen Hallo ernst en omvang van een probleem - selectie is de eerste stap Hallo na detectie. Moeten we Hallo-team om middernacht houden? Of kan het blijven totdat Hallo volgende handige gat in Hallo achterstand? Er zijn enkele belangrijke vragen in de selectie.

Hoe vaak gebeurt dit? Hallo grafieken op de overzichtsblade Hallo geven een perspectief tooa probleem. Bijvoorbeeld gegenereerd Hallo Fabrikam toepassing vier waarschuwingen voor web-test een nacht. Bekijkt hello grafiek in de ochtend hello, kan Hallo team zien dat er immers rode punten zijn nog steeds de meeste Hallo tests is alsof groen. Dieper ingegaan op Hallo beschikbaarheid grafiek, werd het ons duidelijk dat deze problemen uit één testlocatie zijn. Dit is natuurlijk een netwerkprobleem die invloed hebben op slechts één route en schakelt zichzelf waarschijnlijk.  

Een indrukwekkende en stabiele stijging Hallo grafiek van het aantal uitzonderingen is of reactietijden is daarentegen natuurlijk iets toopanic over.

Een e-mailbericht nuttig selectie is probeer het zelf. Als u in Hallo uitvoert hetzelfde probleem die u kent het echte is.

Welke fractie van de gebruikers worden beïnvloed? Hallo Faalpercentage tooobtain een ruwe antwoord delen door het aantal sessies van Hallo.

![Diagrammen van mislukte aanvragen en sessies](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Wanneer er trage reacties, met elkaar vergelijken Hallo tabel met de traagste reageert aanvragen Hallo gebruik frequentie van elke pagina.

Het is belangrijk scenario Hallo geblokkeerd? Als dit een functioneel probleem het verhaal van een bepaalde gebruiker worden geblokkeerd, maakt het uit veel? Als klanten hun rekeningen kunnen niet betalen, is dit ernstige; Als ze niet kunnen de kleur scherm Voorkeuren wijzigen, kunt mogelijk het wachten. detail van Hallo gebeurtenis of uitzondering of Hallo identiteit van langzame pagina Hallo Hallo, vertelt u klanten hebben waar problemen.

## <a name="diagnose-issues"></a>Problemen vaststellen
Diagnose is niet erg Hallo hetzelfde als het opsporen van fouten. Voordat u tracering via Hallo code, moet u een idee van de reden, hebben waar en wanneer Hallo probleem optreedt.

**Wanneer treedt dit?**  hello historisch overzicht geleverd door Hallo gebeurtenissen en metrische gegevens grafieken maakt het eenvoudig toocorrelate effecten met mogelijke oorzaken. Als er onregelmatige pieken in tijd of uitzondering respons, bekijkt hello aanvraag aantal: als deze waar de pieken op Hallo dezelfde time, en vervolgens het lijkt erop dat een probleem met de bronnen. Moet u tooassign meer CPU of geheugen? Of is het een afhankelijkheid opgegeven die niet Hallo load beheren?

**Het is ons?**  Als u een plotselinge afname in de prestaties van een bepaald soort aanvraag - bijvoorbeeld wanneer Hallo klant wil een rekeningoverzicht - hebt vervolgens bestaat de kans is mogelijk een extern subsysteem in plaats van uw webtoepassing. Selecteer Hallo afhankelijkheidsfout frequentie en duur afhankelijkheid tarieven in Metrics Explorer en hun geschiedenisgegevens vergelijken via Hallo na enkele uren of dagen met Hallo probleem gevonden. Als er wijzigingen zijn correleren, kan een externe subsysteem tooblame zijn.  

![Grafieken van afhankelijkheidsfout en duur van aanroepen toodependencies](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Sommige afhankelijkheidsproblemen trage zijn geolocatie problemen. Fabrikam Bank Azure virtuele machines worden gebruikt en dat ze had per ongeluk hun webserver en de server van de accountpartner in verschillende landen gevestigde gedetecteerd. Een aanzienlijk is veroorzaakt door het migreren van een van beide.

**Wat er?** Als het probleem Hallo toobe een afhankelijkheid niet wordt weergegeven, en zo niet altijd er, wordt deze waarschijnlijk veroorzaakt door een recente wijziging. Hallo historische perspectief geleverd door de metrische gegevens en gebeurtenis grafieken Hallo maakt het eenvoudig toocorrelate plotselinge wijzigingen met implementaties. Die wordt beperkt omlaag Hallo Hallo probleem zoekt.

**Wat gebeurt er?** Sommige problemen kunnen slechts zelden en moeilijk tootrack omlaag door het testen offline. Alle doen we tootry toocapture Hallo bug is als deze live optreedt. U kunt inspecteren Hallo stackdumps in uitzonderingenrapporten. Bovendien kunt u tracering-aanroepen, schrijven met uw favoriete framework voor logboekregistratie of TrackTrace() of TrackEvent().  

Fabrikam had een onregelmatig probleem met tussen account overdrachten, maar alleen met bepaalde accounttypen. toounderstand betere wat is gebeurt, ze TrackTrace() aanroepen ingevoegd op de belangrijkste punten in het Hallo-code, Hallo accounttype als een aanroep van de eigenschap tooeach koppelen. Dat was het eenvoudig toofilter uit alleen de traceringen in diagnostische gegevens doorzoeken. Ze ook parameterwaarden als eigenschappen en metingen toohello traceringsaanroepen gekoppeld.

## <a name="respond-toodiscovered-issues"></a>Toodiscovered problemen reageren
Zodra u Hallo probleem hebt vastgesteld, kunt u een plan toofix deze. Mogelijk moet u tooroll weer een recente wijziging, of misschien u kunt alleen opwekken en op te lossen. Als Hallo herstel is voltooid, Application Insights kunt u zien of u is voltooid.  

Ontwikkelteam van Fabrikam Bank nemen een meer gestructureerde benadering tooperformance meting dan ze toobefore ze Application Insights gebruikt gebruikt.

* Ze instellen prestatiedoelen in termen van specifieke maatregelen in Application Insights-overzichtspagina Hallo.
* Ze ontwerpen prestatiemetingen in de toepassing hello van Hallo starten, zoals Hallo metrische gegevens die het meten van de voortgang van de gebruiker via 'schoorstenen'.  


## <a name="monitor-user-activity"></a>Monitor gebruikersactiviteit
Wanneer reactietijd consistent goed is en er enkele uitzonderingen zijn, kunt Hallo dev-team op toousability verplaatsen. Ze nadenken over hoe tooimprove Hallo gebruikerservaring en hoe tooencourage meer gebruikers tooachieve Hallo gewenst doelstellingen.

Application Insights kunnen ook worden gebruikt toolearn wat gebruikers met een app doen. Zodra soepel wordt uitgevoerd, ook Hallo team willen er welke functies zijn de meest populaire Hallo tooknow wat gebruikers wel en hebben problemen met en hoe vaak ze terugkeren. Waarmee ze hun werk toekomstige prioriteren. En ze kunnen toomeasure Hallo succes van elk onderdeel als onderdeel van de ontwikkelingscyclus Hallo plannen. 

Een typische gebruiker reis via de website Hallo heeft bijvoorbeeld een duidelijke 'trechter'. Veel klanten bekijken Hallo frequenties van verschillende soorten lening. Een kleiner getal gaat toofill Hallo aanhalingstekens vorm. Van mensen die aan een aanhalingsteken, is enkele opwekken en verricht Hallo lening.

![Paginaweergave geteld](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Hallo bedrijven kunt u overweegt waar de grootste nummers op Hallo van klanten neerzetten, werken uit hoe tooget meer gebruikers via toohello onderaan Hallo trechter. In sommige gevallen is er mogelijk een gebruikersfout ervaring (UX) - bijvoorbeeld Hallo 'volgende' om is harde toofind of Hallo-instructies zijn niet duidelijk. Er zijn meer waarschijnlijk meer belangrijke zakelijke redenen voor drop-outs: misschien Hallo lening tarieven te hoog zijn.

Welke redenen Hallo kunt Hallo gegevens Hallo team komen wat gebruikers doen. Meer bijhouden aanroepen kunnen worden ingevoegd toowork meer details. TrackEvent() gebruikte toocount kunnen worden eventuele acties van de gebruiker, van kleine details Hallo van afzonderlijke knop klikt, toosignificant prestaties, zoals een lening af te betalen.

Hallo-team is gebruikte toohaving informatie ophalen over gebruikersactiviteit. Tegenwoordig wanneer ze een nieuwe functie ontwerpt, werken ze uit hoe ze feedback over het gebruik ervan krijgen. Ze ontwerpen bijhouden aanroepen in Hallo-functie van Hallo begin. Hallo feedback tooimprove Hallo functie van elke ontwikkelingscyclus gebruikt.

[Meer informatie over het bijhouden van gebruik](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Hallo DevOps cyclus toepassen
Dit is dus hoe een team gebruik Application Insights niet alleen toofix afzonderlijke uitgeeft, maar tooimprove levenscyclus van de ontwikkeling. Ik hoop dat het enkele ideeën over hoe Application Insights u met de prestaties van Toepassingsbeheer in uw eigen toepassingen helpen kan hebt gekregen.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen
U kunt aan de slag op verschillende manieren, afhankelijk van het Hallo-kenmerken van uw toepassing. Kies wat u het beste past:

* [ASP.NET-webtoepassing](app-insights-asp-net.md)
* [Java-webtoepassing](app-insights-java-get-started.md)
* [Node.js-webtoepassing](app-insights-nodejs.md)
* Al geïmplementeerde apps, die worden gehost op [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md), of [Azure](app-insights-azure.md).
* [Webpagina's](app-insights-javascript.md) -App met één pagina of normale webpagina - Gebruik deze zelf of in tooany toevoeging van Hallo serveropties.
* [Beschikbaarheidstests](app-insights-monitor-web-app-availability.md) tootest uw app uit Hallo openbare internet.
