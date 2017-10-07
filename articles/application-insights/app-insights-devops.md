---
title: aaaWeb APM - Azure Application Insights | Microsoft Docs
description: Hoe Application Insights in Hallo devOps cyclus past
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Diepe diagnostische gegevens voor web-apps en services met Application Insights
## <a name="why-do-i-need-application-insights"></a>Waarom moet ik Application Insights?
Application Insights wordt uw actieve web-app bewaakt. Het vertelt u over de fouten en prestatieproblemen en helpt u bij het analyseren hoe klanten gebruiken voor uw app. Het werkt voor apps die worden uitgevoerd op verschillende platforms (ASP.NET, J2EE, Node.js,...) en wordt gehost in Hallo Cloud of on-premises. 

![Aspecten van Hallo complexiteit van het leveren van web-apps](./media/app-insights-devops/010.png)

Het is essentieel toomonitor een moderne toepassingen terwijl deze wordt uitgevoerd. Het belangrijkste is dat wilt u dat toodetect fouten voordat de meeste van uw klanten. U ook wilt toodiscover en oplossen van prestatieproblemen die terwijl niet onherstelbare mogelijk dingen vertragen of ongemak tooyour gebruikers kan veroorzaken. En wanneer Hallo systeem tooyour tevredenheid uitvoert, wilt u welke Hallo gebruikers met het doen tooknow: zijn ze met de meest recente functie Hallo? Slaagt ze ermee?

Moderne webtoepassingen zijn ontwikkeld in een cyclus van continue levering: een nieuwe functie of verbetering; vrijgeven Houd rekening met hoe goed werkt voor gebruikers Hallo; plan Hallo volgende verhoging van de ontwikkeling op basis van deze kennis van. Een belangrijk onderdeel van deze cyclus is Hallo observatie-fase. Application Insights biedt Hallo extra toomonitor een webtoepassing voor prestaties en het gebruik.

Hallo zeer belangrijk aspect van dit proces is en diagnose van diagnostische gegevens. Als de toepassing hello mislukt, is business wordt verbroken. Hallo voornaamste rol van een controle framework derhalve toodetect fouten betrouwbaar, mededeling u onmiddellijk en toopresent dat u met Hallo informatie toodiagnose Hallo probleem nodig. Dit is precies wat Application Insights doet.

### <a name="where-do-bugs-come-from"></a>Waar komen bugs vandaan?
Fouten in de web-systemen worden doorgaans veroorzaakt door problemen met de configuratie of ongeldige interacties tussen hun veel onderdelen. Hallo eerste taak bij het aanpakken van een incident live site is daarom tooidentify Hallo locus van Hallo probleem: welk onderdeel of relatie is Hallo oorzaak?

Sommige van ons die met grijze haar, kan een eenvoudigere era waarin een computer wordt uitgevoerd in één computer onthouden. Hallo ontwikkelaars zou testen zorgvuldig door voordat u levert. en zelden hebben verzonden, zou Zie of denken. Hallo gebruikers zou hebben tooput up met Hallo achtergebleven bugs jaren. 

Dingen zijn nu zo heel verschillend. Uw app heeft tal van verschillende apparaten toorun op en kan moeilijk tooguarantee Hallo exact hetzelfde gedrag op elkaar. Hosting-apps in de cloud Hallo betekent fouten kunnen snel worden opgelost, maar het betekent ook continue concurrentie en Hallo verwachting van nieuwe functies met regelmatige tussenpozen. 

In deze voorwaarden hello alleen manier tookeep die vast besturingselement in een Hallo bug aantal is het automatisch eenheid testen. Het niet mogelijk toomanually test alles op elke levering opnieuw. Testen van eenheden is heel gebruikelijk deel uit van Hallo buildproces. Hulpprogramma's zoals Hallo Xamarin-Testcloud u helpen met geautomatiseerde UI testen op meerdere browserversies. Deze tests regelingen kunnen we toohope die Hallo frequentie van fouten die zijn gevonden in een app kan worden bewaard tooa minimale.

Typische webtoepassingen hebben veel live onderdelen. In toevoeging toohello client (in een browser of een apparaat-app) en het Hallo-webserver is het waarschijnlijk toobe aanzienlijke back-end-verwerking. Hallo back-end is mogelijk een pijplijn van onderdelen of een verzameling lossere samenwerkende onderdelen. Veel van deze niet in uw beheer- en - ze zijn externe services waarvan u afhankelijk zijn.

In de configuraties in dergelijke kan het moeilijk en uneconomical tootest, worden of voorzien, elke modus mislukken, anders dan in Hallo live systeem zelf. 

### <a name="questions-"></a>Vragen...
Enkele vragen we vragen we bij het ontwikkelen van een web-systeem:

