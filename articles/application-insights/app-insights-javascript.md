---
title: aaaAzure Application Insights voor JavaScript web-apps | Microsoft Docs
description: Verzamel tellingen van het aantal paginaweergaven en sessies, webclientgegevens en gebruikspatronen. Detecteer uitzonderingen en prestatieproblemen in JavaScript-webpagina's.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights voor webpagina’s
Lees over Hallo prestaties en het gebruik van uw webpagina's of app. Als u [Application Insights](app-insights-overview.md) tooyour pagina script, krijgt u de tijdsinstellingen van pagina's en AJAX-aanroepen, tellingen en details van browseruitzonderingen en AJAX-fouten, evenals gebruikers en aantallen sessie. Al deze gegevens kunnen worden gesegmenteerd op pagina, clientbesturingssysteem en browserversie, geografische locatie en andere dimensies. U kunt waarschuwingen instellen voor foutaantallen of het langzaam laden van de pagina. En door het invoegen van traceringsaanroepen in uw JavaScript-code, kunt u bijhouden hoe verschillende functies van uw webpagina-toepassing hello worden gebruikt.

Application Insights kan met elke webpagina worden gebruikt. Het enige wat u hiervoor hoeft te doen, is een klein stukje JavaScript toevoegen. Als de webservice [Java](app-insights-java-get-started.md) of [ASP.NET](app-insights-asp-net.md) is, kunt u telemetrie van uw server en clients integreren.

![Open de resource van uw app in portal.azure.com en klik op Browser](./media/app-insights-javascript/03.png)

