---
title: Application Insights telemetrie correlatie aaaAzure | Microsoft Docs
description: Application Insights telemetrie correlatie
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
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>De correlatie telemetrie in Application Insights

Hallo wereld van micro services moet elke logische bewerking werk dat in de verschillende onderdelen van Hallo-service. Elk van deze onderdelen afzonderlijk kan worden bewaakt met [Application Insights](app-insights-overview.md). Hallo web-app onderdeel communiceert met de gebruikersreferenties voor authenticatie provider onderdeel toovalidate, en met Hallo API tooget onderdeelgegevens voor visualisatie. Hallo-API-onderdeel op zijn beurt kunt opvragen van gegevens van andere services en onderdelen van de cache-serviceprovider gebruiken en waarschuwen Hallo facturering component over deze aanroep. Application Insights ondersteunt gedistribueerde telemetrie correlatie. Hiermee kunt u toodetect welk onderdeel verantwoordelijk voor fouten of vermindering in prestaties is.

Dit artikel wordt uitgelegd Hallo-gegevensmodel dat is gebruikt door de Application Insights toocorrelate telemetrie verzonden door meerdere onderdelen. Er wordt aangegeven Hallo context doorgifte van technieken en protocollen. Het omvat tevens Hallo-implementatie van de correlatie-concepten Hallo op verschillende talen en platforms.

## <a name="telemetry-correlation-data-model"></a>Telemetrie correlatie-gegevensmodel

Application Insights definieert een [gegevensmodel](application-insights-data-model.md) voor gedistribueerde telemetrie correlatie. tooassociate telemetrie met logische bewerking hello, elk telemetrie-item heeft een contextveld `operation_Id`. Deze id wordt gedeeld door elk telemetrie-item in de tracering Hallo gedistribueerd. Dus zelfs met verlies van telemetrie van één laag kunt u nog steeds telemetrie die zijn gerapporteerd door de andere onderdelen koppelen.

Gedistribueerde logische bewerking bestaat gewoonlijk uit een reeks kleinere bewerkingen - aanvragen verwerkt door één van Hallo-onderdelen. Deze bewerkingen zijn gedefinieerd door [aanvragen telemetrie](application-insights-data-model-request-telemetry.md). Elke aanvraagtelemetrie heeft zijn eigen `id` die deze globaal unieke wijze identificeert. En alle telemetrie - traceringen, uitzonderingen, enz. die zijn gekoppeld aan deze aanvraag moet Hallo ingesteld `operation_parentId` toohello waarde van Hallo aanvraag `id`.

Elke uitgaande bewerking zoals HTTP-aanroep tooanother onderdeel dat wordt vertegenwoordigd door [afhankelijkheidstelemetrie](application-insights-data-model-dependency-telemetry.md). Afhankelijkheidstelemetrie definieert ook een eigen `id` globaal uniek is. Aanvraagtelemetrie, door deze afhankelijkheidsaanroep gestart wordt gebruikt als `operation_parentId`.

Hallo-weergave van het gebruik van gedistribueerde logische bewerking kunt u `operation_Id`, `operation_parentId`, en `request.id` met `dependency.id`. Deze velden definiëren eveneens Hallo oorzakelijk verband volgorde van telemetrie aanroepen.

Traces van onderdelen mogelijk andere gelijksoortig toohello Ga in de omgeving micro services. Elk onderdeel hebben een eigen instrumentatiesleutel in Application Insights. tooget telemetrie voor logische bewerking hello, moet u tooquery gegevens van elke opslag. Wanneer het aantal gelijksoortig grote is, moet u toohave een hint op waar toolook volgende.

Application Insights-gegevensmodel definieert twee velden toosolve dit probleem: `request.source` en `dependency.target`. het eerste veld Hallo identificeert Hallo-component die Hallo afhankelijkheid aanvraag gestart en Hallo identificeert tweede welk onderdeel antwoord Hallo van Hallo afhankelijkheidsaanroep wordt geretourneerd.


## <a name="example"></a>Voorbeeld

U gaat nu een voorbeeld van een toepassing STOCK prijzen Hallo een prijs van een bestand met de externe API Hallo voorraden API aangeroepen wordt weergegeven. Hallo STOCK prijzen toepassing heeft een pagina `Stock page` geopend met behulp van Hallo client web browser `GET /Home/Stock`. query's Hallo-toepassing hello STOCK API met behulp van een HTTP-aanroep `GET /api/stock/value`.

U kunt analyseren resulterende telemetrie een query uit te voeren:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

In Hallo resultaat weergave opmerking dat alle telemetrie-items Hallo hoofdmap delen `operation_Id`. Ajax aanroep uitgevoerd vanaf de pagina Hallo - nieuwe unieke id `qJSXU` is toegewezen toohello afhankelijkheidstelemetrie en pageView van id wordt gebruikt als `operation_ParentId`. Serveraanvraag gebruikt op zijn beurt van ajax-id als `operation_ParentId`, enzovoort.

