---
title: Enterprise-API's facturering aaaAzure | Microsoft Docs
description: Meer informatie over Hallo rapportage-API's waarmee Azure Enterprise-klanten toopull verbruiksgegevens programmatisch.
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a>Overzicht van de rapportage-API's voor Enterprise-klanten
Hallo rapportage-API's kunnen Azure Enterprise-klanten tooprogrammatically pull gebruiks- en factureringsgegevens in de gewenste hulpprogramma's voor gegevensanalyse. 

## <a name="enabling-data-access-toohello-api"></a>Data access-toohello API inschakelen
* **Genereren of Hallo API-sleutel ophalen** - logboek in toohello Enterprise portal en volg Hallo zelfstudie onder Help - rapportage-API's. de eerste sectie Hallo onder deze help-artikel wordt uitgelegd hoe toogenerate of ophalen Hallo API-sleutel voor Hallo inschrijving opgegeven.
* **Sleutels doorgeven in een Hallo API** -Hallo API-sleutel moet toobe doorgegeven voor elke aanroep voor verificatie en autorisatie. Hallo volgende-eigenschap moet toobe toohello HTTP-headers

|Aanvraag-Header-sleutel | Waarde|
|-|-|
|Autorisatie| Hallo-waarde opgeven die in deze indeling: **bearer {API_KEY}** <br/> Voorbeeld: bearer eyr... 09|

## <a name="consumption-apis"></a>Verbruik API 's
Een Swagger-eindpunt is beschikbaar [hier](https://consumption.azure.com/swagger/ui/index) voor Hallo API's die zijn beschreven hieronder moet eenvoudig introspection van Hallo API en Hallo mogelijkheid toogenerate client-SDK's inschakelen met behulp van [AutoRest](https://github.com/Azure/AutoRest) of [ Swagger codegen gebruikt](http://swagger.io/swagger-codegen/). Gegevens vanaf 1 mei 2014 is beschikbaar via deze API. 

* **Saldo en samenvatting** - hello [saldo en samenvatting API](billing-enterprise-api-balance-summary.md) biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen, kosten voor Azure Marketplace, correcties en overschrijding kosten.

* **Informatie over het gebruik** - hello [gebruik Detail API](billing-enterprise-api-usage-detail.md) per dag opgesplitst verbruikte aantallen en de geschatte kosten door een inschrijving biedt. Hallo resultaat bevat ook informatie over exemplaren, meters en afdelingen. Hallo API kan worden doorzocht door facturering periode of door een opgegeven begin- en einddatum. 

* **Marketplace Store kosten** - hello [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md) retourneert Hallo op gebruik gebaseerde marketplace-kosten uitsplitsing per dag voor Hallo opgegeven facturering periode of begin- en einddatums (één keer kosten zijn niet opgenomen) .

* **Prijslijst** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) Hallo toepasselijke frequentie voor elke Meter voor registratie en facturering periode Hallo biedt. 

## <a name="helper-apis"></a>Helper-API 's
 **Lijst van facturering perioden** - hello [facturering perioden API](billing-enterprise-api-billing-periods.md) retourneert een lijst met facturering perioden die gegevens over het verbruik voor Hallo inschrijving in omgekeerde volgorde opgegeven hebben. Elke categorie bevat een eigenschap toohello API route voor Hallo vier gegevenssets - BalanceSummary, UsageDetails Marketplace-kosten en prijslijst aan te wijzen.


## <a name="api-response-codes"></a>API-reactiecodes  
|Statuscode van antwoord|Bericht|Beschrijving|
|-|-|-|
|200| OK|Er is geen fout|
|401| Niet geautoriseerd| API-sleutel niet wordt gevonden, ongeldig, verlopen enzovoort.|
|404| Niet beschikbaar| Rapport eindpunt is niet gevonden|
|400| Onjuiste aanvraag| Ongeldige parameters: datumbereiken, EA nummers, enz.|
|500| Server-fout| Fout bij verwerking van aanvraag Unexoected| 