* Mijn app vastloopt? 
* Wat is precies? -Als een aanvraag is mislukt, wil ik tooknow hoe deze er gekomen. Er moet een tracering van gebeurtenissen...
* Mijn app snel genoeg is? Hoe lang duurt toorespond tootypical aanvragen?
* Kan Hallo server ingang Hallo laden? Als Hallo snelheid van aanvragen stijgt, Hallo reactietijd hebben constante?
* Hoe responsief zijn mijn afhankelijkheden - Hallo REST-API's, databases en andere onderdelen die mijn app aanroept. In het bijzonder als Hallo system traag is, is het mijn onderdeel of krijg ik trage reacties van iemand anders?
* Mijn app is omhoog of omlaag? Kan het worden afgeleid uit Hallo wereld? Informeer mij als deze wordt gestopt...
* Wat is de hoofdoorzaak Hallo? Hallo-fout in mijn-onderdeel of een afhankelijkheid is? Is het een communicatieprobleem?
* Hoeveel gebruikers ondervinden gevolgen? Als er meer dan één probleem tootackle, dit is zeer belangrijk Hallo?

## <a name="what-is-application-insights"></a>Wat is Application Insights?
![Basiswerkstroom van Application Insights](./media/app-insights-devops/020.png)

1. Application Insights instrumenten van uw app en telemetrie over deze verzendt terwijl Hallo-app wordt uitgevoerd. U kunt u Application Insights-SDK Hallo in Hallo app of u instrumentation tijdens runtime kunt toepassen. Hallo eerste methode is flexibeler, als u uw eigen telemetrie toohello reguliere modules kunt toevoegen.
2. Hallo telemetrie verzonden toohello Application Insights-portal, waar ze worden opgeslagen en verwerkt. (Hoewel Application Insights wordt gehost in Microsoft Azure, te controleren alle web-apps - niet alleen Azure apps.)
3. Hallo telemetrie is tooyou in Hallo vorm van grafieken en tabellen van gebeurtenissen worden opgenomen.

Er zijn twee typen telemetrie: cumulatieve en raw-exemplaren. 

* Exemplaargegevens bevat bijvoorbeeld een rapport van een aanvraag die is ontvangen door uw web-app. U kunt vinden voor en inspecteren Hallo-details van een aanvraag met Hallo zoekfunctie in Hallo Application Insights-portal. Hallo exemplaar zou gegevens bevatten zoals hoe lang uw app toorespond toohello aanvraag duurde, evenals Hallo aangevraagde URL, bij benadering de positie van de client hello en andere gegevens.
* Geaggregeerde gegevens bevat het aantal gebeurtenissen per tijdseenheid, zodat u Hallo percentage aanvragen met reactietijden Hallo kunt vergelijken. Dit omvat ook gemiddelden van metrische gegevens zoals reactietijden van de aanvraag.

Hallo hoofdcategorieën van gegevens zijn:

* Aanvragen tooyour app (meestal HTTP-aanvragen) met de gegevens op de URL, reactietijden, en slagen of mislukken.
* Afhankelijkheden - REST en SQL aanroepen van uw app, ook met URI, responstijden en geslaagd
* Uitzonderingen, met inbegrip van stack-traces.
* Pagina weergavegegevens die afkomstig van Hallo de browser van gebruikers zijn.
* Metrische gegevens zoals prestatiemeteritems, evenals metrische gegevens die u zelf schrijven. 
* Aangepaste gebeurtenissen, waarmee u tootrack zakelijke gebeurtenissen kunt
* Logboektraceringen ten behoeve van foutopsporing.

