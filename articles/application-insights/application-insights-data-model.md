---
title: Application Insights telemetrie-gegevensmodel aaaAzure | Microsoft Docs
description: Overzicht beveiligingsmodel Application Insights-gegevens
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Application Insights telemetrie-gegevensmodel

[Azure Application Insights](app-insights-overview.md) verzendt telemetrie van uw web application toohello Azure-portal, zodat u Hallo prestaties en het gebruik van uw toepassing analyseren kunt. Hallo telemetrie model is gestandaardiseerd zodat het mogelijk toocreate platform en taalonafhankelijke bewaking. 

Gegevens die worden verzameld door Application Insights modellen dit patroon van een typische toepassing kan worden uitgevoerd:

![Application Insights-toepassingsmodel](./media/application-insights-data-model/application-insights-data-model.png)

Hallo zijn volgende typen telemetrie gebruikte toomonitor Hallo uitvoering van uw app. Hallo worden volgende drie typen doorgaans automatisch verzameld door Hallo Application Insights-SDK van Hallo web application framework:

* [**Aanvraag** ](application-insights-data-model-request-telemetry.md) -toolog een aanvraag ontvangen door uw app wordt gegenereerd. Bijvoorbeeld, Hallo Application Insights web SDK genereert automatisch een aanvraag telemetrie-item voor elke HTTP-aanvraag die uw web-app ontvangt. 

    Een **bewerking** is Hallo threads van uitvoering die een aanvraag wordt verwerkt. U kunt ook [code schrijven](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor andere typen bewerking, zoals een 'ontwaken' in een web-taak of de functie die regelmatig gegevens verwerkt.  Een id heeft. elke bewerking Deze ID die gebruikt too[group]((application-insights-correlation.md) worden kan alle telemetrie gegenereerd tijdens het Hallo-aanvraag wordt verwerkt door uw app. Elke bewerking ofwel slaagt of mislukt en heeft een tijdsduur.
* [**Uitzondering** ](application-insights-data-model-exception-telemetry.md) -vertegenwoordigt doorgaans een uitzondering dat ervoor zorgt een toofail bewerking dat.
* [**Afhankelijkheid** ](application-insights-data-model-dependency-telemetry.md) -vertegenwoordigt een aanroep van uw app tooan externe service of de opslag, zoals een REST-API of de SQL. In ASP.NET, afhankelijkheid aanroepen tooSQL zijn gedefinieerd door `System.Data`. Aanroepen tooHTTP eindpunten zijn gedefinieerd door `System.Net`. 

Application Insights biedt drie extra gegevenstypen voor aangepaste telemetrie:

* [Tracering](application-insights-data-model-trace-telemetry.md) - gebruikt hetzij rechtstreeks of via een netwerkadapter tooimplement Diagnostische logboekregistratie met behulp van een instrumentation framework dat is bekend tooyou zoals `Log4Net` of `System.Diagnostics`.
* [Gebeurtenis](application-insights-data-model-event-telemetry.md) -toocapture gebruikersinteractie met uw service, gebruikspatronen tooanalyze doorgaans worden gebruikt.
* [Metriek](application-insights-data-model-metric-telemetry.md) -tooreport periodieke scalaire metingen gebruikt.

Elk telemetrie-item kunt definiëren Hallo [contextgegevens](application-insights-data-model-context.md) toepassing versie of gebruiker sessie-id. Context is een reeks sterk getypeerde velden die blokkering bepaalde scenario's opgeheven. Wanneer de toepassingsversie correct is geïnitialiseerd, kan Application Insights nieuwe patronen in het gedrag van toepassingen opnieuw implementeren gaande gecorreleerd detecteren. Sessie-id kan bestaan gebruikte toocalculate Hallo storing of een probleem gevolgen voor gebruikers. Afhankelijkheid unieke tellingen van sessie-id-waarden voor bepaalde berekenen mislukt, fouttracering of kritieke uitzondering biedt een goed inzicht botsingen.

Application Insights telemetrie model definieert een manier te[correleren](application-insights-correlation.md) telemetrie toohello bewerking waarvan het deel uitmaakt. Bijvoorbeeld, een aanvraag kunt u een SQL-Database-aanroepen en de geregistreerde diagnostische gegevens. Hallo correlatie context voor de telemetrie-items die deze toohello vorige-aanvraagtelemetrie koppelen, kunt u instellen.

## <a name="schema-improvements"></a>Schema-verbeteringen

Application Insights-gegevensmodel is een eenvoudige en eenvoudige maar krachtige manier toomodel telemetrie van uw toepassing. We streven ernaar tookeep Hallo model eenvoudige en compacte toosupport essentiële scenario's en tooextend Hallo schema voor ervaren gebruikers toestaan.

tooreport data model- of schema problemen en suggesties gebruiken GitHub [ApplicationInsights-startpagina](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) opslagplaats.

## <a name="next-steps"></a>Volgende stappen

- [Aangepaste telemetrie schrijven](app-insights-api-custom-events-metrics.md)
- Meer informatie over hoe te[uitbreiden en het filteren van telemetrie](app-insights-api-filtering-sampling.md).
- Gebruik [steekproeven](app-insights-sampling.md) toominimize hoeveelheid telemetrie op basis van gegevensmodel.
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.
