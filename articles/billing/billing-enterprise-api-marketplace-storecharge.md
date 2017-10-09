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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="6e8ec-103">Rapportage-API's voor Enterprise-klanten - Marketplace Store kosten</span><span class="sxs-lookup"><span data-stu-id="6e8ec-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="6e8ec-104">Hallo Marketplace Store kosten API retourneert Hallo marketplace op gebruik gebaseerde kosten uitsplitsing per dag voor Hallo opgegeven facturering periode of begin- en einddatums (één keer kosten zijn niet opgenomen).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-104">hello Marketplace Store Charge API returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="6e8ec-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="6e8ec-105">Request</span></span> 
<span data-ttu-id="6e8ec-106">Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="6e8ec-107">Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span> <span data-ttu-id="6e8ec-108">Aangepaste tijdsbereik kunnen worden opgegeven met Hallo gestart en datumparameters die tijdig Hallo indeling JJJJ-MM-dd Hallo maximale ondersteund bereik 36 maanden is eindigen.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-108">Custom time ranges can be specified with hello start and end date parameters that are in hello format yyyy-MM-dd, hello maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="6e8ec-109">Methode</span><span class="sxs-lookup"><span data-stu-id="6e8ec-109">Method</span></span> | <span data-ttu-id="6e8ec-110">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="6e8ec-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="6e8ec-111">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="6e8ec-111">GET</span></span>|<span data-ttu-id="6e8ec-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="6e8ec-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="6e8ec-113">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="6e8ec-113">GET</span></span>|<span data-ttu-id="6e8ec-114">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="6e8ec-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="6e8ec-115">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="6e8ec-115">GET</span></span>|<span data-ttu-id="6e8ec-116">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 01-01-2017 & endTime = 2017-01-10</span><span class="sxs-lookup"><span data-stu-id="6e8ec-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="6e8ec-117">toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-117">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="6e8ec-118">Antwoord</span><span class="sxs-lookup"><span data-stu-id="6e8ec-118">Response</span></span>
 
    
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
    

<span data-ttu-id="6e8ec-119">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="6e8ec-119">**Response property definitions**</span></span>

