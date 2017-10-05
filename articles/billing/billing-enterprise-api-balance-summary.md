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
# <a name="reporting-apis-for-enterprise-customers---balance-and-summary"></a><span data-ttu-id="8411f-103">Rapportage-API's voor Enterprise-klanten - saldo en samenvatting</span><span class="sxs-lookup"><span data-stu-id="8411f-103">Reporting APIs for Enterprise customers - Balance and Summary</span></span>

<span data-ttu-id="8411f-104">Het saldo en samenvatting API biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen Azure Marketplace kosten, aanpassingen en overschrijding kosten.</span><span class="sxs-lookup"><span data-stu-id="8411f-104">The Balance and Summary API offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments, and overage charges.</span></span>


##<a name="request"></a><span data-ttu-id="8411f-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8411f-105">Request</span></span> 
<span data-ttu-id="8411f-106">Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="8411f-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="8411f-107">Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8411f-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="8411f-108">Methode</span><span class="sxs-lookup"><span data-stu-id="8411f-108">Method</span></span> | <span data-ttu-id="8411f-109">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="8411f-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="8411f-110">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="8411f-110">GET</span></span>| <span data-ttu-id="8411f-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="8411f-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/balancesummary</span></span>|
|<span data-ttu-id="8411f-112">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="8411f-112">GET</span></span>| <span data-ttu-id="8411f-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / balancesummary</span><span class="sxs-lookup"><span data-stu-id="8411f-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/balancesummary</span></span>|

> [!Note]
> <span data-ttu-id="8411f-114">Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.</span><span class="sxs-lookup"><span data-stu-id="8411f-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="8411f-115">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8411f-115">Response</span></span>

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


<span data-ttu-id="8411f-116">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="8411f-116">**Response property definitions**</span></span>

