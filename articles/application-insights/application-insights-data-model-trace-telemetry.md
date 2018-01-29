---
title: Azure Application Insights telemetrie gegevensmodel - Tracetelemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor tracetelemetrie
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
ms.author: mbullwin
ms.openlocfilehash: 0398774e21d89fd084e6929bc5e410697d2aafaa
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/01/2017
---
# <a name="trace-telemetry-application-insights-data-model"></a>Telemetrie traceren: Application Insights-gegevensmodel

Telemetrie traceren (in [Application Insights](app-insights-overview.md)) vertegenwoordigt `printf` stijl trace-instructies die tekst doorzocht. `Log4Net`, `NLog`, en andere vermeldingen in logboekbestanden op basis van tekst worden vertaald naar exemplaren van dit type. De tracering heeft geen metingen als een uitbreidbaarheid.

## <a name="message"></a>Bericht

Trace-bericht.

Maximale lengte: 32768 tekens

## <a name="severity-level"></a>Ernstniveau

Ernstniveau traceren. Waarde kan zijn `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="custom-properties"></a>Aangepaste eigenschappen

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a>Volgende stappen

- [.NET-traceerlogboeken in Application Insights verkennen](app-insights-asp-net-trace-logs.md).
- [Java in Application Insights traceerlogboeken verkennen](app-insights-java-trace-logs.md).
- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- [Aangepaste traceersessie telemetrie schrijven](app-insights-api-custom-events-metrics.md#tracktrace)
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.