|<span data-ttu-id="6e8ec-120">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="6e8ec-120">Property Name</span></span>| <span data-ttu-id="6e8ec-121">Type</span><span class="sxs-lookup"><span data-stu-id="6e8ec-121">Type</span></span>| <span data-ttu-id="6e8ec-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e8ec-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="6e8ec-123">id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-123">id</span></span>|<span data-ttu-id="6e8ec-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-124">string</span></span>|<span data-ttu-id="6e8ec-125">Unieke Id voor Hallo marketplace-kosten item</span><span class="sxs-lookup"><span data-stu-id="6e8ec-125">Unique Id for hello marketplace charge item</span></span>|
|<span data-ttu-id="6e8ec-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="6e8ec-126">subscriptionGuid</span></span>|<span data-ttu-id="6e8ec-127">GUID</span><span class="sxs-lookup"><span data-stu-id="6e8ec-127">Guid</span></span>|<span data-ttu-id="6e8ec-128">Hallo abonnement-Guid</span><span class="sxs-lookup"><span data-stu-id="6e8ec-128">hello Subscription Guid</span></span>|
|<span data-ttu-id="6e8ec-129">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="6e8ec-129">subscriptionName</span></span>|<span data-ttu-id="6e8ec-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-130">string</span></span>|<span data-ttu-id="6e8ec-131">Hallo naam abonnement</span><span class="sxs-lookup"><span data-stu-id="6e8ec-131">hello Subscription Name</span></span>|
|<span data-ttu-id="6e8ec-132">meterId</span><span class="sxs-lookup"><span data-stu-id="6e8ec-132">meterId</span></span>|<span data-ttu-id="6e8ec-133">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-133">string</span></span>|<span data-ttu-id="6e8ec-134">ID voor Hallo verzonden Meter</span><span class="sxs-lookup"><span data-stu-id="6e8ec-134">Id for hello emitted Meter</span></span>|
|<span data-ttu-id="6e8ec-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="6e8ec-135">usageStartDate</span></span>|<span data-ttu-id="6e8ec-136">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="6e8ec-136">DateTime</span></span>|<span data-ttu-id="6e8ec-137">De begintijd voor Hallo gebruik record</span><span class="sxs-lookup"><span data-stu-id="6e8ec-137">Start time for hello usage record</span></span>|
|<span data-ttu-id="6e8ec-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="6e8ec-138">usageEndDate</span></span>|<span data-ttu-id="6e8ec-139">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="6e8ec-139">DateTime</span></span>|<span data-ttu-id="6e8ec-140">Eindtijd van de Hallo gebruik record</span><span class="sxs-lookup"><span data-stu-id="6e8ec-140">End time for hello usage record</span></span>|
|<span data-ttu-id="6e8ec-141">offerName</span><span class="sxs-lookup"><span data-stu-id="6e8ec-141">offerName</span></span>|<span data-ttu-id="6e8ec-142">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-142">string</span></span>|<span data-ttu-id="6e8ec-143">de naam van de aanbieding Hallo</span><span class="sxs-lookup"><span data-stu-id="6e8ec-143">hello Offer name</span></span>|
|<span data-ttu-id="6e8ec-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e8ec-144">resourceGroup</span></span>|<span data-ttu-id="6e8ec-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-145">string</span></span>|<span data-ttu-id="6e8ec-146">Hallo resource groep</span><span class="sxs-lookup"><span data-stu-id="6e8ec-146">hello resource Group</span></span>|
|<span data-ttu-id="6e8ec-147">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-147">instanceId</span></span>|<span data-ttu-id="6e8ec-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-148">string</span></span>|<span data-ttu-id="6e8ec-149">Exemplaar-Id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-149">Instance Id</span></span>|
|<span data-ttu-id="6e8ec-150">aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="6e8ec-150">additionalInfo</span></span>|<span data-ttu-id="6e8ec-151">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-151">string</span></span>|<span data-ttu-id="6e8ec-152">Aanvullende informatie JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-152">Additional info JSON string</span></span>|
|<span data-ttu-id="6e8ec-153">tags</span><span class="sxs-lookup"><span data-stu-id="6e8ec-153">tags</span></span>|<span data-ttu-id="6e8ec-154">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-154">string</span></span>|<span data-ttu-id="6e8ec-155">Tag JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-155">Tag JSON string</span></span>|
|<span data-ttu-id="6e8ec-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="6e8ec-156">orderNumber</span></span>|<span data-ttu-id="6e8ec-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-157">string</span></span>|<span data-ttu-id="6e8ec-158">Hallo volgordenummer</span><span class="sxs-lookup"><span data-stu-id="6e8ec-158">hello order number</span></span>|
|<span data-ttu-id="6e8ec-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="6e8ec-159">unitOfMeasure</span></span>|<span data-ttu-id="6e8ec-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-160">string</span></span>|<span data-ttu-id="6e8ec-161">Eenheid voor Hallo meter</span><span class="sxs-lookup"><span data-stu-id="6e8ec-161">Unit of measure for hello meter</span></span>|
|<span data-ttu-id="6e8ec-162">CostCenter</span><span class="sxs-lookup"><span data-stu-id="6e8ec-162">costCenter</span></span>|<span data-ttu-id="6e8ec-163">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-163">string</span></span>|<span data-ttu-id="6e8ec-164">Hallo kosten center</span><span class="sxs-lookup"><span data-stu-id="6e8ec-164">hello cost center</span></span>|
|<span data-ttu-id="6e8ec-165">accountId</span><span class="sxs-lookup"><span data-stu-id="6e8ec-165">accountId</span></span>|<span data-ttu-id="6e8ec-166">int</span><span class="sxs-lookup"><span data-stu-id="6e8ec-166">int</span></span>|<span data-ttu-id="6e8ec-167">Hallo account-Id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-167">hello account Id</span></span>|
|<span data-ttu-id="6e8ec-168">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="6e8ec-168">accountName</span></span>|<span data-ttu-id="6e8ec-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-169">string</span></span> |<span data-ttu-id="6e8ec-170">Hallo-accountnaam</span><span class="sxs-lookup"><span data-stu-id="6e8ec-170">hello Account Name</span></span>|
|<span data-ttu-id="6e8ec-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="6e8ec-171">accountOwnerId</span></span>|<span data-ttu-id="6e8ec-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-172">string</span></span>|<span data-ttu-id="6e8ec-173">Hallo Account eigenaar-Id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-173">hello Account Owner Id</span></span>|
|<span data-ttu-id="6e8ec-174">DepartmentID gemeenschappelijk hebben</span><span class="sxs-lookup"><span data-stu-id="6e8ec-174">departmentId</span></span>|<span data-ttu-id="6e8ec-175">int</span><span class="sxs-lookup"><span data-stu-id="6e8ec-175">int</span></span>|<span data-ttu-id="6e8ec-176">Hallo afdeling Id</span><span class="sxs-lookup"><span data-stu-id="6e8ec-176">hello department Id</span></span>|
|<span data-ttu-id="6e8ec-177">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="6e8ec-177">departmentName</span></span>|<span data-ttu-id="6e8ec-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-178">string</span></span>|<span data-ttu-id="6e8ec-179">de naam van de afdeling Hallo</span><span class="sxs-lookup"><span data-stu-id="6e8ec-179">hello department name</span></span>|
|<span data-ttu-id="6e8ec-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="6e8ec-180">publisherName</span></span>|<span data-ttu-id="6e8ec-181">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-181">string</span></span>|<span data-ttu-id="6e8ec-182">naam van de uitgever Hallo</span><span class="sxs-lookup"><span data-stu-id="6e8ec-182">hello publisher name</span></span>|
|<span data-ttu-id="6e8ec-183">planName</span><span class="sxs-lookup"><span data-stu-id="6e8ec-183">planName</span></span>|<span data-ttu-id="6e8ec-184">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e8ec-184">string</span></span>|<span data-ttu-id="6e8ec-185">de naam van de Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="6e8ec-185">hello Plan name</span></span>|
|<span data-ttu-id="6e8ec-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="6e8ec-186">consumedQuantity</span></span>|<span data-ttu-id="6e8ec-187">Decimale</span><span class="sxs-lookup"><span data-stu-id="6e8ec-187">decimal</span></span>|<span data-ttu-id="6e8ec-188">Verbruikt aantal tijdens deze periode</span><span class="sxs-lookup"><span data-stu-id="6e8ec-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="6e8ec-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="6e8ec-189">resourceRate</span></span>|<span data-ttu-id="6e8ec-190">Decimale</span><span class="sxs-lookup"><span data-stu-id="6e8ec-190">decimal</span></span>|<span data-ttu-id="6e8ec-191">Prijs per eenheid voor Hallo meter</span><span class="sxs-lookup"><span data-stu-id="6e8ec-191">Unit price for hello meter</span></span>|
|<span data-ttu-id="6e8ec-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="6e8ec-192">extendedCost</span></span>|<span data-ttu-id="6e8ec-193">Decimale</span><span class="sxs-lookup"><span data-stu-id="6e8ec-193">decimal</span></span>|<span data-ttu-id="6e8ec-194">Geschatte kosten op basis van de hoeveelheid verbruikte en Extended kosten</span><span class="sxs-lookup"><span data-stu-id="6e8ec-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="6e8ec-195">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6e8ec-195">See also</span></span>

* [<span data-ttu-id="6e8ec-196">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="6e8ec-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="6e8ec-197">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="6e8ec-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="6e8ec-198">Saldo en samenvatting API</span><span class="sxs-lookup"><span data-stu-id="6e8ec-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="6e8ec-199">Prijs blad API</span><span class="sxs-lookup"><span data-stu-id="6e8ec-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)