---
title: Enterprise-API's facturering aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 017cecc57ad6bdeb402b5d9d57fc95df9b033a42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-reporting-apis-for-enterprise-customers"></a><span data-ttu-id="2beea-103">Overzicht van de rapportage-API's voor Enterprise-klanten</span><span class="sxs-lookup"><span data-stu-id="2beea-103">Overview of Reporting APIs for Enterprise customers</span></span>
<span data-ttu-id="2beea-104">Hallo rapportage-API's kunnen Azure Enterprise-klanten tooprogrammatically pull gebruiks- en factureringsgegevens in de gewenste hulpprogramma's voor gegevensanalyse.</span><span class="sxs-lookup"><span data-stu-id="2beea-104">hello Reporting APIs enable Enterprise Azure customers tooprogrammatically pull consumption and billing data into preferred data analysis tools.</span></span> 

## <a name="enabling-data-access-toohello-api"></a><span data-ttu-id="2beea-105">Data access-toohello API inschakelen</span><span class="sxs-lookup"><span data-stu-id="2beea-105">Enabling data access toohello API</span></span>
* <span data-ttu-id="2beea-106">**Genereren of Hallo API-sleutel ophalen** - logboek in toohello Enterprise portal en volg Hallo zelfstudie onder Help - rapportage-API's.</span><span class="sxs-lookup"><span data-stu-id="2beea-106">**Generate or retrieve hello API key** - Log in toohello Enterprise portal and follow hello tutorial under Help - Reporting APIs.</span></span> <span data-ttu-id="2beea-107">de eerste sectie Hallo onder deze help-artikel wordt uitgelegd hoe toogenerate of ophalen Hallo API-sleutel voor Hallo inschrijving opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2beea-107">hello first section under this help article explains how toogenerate or retrieve hello API key for hello specified enrollment.</span></span>
* <span data-ttu-id="2beea-108">**Sleutels doorgeven in een Hallo API** -Hallo API-sleutel moet toobe doorgegeven voor elke aanroep voor verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="2beea-108">**Passing keys in hello API** - hello API key needs toobe passed for each call for Authentication and Authorization.</span></span> <span data-ttu-id="2beea-109">Hallo volgende-eigenschap moet toobe toohello HTTP-headers</span><span class="sxs-lookup"><span data-stu-id="2beea-109">hello following property needs toobe toohello HTTP headers</span></span>

|<span data-ttu-id="2beea-110">Aanvraag-Header-sleutel</span><span class="sxs-lookup"><span data-stu-id="2beea-110">Request Header Key</span></span> | <span data-ttu-id="2beea-111">Waarde</span><span class="sxs-lookup"><span data-stu-id="2beea-111">Value</span></span>|
|-|-|
|<span data-ttu-id="2beea-112">Autorisatie</span><span class="sxs-lookup"><span data-stu-id="2beea-112">Authorization</span></span>| <span data-ttu-id="2beea-113">Hallo-waarde opgeven die in deze indeling: **bearer {API_KEY}**</span><span class="sxs-lookup"><span data-stu-id="2beea-113">Specify hello value in this format: **bearer {API_KEY}**</span></span> <br/> <span data-ttu-id="2beea-114">Voorbeeld: bearer eyr... 09</span><span class="sxs-lookup"><span data-stu-id="2beea-114">Example: bearer eyr....09</span></span>|

