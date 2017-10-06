---
title: aaaMonitor de status van uw app en het gebruik met Application Insights
description: Aan de slag met Application Insights. Analyseer gebruik, beschikbaarheid en prestaties van uw on-premises of de Microsoft Azure-toepassingen.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a>Prestaties in webtoepassingen controleren


Zorg ervoor dat uw toepassing goed presteert en vindt u informatie snel over fouten. [Application Insights] [ start] u vertellen over prestatieproblemen en uitzonderingen en helpen u te vinden en diagnose Hallo hoofdmap oorzaken.

Application Insights kunnen Java- en ASP.NET-webtoepassingen en services, WCF-services bewaken. Ze kunnen worden gehost op locatie, op virtuele machines, of als Microsoft Azure websites. 

Aan de clientzijde hello, Application Insights kan duren voordat telemetrie van webpagina's en een groot aantal apparaten, zoals iOS, Android en Windows Store-apps.

>[!Note]
> We hebben een nieuwe ervaring beschikbaar gesteld voor langzame pagina's uitvoeren in uw webtoepassing kan vinden. Als u geen toegang tot tooit, het inschakelen door het configureren van uw opties preview Hello [Preview blade](app-insights-previews.md). Meer informatie over deze nieuwe ervaring in [opsporen en oplossen van knelpunten met Hallo interactieve prestaties onderzoek](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).

## <a name="setup"></a>Instellen van de bewaking van toepassingsprestaties
Als u nog tooyour Application Insights hebt toegevoegd (dat wil zeggen, als er geen ApplicationInsights.config) project, kies een van de volgende manieren tooget gestart:

* [ASP.NET-web-apps](app-insights-asp-net.md)
  * [Uitzondering bewaking toevoegen](app-insights-asp-net-exceptions.md)
  * [Bewaking van afhankelijkheid toevoegen](app-insights-monitor-performance-live-website-now.md)
* [J2EE-web-apps](app-insights-java-get-started.md)
  * [Bewaking van afhankelijkheid toevoegen](app-insights-java-agent.md)

