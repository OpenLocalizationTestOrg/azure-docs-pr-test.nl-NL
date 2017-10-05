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
# <a name="reporting-apis-for-enterprise-customers---marketplace-store-charge"></a><span data-ttu-id="90914-103">Rapportage-API's voor Enterprise-klanten - Marketplace Store kosten</span><span class="sxs-lookup"><span data-stu-id="90914-103">Reporting APIs for Enterprise customers - Marketplace Store Charge</span></span>

<span data-ttu-id="90914-104">De Marketplace Store kosten-API retourneert de uitsplitsing op gebruik gebaseerde marketplace-kosten per dag voor de opgegeven periode facturering of de begin- en einddatums (één keer kosten zijn niet opgenomen).</span><span class="sxs-lookup"><span data-stu-id="90914-104">The Marketplace Store Charge API returns the usage-based marketplace charges breakdown by day for the specified Billing Period or start and end dates (one time fees are not included).</span></span>

##<a name="request"></a><span data-ttu-id="90914-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="90914-105">Request</span></span> 
<span data-ttu-id="90914-106">Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="90914-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="90914-107">Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="90914-107">If a billing period is not specified, then data for the current billing period is returned.</span></span> <span data-ttu-id="90914-108">Aangepaste tijdsbereik kunnen worden opgegeven met het begin en einde datumparameters die zich in de indeling JJJJ-MM-dd, is het maximum aantal ondersteunde tijdsbereik 36 maanden.</span><span class="sxs-lookup"><span data-stu-id="90914-108">Custom time ranges can be specified with the start and end date parameters that are in the format yyyy-MM-dd, the maximum supported time range is 36 months.</span></span>  

|<span data-ttu-id="90914-109">Methode</span><span class="sxs-lookup"><span data-stu-id="90914-109">Method</span></span> | <span data-ttu-id="90914-110">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="90914-110">Request URI</span></span>|
|-|-|
|<span data-ttu-id="90914-111">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="90914-111">GET</span></span>|<span data-ttu-id="90914-112">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="90914-112">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacecharges</span></span>|
|<span data-ttu-id="90914-113">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="90914-113">GET</span></span>|<span data-ttu-id="90914-114">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / marketplacecharges</span><span class="sxs-lookup"><span data-stu-id="90914-114">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/marketplacecharges</span></span>|
|<span data-ttu-id="90914-115">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="90914-115">GET</span></span>|<span data-ttu-id="90914-116">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / marketplacechargesbycustomdate? startTime = 01-01-2017 & endTime = 2017-01-10</span><span class="sxs-lookup"><span data-stu-id="90914-116">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/marketplacechargesbycustomdate?startTime=2017-01-01&endTime=2017-01-10</span></span>|

> [!Note]
> <span data-ttu-id="90914-117">Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.</span><span class="sxs-lookup"><span data-stu-id="90914-117">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="90914-118">Antwoord</span><span class="sxs-lookup"><span data-stu-id="90914-118">Response</span></span>
 
    
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
    

<span data-ttu-id="90914-119">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="90914-119">**Response property definitions**</span></span>

