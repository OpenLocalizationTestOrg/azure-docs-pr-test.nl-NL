---
title: aaaAzure facturering Enterprise-API's - prijslijst | Microsoft Docs
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a>Rapportage-API's voor Enterprise-klanten - prijslijst

Hallo Price Sheet API biedt Hallo toepasselijke frequentie voor elke Meter voor Hallo opgegeven registratie en facturering periode.

##<a name="request"></a>Aanvraag
Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd.

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / prijslijst|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / prijslijst|

> [!Note]
> toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.
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
>Als u van Hallo Preview-API gebruikmaakt, is meterId veld niet beschikbaar.
>

**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|id| Tekenreeks| Hallo unieke Id die staat voor een bepaald prijslijst item (meter door periode facturering)|
|billingPeriodId| Tekenreeks| Hallo unieke Id die staat voor een bepaalde periode voor facturering|
|meterId| Tekenreeks| Hallo-id voor Hallo meter. Het kan toegewezen toohello gebruik meterId zijn.|
|meterName| Tekenreeks| de naam van de meter Hallo|
|unitOfMeasure| Tekenreeks| Hallo eenheid voor het meten van Hallo-service|
|includedQuantity| Decimale| Aantal dat is opgenomen |
|partNumber| Tekenreeks| Hallo-onderdeelnummer Hallo Meter gekoppeld|
|prijs per eenheid| Decimale| prijs per eenheid Hallo voor Hallo meter|
|currencyCode| Tekenreeks| Hallo-valutacode voor Hallo prijs per eenheid|
<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md)

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md)