## <a name="case-study-real-madrid-fc"></a>Casestudy: Echte Madrid F.C.
Hallo-webservice van [echte Madrid Football vereniging](http://www.realmadrid.com/) ongeveer 450 miljoen ventilatoren Hallo wereld fungeert. Ventilatoren krijgen tot beide webbrowsers en Hallo van vereniging mobiele apps. Ventilatoren kunnen niet alleen tickets boek, maar ook toegang tot informatie en videoclips op resultaten, spelers en toekomstige games. Ze kunnen zoeken met filters zoals getallen van doelstellingen berekend. Er zijn ook koppelingen toosocial media. Hallo-gebruikerservaring maximaal kan worden aangepast en is bedoeld als een communicatie in twee richtingen tooengage ventilatoren.

Hallo oplossing [is een systeem van services en toepassingen op Microsoft Azure](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). Schaalbaarheid is een belangrijke vereiste: verkeer variabele en zeer hoge volumes kunnen bereiken tijdens en rond overeenkomsten.

Voor echte Madrid is essentieel toomonitor Hallo de systeemprestaties. Azure Application Insights biedt een uitgebreid overzicht in Hallo-systeem, zodat een betrouwbare en een hoge mate van service. 

Hallo vereniging wordt ook diepgaand inzicht in de ventilatoren: waar ze zijn (slechts 3% zijn in Spanje), welke interesse hebben spelers, historische resultaten, en toekomstige games en hoe ze toomatch resultaten reageren.

De meeste van deze telemetrische gegevens automatisch worden verzameld door geen toegevoegde code waarmee Hallo oplossing vereenvoudigd en operationele complexiteit beperkt.  Voor echte Madrid, Application Insights behandelt 3,8 miljard telemetrie punten elke maand.

Echte Madrid gebruikt Hallo Power BI-module tooview hun telemetrie.

![Power BI-weergave van telemetrie in Application Insights](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Slimme detectie
[Proactieve diagnoses](app-insights-proactive-diagnostics.md) is een recente functie. Zonder speciale configuratie door u, Application Insights automatisch detecteert en waarschuwt u over ongebruikelijke verhogingen van uitvalpercentage in uw app. Is het slim genoeg tooignore een achtergrond van incidentele fouten en verhogingen die evenredige ook gewoon tooa toename van aanvragen. Dus bijvoorbeeld, werkt als er is een fout in een van de Hallo services die u afhankelijk zijn, of als nieuwe Hallo bouwen u zojuist hebt geïmplementeerd niet zo goed en u over deze weet Als u uw e-mailadres bekijkt. (En er zijn webhooks, zodat u andere apps kunt activeren.)

Een ander aspect van deze functie wordt een dagelijkse gedetailleerde analyse van uw telemetrie, zoeken naar ongebruikelijke patronen van de prestaties van vaste toodiscover worden uitgevoerd. Bijvoorbeeld, vindt het trage prestaties die hoort bij een bepaald geografisch gebied of met een bepaalde browser-versie.

In beide gevallen Hallo waarschuwing niet alleen vertelt u Hallo symptomen het wordt gedetecteerd, maar ook kunt u gegevens die u moet toohelp diagnosticeren Hallo probleem zoals relevante uitzonderingenrapporten.

![E-mail van proactieve diagnostische gegevens](./media/app-insights-devops/030.png)

Klant Samtec gezegd: 'we gevonden tijdens een recente functie cutover, een onder uitgebreide database die is roept de limieten en time-outs veroorzaakt. Waarschuwingen met proactieve detectie is geleverd door letterlijk we Hallo probleem, zeer bijna realtime zijn gesorteerd geadverteerd. Deze waarschuwing samen met hello Azure-platform waarschuwingen geholpen ons Hallo bijna onmiddellijk kunt oplossen. Totale downtime < 10 minuten."

## <a name="live-metrics-stream"></a>Metrische gegevens livestream
Implementatie van de laatste build Hallo mag een WENSENDE ervaring. Als er problemen zijn, u tooknow over deze meteen, zodat u kunt back uit, indien nodig. Metrische gegevens livestream biedt u de belangrijkste metrische gegevens met een latentie van ongeveer 1 seconde.

![Live metrische gegevens](./media/app-insights-devops/040.png)

En kunt u direct een steekproef van eventuele fouten en uitzonderingen te controleren.

![Live foutgebeurtenissen](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Toepassingskaart
De toepassingstoewijzing detecteert automatisch de Toepassingstopologie van uw elementlay Hallo prestatiegegevens boven op het toolet u eenvoudig identificeren van knelpunten en problematisch stromen in uw hele gedistribueerde omgeving. Hiermee kunt u toodiscover toepassingsafhankelijkheden op Azure-Services. U kunt Hallo probleem sorteren door als het code-gerelateerde begrijpen of afhankelijkheid gerelateerd en optreden van een enkele locatie lager niveau gerelateerde diagnostische gegevens. Uw toepassing is bijvoorbeeld mogelijk beschadigd vanwege tooperformance verslechtering van de SQL-laag. Met de toepassingstoewijzing, kunt u direct bekijken en inzoomen Hallo SQL Index Advisor of Query Insights-ervaring.

![Toepassingskaart](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights Analytics
Met [Analytics](app-insights-analytics.md), kunt u een willekeurige query's schrijven in een krachtige SQL-achtige taal.  Diagnose van over Hallo hele app stack wordt eenvoudig verschillende perspectieven verbinding en kunt u Hallo juiste vragen toocorrelate prestaties van de Service met metrische bedrijfswaarden en klantervaring vragen. 

U kunt uw telemetrie-instantie en metrische onbewerkte gegevens worden opgeslagen in de portal Hallo opvragen. Hallo taal bevat filter, join, aggregatie en andere bewerkingen. U kunt velden berekenen en uitvoeren van statistische analyse. Er zijn in tabelvorm en grafische visualisaties.

![Query's en resultaten grafiek](./media/app-insights-devops/025.png)

Bijvoorbeeld, is het eenvoudig:

* De toepassingsaanvraag prestatiegegevens door de klant lagen toounderstand hun ervaring segmenteren.
* Zoeken naar specifieke foutcodes of namen van aangepaste gebeurtenis tijdens live site onderzoeken.
* Inzoomen op Hallo app-gebruik van specifieke klanten toounderstand hoe de functies zijn aangeschaft en vastgesteld.
* Sessies en reactietijden voor specifieke gebruikers tooenable ondersteuning en bewerkingen teams tooprovide instant klantondersteuning bijhouden.
* Veelgebruikte app functies tooanswer functie prioriteitsaanduiding vragen bepalen.

Klant DNN gezegd: 'Application Insights is voorzien van ons Hallo deel van de vergelijking Hallo voor kunnen toocombine, sorteren en filteren van gegevens naar behoefte ontbreekt. Ons team toouse toestaan hun eigen toofind draaien en ervaring gegevens met een krachtige querytaal kan we toofind insights en oplossen van problemen die we niet wist dat we hebben gehad. Een groot aantal interessante antwoorden afkomstig zijn van Hallo vragen vanaf *' ik wonder als...'.*'

## <a name="development-tools-integration"></a>Development tools-integratie
### <a name="configuring-application-insights"></a>Application Insights configureren
Visual Studio en Eclipse hebben extra tooconfigure Hallo juist SDK-pakketten voor Hallo-project die u ontwikkelt. Er is een menu opdracht tooadd Application Insights.

Als u per ongeluk toobe met behulp van een framework voor logboekregistratie van trace zoals Log4N, NLog of System.Diagnostics.Trace, vervolgens krijgt u Hallo optie toosend Hallo logboeken tooApplication Insights samen met de Hallo andere telemetrie, zodat u eenvoudig hello traceringen met aanvragen correleren kunt , afhankelijkheidsaanroepen en uitzonderingen.

### <a name="search-telemetry-in-visual-studio"></a>Zoeken telemetrie in Visual Studio
Bij de ontwikkeling en foutopsporing van een functie, kunt u weergeven en doorzoeken telemetrie rechtstreeks in Visual Studio, met dezelfde faciliteiten als in de webportal Hallo zoeken Hallo Hallo.

En wanneer Application Insights zich een uitzondering aanmeldt, kunt u Hallo gegevenspunt bekijken in Visual Studio en de relevante code rechte toohello gaan.

![Visual Studio zoeken](./media/app-insights-devops/060.png)

Tijdens de foutopsporing hebt u Hallo optie tookeep Hallo telemetrie in uw ontwikkelcomputer bekijken in Visual Studio, maar zonder het te verzenden toohello-portal. Deze optie voor lokale voorkomt de combinatie van foutopsporing met telemetrie voor productie.

### <a name="build-annotations"></a>Aantekeningen maken
Als u Visual Studio Team Services toobuild en implementeer uw app weergegeven implementatie aantekeningen in de grafieken in Hallo-portal. Als uw meest recente release geen effect op Hallo metrische gegevens heeft, wordt het duidelijk.

![Aantekeningen maken](./media/app-insights-devops/070.png)

### <a name="work-items"></a>Werkitems
Wanneer een waarschuwing wordt gegenereerd, maken Application Insights automatisch een werkitem in uw werk traceringssysteem.

## <a name="but-what-about"></a>Maar hoe zit...?
* [Privacy- en](app-insights-data-retention-privacy.md) -uw telemetrie op Azure beveiligde servers wordt gehouden.
* Prestatie - impact Hallo is zeer weinig. Telemetrie in batch wordt verwerkt.
* [Prijzen](app-insights-pricing.md) : U kunt aan de slag gratis en die blijft terwijl u in de laag volume bent.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen
Aan de slag met Application Insights is eenvoudig. belangrijkste Hallo-opties zijn:

* Softwareontwikkelaars een web-app al actief. Hierdoor kunt u alle Hallo ingebouwde prestatietelemetrie. Is beschikbaar voor [Java](app-insights-java-live.md) en [IIS-servers](app-insights-monitor-performance-live-website-now.md), en ook voor [Azure-web-apps](app-insights-azure.md).
* Uw project instrumenteren tijdens de ontwikkeling. U kunt dit doen voor [ASP.NET](app-insights-asp-net.md) of [Java](app-insights-java-get-started.md) apps, evenals [Node.js](app-insights-nodejs.md) en een groot aantal [andere typen](app-insights-platforms.md). 
* Instrument [elke webpagina](app-insights-javascript.md) door een korte codefragment toe te voegen.

