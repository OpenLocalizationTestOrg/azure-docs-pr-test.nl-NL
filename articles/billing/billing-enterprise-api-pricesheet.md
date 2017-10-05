---
title: Azure API's van Enterprise - prijslijst facturering | Microsoft Docs
description: Meer informatie over de rapportage-API's waarmee Azure Enterprise-klanten voor het ophalen van gegevens over het verbruik programmatisch.
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>Rapportage-API's voor Enterprise-klanten - prijslijst

De prijs blad API biedt het tarief voor elke meten voor de opgegeven registratie en facturering periode.

##<a name="request"></a>Aanvraag
Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd.

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / prijslijst|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / prijslijst|

> [!Note]
> Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.
>

## <a name="response"></a>Antwoord

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
>Als u de Preview-API gebruikt, is meterId veld niet beschikbaar.
>

**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|id| Tekenreeks| De unieke Id die staat voor een bepaald prijslijst item (meter door periode facturering)|
|billingPeriodId| Tekenreeks| De unieke Id die staat voor een bepaalde periode voor facturering|
|meterId| Tekenreeks| De id voor de meter. Deze kan worden toegewezen aan de meterId informatie over het gebruik.|
|meterName| Tekenreeks| De naam van de meter|
|unitOfMeasure| Tekenreeks| De eenheid voor het meten van de service|
|includedQuantity| Decimale| Aantal dat is opgenomen |
|partNumber| Tekenreeks| Het onderdeelnummer die zijn gekoppeld aan de Meter|
|prijs per eenheid| Decimale| De prijs per eenheid voor de meter|
|currencyCode| Tekenreeks| De valutacode voor de prijs per eenheid|
<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md)

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md)
