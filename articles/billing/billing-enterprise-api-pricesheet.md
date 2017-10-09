---
title: aaaAzure facturering Enterprise-API's - prijslijst | Microsoft Docs
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
ms.openlocfilehash: 4cfe694c63fba266d117054b046d9caacb3b7197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---price-sheet"></a><span data-ttu-id="4d443-103">Rapportage-API's voor Enterprise-klanten - prijslijst</span><span class="sxs-lookup"><span data-stu-id="4d443-103">Reporting APIs for Enterprise customers - Price Sheet</span></span>

<span data-ttu-id="4d443-104">Hallo Price Sheet API biedt Hallo toepasselijke frequentie voor elke Meter voor Hallo opgegeven registratie en facturering periode.</span><span class="sxs-lookup"><span data-stu-id="4d443-104">hello Price Sheet API provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span>

##<a name="request"></a><span data-ttu-id="4d443-105">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="4d443-105">Request</span></span>
<span data-ttu-id="4d443-106">Algemene Kopteksteigenschappen voor die toobe toegevoegd moeten zijn opgegeven [hier](billing-enterprise-api.md).</span><span class="sxs-lookup"><span data-stu-id="4d443-106">Common header properties that need toobe added are specified [here](billing-enterprise-api.md).</span></span> <span data-ttu-id="4d443-107">Als een factureringsperiode niet is opgegeven, klikt u vervolgens gegevens voor de huidige facturering Hallo periode geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4d443-107">If a billing period is not specified, then data for hello current billing period is returned.</span></span>

|<span data-ttu-id="4d443-108">Methode</span><span class="sxs-lookup"><span data-stu-id="4d443-108">Method</span></span> | <span data-ttu-id="4d443-109">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="4d443-109">Request URI</span></span>|
|-|-|
|<span data-ttu-id="4d443-110">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="4d443-110">GET</span></span>|<span data-ttu-id="4d443-111">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} / prijslijst</span><span class="sxs-lookup"><span data-stu-id="4d443-111">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/pricesheet</span></span>|
|<span data-ttu-id="4d443-112">TOEVOEGEN</span><span class="sxs-lookup"><span data-stu-id="4d443-112">GET</span></span>|<span data-ttu-id="4d443-113">https://consumption.Azure.com/v2/enrollments/ {enrollmentNumber} /billingPeriods/ {billingPeriod} / prijslijst</span><span class="sxs-lookup"><span data-stu-id="4d443-113">https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/pricesheet</span></span>|

> [!Note]
> <span data-ttu-id="4d443-114">toouse hello preview-versie van de API, v2 vervangen door v1 in Hallo bovenstaande URL.</span><span class="sxs-lookup"><span data-stu-id="4d443-114">toouse hello preview version of API, replace v2 with v1 in hello above URL.</span></span>
>

## <a name="response"></a><span data-ttu-id="4d443-115">Antwoord</span><span class="sxs-lookup"><span data-stu-id="4d443-115">Response</span></span>

    
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
><span data-ttu-id="4d443-116">Als u van Hallo Preview-API gebruikmaakt, is meterId veld niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4d443-116">If you are using hello Preview API, meterId field is not available.</span></span>
>

<span data-ttu-id="4d443-117">**Broneigenschapdefinities antwoord**</span><span class="sxs-lookup"><span data-stu-id="4d443-117">**Response property definitions**</span></span>