U hebt een abonnement te[Microsoft Azure](https://azure.com). Als uw team een organisatie-abonnement heeft, vraagt u Hallo eigenaar tooadd uw tooit Microsoft-Account. Ontwikkeling en kleinschalig gebruik kosten u niets.

## <a name="set-up-application-insights-for-your-web-page"></a>Application Insights instellen voor uw webpagina
Hallo loader code codefragment tooyour webpagina's, als volgt toevoegen.

### <a name="open-or-create-application-insights-resource"></a>Een Application Insights-resource openen of maken
Hallo Application Insights-resource worden gegevens over de prestaties en het gebruik van uw pagina wordt weergegeven. 

Meld u aan bij de [Azure Portal](https://portal.azure.com).

Als u al een controle voor de serverzijde Hallo van uw app ingesteld, hebt u al een resource:

![Kies Bladeren, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-find.png)

Als u nog geen resource hebt, maakt u er een:

![Kies Nieuw, Ontwikkelaarsservices, Application Insights.](./media/app-insights-javascript/01-create.png)

*Heb u op dit moment vragen?* [Meer over het maken van een resource](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Hallo SDK script tooyour app of webpagina toevoegen
Haal Hallo script voor webpagina's in Snel starten:

![Op de overzichtsblade van uw app, kiest u snel starten, kunt u code toomonitor mijn webpagina's. Hallo script kopiëren.](./media/app-insights-javascript/02-monitor-web-page.png)

Voeg Hallo script net vóór Hallo `</head>` tag van elke pagina die u wilt tootrack. Als uw website een basispagina heeft, kunt u er Hallo script plaatsen. Bijvoorbeeld:

* In een ASP.NET-MVC-project plaatst u het in `View\Shared\_Layout.cshtml`
* Open in een SharePoint-site op Hallo van het Configuratiescherm, [Site-instellingen / basispagina](app-insights-sharepoint.md).

Hallo-script bevat de instrumentatiesleutel Hallo waarin wordt verwezen Hallo gegevens tooyour Application Insights-resource. 

([Nadere uitleg van Hallo-script. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Als u een bekend webpaginaframework gebruikt, is het een goed idee om op zoek te gaan naar een geschikte Application Insights-adapter. Er is bijvoorbeeld een [AngularJS-module](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Gedetailleerde configuratie
U kunt diverse [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) instellen. In de meeste gevallen is dat echter niet nodig. U kunt bijvoorbeeld uitschakelen of beperken Hallo aantal Ajax-aanroepen per paginaweergave (tooreduce verkeer) gerapporteerd. Of u kunt de foutopsporing modus toohave telemetrie verplaatsen snel via Hallo pipeline instellen zonder in batch worden opgenomen.

tooset deze parameters zoekt u deze regel in het codefragment Hallo en meer door komma's gescheiden items toevoegen nadat deze:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Hallo [beschikbare parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) omvatten:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Uw app uitvoeren
Uw web-app uitvoeren, gebruiken een tijdens toogenerate Telemetrie en wacht een paar seconden. U kunt uitvoeren met behulp van Hallo **F5** sleutel op uw ontwikkelcomputer of publiceren en door gebruikers laten uitproberen aan.

Als u toocheck Hallo telemetrie wilt dat een web-app tooApplication Insights verzendt, gebruikt u de foutopsporingsprogramma's van de browser (**F12** in veel browsers). Gegevens worden toodc.services.visualstudio.com verzonden.

## <a name="explore-your-browser-performance-data"></a>Gegevens over uw browserprestaties verkennen
Open Hallo Browser blade tooshow geaggregeerd prestatiegegevens van de browsers van uw gebruikers.

![Open de resource van uw app in portal.azure.com en klik op Instellingen, Browser](./media/app-insights-javascript/03.png)

*Zijn er nog geen gegevens? Klik op **vernieuwen** bovenaan Hallo Hallo pagina. Ziet u nog steeds niets? Raadpleeg [Probleemoplossing](app-insights-troubleshoot-faq.md).*

Hallo Browser blade is een [Metrics Explorer-blade](app-insights-metrics-explorer.md) met vooraf ingestelde filters en grafiekselecties. U kunt het tijdsbereik hello, filters en configuratie van de grafiek bewerken als u wilt en Hallo resultaat als favoriet opslaan. Klik op **standaardwaarden herstellen** tooget back toohello oorspronkelijke bladeconfiguratie.

## <a name="page-load-performance"></a>Laadprestaties van de pagina
Hallo is top een grafieksegment met laadtijden van pagina's. totale hoogte van de grafiek Hallo Hallo vertegenwoordigt Hallo gemiddelde tijd tooload en weergave van pagina's van uw app in browsers van uw gebruikers. Hallo tijd wordt gemeten vanaf wanneer Hallo browser Hallo eerste HTTP-aanvraag tot alle synchrone load gebeurtenissen zijn verwerkt verzendt, met inbegrip van indeling en de scripts uitgevoerd. Asynchrone taken, zoals het laden van de webonderdelen van AJAX-aanroepen, zijn niet opgenomen.

Hallo grafiek segmenteert Hallo totale paginalaadtijd in Hallo [standaardtijdsinstellingen gedefinieerd door W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Houd er rekening mee dat Hallo *netwerk verbinden* is vaak lager dan u verwacht, omdat het is een gemiddelde over alle aanvragen van Hallo browser toohello-server. Veel afzonderlijke aanvragen hebben een verbindingstijd van 0, omdat er al een actieve verbinding toohello-server.

### <a name="slow-loading"></a>Worden pagina’s traag geladen?
Het traag laden van pagina is voor uw gebruikers een belangrijke bron van ergernis. Als het Hallo-grafiek aangeeft dat pagina traag worden geladen, is het eenvoudig toodo wat diagnostisch onderzoek.

Hallo diagram toont Hallo gemiddelde paginalaadtijd in uw app. toosee als Hallo probleem zich beperkt tooparticular pagina's, uiterlijk verder omlaag Hallo blade, waarbij er een raster gesegmenteerd op pagina-URL:

![](./media/app-insights-javascript/09-page-perf.png)

U ziet Hallo aantal paginaweergaven en de standaarddeviatie. Als het Hallo-aantal pagina's zeer laag is, klikt u vervolgens Hallo probleem is niet dat gebruikers ondervonden veel. Een hoge standaarddeviatie (vergelijkbaar toohello gemiddelde) geeft aan dat er grote verschillen bestaan tussen de afzonderlijke metingen.

**Zoom in op een URL en een paginaweergave.** Klik op elke pagina naam toosee een blade van de browser grafieken gefilterde alleen toothat URL; en vervolgens op een exemplaar van een paginaweergave.

![](./media/app-insights-javascript/35.png)

Klik op `...` voor een volledige lijst met eigenschappen voor die gebeurtenis of Controleer Hallo Ajax-aanroepen en gerelateerde gebeurtenissen. Trage Ajax-aanroepen Hallo van invloed zijn op de algemene laadtijd van pagina als beide synchroon gebeuren. Gerelateerde gebeurtenissen omvatten serveraanvragen voor Hallo dezelfde URL (als u Application Insights hebt ingesteld op uw webserver).

**Paginaprestaties over langere tijd.** Wijzigen terug op de blade Browsers Hallo Hallo laadtijd voor paginaweergave raster in een grafiek regel toosee als er pieken op bepaalde tijden:

![Klik op Hallo-head van Hallo raster en een nieuw grafiektype selecteren](./media/app-insights-javascript/10-page-perf-area.png)

**Segmenteer op andere dimensies.** Uw pagina's mogelijk langzamer tooload op een bepaalde browser, clientbesturingssysteem of gebruiker plaats? Voeg een nieuwe grafiek toe en Experimenteer met Hallo **Group by** dimensie.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>AJAX-prestaties
Zorg ervoor dat eventuele AJAX-aanroepen op uw webpagina's goed worden uitgevoerd. Ze zijn vaak gebruikte toofill onderdelen van uw pagina asynchroon. Hoewel hello algemene pagina onmiddellijk laadt waarschijnlijk, uw gebruikers zich gaan ergeren doordat ze steeds op lege webonderdelen, wachten op gegevens tooappear bevat.

AJAX-aanroepen vanuit uw webpagina worden weergegeven op de blade Browsers Hallo als afhankelijkheden.

Samenvattingsgrafieken in Hallo bovenste gedeelte van de blade Hallo:

![](./media/app-insights-javascript/31.png)

en verder naar beneden gedetailleerde rasters:

![](./media/app-insights-javascript/33.png)

Klik op een rij voor specifieke informatie.

> [!NOTE]
> Als u een filter voor Hallo-Browsers op Hallo blade verwijdert, worden zowel de server als de AJAX-afhankelijkheden opgenomen in deze grafieken. Klik op standaardinstellingen herstellen tooreconfigure Hallo filter.
> 
> 

**toodrill in mislukte Ajax-aanroepen** Schuif naar beneden toohello met afhankelijkheidsfouten en klik vervolgens op een specifieke rij toosee-exemplaren.

![](./media/app-insights-javascript/37.png)


Klik op `...` voor Hallo volledige telemetrie voor een Ajax-aanroep.

### <a name="no-ajax-calls-reported"></a>Zijn er geen AJAX-aanroepen gemeld?
AJAX-aanroepen zijn HTTP/HTTPS-aanroepen vanuit Hallo-script van de webpagina. Als u ze gerapporteerd niet ziet, controleert u dat codefragment Hallo Hallo niet ingesteld `disableAjaxTracking` of `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Browseruitzonderingen
Op de blade Browsers hello wordt een grafiek met samenvattingen uitzonderingen en een raster met typen uitzonderingen lager Hallo-blade.

![](./media/app-insights-javascript/39.png)

Als er geen browseruitzonderingen gerapporteerd, controleert die codefragment Hallo Hallo niet ingesteld `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>De afzonderlijke paginaweergavegebeurtenissen inspecteren

Meestal wordt telemetrie van paginaweergaven geanalyseerd door Application Insights en ziet u alleen cumulatieve rapporten, het gemiddelde van alle gebruikers. Maar voor foutopsporing kunt u ook zoeken op afzonderlijke paginaweergavegebeurtenissen.

Hallo diagnostische gegevens doorzoeken blade ingesteld Filters tooPage weergeven.

![](./media/app-insights-javascript/12-search-pages.png)

Selecteer een gebeurtenis toosee meer details. Klik in Hallo pagina met details op '...' toosee nog meer details.

> [!NOTE]
> Als u [Search](app-insights-diagnostic-search.md), aankondiging dat u volledige woorden toomatch hebt: 'Abou' of 'bout' komen niet overeen met 'About'.
> 
> 

U kunt ook Hallo krachtige [querytaal van logboekanalyse](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch paginaweergaven.

### <a name="page-view-properties"></a>Eigenschappen van paginaweergaven
* **Duur van paginaweergave** 
  
  * Standaard Hallo keer dat er vergt tooload Hallo pagina, van de client aanvraag toofull laden (inclusief hulpbestanden, maar uitgezonderd asynchrone taken zoals Ajax-aanroepen). 
  * Als u instelt `overridePageViewDuration` in Hallo [paginaconfiguratie](#detailed-configuration), eerst interval tussen client aanvraag tooexecution Hallo Hallo `trackPageView`. Als u trackPageView vanaf de normale positie na de initialisatie van Hallo script hello verplaatst, wordt een andere waarde weer.
  * Als `overridePageViewDuration` is ingesteld en een duurargument is opgegeven in Hallo `trackPageView()` aanroep, Hallo argumentwaarde in plaats daarvan wordt gebruikt. 

## <a name="custom-page-counts"></a>Aangepast telling van het aantal paginaweergaven
Het aantal pagina's wordt standaard elke keer dat een nieuwe pagina wordt geladen in de browser Hallo van client.  Maar u kunt de aanvullende paginaweergaven toocount. Bijvoorbeeld, een pagina kan de inhoud worden weergegeven in tabbladen en u wilt toocount een pagina wanneer de gebruiker Hallo tabbladen overschakelt. Of JavaScript-code in Hallo pagina laadt nieuwe inhoud zonder Hallo browser URL.

Invoegen Hallo betreffende punt in uw clientcode een JavaScript-aanroep als volgt:

    appInsights.trackPageView(myPageName);

naam van de pagina Hallo mag dezelfde tekens als een URL, maar alles na '#' hello of '? ' wordt genegeerd.

## <a name="usage-tracking"></a>Gebruik bijhouden
Wilt u toofind uit wat gebruikers met uw app doen?

* [Meer informatie over het bijhouden van gebruik](app-insights-web-track-usage.md)
* [Meer informatie over de API voor aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Video


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Volgende stappen
* [Bijhouden van gebruik](app-insights-web-track-usage.md)
* [Aangepaste gebeurtenissen en metrische gegevens](app-insights-api-custom-events-metrics.md)
* [Bouwen-meten-leren](app-insights-web-track-usage.md)

