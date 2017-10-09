---
title: aaaUser, sessie en gebeurtenis analyse in Azure Application Insights | Microsoft docs
description: Demografische analyse van gebruikers van uw web-app.
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Analyse van de gebruikers, sessies en gebeurtenissen in Application Insights

Weten wanneer mensen uw web-app gebruikt, welke pagina's die ze zijn het meest geïnteresseerd, waar uw gebruikers zich bevinden, welke browsers en besturingssystemen die ze gebruiken. Bedrijfs- en gebruiksgegevens telemetrie analyseren met behulp van [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Aan de slag

Als er geen gegevens in het Hallo-gebruikers, sessies of blades gebeurtenissen in Application Insights-portal Hallo nog [meer informatie over hoe tooget gestart met gebruik van hulpprogramma's voor Hallo](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>Hallo gebruikers, sessies en gebeurtenissen segmentering hulpprogramma

Drie Hallo gebruik blades gebruiken dezelfde hulpprogramma tooslice en opdelen telemetrie van uw web-app uit drie perspectieven Hallo. Door het filteren en Hallo gegevens gesplitst, kunt u inzicht in Hallo relatieve gebruik van verschillende pagina's en onderdelen onthullen.

* **Gebruikers hulpprogramma**: hoeveel mensen uw app en de bijbehorende functies gebruikt.  Gebruikers worden met behulp van anonieme id's die zijn opgeslagen in de browsercookies geteld. Verschillende browsers of machines met één persoon wordt geteld als meer dan één gebruiker.
* **Sessies hulpprogramma**: het aantal sessies van gebruikersactiviteit bepaalde pagina's en functies van uw app hebt opgenomen. Een sessie worden geteld nadat half uur gebruiker inactief of nadat continue 24 uur van gebruik.
* **Gebeurtenissen hulpprogramma**: hoe vaak bepaalde pagina's en functies van uw app worden gebruikt. Een paginaweergave geteld als een pagina in een browser wordt geladen vanuit uw app, mits u [geïnstrumenteerd deze](app-insights-javascript.md). 

    Een aangepaste gebeurtenis vertegenwoordigt een exemplaar van dat er iets gebeurt in uw app, vaak een gebruikersinteractie zoals een knop klikt u op of Hallo van een taak is voltooid. U code invoegen in uw app te[aangepaste gebeurtenissen genereren](app-insights-api-custom-events-metrics.md#trackevent).

![Gebruik hulpprogramma](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Uitvoeren van query's voor bepaalde gebruikers 

Bekijk verschillende groepen gebruikers aan de queryopties Hallo HALLO hallo gebruikers hulpprogramma bovenaan in het aanpassen: 

* Wie gebruikt: Kies aangepaste gebeurtenissen en paginaweergaven. 
* Tijdens: Kies een tijdsbereik. 
* Door: Kies toobucket Hallo hoe gegevens door een bepaalde periode of door een andere eigenschap zoals browser of een plaats. 
* Splitsen: Kies een eigenschap door welke toosplit of segment Hallo-gegevens. 
* Filters toevoegen: Beperk Hallo query toocertain gebruikers, sessies of gebeurtenissen op basis van hun eigenschappen, zoals de browser of een plaats. 
 
## <a name="saving-and-sharing-reports"></a>Opslaan en delen van rapporten 
U kunt gebruikers rapporten, ofwel private alleen tooyou in sectie Hallo mijn rapporten opslaan of gedeeld met iedereen met toegang toothis Application Insights-resource anders in Hallo sectie gedeelde rapporten.  
 
Tijdens het opslaan van een rapport of de eigenschappen bewerken, kiest u 'Huidige relatief tijdsbereik' toosave die een rapport voortdurend wordt vernieuwd gegevens, een vaste hoeveelheid tijd als u terugkeert.  
 
Kies 'Huidige absoluut tijdsbereik' toosave een rapport met een vaste set van gegevens. Houd er rekening mee dat de gegevens in Application Insights alleen worden opgeslagen voor 90 dagen, dus als er meer dan 90 dagen zijn verstreken sinds een rapport met een absoluut tijdsbereik is opgeslagen, Hallo rapport leeg, weergegeven. 
 
## <a name="example-instances"></a>Voorbeeld-exemplaren

Hallo voorbeeld exemplaren in deze sectie bevat informatie over een aantal afzonderlijke gebruikers, sessies of gebeurtenissen die door de huidige query Hallo worden vergeleken. Overweegt en verkennen Hallo gedrag van personen in toevoeging tooaggregates, krijgt u inzicht in hoe mensen uw app daadwerkelijk gebruiken. 
 
## <a name="insights"></a>Inzichten 

Hallo Insights zijbalk bevat grote clusters van gebruikers die algemene eigenschappen voor delen. Deze clusters kunnen onthullen verrassend trends in hoe mensen uw app gebruiken. Als bijvoorbeeld 40% van alle Hallo informatie over het gebruik van uw app afkomstig is van mensen met een enkele functie.  


## <a name="next-steps"></a>Volgende stappen
- Gebruik tooenable optreedt, te beginnen met het verzenden [aangepaste gebeurtenissen](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) of [paginaweergaven](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Als u al aangepaste gebeurtenissen of paginaweergaven verkennen Hallo gebruik hulpprogramma's voor toolearn verzendt hoe gebruikers de service gebruiken.
    - [Trechters](usage-funnels.md)
    - [Retentie](app-insights-usage-retention.md)
    - [Gebruikersstromen](app-insights-usage-flows.md)
    - [Werkmappen](app-insights-usage-workbooks.md)
    - [Gebruikerscontext toevoegen](app-insights-usage-send-user-context.md)

