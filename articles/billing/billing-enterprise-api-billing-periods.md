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
# <a name="reporting-apis-for-enterprise-customers---billing-periods"></a><span data-ttu-id="4df6c-103">Rapportage-API's voor Enterprise-klanten - punten facturering</span><span class="sxs-lookup"><span data-stu-id="4df6c-103">Reporting APIs for Enterprise customers - Billing Periods</span></span>

<span data-ttu-id="4df6c-104">Hallo facturering perioden API retourneert een lijst met perioden met gegevens over het verbruik voor Hallo facturering opgegeven inschrijving in omgekeerde volgorde.</span><span class="sxs-lookup"><span data-stu-id="4df6c-104">hello Billing Periods API returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="4df6c-105">Elke categorie bevat een eigenschap toohello API route voor Hallo vier gegevenssets - BalanceSummary, UsageDetails Marktplace kosten en prijslijst aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="4df6c-105">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marktplace Charges, and PriceSheet.</span></span> <span data-ttu-id="4df6c-106">Als Hallo periode geen gegevens bevat, is de overeenkomstige eigenschap Hallo null.</span><span class="sxs-lookup"><span data-stu-id="4df6c-106">If hello period does not have data, hello corresponding property is null.</span></span> 


##<a name="request"></a><span data-ttu-id="4df6c-107">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="4df6c-107">Request</span></span> 
<span data-ttu-id="4df6c-108">Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="4df6c-108">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> 

|<span data-ttu-id="4df6c-109">Methode</span><span class="sxs-lookup"><span data-stu-id="4df6c-109">Method</span></span> | <span data-ttu-id="4df6c-110">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="4df6c-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="4df6c-111">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="4df6c-111">GET</span></span>| <span data-ttu-id="4df6c-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / billingperiods</span><span class="sxs-lookup"><span data-stu-id="4df6c-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingperiods</span></span>|

> [!Note]
> <span data-ttu-id="4df6c-113">toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.</span><span class="sxs-lookup"><span data-stu-id="4df6c-113">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="4df6c-114">Antwoord</span><span class="sxs-lookup"><span data-stu-id="4df6c-114">Response</span></span>
 
    
    
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
    

<span data-ttu-id="4df6c-115">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="4df6c-115">**Response property definitions**</span></span>

|<span data-ttu-id="4df6c-116">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="4df6c-116">Property Name</span></span>| <span data-ttu-id="4df6c-117">Type</span><span class="sxs-lookup"><span data-stu-id="4df6c-117">Type</span></span>| <span data-ttu-id="4df6c-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4df6c-118">Description</span></span>
|-|-|-|
|<span data-ttu-id="4df6c-119">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="4df6c-119">billingPeriodId</span></span>| <span data-ttu-id="4df6c-120">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4df6c-120">string</span></span>| <span data-ttu-id="4df6c-121">Hallo unieke Id die staat voor een bepaalde periode voor facturering</span><span class="sxs-lookup"><span data-stu-id="4df6c-121">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="4df6c-122">billingStart</span><span class="sxs-lookup"><span data-stu-id="4df6c-122">billingStart</span></span>| <span data-ttu-id="4df6c-123">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="4df6c-123">datetime</span></span>| <span data-ttu-id="4df6c-124">Hallo de begindatum van het type string ISO 8601</span><span class="sxs-lookup"><span data-stu-id="4df6c-124">ISO 8601 string representing hello period start date</span></span>|
|<span data-ttu-id="4df6c-125">billingEnd</span><span class="sxs-lookup"><span data-stu-id="4df6c-125">billingEnd</span></span>| <span data-ttu-id="4df6c-126">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="4df6c-126">datetime</span></span>| <span data-ttu-id="4df6c-127">Hallo einddatum type string ISO 8601</span><span class="sxs-lookup"><span data-stu-id="4df6c-127">ISO 8601 string representing hello period end date</span></span>|
|<span data-ttu-id="4df6c-128">balanceSummary</span><span class="sxs-lookup"><span data-stu-id="4df6c-128">balanceSummary</span></span>| <span data-ttu-id="4df6c-129">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4df6c-129">string</span></span>| <span data-ttu-id="4df6c-130">Hallo URL-pad toohello saldo samenvattingsgegevens voor deze periode van routes</span><span class="sxs-lookup"><span data-stu-id="4df6c-130">hello URL path that routes toohello Balance Summary data for this period</span></span>|
|<span data-ttu-id="4df6c-131">usageDetails</span><span class="sxs-lookup"><span data-stu-id="4df6c-131">usageDetails</span></span>| <span data-ttu-id="4df6c-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4df6c-132">string</span></span>| <span data-ttu-id="4df6c-133">Hallo URL-pad toohello informatie over het gebruik gegevens voor deze periode van routes</span><span class="sxs-lookup"><span data-stu-id="4df6c-133">hello URL path that routes toohello Usage Details data for this period</span></span>|
|<span data-ttu-id="4df6c-134">marketplaceCharges</span><span class="sxs-lookup"><span data-stu-id="4df6c-134">marketplaceCharges</span></span>| <span data-ttu-id="4df6c-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4df6c-135">string</span></span>| <span data-ttu-id="4df6c-136">Hallo URL-pad toohello Marketplace-kosten gegevens voor deze periode van routes</span><span class="sxs-lookup"><span data-stu-id="4df6c-136">hello URL path that routes toohello Marketplace Charges data for this period</span></span>|
|<span data-ttu-id="4df6c-137">Prijslijst</span><span class="sxs-lookup"><span data-stu-id="4df6c-137">priceSheet</span></span>| <span data-ttu-id="4df6c-138">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4df6c-138">string</span></span>| <span data-ttu-id="4df6c-139">Hallo URL-pad toohello prijslijst gegevens voor deze periode van routes</span><span class="sxs-lookup"><span data-stu-id="4df6c-139">hello URL path that routes toohello PriceSheet data for this period</span></span>|

<br/>
## <a name="see-also"></a><span data-ttu-id="4df6c-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4df6c-140">See also</span></span>

* [<span data-ttu-id="4df6c-141">Saldo en samenvatting API</span><span class="sxs-lookup"><span data-stu-id="4df6c-141">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="4df6c-142">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="4df6c-142">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="4df6c-143">Marketplace Store kosten API</span><span class="sxs-lookup"><span data-stu-id="4df6c-143">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="4df6c-144">Prijs blad API</span><span class="sxs-lookup"><span data-stu-id="4df6c-144">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)