|<span data-ttu-id="8411f-117">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="8411f-117">Property Name</span></span>| <span data-ttu-id="8411f-118">Type</span><span class="sxs-lookup"><span data-stu-id="8411f-118">Type</span></span>| <span data-ttu-id="8411f-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8411f-119">Description</span></span>
|-|-|-|
|<span data-ttu-id="8411f-120">id</span><span class="sxs-lookup"><span data-stu-id="8411f-120">id</span></span>|<span data-ttu-id="8411f-121">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8411f-121">string</span></span>|<span data-ttu-id="8411f-122">De unieke Id voor een specifieke factureringsperiode en de inschrijving</span><span class="sxs-lookup"><span data-stu-id="8411f-122">The unique Id for a specific billing period and enrollment</span></span>|
|<span data-ttu-id="8411f-123">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="8411f-123">billingPeriodId</span></span>|<span data-ttu-id="8411f-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8411f-124">string</span></span> |<span data-ttu-id="8411f-125">De Id van de factureringsperiode</span><span class="sxs-lookup"><span data-stu-id="8411f-125">The billing period Id</span></span>|
|<span data-ttu-id="8411f-126">currencyCode</span><span class="sxs-lookup"><span data-stu-id="8411f-126">currencyCode</span></span>|<span data-ttu-id="8411f-127">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8411f-127">string</span></span> |<span data-ttu-id="8411f-128">De valutacode</span><span class="sxs-lookup"><span data-stu-id="8411f-128">The currency code</span></span>|
|<span data-ttu-id="8411f-129">beginningBalance</span><span class="sxs-lookup"><span data-stu-id="8411f-129">beginningBalance</span></span>|<span data-ttu-id="8411f-130">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-130">decimal</span></span>| <span data-ttu-id="8411f-131">Het beginsaldo voor de factureringsperiode</span><span class="sxs-lookup"><span data-stu-id="8411f-131">The beginning balance for the billing period</span></span>|
|<span data-ttu-id="8411f-132">endingBalance</span><span class="sxs-lookup"><span data-stu-id="8411f-132">endingBalance</span></span>|<span data-ttu-id="8411f-133">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-133">decimal</span></span>| <span data-ttu-id="8411f-134">Het eindsaldo voor de factureringsperiode (voor open perioden die dit wordt dagelijks bijgewerkt)</span><span class="sxs-lookup"><span data-stu-id="8411f-134">The ending balance for the billing period (for open periods this will be updated daily)</span></span>|
|<span data-ttu-id="8411f-135">newPurchases</span><span class="sxs-lookup"><span data-stu-id="8411f-135">newPurchases</span></span>|<span data-ttu-id="8411f-136">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-136">decimal</span></span>| <span data-ttu-id="8411f-137">Totaalbedrag nieuwe aankoop</span><span class="sxs-lookup"><span data-stu-id="8411f-137">Total new purchase amount</span></span>|
|<span data-ttu-id="8411f-138">aanpassingen aan</span><span class="sxs-lookup"><span data-stu-id="8411f-138">adjustments</span></span>|<span data-ttu-id="8411f-139">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-139">decimal</span></span>| <span data-ttu-id="8411f-140">Aanpassing van de totale hoeveelheid</span><span class="sxs-lookup"><span data-stu-id="8411f-140">Total adjustment amount</span></span>|
|<span data-ttu-id="8411f-141">gebruikt</span><span class="sxs-lookup"><span data-stu-id="8411f-141">utilized</span></span>|<span data-ttu-id="8411f-142">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-142">decimal</span></span>| <span data-ttu-id="8411f-143">Totaal gebruik voor vastlegging</span><span class="sxs-lookup"><span data-stu-id="8411f-143">Total Commitment usage</span></span>|
|<span data-ttu-id="8411f-144">serviceOverage</span><span class="sxs-lookup"><span data-stu-id="8411f-144">serviceOverage</span></span>|<span data-ttu-id="8411f-145">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-145">decimal</span></span>| <span data-ttu-id="8411f-146">Overschrijding voor Azure-services</span><span class="sxs-lookup"><span data-stu-id="8411f-146">Overage for Azure services</span></span>|
|<span data-ttu-id="8411f-147">chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8411f-147">chargesBilledSeparately</span></span>|<span data-ttu-id="8411f-148">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-148">decimal</span></span>| <span data-ttu-id="8411f-149">Kosten worden afzonderlijk gefactureerd</span><span class="sxs-lookup"><span data-stu-id="8411f-149">Charges Billed separately</span></span>|
|<span data-ttu-id="8411f-150">totalOverage</span><span class="sxs-lookup"><span data-stu-id="8411f-150">totalOverage</span></span>|<span data-ttu-id="8411f-151">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-151">decimal</span></span>| <span data-ttu-id="8411f-152">serviceOverage + chargesBilledSeparately</span><span class="sxs-lookup"><span data-stu-id="8411f-152">serviceOverage + chargesBilledSeparately</span></span>|
|<span data-ttu-id="8411f-153">totalUsage</span><span class="sxs-lookup"><span data-stu-id="8411f-153">totalUsage</span></span>|<span data-ttu-id="8411f-154">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-154">decimal</span></span>| <span data-ttu-id="8411f-155">Azure-service streven + totale overschrijding</span><span class="sxs-lookup"><span data-stu-id="8411f-155">Azure service commitment + total Overage</span></span>|
|<span data-ttu-id="8411f-156">azureMarketplaceServiceCharges</span><span class="sxs-lookup"><span data-stu-id="8411f-156">azureMarketplaceServiceCharges</span></span>|<span data-ttu-id="8411f-157">Decimale</span><span class="sxs-lookup"><span data-stu-id="8411f-157">decimal</span></span>| <span data-ttu-id="8411f-158">Totale kosten voor Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8411f-158">Total charges for Azure Marketplace</span></span>|
|<span data-ttu-id="8411f-159">newPurchasesDetails</span><span class="sxs-lookup"><span data-stu-id="8411f-159">newPurchasesDetails</span></span>|<span data-ttu-id="8411f-160">JSON-tekenreeksmatrix met naam-waardeparen</span><span class="sxs-lookup"><span data-stu-id="8411f-160">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8411f-161">Lijst met nieuwe aankopen</span><span class="sxs-lookup"><span data-stu-id="8411f-161">List of new purchases</span></span>|
|<span data-ttu-id="8411f-162">adjustmentDetails</span><span class="sxs-lookup"><span data-stu-id="8411f-162">adjustmentDetails</span></span>|<span data-ttu-id="8411f-163">JSON-tekenreeksmatrix met naam-waardeparen</span><span class="sxs-lookup"><span data-stu-id="8411f-163">JSON string array of Name Value pairs</span></span>|<span data-ttu-id="8411f-164">Lijst met aanpassingen (aanbieding tegoed, u tegoed enz.)</span><span class="sxs-lookup"><span data-stu-id="8411f-164">List of Adjustments (Promo credit, SIE credit etc.)</span></span> |


<br/>
## <a name="see-also"></a><span data-ttu-id="8411f-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8411f-165">See also</span></span>

* [<span data-ttu-id="8411f-166">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="8411f-166">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="8411f-167">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="8411f-167">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="8411f-168">Marketplace Store kosten API</span><span class="sxs-lookup"><span data-stu-id="8411f-168">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md) 

* [<span data-ttu-id="8411f-169">Prijs blad API</span><span class="sxs-lookup"><span data-stu-id="8411f-169">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)