---
title: aaaAzure Application Insights telemetrie Data Model - gebeurtenis telemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor telemetrie van gebeurtenis
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
ms.openlocfilehash: cd7dc3c5f4f3df22b7a52ee79fcad566a27a9f4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-telemetry-application-insights-data-model"></a>Gebeurtenis telemetrie: Application Insights-gegevensmodel

Kunt u de gebeurtenis telemetrie-items maken (in [Application Insights](app-insights-overview.md)) toorepresent een gebeurtenis die is opgetreden in uw toepassing. Het is doorgaans een gebruikersinteractie zoals knop klikt u op of afhandeling bestellen. Het kan ook een gebeurtenis van de levenscyclus van de toepassing zoals configuratie of de initialisatie van de update zijn. 

Semantisch, gebeurtenissen al dan niet gecorreleerde toorequests. Gebeurtenis telemetrie is echter belangrijker dan de wijzigingsaanvragen of traceringen als goed gebruikt. Gebeurtenissen vertegenwoordigen de zakelijke Telemetrie en moet een onderwerpnaam tooseparate minder agressieve [steekproeven](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Naam

De naam van de gebeurtenis. de juiste groepering tooallow en nuttig metrische gegevens, beperkt uw toepassing zodat er een klein aantal afzonderlijke gebeurtenisnamen gegenereerd. Bijvoorbeeld, gebruik niet een afzonderlijke naam voor elk gegenereerde exemplaar van een gebeurtenis.

Maximale lengte: 512 tekens

## <a name="custom-properties"></a>Aangepaste eigenschappen

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Aangepaste metingen

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Volgende stappen

- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- [Aangepaste gebeurtenis telemetrie schrijven](app-insights-api-custom-events-metrics.md#trackevent)
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.