## <a name="view"></a>Maatstaven voor prestaties verkennen
In [hello Azure-portal](https://portal.azure.com), bladeren toohello Application Insights-resource die u hebt ingesteld voor uw toepassing. overzichtsblade Hello ziet basic prestatiegegevens:

Klik op een grafiek toosee meer detail en toosee resultaten voor een langere periode. Klik bijvoorbeeld op Hallo aanvragen tegel en selecteer vervolgens een tijdsbereik:

![Klik door toomore gegevens en selecteer een tijdsbereik](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

Klik op een grafiek toochoose welke metrische gegevens worden weergegeven, of Voeg een nieuwe grafiek toe en selecteer de metrische gegevens:

![Klik op een grafiek toochoose metrische gegevens](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> **Schakel alle Hallo metrische gegevens** toosee volledige selectie Hallo die beschikbaar is. Hallo metrische gegevens kunnen worden onderverdeeld in groepen; Wanneer een lid van een groep is geselecteerd, worden alleen hello andere leden van die groep weergegeven.

## <a name="metrics"></a>Wat doet u alle gemiddelde? Tegels van de prestaties en rapporten
Er zijn verschillende maatstaven voor prestaties die kunt u krijgen. Laten we beginnen met degenen die standaard worden weergegeven op de blade voor Hallo-toepassing.

### <a name="requests"></a>Aanvragen
Hallo aantal HTTP-aanvragen ontvangen in een opgegeven periode. Vergelijk dit met Hallo resultaten op andere rapporten toosee hoe uw app omgaat als Hallo belasting varieert.

HTTP-aanvragen bevatten alle GET of POST-aanvragen voor pagina's, gegevens en installatiekopieën.

Klik op Hallo tegel tooget tellingen voor specifieke URL's.

### <a name="average-response-time"></a>Gemiddelde reactietijd
Metingen Hallo tijd tussen een webaanvraag invoeren van uw toepassing en het Hallo-antwoord geretourneerd.

Hallo punten weergeven zwevend gemiddelde. Als er een groot aantal aanvragen, is er mogelijk enkele die afwijken van Hallo gemiddelde zonder een duidelijke piek of dip in Hallo-grafiek.

Zoek naar ongebruikelijke pieken. In het algemeen verwacht antwoord tijd toorise met een toename van aanvragen. Als Hallo aanleiding onevenredige is, kan uw app een limiet resource zoals CPU of Hallo capaciteit van een service die wordt gebruikt raken.

Klik op Hallo tegel tooget tijden voor specifieke URL's.

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a>Traagste aanvragen
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

Toont welke aanvragen mogelijk prestaties afstemmen.

### <a name="failed-requests"></a>Mislukte aanvragen
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

Een aantal aanvragen dat niet-onderschepte uitzonderingen heeft geretourneerd.

Hallo tegel toosee Hallo details van specifieke fouten op en selecteer een afzonderlijke aanvraag toosee de details. 

Alleen een representatieve steekproef van fouten wordt voor afzonderlijke inspectie bewaard.

### <a name="other-metrics"></a>Andere metrische gegevens
toosee welke andere metrische gegevens weergeven, klikt u op een grafiek en schakelt u alle Hallo metrische gegevens toosee Hallo volledige set. Klik op (i) toosee elke metriek definitie.

![Selectie van alle metrische gegevens toosee Hallo hele set opheffen](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

Selecteren van elke Hallo metrische schakelt Hallo anderen die kan niet worden weergegeven op hetzelfde diagram.

## <a name="set-alerts"></a>Waarschuwingen instellen
op de hoogte met e-mailadres van ongebruikelijke waarden van een metriek toobe een waarschuwing toevoegen. U kunt toohello accountbeheerders voor toosend Hallo e of e-mailadressen toospecific.

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

Hallo-bron voordat Hallo andere eigenschappen instellen. Kies de Hallo webtest bronnen geen als u wilt dat tooset waarschuwingen van prestaties of de meetgegevens voor softwaregebruik op.

Worden zorgvuldige toonote Hallo eenheden waarin u wordt gevraagd tooenter Hallo drempelwaarde.

*Waarschuwing knop Hallo toevoegen wordt niet weergegeven.* -Is dit een groep account toowhich u alleen-lezen toegang hebben? Neem contact op met de accountbeheerder Hallo.

## <a name="diagnosis"></a>Oplossen van problemen
Hier volgen enkele tips voor het zoeken en onderzoeken van prestatieproblemen:

* Instellen van [webtests] [ availability] toobe gewaarschuwd als uw website uitvalt of onjuist of traag reageert. 
* Hallo aanvraag aantal met andere toosee metrische gegevens vergelijken als mislukte of trage reactie gerelateerde tooload zijn.
* [Invoegen en zoek trace-instructies] [ diagnostic] in uw code toohelp speldenpunt problemen.
* Bewaken van uw Web-app in bewerking met [livestream metrische gegevens][livestream].
* Hallo-status van uw .net-toepassing met vastleggen [momentopname foutopsporingsprogramma][snapshot].

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a>Zoek en corrigeer de knelpunten met een interactieve prestaties onderzoek

U kunt Hallo nieuwe Application Insights interactieve prestaties onderzoek toolocate gebieden van uw Web-app die de algehele prestaties vertragen. U kunt snel zoeken naar specifieke's die vertragen en Hallo [Profiling hulpprogramma](app-insights-profiler.md) toosee als er een correlatie tussen deze pagina's.

### <a name="create-a-list-of-slow-performing-pages"></a>Een lijst met langzame presterende pagina's maken 

Hallo eerste stap voor het vinden van prestatieproblemen is tooget een lijst met Hallo traag reageert pagina's. de onderstaande schermafdruk Hallo wordt gedemonstreerd met behulp van Hallo prestaties blade tooget een lijst met mogelijke tooinvestigate pagina's verder. Snel ziet u op deze pagina dat er een vertraging in Hallo reactietijd van Hallo-app op ongeveer 18:00 uur en nogmaals op ongeveer 10 uur was. U ziet ook dat Hallo GET klantgegevens/bewerking heeft enkele langlopende bewerkingen met een gemiddelde responstijd 507.05 tijd in milliseconden. 

![Application Insights interactieve prestaties](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a>Inzoomen op bepaalde pagina 's

Zodra u een momentopname van de prestaties van uw app hebt, kunt u meer informatie krijgen op specifieke bewerkingen trage prestaties. Klik op elke bewerking in Hallo lijst toosee Hallo details, zoals hieronder wordt weergegeven. U kunt zien als Hallo prestaties is gebaseerd op een afhankelijkheid uit Hallo grafiek. Ook ziet u hoeveel gebruikers ervaren Hallo verschillende responstijden. 

![Application Insights operations blade](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a>Inzoomen op een specifieke tijdsperiode

Nadat u een punt in tijd tooinvestigate hebt geïdentificeerd, Inzoomen nog verder toolook op Hallo specifieke bewerkingen die mogelijk Hallo prestaties vertraging veroorzaakt. Als u klikt op in een bepaald punt in tijd krijgt u details op Hallo van Hallo pagina zoals hieronder wordt weergegeven. In Hallo ziet voorbeeld hieronder u Hallo bewerkingen die worden vermeld voor een bepaalde periode samen met reactiecodes Hallo-server en de duur van de Hallo-bewerking. U hebt ook Hallo-url voor het openen van een TFS-werkitem als u deze informatie tooyour-ontwikkelteam toosend nodig.

![Application Insights tijdsegment](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a>Inzoomen op een specifieke bewerking

Nadat u een punt in tijd tooinvestigate hebt geïdentificeerd, Inzoomen nog verder toolook op Hallo specifieke bewerkingen die mogelijk Hallo prestaties vertraging veroorzaakt. Klik op een bewerking van Hallo lijst toosee Hallo details van Hallo bewerking zoals hieronder wordt weergegeven. In dit voorbeeld u ziet dat Hallo-bewerking is mislukt en Application Insights Hallo details van Hallo is opgegeven heeft een uitzondering Hallo toepassing geretourneerd. U kunt een TFS-werkitem opnieuw gemakkelijk van deze blade maken.

![Application Insights bewerking blade](./media/app-insights-web-monitor-performance/performance3.png)


## <a name="next"></a>Volgende stappen
[Webtests] [ availability] -hebt verzonden webaanvragen tooyour toepassing met regelmatige tussenpozen van Hallo wereld.

[Vastleggen en zoeken van diagnostische traceringen] [ diagnostic] - traceringsaanroepen invoegen en doorzoeken Hallo resultaten toopinpoint problemen.

[Gebruik bijhouden] [ usage] -weten hoe mensen uw toepassing gebruiken.

[Het oplossen van problemen] [ qna] - en Q & A



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



