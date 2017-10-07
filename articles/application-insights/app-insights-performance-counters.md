---
title: aaaPerformance tellers in Application Insights | Microsoft Docs
description: Systeem- en aangepaste .NET-prestatiemeters in Application Insights bewaken.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Systeemprestatiemeteritems in Application Insights
Windows biedt een groot aantal [prestatiemeteritems](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) zoals bezetting CPU, geheugen, schijf en netwerkgebruik. U kunt ook uw eigen links definiëren. [Application Insights](app-insights-overview.md) kunt weergeven met deze prestatiemeteritems als uw toepassing wordt uitgevoerd onder IIS op een lokale host of virtuele machine toowhich u beheerderstoegang hebben. Hallo grafieken geven Hallo resources beschikbaar tooyour live-toepassing en kunnen tooidentify onbalans load tussen serverexemplaren.

Prestatiemeteritems weergegeven in de blade Servers hello, waaronder een tabel die segmenten door server-exemplaar.

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Prestatie-items zijn niet beschikbaar voor Web-Apps van Azure. Maar u kunt [Azure Diagnostics tooApplication Insights verzenden](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Items weergeven
Hallo Servers blade ziet u een standaardset prestatiemeteritems. 

toosee andere tellers op Hallo grafieken op Hallo Servers blade bewerken of open een nieuw [Metrics Explorer](app-insights-metrics-explorer.md) blade en voegen nieuwe grafieken. 

Hallo beschikbare items worden weergegeven als metrische gegevens wanneer u een grafiek bewerken.

![Prestatie-items die zijn gerapporteerd in Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

toosee uw nuttigst grafieken op één plek maken een [dashboard](app-insights-dashboards.md) en tooit vastmaken.

## <a name="add-counters"></a>Items toevoegen
Als Hallo-prestatiemeteritem die u wilt dat niet wordt weergegeven in de lijst Hallo van metrische gegevens, gebeurt dit omdat Hallo Application Insights-SDK wordt niet worden verzameld in uw webserver. U kunt deze configureren toodo dus.

1. Ontdek welke items beschikbaar in uw server zijn met behulp van deze PowerShell-opdracht op Hallo-server:
   
    `Get-Counter -ListSet *`
   
    (Zie [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)
2. Open ApplicationInsights.config.
   
   * Als u Application Insights tooyour app toegevoegd tijdens de ontwikkeling, bewerk ApplicationInsights.config in uw project en klik vervolgens opnieuw implementeren tooyour servers.
   * Als u de Status Monitor tooinstrument een web-app tijdens runtime gebruikt, moet u ApplicationInsights.config vinden in de hoofdmap Hallo van Hallo-app in IIS. Deze er op elk serverexemplaar bijwerken.
3. Hallo prestaties collector richtlijn bewerken:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

U kunt vastleggen standaard tellers en die dat u zelf hebt geïmplementeerd. `\Objects\Processes`een voorbeeld van een standaard prestatiemeteritem is beschikbaar op alle Windows-systemen. `\Sales(photo)\# Items Sold`is een voorbeeld van een aangepaste teller die mogelijk zijn geïmplementeerd in een webservice. 

Hallo-indeling is `\Category(instance)\Counter"`, of gewoon voor categorieën waarvoor geen exemplaren `\Category\Counter`.

`ReportAs`is vereist voor de namen van prestatiemeteritems die komen niet overeen met `[a-zA-Z()/-_ \.]+` -dat wil zeggen, ze tekens bevatten die niet zijn opgenomen in de volgende sets Hallo: letters, ronde haakjes, schuine streep, afbreekstreepje, onderstrepingstekens, ruimte, punt.

Als u een exemplaar opgeeft, worden verzameld als een dimensie 'CounterInstanceName' Hallo metriek gerapporteerd.

### <a name="collecting-performance-counters-in-code"></a>Verzamelen van prestatiemeteritems in de code
de systeemprestaties toocollect prestatiemeteritems en verzend tooApplication Insights, kunt u onderstaande Hallo stukje aanpassen:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Of u kunt doen Hallo hetzelfde met aangepaste metrische gegevens die u hebt gemaakt:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Prestatiemeters in Analytics
U kunt zoeken en weergeven van de teller prestatierapporten in [Analytics](app-insights-analytics.md).

Hallo **performanceCounters** schema beschrijft Hallo `category`, `counter` naam, en `instance` naam van elk prestatiemeteritem.  Hallo telemetrie voor elke toepassing ziet u alleen Hallo items voor die toepassing. Bijvoorbeeld: toosee welke items zijn beschikbaar: 

![Prestatiemeters in Application Insights analytics](./media/app-insights-performance-counters/analytics-performance-counters.png)

(Exemplaar van prestatiemeteritem toohello hier de instantie' verwijst, niet Hallo functie of servergroep exemplaar van de machine. naam exemplaar Prestatiemeter Hallo doorgaans segmenten items zoals processortijd met de naam van de toepassing of proces Hallo Hallo.)

een grafiek van het beschikbare geheugen over Hallo recente periode tooget: 

![Geheugen timechart in Application Insights analytics](./media/app-insights-performance-counters/analytics-available-memory.png)

Zoals u andere telemetrie **performanceCounters** heeft ook een kolom `cloud_RoleInstance` die aangeeft dat de identiteit Hallo van Hallo host server-exemplaar waarop uw app wordt uitgevoerd. Bijvoorbeeld: toocompare Hallo prestaties van uw app op verschillende computers Hallo: 

![Prestaties gesegmenteerd op rolinstantie in Application Insights analytics](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET en Application Insights tellingen
*Wat is Hallo verschil tussen Hallo uitzondering snelheid en uitzonderingen metrische gegevens?*

* *Snelheid van de uitzondering* is van een prestatiemeteritem voor het systeem. Hallo CLR telt alle Hallo verwerkte en onverwerkte uitzonderingen die worden gegenereerd en Hallo totaal in een interval van steekproeven verdeelt door Hallo lengte van hello-interval. Hallo Application Insights-SDK dit resultaat verzamelt en verzendt het toohello-portal.
* *Uitzonderingen* is een telling van Hallo TrackException-rapporten ontvangen door het Hallo-portal op Hallo steekproefinterval van Hallo-grafiek. Het bevat alleen Hallo verwerkte uitzonderingen waar u TrackException aanroept in uw code en niet alle opgenomen hebt geschreven [onverwerkte uitzonderingen](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Waarschuwingen
Net als andere metrische gegevens, kunt u [een waarschuwing instellen](app-insights-alerts.md) toowarn die u als een prestatiemeteritem gaat buiten een grens die u opgeeft. Open de blade beveiligingswaarschuwingen Hallo en klik op waarschuwing toevoegen.

## <a name="next"></a>Volgende stappen
* [Bijhouden van afhankelijkheid](app-insights-asp-net-dependencies.md)
* [Uitzonderingen bijhouden](app-insights-asp-net-exceptions.md)