|<span data-ttu-id="4d443-118">De naam van eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d443-118">Property Name</span></span>| <span data-ttu-id="4d443-119">Type</span><span class="sxs-lookup"><span data-stu-id="4d443-119">Type</span></span>| <span data-ttu-id="4d443-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4d443-120">Description</span></span>
|-|-|-|
|<span data-ttu-id="4d443-121">id</span><span class="sxs-lookup"><span data-stu-id="4d443-121">id</span></span>| <span data-ttu-id="4d443-122">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-122">string</span></span>| <span data-ttu-id="4d443-123">Hallo unieke Id die staat voor een bepaald prijslijst item (meter door periode facturering)</span><span class="sxs-lookup"><span data-stu-id="4d443-123">hello unique Id that represents a particular PriceSheet item (meter by billing period)</span></span>|
|<span data-ttu-id="4d443-124">billingPeriodId</span><span class="sxs-lookup"><span data-stu-id="4d443-124">billingPeriodId</span></span>| <span data-ttu-id="4d443-125">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-125">string</span></span>| <span data-ttu-id="4d443-126">Hallo unieke Id die staat voor een bepaalde periode voor facturering</span><span class="sxs-lookup"><span data-stu-id="4d443-126">hello unique Id that represents a particular Billing period</span></span>|
|<span data-ttu-id="4d443-127">meterId</span><span class="sxs-lookup"><span data-stu-id="4d443-127">meterId</span></span>| <span data-ttu-id="4d443-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-128">string</span></span>| <span data-ttu-id="4d443-129">Hallo-id voor Hallo meter.</span><span class="sxs-lookup"><span data-stu-id="4d443-129">hello identifier for hello meter.</span></span> <span data-ttu-id="4d443-130">Het kan toegewezen toohello gebruik meterId zijn.</span><span class="sxs-lookup"><span data-stu-id="4d443-130">It can be mapped toohello usage meterId.</span></span>|
|<span data-ttu-id="4d443-131">meterName</span><span class="sxs-lookup"><span data-stu-id="4d443-131">meterName</span></span>| <span data-ttu-id="4d443-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-132">string</span></span>| <span data-ttu-id="4d443-133">de naam van de meter Hallo</span><span class="sxs-lookup"><span data-stu-id="4d443-133">hello meter name</span></span>|
|<span data-ttu-id="4d443-134">unitOfMeasure</span><span class="sxs-lookup"><span data-stu-id="4d443-134">unitOfMeasure</span></span>| <span data-ttu-id="4d443-135">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-135">string</span></span>| <span data-ttu-id="4d443-136">Hallo eenheid voor het meten van Hallo-service</span><span class="sxs-lookup"><span data-stu-id="4d443-136">hello Unit of Measure for measuring hello service</span></span>|
|<span data-ttu-id="4d443-137">includedQuantity</span><span class="sxs-lookup"><span data-stu-id="4d443-137">includedQuantity</span></span>| <span data-ttu-id="4d443-138">Decimale</span><span class="sxs-lookup"><span data-stu-id="4d443-138">decimal</span></span>| <span data-ttu-id="4d443-139">Aantal dat is opgenomen</span><span class="sxs-lookup"><span data-stu-id="4d443-139">Quantity that is included</span></span> |
|<span data-ttu-id="4d443-140">partNumber</span><span class="sxs-lookup"><span data-stu-id="4d443-140">partNumber</span></span>| <span data-ttu-id="4d443-141">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-141">string</span></span>| <span data-ttu-id="4d443-142">Hallo-onderdeelnummer Hallo Meter gekoppeld</span><span class="sxs-lookup"><span data-stu-id="4d443-142">hello part number associated with hello Meter</span></span>|
|<span data-ttu-id="4d443-143">prijs per eenheid</span><span class="sxs-lookup"><span data-stu-id="4d443-143">unitPrice</span></span>| <span data-ttu-id="4d443-144">Decimale</span><span class="sxs-lookup"><span data-stu-id="4d443-144">decimal</span></span>| <span data-ttu-id="4d443-145">prijs per eenheid Hallo voor Hallo meter</span><span class="sxs-lookup"><span data-stu-id="4d443-145">hello unit price for hello meter</span></span>|
|<span data-ttu-id="4d443-146">currencyCode</span><span class="sxs-lookup"><span data-stu-id="4d443-146">currencyCode</span></span>| <span data-ttu-id="4d443-147">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4d443-147">string</span></span>| <span data-ttu-id="4d443-148">Hallo-valutacode voor Hallo prijs per eenheid</span><span class="sxs-lookup"><span data-stu-id="4d443-148">hello currency code for hello unitPrice</span></span>|
<br/>
## <a name="see-also"></a><span data-ttu-id="4d443-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4d443-149">See also</span></span>

* [<span data-ttu-id="4d443-150">Facturering perioden API</span><span class="sxs-lookup"><span data-stu-id="4d443-150">Billing Periods API</span></span>](billing-enterprise-api-billing-periods.md)

* [<span data-ttu-id="4d443-151">Gebruik Detail API</span><span class="sxs-lookup"><span data-stu-id="4d443-151">Usage Detail API</span></span>](billing-enterprise-api-usage-detail.md)

* [<span data-ttu-id="4d443-152">Saldo en samenvatting API</span><span class="sxs-lookup"><span data-stu-id="4d443-152">Balance and Summary API</span></span>](billing-enterprise-api-balance-summary.md)

* [<span data-ttu-id="4d443-153">Marketplace Store kosten API</span><span class="sxs-lookup"><span data-stu-id="4d443-153">Marketplace Store Charge API</span></span>](billing-enterprise-api-marketplace-storecharge.md)