|<span data-ttu-id="90914-120">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="90914-120">Property Name</span></span>| <span data-ttu-id="90914-121">Type</span><span class="sxs-lookup"><span data-stu-id="90914-121">Type</span></span>| <span data-ttu-id="90914-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="90914-122">Description</span></span>
|-|-|-|
|<span data-ttu-id="90914-123">id</span><span class="sxs-lookup"><span data-stu-id="90914-123">id</span></span>|<span data-ttu-id="90914-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-124">string</span></span>|<span data-ttu-id="90914-125">Unieke Id voor de marketplace-kosten-item</span><span class="sxs-lookup"><span data-stu-id="90914-125">Unique Id for the marketplace charge item</span></span>|
|<span data-ttu-id="90914-126">subscriptionGuid</span><span class="sxs-lookup"><span data-stu-id="90914-126">subscriptionGuid</span></span>|<span data-ttu-id="90914-127">GUID</span><span class="sxs-lookup"><span data-stu-id="90914-127">Guid</span></span>|<span data-ttu-id="90914-128">De abonnement-Guid</span><span class="sxs-lookup"><span data-stu-id="90914-128">The Subscription Guid</span></span>|
|<span data-ttu-id="90914-129">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="90914-129">subscriptionName</span></span>|<span data-ttu-id="90914-130">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-130">string</span></span>|<span data-ttu-id="90914-131">Naam van het abonnement</span><span class="sxs-lookup"><span data-stu-id="90914-131">The Subscription Name</span></span>|
|<span data-ttu-id="90914-132">meterId</span><span class="sxs-lookup"><span data-stu-id="90914-132">meterId</span></span>|<span data-ttu-id="90914-133">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-133">string</span></span>|<span data-ttu-id="90914-134">ID voor de Meter verzonden</span><span class="sxs-lookup"><span data-stu-id="90914-134">Id for the emitted Meter</span></span>|
|<span data-ttu-id="90914-135">usageStartDate</span><span class="sxs-lookup"><span data-stu-id="90914-135">usageStartDate</span></span>|<span data-ttu-id="90914-136">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="90914-136">DateTime</span></span>|<span data-ttu-id="90914-137">De begintijd voor de record gebruik</span><span class="sxs-lookup"><span data-stu-id="90914-137">Start time for the usage record</span></span>|
|<span data-ttu-id="90914-138">usageEndDate</span><span class="sxs-lookup"><span data-stu-id="90914-138">usageEndDate</span></span>|<span data-ttu-id="90914-139">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="90914-139">DateTime</span></span>|<span data-ttu-id="90914-140">De eindtijd voor de record gebruik</span><span class="sxs-lookup"><span data-stu-id="90914-140">End time for the usage record</span></span>|
|<span data-ttu-id="90914-141">offerName</span><span class="sxs-lookup"><span data-stu-id="90914-141">offerName</span></span>|<span data-ttu-id="90914-142">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-142">string</span></span>|<span data-ttu-id="90914-143">De naam van de aanbieding</span><span class="sxs-lookup"><span data-stu-id="90914-143">The Offer name</span></span>|
|<span data-ttu-id="90914-144">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="90914-144">resourceGroup</span></span>|<span data-ttu-id="90914-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-145">string</span></span>|<span data-ttu-id="90914-146">De resource-groep</span><span class="sxs-lookup"><span data-stu-id="90914-146">The resource Group</span></span>|
|<span data-ttu-id="90914-147">Exemplaar-id</span><span class="sxs-lookup"><span data-stu-id="90914-147">instanceId</span></span>|<span data-ttu-id="90914-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-148">string</span></span>|<span data-ttu-id="90914-149">Exemplaar-Id</span><span class="sxs-lookup"><span data-stu-id="90914-149">Instance Id</span></span>|
|<span data-ttu-id="90914-150">aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="90914-150">additionalInfo</span></span>|<span data-ttu-id="90914-151">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-151">string</span></span>|<span data-ttu-id="90914-152">Aanvullende informatie JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-152">Additional info JSON string</span></span>|
|<span data-ttu-id="90914-153">tags</span><span class="sxs-lookup"><span data-stu-id="90914-153">tags</span></span>|<span data-ttu-id="90914-154">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-154">string</span></span>|<span data-ttu-id="90914-155">Tag JSON-tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-155">Tag JSON string</span></span>|
|<span data-ttu-id="90914-156">orderNumber</span><span class="sxs-lookup"><span data-stu-id="90914-156">orderNumber</span></span>|<span data-ttu-id="90914-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-157">string</span></span>|<span data-ttu-id="90914-158">Het nummer van de</span><span class="sxs-lookup"><span data-stu-id="90914-158">The order number</span></span>|
|<span data-ttu-id="90914-159">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="90914-159">unitOfMeasure</span></span>|<span data-ttu-id="90914-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-160">string</span></span>|<span data-ttu-id="90914-161">Eenheid voor de meter</span><span class="sxs-lookup"><span data-stu-id="90914-161">Unit of measure for the meter</span></span>|
|<span data-ttu-id="90914-162">CostCenter</span><span class="sxs-lookup"><span data-stu-id="90914-162">costCenter</span></span>|<span data-ttu-id="90914-163">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-163">string</span></span>|<span data-ttu-id="90914-164">De kostenplaats</span><span class="sxs-lookup"><span data-stu-id="90914-164">The cost center</span></span>|
|<span data-ttu-id="90914-165">accountId</span><span class="sxs-lookup"><span data-stu-id="90914-165">accountId</span></span>|<span data-ttu-id="90914-166">int</span><span class="sxs-lookup"><span data-stu-id="90914-166">int</span></span>|<span data-ttu-id="90914-167">De account-Id</span><span class="sxs-lookup"><span data-stu-id="90914-167">The account Id</span></span>|
|<span data-ttu-id="90914-168">Accountnaam</span><span class="sxs-lookup"><span data-stu-id="90914-168">accountName</span></span>|<span data-ttu-id="90914-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-169">string</span></span> |<span data-ttu-id="90914-170">De accountnaam</span><span class="sxs-lookup"><span data-stu-id="90914-170">The Account Name</span></span>|
|<span data-ttu-id="90914-171">accountOwnerId</span><span class="sxs-lookup"><span data-stu-id="90914-171">accountOwnerId</span></span>|<span data-ttu-id="90914-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-172">string</span></span>|<span data-ttu-id="90914-173">De Account eigenaar-Id</span><span class="sxs-lookup"><span data-stu-id="90914-173">The Account Owner Id</span></span>|
|<span data-ttu-id="90914-174">DepartmentID gemeenschappelijk hebben</span><span class="sxs-lookup"><span data-stu-id="90914-174">departmentId</span></span>|<span data-ttu-id="90914-175">int</span><span class="sxs-lookup"><span data-stu-id="90914-175">int</span></span>|<span data-ttu-id="90914-176">De Id van de afdeling</span><span class="sxs-lookup"><span data-stu-id="90914-176">The department Id</span></span>|
|<span data-ttu-id="90914-177">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="90914-177">departmentName</span></span>|<span data-ttu-id="90914-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-178">string</span></span>|<span data-ttu-id="90914-179">Naam van de afdeling</span><span class="sxs-lookup"><span data-stu-id="90914-179">The department name</span></span>|
|<span data-ttu-id="90914-180">publisherName</span><span class="sxs-lookup"><span data-stu-id="90914-180">publisherName</span></span>|<span data-ttu-id="90914-181">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-181">string</span></span>|<span data-ttu-id="90914-182">Naam van de uitgever</span><span class="sxs-lookup"><span data-stu-id="90914-182">The publisher name</span></span>|
|<span data-ttu-id="90914-183">planName</span><span class="sxs-lookup"><span data-stu-id="90914-183">planName</span></span>|<span data-ttu-id="90914-184">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="90914-184">string</span></span>|<span data-ttu-id="90914-185">Naam van het abonnement</span><span class="sxs-lookup"><span data-stu-id="90914-185">The Plan name</span></span>|
|<span data-ttu-id="90914-186">consumedQuantity</span><span class="sxs-lookup"><span data-stu-id="90914-186">consumedQuantity</span></span>|<span data-ttu-id="90914-187">Decimale</span><span class="sxs-lookup"><span data-stu-id="90914-187">decimal</span></span>|<span data-ttu-id="90914-188">Verbruikt aantal tijdens deze periode</span><span class="sxs-lookup"><span data-stu-id="90914-188">Consumed Quantity during this time period</span></span>|
|<span data-ttu-id="90914-189">resourceRate</span><span class="sxs-lookup"><span data-stu-id="90914-189">resourceRate</span></span>|<span data-ttu-id="90914-190">Decimale</span><span class="sxs-lookup"><span data-stu-id="90914-190">decimal</span></span>|<span data-ttu-id="90914-191">Prijs per eenheid voor de meter</span><span class="sxs-lookup"><span data-stu-id="90914-191">Unit price for the meter</span></span>|
|<span data-ttu-id="90914-192">extendedCost</span><span class="sxs-lookup"><span data-stu-id="90914-192">extendedCost</span></span>|<span data-ttu-id="90914-193">Decimale</span><span class="sxs-lookup"><span data-stu-id="90914-193">decimal</span></span>|<span data-ttu-id="90914-194">Geschatte kosten op basis van de hoeveelheid verbruikte en Extended kosten</span><span class="sxs-lookup"><span data-stu-id="90914-194">Estimated charge based on Consumed Quantity and Extended cost</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="90914-195">Zie ook</span><span class="sxs-lookup"><span data-stu-id="90914-195">See also</span></span>

* [<span data-ttu-id="90914-196">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="90914-196">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="90914-197">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="90914-197">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md) 

* [<span data-ttu-id="90914-198">Saldo en samenvatting API</span><span class="sxs-lookup"><span data-stu-id="90914-198">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="90914-199">Prijs blad API</span><span class="sxs-lookup"><span data-stu-id="90914-199">Price Sheet API</span></span>](billing-enterprise-api-pricesheet.md)