| itemType   | naam                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Vooraf gedefinieerde pagina                |              | STYz               | STYz         |
| afhankelijkheid | GET-/Home/voorraad           | qJSXU        | STYz               | STYz         |
| Aanvraag    | GET-startpagina/voorraad            | KqKwlrSt9PA = | qJSXU              | STYz         |
| afhankelijkheid | /Api/stock/value ophalen      | bBrf2L7mm2g = | KqKwlrSt9PA =       | STYz         |

Wanneer Hallo nu aanroep `GET /api/stock/value` tooan externe service aangebracht gewenste tooknow Hallo identiteit van die server. U kunt instellen `dependency.target` veld op de juiste wijze. Wanneer de externe service Hallo biedt geen ondersteuning voor het controle - `target` toohello hostnaam van Hallo service, zoals is ingesteld `stock-prices-api.com`. Echter als die service zichzelf identificeert door te retourneren van een vooraf gedefinieerde HTTP-header - `target` Hallo service-identiteit waarmee de Application Insights toobuild gedistribueerd trace door het uitvoeren van query's telemetrie van die service bevat. 

## <a name="correlation-headers"></a>Correlatie headers

We werken over RFC voorstel voor Hallo [correlatie HTTP-protocol](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Dit voorstel definieert twee headers worden gebruikt:

- `Request-Id`Hallo globaal unieke id van Hallo-aanroep uitvoeren
- `Correlation-Context`-Hallo de naam van waarde-paren verzameling Hallo gedistribueerd trace eigenschappen uitvoeren

Hallo standaard definieert ook twee schema's van `Request-Id` generatie - platte en hiërarchische. Met de platte schema hello, er is een bekende `Id` sleutel gedefinieerd voor Hallo `Correlation-Context` verzameling.

Application Insights definieert Hallo [extensie](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) voor Hallo correlatie HTTP-protocol. Hierbij `Request-Context` naam / waardeparen toopropagate Hallo verzameling eigenschappen die worden gebruikt door de onmiddellijke aanroeper Hallo of opgeroepen. Application Insights-SDK maakt gebruik van deze header tooset `dependency.target` en `request.source` velden.

## <a name="open-tracing-and-application-insights"></a>Open tracering en Application Insights

[Open tracering](http://opentracing.io/) en Application Insights gegevens ziet er modellen 

- `request`, `pageView` te toegewezen**Span** met`span.kind = server`
- `dependency`toegewezen te**Span** met`span.kind = client`
- `id`van een `request` en `dependency` te toegewezen**Span.Id**
- `operation_Id`toegewezen te**TraceId**
- `operation_ParentId`toegewezen te**verwijzing** van het type`ChileOf`

Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.

Zie [specificatie](https://github.com/opentracing/specification/blob/master/specification.md) en [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md) voor definities van de concepten Open tracering.


## <a name="telemetry-correlation-in-net"></a>Telemetrie correlatie in .NET

Na verloop van tijd .NET gedefinieerd aantal manieren toocorrelate Telemetrie en diagnostische logboeken. Er is `System.Diagnostics.CorrelationManager` zodat tootrack [LogicalOperationStack en ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`en Windows (ETW) definiëren Hallo methode [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger`maakt gebruik van [logboek Scopes](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF- en HTTP-kabel van 'huidige' context doorgeven.

Deze methoden niet echter ondersteuning voor automatische gedistribueerde tracering inschakelen. `DiagnosticsSource`is een manier toosupport automatische cross-machine correlatie. .NET-bibliotheken ondersteunen diagnostische gegevens en automatische cross machine doorgifte van Hallo correlatie context via Hallo transport zoals http toestaan.

Hallo [tooActivities begeleiden](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) wordt uitgelegd Hallo basisbeginselen van het bijhouden van activiteiten in de bron van de diagnostische gegevens. 

ASP.NET Core 2.0 ondersteunt extractie van Http-Headers en nieuwe activiteit vanaf Hallo. 

`System.Net.HttpClient`versie `<fill in>` ondersteunt automatische injectie van Hallo correlatie Http-Headers en bij te houden Hallo http-aanroep als een activiteit.

Er is een nieuwe Http-Module [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) voor ASP.NET, klassiek Hallo. Deze module implementeert telemetrie correlatie met DiagnosticsSource. Deze activiteit op basis van binnenkomende aanvraagheaders wordt gestart. Deze correleert ook telemetrie van de verschillende stadia Hallo van aanvraagverwerking. Ook voor gevallen Hallo wanneer elke fase van de verwerking van IIS wordt uitgevoerd op een andere beheren threads.

Application Insights-SDK versie `2.4.0-beta1` DiagnosticsSource en activiteit toocollect telemetrie gebruikt en deze koppelen aan de huidige activiteit Hallo. 

## <a name="next-steps"></a>Volgende stappen

- [Aangepaste telemetrie schrijven](app-insights-api-custom-events-metrics.md)
- Ingebouwde alle onderdelen van uw micro-service op de Application Insights. Bekijk [ondersteunde platforms](app-insights-platforms.md).
- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- Meer informatie over hoe te[uitbreiden en het filteren van telemetrie](app-insights-api-filtering-sampling.md).
