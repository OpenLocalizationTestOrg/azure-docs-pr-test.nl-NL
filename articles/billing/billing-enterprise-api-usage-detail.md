---
title: aaaAzure facturering Enterprise-API's - informatie over het gebruik | Microsoft Docs
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
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>Rapportage-API's voor Enterprise-klanten - informatie over het gebruik

Hallo gebruik Detail API biedt per dag opgesplitst verbruikte aantallen en de geschatte kosten door een inschrijving. Hallo resultaat bevat ook informatie over exemplaren, meters en afdelingen. Hallo API kan worden doorzocht door facturering periode of door een opgegeven begin- en einddatum. 
## <a name="consumption-apis"></a>Verbruik API 's


##<a name="request"></a>Aanvraag 
Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md). Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd. Aangepaste tijdsbereik kunnen worden opgegeven met Hallo gestart en datumparameters in Hallo indeling JJJJ-MM-dd. beëindigen Hallo maximale ondersteunde tijdsbereik is 36 maanden.  

|Methode | Aanvraag-URI|
|-|-|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetails 
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / usagedetails|
|TOEVOEGEN|https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / usagedetailsbycustomdate? startTime = 01-01-2017 & endTime = 2017-01-10|

> [!Note]
> toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.
>

## <a name="response"></a>Antwoord

> Vanwege het potentieel grote hoeveelheid gegevens Hallo resultaat toohello set wisselbaar geheugen. Hallo nextLink eigenschap, indien aanwezig, geeft u Hallo-koppeling voor de volgende pagina Hallo van gegevens. Als het Hallo-koppeling is leeg, geeft aan dat de laatste pagina Hallo is. 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**Broneigenschapdefinities antwoord**

|De naam van eigenschap| Type| Beschrijving
|-|-|-|
|id| Tekenreeks| Hallo unieke Id voor Hallo API-aanroep. |
|Gegevens| JSON-matrix| Matrix van de details van het dagelijkse gebruik voor elke instance\meter Hello.|
|nextLink| Tekenreeks| Wanneer er meer pagina's met gegevens Hallo nextLink punten toohello URL tooreturn Hallo volgende pagina van gegevens. |
|accountId| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|product-id| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|resourceLocationId| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|consumedServiceID| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|DepartmentID gemeenschappelijk hebben| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|accountOwnerEmail| Tekenreeks| E-mailaccount van de accounteigenaar Hallo. |
|Accountnaam| Tekenreeks| De naam van de klant die is ingevoerd van Hallo-account. |
|serviceAdministratorId| Tekenreeks| E-mailadres van de Service-beheerder. |
|subscriptionId| int| Veld is verouderd. Aanwezig voor achterwaartse compatibiliteit. |
|subscriptionGuid| Tekenreeks| Globale unieke id voor het Hallo-abonnement. |
|SubscriptionName| Tekenreeks| De naam van het Hallo-abonnement. |
|Datum| Tekenreeks| Hallo datum waarop verbruik heeft plaatsgevonden. |
|Product| Tekenreeks| Meer informatie over het Hallo-meter. Voorbeeld: A1 (VM) Windows - Azië en Stille Oceaan Oost|
|meterId| Tekenreeks| Hallo-id voor Hallo meter die gebruik verzonden. |
|meterCategory| Tekenreeks| Hello Azure-platform-service die is gebruikt. |
|meterSubCategory| Tekenreeks| Definieert hello Azure servicetype die Hallo snelheid kan beïnvloeden. Voorbeeld: A1 VM (niet-Windows|
|meterRegion| Tekenreeks| Geeft de locatie Hallo van Hallo-datacenter voor bepaalde services die worden berekend op basis van locatie datacenter. |
|meterName| Tekenreeks| Naam van de meter Hallo. |
|consumedQuantity| dubbele| Hallo hoeveelheid Hallo meter die is verbruikt. |
|resourceRate| dubbele| Hallo-snelheid is van toepassing per factureerbare eenheid. |
|Kosten| dubbele| Hallo kosten die zijn gedaan voor Hallo meter. |
|resourceLocation| Tekenreeks| Identificeert Hallo datacenter waarop Hallo meter wordt uitgevoerd. |
|consumedService| Tekenreeks| Hello Azure-platform-service die is gebruikt. |
|Exemplaar-id| Tekenreeks| Deze id heet Hallo Hallo resource of Hallo volledig gekwalificeerde Resource-ID. Zie voor meer informatie [Azure Resource Manager-API](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| Tekenreeks| Metagegevens van de interne Azure-Service. |
|serviceInfo2| Tekenreeks| Bijvoorbeeld, een type installatiekopie voor een virtuele machine en de naam van de Internet-provider voor ExpressRoute. |
|aanvullende informatie| Tekenreeks| Service-specifieke metagegevens. Bijvoorbeeld, een type installatiekopie voor een virtuele machine. |
|tags| Tekenreeks| Klant labels toegevoegd. Zie voor meer informatie [ordenen van uw Azure-resources met labels](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags). |
|storeServiceIdentifier| Tekenreeks| Deze kolommen wordt niet gebruikt. Aanwezig voor achterwaartse compatibiliteit. |
|DepartmentName| Tekenreeks| Naam van het Hallo-afdeling. |
|CostCenter| Tekenreeks| Hallo-kostenplaats die Hallo gebruik is gekoppeld. |
|unitOfMeasure| Tekenreeks| Hallo-eenheid die Hallo-service wordt in rekening gebracht in identificeert. Voorbeeld: GB, uur, 10.000 s. |
|resourceGroup| Tekenreeks| Hallo-resourcegroep in welke Hallo geïmplementeerde meter wordt uitgevoerd in. Zie voor meer informatie [Overzicht van Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
<br/>
## <a name="see-also"></a>Zie ook

* [Facturering perioden API](billing-enterprise-api-billing-periods.md)

* [Saldo en samenvatting API](billing-enterprise-api-balance-summary.md)

* [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md) 

* [Prijs blad API](billing-enterprise-api-pricesheet.md)
