---
title: aaaAzure Application Insights telemetrie Data Model - Afhankelijkheidstelemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor afhankelijkheidstelemetrie
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/17/2017
ms.author: bwren
ms.openlocfilehash: cd5ab7c61d3498e4aa2a0aa0c8b0d106a92912e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="dependency-telemetry-application-insights-data-model"></a>Afhankelijkheidstelemetrie: Application Insights-gegevensmodel

Afhankelijkheidstelemetrie (in [Application Insights](app-insights-overview.md)) vertegenwoordigt een interactie van Hallo bewaakt onderdeel met een externe component zoals SQL of een HTTP-eindpunt.

## <a name="name"></a>Naam

Naam van Hallo-opdracht met deze afhankelijkheidsaanroep is gestart. De kardinaliteit van de lage waarde. Voorbeelden zijn opgeslagen procedurenaam en sjabloon voor URL-pad.

## <a name="id"></a>Id

Id van een exemplaar van de aanroep van afhankelijkheid. Gebruikt voor correlatie met Hallo telemetrie-item voor aanvraag toothis afhankelijkheidsaanroep dat overeenkomt. Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.

## <a name="data"></a>Gegevens

Opdracht die door deze afhankelijkheidsaanroep gestart. Voorbeelden zijn SQL-instructie en HTTP-URL met alle queryparameters.

## <a name="type"></a>Type

Afhankelijkheid typenaam. De waarde van de lage kardinaliteit voor logische groepering van afhankelijkheden en de interpretatie van andere velden zoals commandName en resultCode. Voorbeelden zijn SQL Azure-tabel en HTTP.

## <a name="target"></a>doel

Site van het doel van een afhankelijkheidsaanroep van. Voorbeelden zijn servernaam, hostadres. Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.

## <a name="duration"></a>Duur

Duur in de indeling van aanvraag: `DD.HH:MM:SS.MMMMMM`. Moet kleiner zijn dan `1000` dagen.

## <a name="result-code"></a>Resultaatcode

De resultaatcode van een afhankelijkheidsaanroep van. Voorbeelden zijn SQL-foutcode en HTTP-statuscode.

## <a name="success"></a>Geslaagd

De vermelding van geslaagde of mislukte aanroep.

## <a name="custom-properties"></a>Aangepaste eigenschappen

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Aangepaste metingen

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a>Volgende stappen

- Instellen voor bijhouden van afhankelijkheid [.NET](app-insights-asp-net-dependencies.md).
- Instellen voor bijhouden van afhankelijkheid [Java](app-insights-java-agent.md).
- [Aangepaste afhankelijkheidstelemetrie schrijven](app-insights-api-custom-events-metrics.md#trackdependency)
- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.
