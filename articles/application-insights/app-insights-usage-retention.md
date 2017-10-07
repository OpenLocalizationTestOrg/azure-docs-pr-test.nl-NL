---
title: analyse van de aaaUser bewaren voor webtoepassingen met Azure Application Insights | Microsoft docs
description: Hoeveel gebruikers retourneren tooyour app?
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a>Analyse van de gebruiker bewaren voor webtoepassingen met Application Insights

Hallo bewaren functie in [Azure Application Insights](app-insights-overview.md) helpt u hoeveel gebruikers analyseren retourneren tooyour app, en hoe vaak ze bepaalde taken uitvoeren of deze doelstellingen te bereiken. Als u een game site uitvoert, kan u bijvoorbeeld Hallo aantallen gebruikers die toohello site na het verlies van een game met Hallo getal retourneren en nadat winnen retourneren vergelijken. Deze informatie kunt u zowel uw gebruikerservaring en de bedrijfsstrategie verbeteren.

## <a name="get-started"></a>Aan de slag

Als er geen gegevens in Hallo bewaren hulpprogramma in de Application Insights-portal Hallo nog [meer informatie over hoe tooget gestart met gebruik van hulpprogramma's voor Hallo](app-insights-usage-overview.md).

## <a name="hello-retention-tool"></a>Hallo bewaren hulpprogramma

![Retentie-informatie](./media/app-insights-usage-retention/retention.png)

1. Hallo werkbalk kan gebruikers de nieuwe bewaarperiode rapporten toocreate, bestaande bewaren rapporten openen, huidige bewaren rapport opslaan of opslaan als, wijzigingen toosaved rapporten herstellen, gegevens op Hallo rapport, delen via e-mail of directe koppeling en toegang Hallo vernieuwen pagina met documentatie. 
2. Standaard bevat bewaren alle gebruikers die u hebt vervolgens terug documentatie en iets anders heeft gedurende een periode. U kunt andere combinatie van gebeurtenissen toonarrow Hallo concentreren op specifieke gebruikersactiviteiten selecteren.
3. Een of meer filters toevoegen op Eigenschappen. Bijvoorbeeld, kunt u zich richten op gebruikers in een bepaald land of regio. Klik op **Update** na het Hallo-filters instellen. 
4. Hallo algehele bewaren diagram toont een overzicht van de gebruiker bewaren op Hallo geselecteerde periode. 
5. Hallo raster toont Hallo aantal gebruikers volgens toohello opbouwfunctie voor query's in #2 bewaard. Vertegenwoordigt een cohort van gebruikers die een gebeurtenis uitgevoerd in de Hallo tijd weergegeven van elke rij. Elke cel in rij Hallo bevat ten minste eenmaal in een latere periode hoeveel die cohort geretourneerd. Sommige gebruikers mogelijk geretourneerd uit meer dan één periode. 
6. Hallo insights kaarten weergeven bovenste vijf gang worden gezet gebeurtenissen en bovenste vijf geretourneerd gebeurtenissen toogive gebruikers een beter begrip van de retentie-rapport. 

![Bewaartermijn muis aanwijzen](./media/app-insights-usage-retention/hover.png)

Gebruikers kunnen de muisaanwijzer cellen op Hallo bewaren hulpprogramma tooaccess Hallo analytics-knop en knopinfo waarin wordt uitgelegd welke cel Hallo betekent. Hallo Analytics-knop gaat gebruikers toohello Analytics hulpprogramma met een vooraf ingestelde query toogenerate gebruikers uit Hallo cel. 

## <a name="use-business-events-tootrack-retention"></a>Gebruik van zakelijke gebeurtenissen tootrack bewaren

tooget hello nuttigst bewaren analyse, meting gebeurtenissen waarbij aanzienlijke zakelijke activiteiten. 

Bijvoorbeeld: veel gebruikers mogelijk open een pagina in uw app zonder Hallo spel die wordt weergegeven. NET Hallo paginaweergaven bijhouden, zou een onnauwkeurige schatting maken van hoeveel mensen tooplay Hallo game retourneren na eerder genieten daarom bieden. tooget duidelijk beeld van de spelers, moet uw app een aangepaste gebeurtenis wanneer een gebruiker daadwerkelijk speelt verzenden.  

Het is raadzaam om aangepaste gebeurtenissen toocode die dit beleid gebruiken voor het bewaren van analyse en acties van de belangrijkste zakelijke vertegenwoordigen. toocapture hello game resultaat, moet u een line-of code toosend een aangepaste gebeurtenis tooApplication Insights toowrite. Als u deze in Hallo webpagina code of in Node.JS schrijft, als volgt uitziet:

```JavaScript
    appinsights.trackEvent("won game");
```

Of in de servercode ASP.NET:

```C#
   telemetry.TrackEvent("won game");
```

[Meer informatie over het schrijven van aangepaste gebeurtenissen](app-insights-api-custom-events-metrics.md#trackevent).


## <a name="next-steps"></a>Volgende stappen
- Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.
    - [Gebruikers, sessies, gebeurtenissen](app-insights-usage-segmentation.md)
    - [Trechters](usage-funnels.md)
    - [Gebruikersstromen](app-insights-usage-flows.md)
    - [Werkmappen](app-insights-usage-workbooks.md)
    - [Gebruikerscontext toevoegen](app-insights-usage-send-user-context.md)