## <a name="consumption-apis"></a><span data-ttu-id="2beea-115">Verbruik API 's</span><span class="sxs-lookup"><span data-stu-id="2beea-115">Consumption APIs</span></span>
<span data-ttu-id="2beea-116">Een Swagger-eindpunt is beschikbaar [hier](https://consumption.azure.com/swagger/ui/index) voor Hallo API's die zijn beschreven hieronder moet eenvoudig introspection van Hallo API en Hallo mogelijkheid toogenerate client-SDK's inschakelen met behulp van [AutoRest](https://github.com/Azure/AutoRest) of [ Swagger codegen gebruikt](http://swagger.io/swagger-codegen/).</span><span class="sxs-lookup"><span data-stu-id="2beea-116">A Swagger endpoint is available [here](https://consumption.azure.com/swagger/ui/index) for hello APIs described below which should enable easy introspection of hello API and hello ability toogenerate client SDKs using [AutoRest](https://github.com/Azure/AutoRest) or [Swagger CodeGen](http://swagger.io/swagger-codegen/).</span></span> <span data-ttu-id="2beea-117">Gegevens vanaf 1 mei 2014 is beschikbaar via deze API.</span><span class="sxs-lookup"><span data-stu-id="2beea-117">Data beginning May 1, 2014 is available through this API.</span></span> 

* <span data-ttu-id="2beea-118">**Saldo en samenvatting** - hello [saldo en samenvatting API](billing-enterprise-api-balance-summary.md) biedt een maandelijkse samenvatting van gegevens op tegoeden, nieuwe aankopen, kosten voor Azure Marketplace, correcties en overschrijding kosten.</span><span class="sxs-lookup"><span data-stu-id="2beea-118">**Balance and Summary** - hello [Balance and Summary API](billing-enterprise-api-balance-summary.md) offers a monthly summary of information on balances, new purchases, Azure Marketplace service charges, adjustments and overage charges.</span></span>

* <span data-ttu-id="2beea-119">**Informatie over het gebruik** - hello [gebruik Detail API](billing-enterprise-api-usage-detail.md) per dag opgesplitst verbruikte aantallen en de geschatte kosten door een inschrijving biedt.</span><span class="sxs-lookup"><span data-stu-id="2beea-119">**Usage Details** - hello [Usage Detail API](billing-enterprise-api-usage-detail.md) offers a daily breakdown of consumed quantities and estimated charges by an Enrollment.</span></span> <span data-ttu-id="2beea-120">Hallo resultaat bevat ook informatie over exemplaren, meters en afdelingen.</span><span class="sxs-lookup"><span data-stu-id="2beea-120">hello result also includes information on instances, meters and departments.</span></span> <span data-ttu-id="2beea-121">Hallo API kan worden doorzocht door facturering periode of door een opgegeven begin- en einddatum.</span><span class="sxs-lookup"><span data-stu-id="2beea-121">hello API can be queried by Billing period or by a specified start and end date.</span></span> 

* <span data-ttu-id="2beea-122">**Marketplace Store kosten** - hello [Marketplace Store kosten API](billing-enterprise-api-marketplace-storecharge.md) retourneert Hallo op gebruik gebaseerde marketplace-kosten uitsplitsing per dag voor Hallo opgegeven facturering periode of begin- en einddatums (één keer kosten zijn niet opgenomen) .</span><span class="sxs-lookup"><span data-stu-id="2beea-122">**Marketplace Store Charge** - hello [Marketplace Store Charge API](billing-enterprise-api-marketplace-storecharge.md) returns hello usage-based marketplace charges breakdown by day for hello specified Billing Period or start and end dates (one time fees are not included).</span></span>

* <span data-ttu-id="2beea-123">**Prijslijst** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) Hallo toepasselijke frequentie voor elke Meter voor registratie en facturering periode Hallo biedt.</span><span class="sxs-lookup"><span data-stu-id="2beea-123">**Price Sheet** - hello [Price Sheet API](billing-enterprise-api-pricesheet.md) provides hello applicable rate for each Meter for hello given Enrollment and Billing Period.</span></span> 

