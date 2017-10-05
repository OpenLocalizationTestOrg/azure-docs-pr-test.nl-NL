---
title: Azure API's van Enterprise - Marketplace-kosten facturering | Microsoft Docs
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
ms.openlocfilehash: 5539623f7ae35e14b6dafe6fdf9efe4bcaba4fd3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>Rapportage-API's voor Enterprise-klanten - Marketplace Store kosten

De Marketplace Store kosten-API retourneert de uitsplitsing op gebruik gebaseerde marketplace-kosten per dag voor de opgegeven periode facturering of de begin- en einddatums (één keer kosten zijn niet opgenomen).

##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd. Aangepaste tijdsbereik kunnen worden opgegeven met het begin en einde datumparameters die zich in de indeling JJJJ-MM-dd, is het maximum aantal ondersteunde tijdsbereik 36 maanden.  

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 01-01-2017 & endTime = 2017-01-10|

> [!Note]
> Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.
>

## <a name="response"></a>Antwoord
 
    
        [
            {
                "id": "id",
                "subscriptionGuid": "00000000-0000-0000-0000-000000000000",
                "subscriptionName": "subName",
                "meterId": "2core",
                "usageStartDate": "2015-09-17T00:00:00Z",
                "usageEndDate": "2015-09-17T23:59:59Z",
                "offerName": "Virtual LoadMaster™ (VLM) for Azure",
                "resourceGroup": "Res group",
                "instanceId": "id",
                "additionalInfo": "{\"ImageType\":null,\"ServiceType\":\"Medium\"}",
                "tags": "",
                "orderNumber": "order",
                "unitOfMeasure": "",
                "costCenter": "100",
                "accountId": 100,
                "accountName": "Account Name",
                "accountOwnerId": "account@live.com",
                "departmentId": 101,
                "departmentName": "Department 1",
                "publisherName": "Publisher 1",
                "planName": "Plan name",
                "consumedQuantity": 1.15,
                "resourceRate": 0.1,
                "extendedCost": 1.11
            },
            ...
        ]
    

**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|id|Tekenreeks|Unieke Id voor de marketplace-kosten-item|
|subscriptionGuid|GUID|De abonnement-Guid|
|SubscriptionName|Tekenreeks|Naam van het abonnement|
|meterId|Tekenreeks|ID voor de Meter verzonden|
|usageStartDate|Datum/tijd|De begintijd voor de record gebruik|
|usageEndDate|Datum/tijd|De eindtijd voor de record gebruik|
|offerName|Tekenreeks|De naam van de aanbieding|
|resourceGroup|Tekenreeks|De resource-groep|
|Exemplaar-id|Tekenreeks|Exemplaar-Id|
|aanvullende informatie|Tekenreeks|Aanvullende informatie JSON-tekenreeks|
|tags|Tekenreeks|Tag JSON-tekenreeks|
|orderNumber|Tekenreeks|Het nummer van de|
|unitOfMeasure|Tekenreeks|Eenheid voor de meter|
|CostCenter|Tekenreeks|De kostenplaats|
|accountId|int|De account-Id|
|Accountnaam|Tekenreeks |De accountnaam|
|accountOwnerId|Tekenreeks|De Account eigenaar-Id|
|DepartmentID gemeenschappelijk hebben|int|De Id van de afdeling|
|DepartmentName|Tekenreeks|Naam van de afdeling|
|publisherName|Tekenreeks|Naam van de uitgever|
|planName|Tekenreeks|Naam van het abonnement|
|consumedQuantity|Decimale|Verbruikt aantal tijdens deze periode|
|resourceRate|Decimale|Prijs per eenheid voor de meter|
|extendedCost|Decimale|Geschatte kosten op basis van de hoeveelheid verbruikte en Extended kosten|
<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md) 

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Prijs blad API](billing-enterprise-api-pricesheet.md)