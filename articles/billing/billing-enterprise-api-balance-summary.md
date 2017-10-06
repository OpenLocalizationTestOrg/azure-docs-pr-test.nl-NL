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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="5f951-103">Rapportage-API's voor Enterprise-klanten - saldo en samenvatting</span><span class="sxs-lookup"><span data-stu-id="5f951-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="5f951-104">Hallo saldo en samenvatting API biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen Azure Marketplace kosten, aanpassingen en overschrijding kosten.</span><span class="sxs-lookup"><span data-stu-id="5f951-104">hello Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="5f951-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="5f951-105">Request</span></span> 
<span data-ttu-id="5f951-106">Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="5f951-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="5f951-107">Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5f951-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="5f951-108">Methode</span><span class="sxs-lookup"><span data-stu-id="5f951-108">Method</span></span> | <span data-ttu-id="5f951-109">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="5f951-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="5f951-110">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="5f951-110">GET</span></span>| <span data-ttu-id="5f951-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="5f951-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="5f951-112">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="5f951-112">GET</span></span>| <span data-ttu-id="5f951-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="5f951-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="5f951-114">toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.</span><span class="sxs-lookup"><span data-stu-id="5f951-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="5f951-115">Antwoord</span><span class="sxs-lookup"><span data-stu-id="5f951-115">Response</span></span>

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


<span data-ttu-id="5f951-116">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="5f951-116">**Response property definitions**</span></span>

|<span data-ttu-id="5f951-117">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="5f951-117">Property Name</span></span>| <span data-ttu-id="5f951-118">Type</span><span class="sxs-lookup"><span data-stu-id="5f951-118">Type</span></span>| <span data-ttu-id="5f951-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5f951-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="5f951-120">id</span><span class="sxs-lookup"><span data-stu-id="5f951-120">id</span></span>|<span data-ttu-id="5f951-121">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5f951-121">string</span></span>|<span data-ttu-id="5f951-122">Hallo unieke Id voor een specifieke factureringsperiode en de inschrijving</span><span class="sxs-lookup"><span data-stu-id="5f951-122">hello unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="5f951-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="5f951-123">billingPeriodId</span></span>|<span data-ttu-id="5f951-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5f951-124">string</span></span> |<span data-ttu-id="5f951-125">Hallo facturering periode-Id</span><span class="sxs-lookup"><span data-stu-id="5f951-125">hello billing period Id</span></span>|
|<span data-ttu-id="5f951-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="5f951-126">currencyCode</span></span>|<span data-ttu-id="5f951-127">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5f951-127">string</span></span> |<span data-ttu-id="5f951-128">Hallo-valutacode</span><span class="sxs-lookup"><span data-stu-id="5f951-128">hello currency code</span></span>|
|<span data-ttu-id="5f951-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="5f951-129">beginningBalance</span></span>|<span data-ttu-id="5f951-130">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-130">decimal</span></span>| <span data-ttu-id="5f951-131">Hallo beginsaldo voor Hallo factureringsperiode</span><span class="sxs-lookup"><span data-stu-id="5f951-131">hello beginning balance for hello billing period</span></span>|
|<span data-ttu-id="5f951-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="5f951-132">endingBalance</span></span>|<span data-ttu-id="5f951-133">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-133">decimal</span></span>| <span data-ttu-id="5f951-134">Hallo eindsaldo voor Hallo factureringsperiode (voor open perioden die dit wordt dagelijks bijgewerkt)</span><span class="sxs-lookup"><span data-stu-id="5f951-134">hello ending balance for hello billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="5f951-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="5f951-135">newPurchases</span></span>|<span data-ttu-id="5f951-136">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-136">decimal</span></span>| <span data-ttu-id="5f951-137">Totaalbedrag nieuwe aankoop</span><span class="sxs-lookup"><span data-stu-id="5f951-137">Total new purchase amount</span></span>|
|<span data-ttu-id="5f951-138">aanpassingen aan</span><span class="sxs-lookup"><span data-stu-id="5f951-138">adjustments</span></span>|<span data-ttu-id="5f951-139">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-139">decimal</span></span>| <span data-ttu-id="5f951-140">Aanpassing van de totale hoeveelheid</span><span class="sxs-lookup"><span data-stu-id="5f951-140">Total adjustment amount</span></span>|
|<span data-ttu-id="5f951-141">gebruikt</span><span class="sxs-lookup"><span data-stu-id="5f951-141">utilized</span></span>|<span data-ttu-id="5f951-142">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-142">decimal</span></span>| <span data-ttu-id="5f951-143">Totaal gebruik voor vastlegging</span><span class="sxs-lookup"><span data-stu-id="5f951-143">Total Commitment usage</span></span>|
|<span data-ttu-id="5f951-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="5f951-144">serviceOverage</span></span>|<span data-ttu-id="5f951-145">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-145">decimal</span></span>| <span data-ttu-id="5f951-146">Overschrijding voor Azure-services</span><span class="sxs-lookup"><span data-stu-id="5f951-146">Overage for Azure services</span></span>|
|<span data-ttu-id="5f951-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="5f951-147">chargesBilledSeparately</span></span>|<span data-ttu-id="5f951-148">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-148">decimal</span></span>| <span data-ttu-id="5f951-149">Kosten worden afzonderlijk gefactureerd</span><span class="sxs-lookup"><span data-stu-id="5f951-149">Charges Billed separately</span></span>|
|<span data-ttu-id="5f951-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="5f951-150">totalOverage</span></span>|<span data-ttu-id="5f951-151">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-151">decimal</span></span>| <span data-ttu-id="5f951-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="5f951-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="5f951-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="5f951-153">totalUsage</span></span>|<span data-ttu-id="5f951-154">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-154">decimal</span></span>| <span data-ttu-id="5f951-155">Azure-service streven + totale overschrijding</span><span class="sxs-lookup"><span data-stu-id="5f951-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="5f951-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="5f951-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="5f951-157">Decimale</span><span class="sxs-lookup"><span data-stu-id="5f951-157">decimal</span></span>| <span data-ttu-id="5f951-158">Totale kosten voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5f951-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="5f951-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="5f951-159">newPurchasesDetails</span></span>|<span data-ttu-id="5f951-160">JSON-tekenreeksmatrix met naam-waardeparen</span><span class="sxs-lookup"><span data-stu-id="5f951-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="5f951-161">Lijst met nieuwe aankopen</span><span class="sxs-lookup"><span data-stu-id="5f951-161">List of new purchases</span></span>|
|<span data-ttu-id="5f951-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="5f951-162">adjustmentDetails</span></span>|<span data-ttu-id="5f951-163">JSON-tekenreeksmatrix met naam-waardeparen</span><span class="sxs-lookup"><span data-stu-id="5f951-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="5f951-164">Lijst met aanpassingen (aanbieding tegoed, u tegoed enz.)</span><span class="sxs-lookup"><span data-stu-id="5f951-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="5f951-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5f951-165">See also</span></span>

* [<span data-ttu-id="5f951-166">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="5f951-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="5f951-167">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="5f951-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="5f951-168">Marketplace Store kosten API</span><span class="sxs-lookup"><span data-stu-id="5f951-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="5f951-169">Prijs blad API</span><span class="sxs-lookup"><span data-stu-id="5f951-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)