## <a name="helper-apis"></a><span data-ttu-id="2beea-124">Helper-API 's</span><span class="sxs-lookup"><span data-stu-id="2beea-124">Helper APIs</span></span>
 <span data-ttu-id="2beea-125">**Lijst van facturering perioden** - hello [facturering perioden API](billing-enterprise-api-billing-periods.md) retourneert een lijst met facturering perioden die gegevens over het verbruik voor Hallo inschrijving in omgekeerde volgorde opgegeven hebben.</span><span class="sxs-lookup"><span data-stu-id="2beea-125">**List Billing Periods** - hello [Billing Periods API](billing-enterprise-api-billing-periods.md) returns a list of billing periods that have consumption data for hello specified Enrollment in reverse chronological order.</span></span> <span data-ttu-id="2beea-126">Elke categorie bevat een eigenschap toohello API route voor Hallo vier gegevenssets - BalanceSummary, UsageDetails Marketplace-kosten en prijslijst aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="2beea-126">Each Period contains a property pointing toohello API route for hello four sets of data - BalanceSummary, UsageDetails, Marketplace Charges, and Price Sheet.</span></span>


## <a name="api-response-codes"></a><span data-ttu-id="2beea-127">API-reactiecodes</span><span class="sxs-lookup"><span data-stu-id="2beea-127">API Response Codes</span></span>  
|<span data-ttu-id="2beea-128">Statuscode van antwoord</span><span class="sxs-lookup"><span data-stu-id="2beea-128">Response Status Code</span></span>|<span data-ttu-id="2beea-129">Bericht</span><span class="sxs-lookup"><span data-stu-id="2beea-129">Message</span></span>|<span data-ttu-id="2beea-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2beea-130">Description</span></span>|
|-|-|-|
|<span data-ttu-id="2beea-131">200</span><span class="sxs-lookup"><span data-stu-id="2beea-131">200</span></span>| <span data-ttu-id="2beea-132">OK</span><span class="sxs-lookup"><span data-stu-id="2beea-132">OK</span></span>|<span data-ttu-id="2beea-133">Er is geen fout</span><span class="sxs-lookup"><span data-stu-id="2beea-133">No error</span></span>|
|<span data-ttu-id="2beea-134">401</span><span class="sxs-lookup"><span data-stu-id="2beea-134">401</span></span>| <span data-ttu-id="2beea-135">Niet geautoriseerd</span><span class="sxs-lookup"><span data-stu-id="2beea-135">Unauthorized</span></span>| <span data-ttu-id="2beea-136">API-sleutel niet wordt gevonden, ongeldig, verlopen enzovoort.</span><span class="sxs-lookup"><span data-stu-id="2beea-136">API Key not found, Invalid, Expired etc.</span></span>|
|<span data-ttu-id="2beea-137">404</span><span class="sxs-lookup"><span data-stu-id="2beea-137">404</span></span>| <span data-ttu-id="2beea-138">Niet beschikbaar</span><span class="sxs-lookup"><span data-stu-id="2beea-138">Unavailable</span></span>| <span data-ttu-id="2beea-139">Rapport eindpunt is niet gevonden</span><span class="sxs-lookup"><span data-stu-id="2beea-139">Report endpoint not found</span></span>|
|<span data-ttu-id="2beea-140">400</span><span class="sxs-lookup"><span data-stu-id="2beea-140">400</span></span>| <span data-ttu-id="2beea-141">Onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="2beea-141">Bad Request</span></span>| <span data-ttu-id="2beea-142">Ongeldige parameters: datumbereiken, EA nummers, enz.</span><span class="sxs-lookup"><span data-stu-id="2beea-142">Invalid params – Date ranges, EA numbers etc.</span></span>|
|<span data-ttu-id="2beea-143">500</span><span class="sxs-lookup"><span data-stu-id="2beea-143">500</span></span>| <span data-ttu-id="2beea-144">Server-fout</span><span class="sxs-lookup"><span data-stu-id="2beea-144">Server Error</span></span>| <span data-ttu-id="2beea-145">Fout bij verwerking van aanvraag Unexoected</span><span class="sxs-lookup"><span data-stu-id="2beea-145">Unexoected error processing request</span></span>| 









