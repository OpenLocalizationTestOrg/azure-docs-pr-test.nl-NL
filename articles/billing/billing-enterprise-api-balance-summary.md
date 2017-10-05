---
title: Azure Enterprise-API's - saldo en samenvatting facturering | Microsoft Docs
description: Meer informatie over het gebruik van Azure facturering en RateCard APIs's die worden gebruikt voor het bieden van inzicht in Azure brongebruik en trends.
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
ms.openlocfilehash: f6b149f0e656d2263705048aa5b644f5bb4a5712
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a>Rapportage-API's voor Enterprise-klanten - saldo en samenvatting

Het saldo en samenvatting API biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen Azure Marketplace kosten, aanpassingen en overschrijding kosten.


##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd.

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary|
|TOEVOEGEN| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary|

> [!Note]
> Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.
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
|id|Tekenreeks|De unieke Id voor een specifieke factureringsperiode en de inschrijving|
|billingPeriodId|Tekenreeks |De Id van de factureringsperiode|
|currencyCode|Tekenreeks |De valutacode|
|beginningBalance|Decimale| Het beginsaldo voor de factureringsperiode|
|endingBalance|Decimale| Het eindsaldo voor de factureringsperiode (voor open perioden die dit wordt dagelijks bijgewerkt)|
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