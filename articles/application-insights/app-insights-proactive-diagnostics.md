---
title: aaaSmart detectie in Azure Application Insights | Microsoft Docs
description: "Application Insights voert een automatische grondige analyse van uw app Telemetrie en waarschuwt u potentiële problemen."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a>Slimme detectie in Application Insights
 Slimme detectie waarschuwt automatisch u over potentiële prestatieproblemen in uw webtoepassing. Proactieve analyse van Hallo telemetrie die uw app te verzendt worden uitgevoerd[Application Insights](app-insights-overview.md). Als er een plotselinge toename van de fout tarieven of afwijkende patronen in de prestaties van de client of server is, krijgt u een waarschuwing. Deze functie heeft geen configuratie nodig. Dit werkt als uw toepassing voldoende telemetrie verzendt.

U kunt Slimme detectie waarschuwingen openen van e-mailberichten Hallo die u ontvangt, en van Hallo Slimme detectie blade.

## <a name="review-your-smart-detections"></a>Bekijk uw smartcard detecties
U kunt detecteren detecties op twee manieren:

* **U ontvangt een e-mailbericht** van Application Insights. Hier volgt een typisch voorbeeld:
  
    ![E-mailmelding](./media/app-insights-proactive-diagnostics/03.png)
  
    Klik op Hallo big knop tooopen gedetailleerder Hallo-portal.
* **Hallo Slimme detectie tegel** op overzicht van uw app blade ziet u een aantal van recente meldingen. Klik op Hallo tegel toosee een lijst met recente meldingen.

![Recente detecties weergeven](./media/app-insights-proactive-diagnostics/04.png)

Selecteer een waarschuwing toosee de details ervan.

## <a name="what-problems-are-detected"></a>Welke problemen worden ontdekt?
Er zijn drie soorten detectie:

* [Detectie - fout afwijkingen van smartcard](app-insights-proactive-failure-diagnostics.md). We gebruiken machine learning tooset Hallo verwacht aantal mislukte aanvragen voor uw app, correleren met load en andere factoren. Als percentage van de mislukte Hallo buiten de verwachte envelop hello gaat, verzonden er een waarschuwing.
* [Detectie - afwijkingen van smartcard](app-insights-proactive-performance-diagnostics.md). Als de reactietijd van een bewerking of een afhankelijkheid duur vergeleken toohistorical basislijn is vertragen of als we een afwijkende patroon in reactietijden of laadtijd van pagina identificeren krijgt u meldingen.   
* [Detectie - problemen met Azure Cloud Service slimme](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/). Als uw app wordt gehost in Azure Cloud Services en een rolinstantie heeft startfouten, vaak worden gerecycled of runtime crashes krijgt u waarschuwingen.

(Hallo help-koppelingen in elke melding duren u relevante artikelen toohello.)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Volgende stappen
Deze diagnostische hulpprogramma's kunnen u controleren Hallo telemetrie van uw app:

* [Metrische explorer](app-insights-metrics-explorer.md)
* [Search explorer](app-insights-diagnostic-search.md)
* [Analytics - krachtige querytaal](app-insights-analytics-tour.md)

Detectie van de smartcard is volledig automatisch. Maar misschien wilt u tooset van sommige waarschuwingen meer?

* [Handmatig geconfigureerde metrische waarschuwingen](app-insights-alerts.md)
* [Webtests voor beschikbaarheid](app-insights-monitor-web-app-availability.md) 

