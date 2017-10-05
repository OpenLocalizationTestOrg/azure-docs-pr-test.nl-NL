---
title: Azure API's van Enterprise - prijslijst facturering | Microsoft Docs
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
ms.openlocfilehash: 2e7d6e883abe4cee13bc5f684baf2a1ea9c6c397
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="ba26e-103">Rapportage-API's voor Enterprise-klanten - prijslijst</span><span class="sxs-lookup"><span data-stu-id="ba26e-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="ba26e-104">De prijs blad API biedt het tarief voor elke meten voor de opgegeven registratie en facturering periode.</span><span class="sxs-lookup"><span data-stu-id="ba26e-104">The Price Sheet API provides the applicable rate for each Meter for the given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="ba26e-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="ba26e-105">Request</span></span>
<span data-ttu-id="ba26e-106">Algemene Kopteksteigenschappen voor die moeten worden toegevoegd, zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="ba26e-106">Common header properties that need to be added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="ba26e-107">Als een factureringsperiode niet is opgegeven, wordt de gegevens voor de huidige factureringsperiode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ba26e-107">If a billing period is not specified, then data for the current billing period is returned.</span></span>

|<span data-ttu-id="ba26e-108">Methode</span><span class="sxs-lookup"><span data-stu-id="ba26e-108">Method</span></span> | <span data-ttu-id="ba26e-109">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="ba26e-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="ba26e-110">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="ba26e-110">GET</span></span>|<span data-ttu-id="ba26e-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / prijslijst</span><span class="sxs-lookup"><span data-stu-id="ba26e-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="ba26e-112">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="ba26e-112">GET</span></span>|<span data-ttu-id="ba26e-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / prijslijst</span><span class="sxs-lookup"><span data-stu-id="ba26e-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="ba26e-114">Voor het gebruik van de preview-versie van de API v1 in de bovenstaande URL vervangen v2.</span><span class="sxs-lookup"><span data-stu-id="ba26e-114">To use the preview version of API, replace v2 with v1 in the above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="ba26e-115">Antwoord</span><span class="sxs-lookup"><span data-stu-id="ba26e-115">Response</span></span>

    
        [
            {
                "id": "enrollments/57354989/billingperiods/201601/products/343/pricesheets",
                "billingPeriodId": "201704",
                "meterId": "dc210ecb-97e8-4522-8134-2385494233c0",
                "meterName": "A1 VM",
                "unitOfMeasure": "100 Hours",
                "includedQuantity": 0,
                "partNumber": "N7H-00015",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            {
                "id": "enrollments/57354989/billingperiods/201601/products/2884/pricesheets",
                "billingPeriodId": "201404",
                "meterId": "dc210ecb-97e8-4522-8134-5385494233c0",
                "meterName": "Locally Redundant Storage Premium Storage - Snapshots - AU East",
                "unitOfMeasure": "100 GB",
                "includedQuantity": 0,
                "partNumber": "N9H-00402",
                "unitPrice": 0.00,
                "currencyCode": "USD"
            },
            ...
        ]
    

> [!Note]
><span data-ttu-id="ba26e-116">Als u de Preview-API gebruikt, is meterId veld niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="ba26e-116">If you are using the Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="ba26e-117">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="ba26e-117">**Response property definitions**</span></span>

|<span data-ttu-id="ba26e-118">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="ba26e-118">Property Name</span></span>| <span data-ttu-id="ba26e-119">Type</span><span class="sxs-lookup"><span data-stu-id="ba26e-119">Type</span></span>| <span data-ttu-id="ba26e-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ba26e-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="ba26e-121">id</span><span class="sxs-lookup"><span data-stu-id="ba26e-121">id</span></span>| <span data-ttu-id="ba26e-122">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-122">string</span></span>| <span data-ttu-id="ba26e-123">De unieke Id die staat voor een bepaald prijslijst item (meter door periode facturering)</span><span class="sxs-lookup"><span data-stu-id="ba26e-123">The unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="ba26e-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="ba26e-124">billingPeriodId</span></span>| <span data-ttu-id="ba26e-125">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-125">string</span></span>| <span data-ttu-id="ba26e-126">De unieke Id die staat voor een bepaalde periode voor facturering</span><span class="sxs-lookup"><span data-stu-id="ba26e-126">The unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="ba26e-127">meterId</span><span class="sxs-lookup"><span data-stu-id="ba26e-127">meterId</span></span>| <span data-ttu-id="ba26e-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-128">string</span></span>| <span data-ttu-id="ba26e-129">De id voor de meter.</span><span class="sxs-lookup"><span data-stu-id="ba26e-129">The identifier for the meter.</span></span> <span data-ttu-id="ba26e-130">Deze kan worden toegewezen aan de meterId informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="ba26e-130">It can be mapped to the usage meterId.</span></span>|
|<span data-ttu-id="ba26e-131">meterName</span><span class="sxs-lookup"><span data-stu-id="ba26e-131">meterName</span></span>| <span data-ttu-id="ba26e-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-132">string</span></span>| <span data-ttu-id="ba26e-133">De naam van de meter</span><span class="sxs-lookup"><span data-stu-id="ba26e-133">The meter name</span></span>|
|<span data-ttu-id="ba26e-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="ba26e-134">unitOfMeasure</span></span>| <span data-ttu-id="ba26e-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-135">string</span></span>| <span data-ttu-id="ba26e-136">De eenheid voor het meten van de service</span><span class="sxs-lookup"><span data-stu-id="ba26e-136">The Unit of Measure for measuring the service</span></span>|
|<span data-ttu-id="ba26e-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="ba26e-137">includedQuantity</span></span>| <span data-ttu-id="ba26e-138">Decimale</span><span class="sxs-lookup"><span data-stu-id="ba26e-138">decimal</span></span>| <span data-ttu-id="ba26e-139">Aantal dat is opgenomen</span><span class="sxs-lookup"><span data-stu-id="ba26e-139">Quantity that is included</span></span> |
|<span data-ttu-id="ba26e-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="ba26e-140">partNumber</span></span>| <span data-ttu-id="ba26e-141">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-141">string</span></span>| <span data-ttu-id="ba26e-142">Het onderdeelnummer die zijn gekoppeld aan de Meter</span><span class="sxs-lookup"><span data-stu-id="ba26e-142">The part number associated with the Meter</span></span>|
|<span data-ttu-id="ba26e-143">prijs per eenheid</span><span class="sxs-lookup"><span data-stu-id="ba26e-143">unitPrice</span></span>| <span data-ttu-id="ba26e-144">Decimale</span><span class="sxs-lookup"><span data-stu-id="ba26e-144">decimal</span></span>| <span data-ttu-id="ba26e-145">De prijs per eenheid voor de meter</span><span class="sxs-lookup"><span data-stu-id="ba26e-145">The unit price for the meter</span></span>|
|<span data-ttu-id="ba26e-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="ba26e-146">currencyCode</span></span>| <span data-ttu-id="ba26e-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ba26e-147">string</span></span>| <span data-ttu-id="ba26e-148">De valutacode voor de prijs per eenheid</span><span class="sxs-lookup"><span data-stu-id="ba26e-148">The currency code for the unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="ba26e-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ba26e-149">See also</span></span>

* [<span data-ttu-id="ba26e-150">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="ba26e-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="ba26e-151">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="ba26e-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="ba26e-152">Saldo en samenvatting API</span><span class="sxs-lookup"><span data-stu-id="ba26e-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="ba26e-153">Marketplace Store kosten API</span><span class="sxs-lookup"><span data-stu-id="ba26e-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
