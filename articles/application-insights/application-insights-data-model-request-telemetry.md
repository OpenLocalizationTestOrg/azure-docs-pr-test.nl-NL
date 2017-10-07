---
title: aaaAzure gegevensmodel voor Application Insights telemetrie - aanvraag telemetrie | Microsoft Docs
description: Application Insights-gegevensmodel voor aanvraagtelemetrie
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
ms.openlocfilehash: 6042975a35f5e672e5adb5390feecc63d0b284b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="request-telemetry-application-insights-data-model"></a>Telemetrie aanvragen: Application Insights-gegevensmodel

Een aanvraag telemetrie-item (in [Application Insights](app-insights-overview.md)) vertegenwoordigt Hallo logische volgorde van de uitvoering is geactiveerd door een externe aanvraag tooyour-toepassing. Elke uitvoering van een aanvraag wordt geïdentificeerd met unieke `ID` en `url` met alle Hallo execution-parameters. U kunt aanvragen groeperen op logische `name` en definieer Hallo `source` van deze aanvraag. De uitvoering van code kan leiden tot `success` of `fail` en heeft een bepaalde `duration`. Geslaagde en mislukte uitvoeringen kunnen worden gegroepeerd door verdere `resultCode`. Begintijd voor Hallo-aanvraagtelemetrie op Hallo envelop niveau gedefinieerd.

Aanvraag telemetrie ondersteunt standaard uitbreidbaarheidsmodel Hallo met behulp van aangepaste `properties` en `measurements`.

## <a name="name"></a>Naam

Naam van de aanvraag Hallo vertegenwoordigt aanvraag Hallo tooprocess pad dat wordt gebruikt. De kardinaliteit van de lage waarde tooallow beter groepering van aanvragen. Voor deze HTTP-aanvragen vertegenwoordigt Hallo HTTP-methode en URL-pad sjabloon zoals `GET /values/{id}` zonder Hallo werkelijke `id` waarde.

Aanvraagnaam 'als zodanig' verzendt Application Insights web SDK met groet tooletter case. Groeperen op UI is hoofdlettergevoelig zodat `GET /Home/Index` afzonderlijk wordt geteld van `GET /home/INDEX` Hoewel vaak ze in Hallo dezelfde resulteren controller en de actie uitvoeren. Hallo reden hiervoor is dat URL's in het algemeen zijn [hoofdlettergevoelig](http://www.w3.org/TR/WD-html40-970708/htmlweb.html). U kunt toosee als alle `404` gebeurd voor Hallo URL's in hoofdletters worden getypt. U kunt meer op de naam van verzameling request door ASP.Net Web SDK in Hallo lezen [blogbericht](http://apmtips.com/blog/2015/02/23/request-name-and-url/).

Maximale lengte: 1024 tekens

## <a name="id"></a>Id

Id van een exemplaar van de aanvraag-aanroep. Gebruikt voor correlatie tussen aanvraag en andere telemetrie-items. ID moet uniek zijn. Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.

Maximale lengte: 128 tekens

## <a name="url"></a>URL

Aanvraag-URL met alle parameters voor query-tekenreeks.

Maximale lengte: 2048 tekens bestaan

## <a name="source"></a>Bron

Bron van het Hallo-aanvraag. Voorbeelden zijn Hallo instrumentatiesleutel van de aanroepfunctie Hallo of Hallo IP-adres van de aanroepfunctie Hallo. Zie voor meer informatie [correlatie](application-insights-correlation.md) pagina.

Maximale lengte: 1024 tekens

## <a name="duration"></a>Duur

Duur in de indeling van aanvraag: `DD.HH:MM:SS.MMMMMM`. Moet positief zijn en kleiner dan `1000` dagen. Dit veld is vereist als aanvraagtelemetrie Hallo opnieuw met de Hallo begin en einde van de Hallo vertegenwoordigt.

## <a name="response-code"></a>Reactiecode

Resultaat van een aanvraag kan worden uitgevoerd. HTTP-statuscode voor HTTP-aanvragen. Kan `HRESULT` waarde of uitzondering type voor andere aanvraagtypen.

Maximale lengte: 1024 tekens

## <a name="success"></a>Geslaagd

De vermelding van geslaagde of mislukte aanroep. Dit veld is vereist. Wanneer niet te expliciet ingesteld`false` -aanvraag toobe geslaagde beschouwd. Stel deze waarde te`false` als de bewerking is onderbroken door uitzondering of foutcode resultaat geretourneerd.

Voor webtoepassingen hello, Application Insights definiëren aanvraag is mislukt bij het Hallo-antwoordcode is minder Hallo `400` of gelijk zijn aan te`401`. Er zijn echter gevallen wanneer deze standaardtoewijzing komt niet overeen met de Hallo semantische van Hallo-toepassing. Antwoordcode `404` kan duiden op 'geen records', die deel van de normale stroom uitmaken kunnen. Ook kan dit wijzen op een verbroken koppeling. Hallo verbroken koppelingen, kunt u ook meer geavanceerde logica implementeren. Alleen wanneer deze koppelingen zich op dezelfde site door te analyseren url verwijzende hello, kunt u verbroken koppelingen markeren als fouten. Of als codefouten wanneer deze vanuit de mobiele toepassing van het bedrijf Hallo gemarkeerd. Op dezelfde manier `301` en `302` geeft aan wanneer deze vanuit het Hallo-client die biedt geen ondersteuning voor omleiding is mislukt.

Gedeeltelijk geaccepteerd inhoud `206` kan duiden op een storing van een algemene aanvraag. Application Insights-eindpunt ontvangt bijvoorbeeld een batch van telemetrie-items als één aanvraag. Deze retourneert `206` wanneer sommige items in Hallo batch zijn niet verwerkt. Toenemende aantal `206` duidt op een probleem dat toobe onderzocht moet. Vergelijkbare logica van toepassing is te`207` meerdere Status waar Hallo geslaagd wellicht Hallo slechtste van afzonderlijke responscodes.

U kunt meer op aanvraag resultaat lezen code en de statuscode in Hallo [blogbericht](http://apmtips.com/blog/2016/12/03/request-success-and-response-code/).

## <a name="custom-properties"></a>Aangepaste eigenschappen

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Aangepaste metingen

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Volgende stappen

- [Aangepaste aanvraagtelemetrie schrijven](app-insights-api-custom-events-metrics.md#trackrequest)
- Zie [gegevensmodel](application-insights-data-model.md) voor Application Insights-typen en data model.
- Meer informatie over hoe te[configureren van ASP.NET Core](app-insights-asp-net.md) een toepassing met Application Insights.
- Bekijk [platforms](app-insights-platforms.md) ondersteund door de Application Insights.
