---
title: aaaAzure facturering Enterprise-API's - saldo en overzicht | Microsoft Docs
description: Meer informatie over het gebruik van Azure-facturering en RateCard APIs's die gebruikt tooprovide inzichten in Azure brongebruik en trends zijn.
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
ms.openlocfilehash: b031de2c347e5abeacd11743cc96024434518918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>Rapportage-API's voor Enterprise-klanten - saldo en samenvatting

Hallo saldo en samenvatting API biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen Azure Marketplace kosten, aanpassingen en overschrijding kosten.


##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd.

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary|
|TOEVOEGEN| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary|

> [!Note]
> toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.
>

## <a name="response"></a>Antwoord

        {
            "id": "enrollments/100/billingperiods/201507/balancesummaries",
            "billingPeriodId": 201507,
            "currencyCode": "USD",
            "beginningBalance": 0,
            "endingBalance": 1.1,
            "newPurchases": 1,
            "adjustments": 1.1,
            "utilized": 1.1,
            "serviceOverage": 1,
            "chargesBilledSeparately": 1,
            "totalOverage": 1,
            "totalUsage": 1.1,
            "azureMarketplaceServiceCharges": 1,
            "newPurchasesDetails": [
                {
                "name": "",
                "value": 1
                }
            ],
            "adjustmentDetails": [
                {
                "name": "Promo Credit",
                "value": 1.1
                },
                {
                "name": "SIE Credit",
                "value": 1.0
                }
            ]
        }


**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|id|Tekenreeks|Hallo unieke Id voor een specifieke factureringsperiode en de inschrijving|
|billingPeriodId|Tekenreeks |Hallo facturering periode-Id|
|currencyCode|Tekenreeks |Hallo-valutacode|
|beginningBalance|Decimale| Hallo beginsaldo voor Hallo factureringsperiode|
|endingBalance|Decimale| Hallo eindsaldo voor Hallo factureringsperiode (voor open perioden die dit wordt dagelijks bijgewerkt)|
|newPurchases|Decimale| Totaalbedrag nieuwe aankoop|
|aanpassingen aan|Decimale| Aanpassing van de totale hoeveelheid|
|gebruikt|Decimale| Totaal gebruik voor vastlegging|
|serviceOverage|Decimale| Overschrijding voor Azure-services|
|chargesBilledSeparately|Decimale| Kosten worden afzonderlijk gefactureerd|
|totalOverage|Decimale| serviceOverage + chargesBilledSeparately|
|totalUsage|Decimale| Azure-service streven + totale overschrijding|
|azureMarketplaceServiceCharges|Decimale| Totale kosten voor Azure Marketplace|
|newPurchasesDetails|JSON-tekenreeksmatrix met naam-waardeparen|Lijst met nieuwe aankopen|
|adjustmentDetails|JSON-tekenreeksmatrix met naam-waardeparen|Lijst met aanpassingen (aanbieding tegoed, u tegoed enz.) |


<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md) 

* [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md) 

* [Prijs blad API](billing-enterprise-api-pricesheet.md)