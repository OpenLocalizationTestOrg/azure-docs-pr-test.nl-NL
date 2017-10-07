---
title: aaaAzure facturering Enterprise-API's - punten facturering | Microsoft Docs
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
ms.openlocfilehash: d4e17f25b22729a7f213306fb019ee0dbeca87ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a>Rapportage-API's voor Enterprise-klanten - punten facturering

Hallo facturering perioden API retourneert een lijst met perioden met gegevens over het verbruik voor Hallo facturering opgegeven inschrijving in omgekeerde volgorde. Elke categorie bevat een eigenschap toohello API route voor Hallo vier gegevenssets - BalanceSummary, UsageDetails Marktplace kosten en prijslijst aan te wijzen. Als Hallo periode geen gegevens bevat, is de overeenkomstige eigenschap Hallo null. 


##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md). 

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN| https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods|

> [!Note]
> toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.
>

## <a name="response"></a>Antwoord
 
    
    
      [
            {
                "billingPeriodId": "201704",
                "billingStart": "2017-04-01T00:00:00Z",
                "billingEnd": "2017-04-30T11:59:59Z",
                "balanceSummary": "/v1/enrollments/100/billingperiods/201704/balancesummary",
                "usageDetails": "/v1/enrollments/100/billingperiods/201704/usagedetails",
                "marketplaceCharges": "/v1/enrollments/100/billingperiods/201704/marketplacecharges",
                "priceSheet": "/v1/enrollments/100/billingperiods/201704/pricesheet"
            },          
            ....
      ]
    

**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|billingPeriodId| Tekenreeks| Hallo unieke Id die staat voor een bepaalde periode voor facturering|
|billingStart| Datum/tijd| Hallo de begindatum van het type string ISO 8601|
|billingEnd| Datum/tijd| Hallo einddatum type string ISO 8601|
|balanceSummary| Tekenreeks| Hallo URL-pad toohello saldo samenvattingsgegevens voor deze periode van routes|
|usageDetails| Tekenreeks| Hallo URL-pad toohello informatie over het gebruik gegevens voor deze periode van routes|
|marketplaceCharges| Tekenreeks| Hallo URL-pad toohello Marketplace-kosten gegevens voor deze periode van routes|
|Prijslijst| Tekenreeks| Hallo URL-pad toohello prijslijst gegevens voor deze periode van routes|

<br/>
## <a name="see-also"></a>Zie ook

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Gebruik Detail API](billing-enterprise-api-usage-detail.md) 

* [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md) 

* [Prijs blad API](billing-enterprise-api-pricesheet.md)