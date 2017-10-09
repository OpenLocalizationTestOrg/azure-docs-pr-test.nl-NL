---
title: aaaAzure facturering Enterprise-API's - Marketplace-kosten | Microsoft Docs
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
ms.openlocfilehash: cdf2836b52df06a4bf5ed71a476fe33662c5363c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a>Rapportage-API's voor Enterprise-klanten - Marketplace Store kosten

Hallo Marketplace Store kosten API retourneert Hallo marketplace op gebruik gebaseerde kosten uitsplitsing per dag voor Hallo opgegeven facturering periode of begin- en einddatums (één keer kosten zijn niet opgenomen).

##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd. Aangepaste tijdsbereik kunnen worden opgegeven met Hallo gestart en datumparameters die tijdig Hallo indeling JJJJ-MM-dd Hallo maximale ondersteund bereik 36 maanden is eindigen.  

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 01-01-2017 & endTime = 2017-01-10|

> [!Note]
> toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.
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
|id|Tekenreeks|Unieke Id voor Hallo marketplace-kosten item|
|subscriptionGuid|GUID|Hallo abonnement-Guid|
|SubscriptionName|Tekenreeks|Hallo naam abonnement|
|meterId|Tekenreeks|ID voor Hallo verzonden Meter|
|usageStartDate|Datum/tijd|De begintijd voor Hallo gebruik record|
|usageEndDate|Datum/tijd|Eindtijd van de Hallo gebruik record|
|offerName|Tekenreeks|de naam van de aanbieding Hallo|
|resourceGroup|Tekenreeks|Hallo resource groep|
|Exemplaar-id|Tekenreeks|Exemplaar-Id|
|aanvullende informatie|Tekenreeks|Aanvullende informatie JSON-tekenreeks|
|tags|Tekenreeks|Tag JSON-tekenreeks|
|orderNumber|Tekenreeks|Hallo volgordenummer|
|unitOfMeasure|Tekenreeks|Eenheid voor Hallo meter|
|CostCenter|Tekenreeks|Hallo kosten center|
|accountId|int|Hallo account-Id|
|Accountnaam|Tekenreeks |Hallo-accountnaam|
|accountOwnerId|Tekenreeks|Hallo Account eigenaar-Id|
|DepartmentID gemeenschappelijk hebben|int|Hallo afdeling Id|
|DepartmentName|Tekenreeks|de naam van de afdeling Hallo|
|publisherName|Tekenreeks|naam van de uitgever Hallo|
|planName|Tekenreeks|de naam van de Hallo-abonnement|
|consumedQuantity|Decimale|Verbruikt aantal tijdens deze periode|
|resourceRate|Decimale|Prijs per eenheid voor Hallo meter|
|extendedCost|Decimale|Geschatte kosten op basis van de hoeveelheid verbruikte en Extended kosten|
<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md) 

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Prijs blad API](billing-enterprise-api-pricesheet.md)