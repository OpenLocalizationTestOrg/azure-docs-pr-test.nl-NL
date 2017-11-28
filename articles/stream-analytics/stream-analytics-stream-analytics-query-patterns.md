---
title: Voorbeelden van aaaQuery voor algemene gebruikspatronen in Stream Analytics | Microsoft Docs
description: Algemene Azure Stream Analytics-querypatronen
keywords: Query-voorbeelden
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="44fb4-104">Voorbeelden van algemene gebruikspatronen van de Stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="44fb4-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="44fb4-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="44fb4-105">Introduction</span></span>
<span data-ttu-id="44fb4-106">Query's in Azure Stream Analytics worden uitgedrukt in een SQL-achtige querytaal.</span><span class="sxs-lookup"><span data-stu-id="44fb4-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="44fb4-107">Deze query's zijn gedocumenteerd in Hallo [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) handleiding.</span><span class="sxs-lookup"><span data-stu-id="44fb4-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="44fb4-108">Dit artikel overzichten oplossingen tooseveral veelvoorkomende querypatronen, op basis van praktijkscenario's.</span><span class="sxs-lookup"><span data-stu-id="44fb4-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="44fb4-109">Het onderhanden werk en toobe bijgewerkt met nieuwe patronen voortdurend voort te zetten.</span><span class="sxs-lookup"><span data-stu-id="44fb4-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="44fb4-110">Query-voorbeeld: gegevenstypen converteren</span><span class="sxs-lookup"><span data-stu-id="44fb4-110">Query example: Convert data types</span></span>
<span data-ttu-id="44fb4-111">**Beschrijving**: Hallo typen eigenschappen definiëren op Hallo-invoerstroom.</span><span class="sxs-lookup"><span data-stu-id="44fb4-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="44fb4-112">Bijvoorbeeld Hallo auto gewicht afkomstig is van de invoerstroom Hallo als tekenreeksen en toobe te geconverteerd moet**INT** tooperform **som** het.</span><span class="sxs-lookup"><span data-stu-id="44fb4-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="44fb4-113">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-113">**Input**:</span></span>

| <span data-ttu-id="44fb4-114">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-114">Make</span></span> | <span data-ttu-id="44fb4-115">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-115">Time</span></span> | <span data-ttu-id="44fb4-116">Gewicht</span><span class="sxs-lookup"><span data-stu-id="44fb4-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-117">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-117">Honda</span></span> |<span data-ttu-id="44fb4-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="44fb4-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="44fb4-119">"1000"</span></span> |
| <span data-ttu-id="44fb4-120">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-120">Honda</span></span> |<span data-ttu-id="44fb4-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="44fb4-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="44fb4-122">"2000"</span></span> |

<span data-ttu-id="44fb4-123">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-123">**Output**:</span></span>

| <span data-ttu-id="44fb4-124">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-124">Make</span></span> | <span data-ttu-id="44fb4-125">Gewicht</span><span class="sxs-lookup"><span data-stu-id="44fb4-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-126">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-126">Honda</span></span> |<span data-ttu-id="44fb4-127">3000</span><span class="sxs-lookup"><span data-stu-id="44fb4-127">3000</span></span> |

<span data-ttu-id="44fb4-128">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="44fb4-129">**Uitleg**: gebruik een **CAST** -instructie in Hallo **gewicht** veld toospecify het gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="44fb4-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="44fb4-130">Hallo-overzicht van ondersteunde gegevenstypen in [gegevenstypen (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="44fb4-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="44fb4-131">Query-voorbeeld: gebruik achtige/niet zoals toodo jokertekens</span><span class="sxs-lookup"><span data-stu-id="44fb4-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="44fb4-132">**Beschrijving**: controleert of de waarde van een veld op Hallo gebeurtenis overeenkomt met een bepaald patroon.</span><span class="sxs-lookup"><span data-stu-id="44fb4-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="44fb4-133">Controleer bijvoorbeeld of Hallo resultaat overschrijven die beginnen met A en eindigen met 9.</span><span class="sxs-lookup"><span data-stu-id="44fb4-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="44fb4-134">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-134">**Input**:</span></span>

| <span data-ttu-id="44fb4-135">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-135">Make</span></span> | <span data-ttu-id="44fb4-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-136">LicensePlate</span></span> | <span data-ttu-id="44fb4-137">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-138">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-138">Honda</span></span> |<span data-ttu-id="44fb4-139">ABC 123</span><span class="sxs-lookup"><span data-stu-id="44fb4-139">ABC-123</span></span> |<span data-ttu-id="44fb4-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-141">Toyota</span></span> |<span data-ttu-id="44fb4-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="44fb4-142">AAA-999</span></span> |<span data-ttu-id="44fb4-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="44fb4-144">Nissan</span></span> |<span data-ttu-id="44fb4-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="44fb4-145">ABC-369</span></span> |<span data-ttu-id="44fb4-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-147">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-147">**Output**:</span></span>

| <span data-ttu-id="44fb4-148">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-148">Make</span></span> | <span data-ttu-id="44fb4-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-149">LicensePlate</span></span> | <span data-ttu-id="44fb4-150">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-151">Toyota</span></span> |<span data-ttu-id="44fb4-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="44fb4-152">AAA-999</span></span> |<span data-ttu-id="44fb4-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="44fb4-154">Nissan</span></span> |<span data-ttu-id="44fb4-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="44fb4-155">ABC-369</span></span> |<span data-ttu-id="44fb4-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-157">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="44fb4-158">**Uitleg**: gebruik Hallo **zoals** instructie toocheck hello **LicensePlate** veld waarde.</span><span class="sxs-lookup"><span data-stu-id="44fb4-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="44fb4-159">Deze moet beginnen met een A, en vervolgens hebt een willekeurige tekenreeks van nul of meer tekens en vervolgens eindigen met een 9.</span><span class="sxs-lookup"><span data-stu-id="44fb4-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="44fb4-160">Query-voorbeeld: Geef de logica voor andere gevallen en-waarden (CASE-instructies)</span><span class="sxs-lookup"><span data-stu-id="44fb4-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="44fb4-161">**Beschrijving**: Geef een andere berekeningen voor het veld, op basis van een bepaald criterium.</span><span class="sxs-lookup"><span data-stu-id="44fb4-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="44fb4-162">Bijvoorbeeld: Geef een beschrijving van de tekenreeks voor het aantal auto's Hallo dezelfde maken is voltooid met een speciaal geval voor 1.</span><span class="sxs-lookup"><span data-stu-id="44fb4-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="44fb4-163">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-163">**Input**:</span></span>

| <span data-ttu-id="44fb4-164">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-164">Make</span></span> | <span data-ttu-id="44fb4-165">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-166">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-166">Honda</span></span> |<span data-ttu-id="44fb4-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-168">Toyota</span></span> |<span data-ttu-id="44fb4-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-170">Toyota</span></span> |<span data-ttu-id="44fb4-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-172">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-172">**Output**:</span></span>

| <span data-ttu-id="44fb4-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="44fb4-173">CarsPassed</span></span> | <span data-ttu-id="44fb4-174">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-175">1 Honda</span></span> |<span data-ttu-id="44fb4-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="44fb4-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="44fb4-177">2 Toyotas</span></span> |<span data-ttu-id="44fb4-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="44fb4-179">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-179">**Solution**:</span></span>

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="44fb4-180">**Uitleg**: Hallo **geval** component, kunnen wij tooprovide een andere berekening op basis van bepaalde criteria (in ons geval Hallo aantal Hallo auto's in Hallo statistische vensterfunctie).</span><span class="sxs-lookup"><span data-stu-id="44fb4-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="44fb4-181">Query-voorbeeld: verzenden gegevens toomultiple levert</span><span class="sxs-lookup"><span data-stu-id="44fb4-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="44fb4-182">**Beschrijving**: verzenden gegevens toomultiple uitvoer doelen van één taak.</span><span class="sxs-lookup"><span data-stu-id="44fb4-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="44fb4-183">Bijvoorbeeld, analyseren van gegevens voor een waarschuwing op basis van drempelwaarden en alle gebeurtenissen tooblob opslag te archiveren.</span><span class="sxs-lookup"><span data-stu-id="44fb4-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="44fb4-184">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-184">**Input**:</span></span>

| <span data-ttu-id="44fb4-185">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-185">Make</span></span> | <span data-ttu-id="44fb4-186">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-187">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-187">Honda</span></span> |<span data-ttu-id="44fb4-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-189">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-189">Honda</span></span> |<span data-ttu-id="44fb4-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-191">Toyota</span></span> |<span data-ttu-id="44fb4-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-193">Toyota</span></span> |<span data-ttu-id="44fb4-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-195">Toyota</span></span> |<span data-ttu-id="44fb4-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-197">**Output1**:</span></span>

| <span data-ttu-id="44fb4-198">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-198">Make</span></span> | <span data-ttu-id="44fb4-199">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-200">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-200">Honda</span></span> |<span data-ttu-id="44fb4-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-202">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-202">Honda</span></span> |<span data-ttu-id="44fb4-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-204">Toyota</span></span> |<span data-ttu-id="44fb4-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-206">Toyota</span></span> |<span data-ttu-id="44fb4-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-208">Toyota</span></span> |<span data-ttu-id="44fb4-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-210">**Output2**:</span></span>

| <span data-ttu-id="44fb4-211">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-211">Make</span></span> | <span data-ttu-id="44fb4-212">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-212">Time</span></span> | <span data-ttu-id="44fb4-213">Count</span><span class="sxs-lookup"><span data-stu-id="44fb4-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-214">Toyota</span></span> |<span data-ttu-id="44fb4-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="44fb4-216">3</span><span class="sxs-lookup"><span data-stu-id="44fb4-216">3</span></span> |

<span data-ttu-id="44fb4-217">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-217">**Solution**:</span></span>

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

<span data-ttu-id="44fb4-218">**Uitleg**: Hallo **INTO** component vertelt Stream Analytics die Hallo toowrite Hallo gegevens toofrom levert deze instructie.</span><span class="sxs-lookup"><span data-stu-id="44fb4-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="44fb4-219">is het doorgeven van Hallo gegevens ontvangen tooan uitvoer die we met de naam van eerste query Hallo **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="44fb4-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="44fb4-220">Hallo tweede query biedt een aantal eenvoudige aggregatie en filteren en het verzendt Hallo resultaten tooa downstream waarschuwingsmethoden systeem.</span><span class="sxs-lookup"><span data-stu-id="44fb4-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="44fb4-221">Opmerking u kunt ook opnieuw gebruiken Hallo resultaten van algemene tabelexpressies hello (CTE's) (zoals **WITH** instructies) in meerdere uitvoer-instructies.</span><span class="sxs-lookup"><span data-stu-id="44fb4-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="44fb4-222">Deze optie heeft Hallo voordeel minder lezers toohello invoerbron te openen.</span><span class="sxs-lookup"><span data-stu-id="44fb4-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="44fb4-223">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="44fb4-223">For example:</span></span> 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a><span data-ttu-id="44fb4-224">Voorbeeld van de query: de unieke waarden tellen</span><span class="sxs-lookup"><span data-stu-id="44fb4-224">Query example: Count unique values</span></span>
<span data-ttu-id="44fb4-225">**Beschrijving**: het getelde aantal unieke waarden die worden weergegeven in de stroom binnen een tijdvenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44fb4-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="44fb4-226">Bijvoorbeeld hoeveel unieke wordt gemaakt van auto's doorgegeven Hallo tolstation stand in een venster 2 seconden?</span><span class="sxs-lookup"><span data-stu-id="44fb4-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="44fb4-227">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-227">**Input**:</span></span>

| <span data-ttu-id="44fb4-228">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-228">Make</span></span> | <span data-ttu-id="44fb4-229">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-230">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-230">Honda</span></span> |<span data-ttu-id="44fb4-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-232">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-232">Honda</span></span> |<span data-ttu-id="44fb4-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-234">Toyota</span></span> |<span data-ttu-id="44fb4-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-236">Toyota</span></span> |<span data-ttu-id="44fb4-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-238">Toyota</span></span> |<span data-ttu-id="44fb4-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="44fb4-240">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="44fb4-240">**Output:**</span></span>

| <span data-ttu-id="44fb4-241">Count</span><span class="sxs-lookup"><span data-stu-id="44fb4-241">Count</span></span> | <span data-ttu-id="44fb4-242">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-243">2</span><span class="sxs-lookup"><span data-stu-id="44fb4-243">2</span></span> |<span data-ttu-id="44fb4-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="44fb4-245">1</span><span class="sxs-lookup"><span data-stu-id="44fb4-245">1</span></span> |<span data-ttu-id="44fb4-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="44fb4-247">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="44fb4-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="44fb4-248">**Uitleg:**
**COUNT (afzonderlijke zorg)** retourneert het aantal afzonderlijke waarden in Hallo Hallo **zorg** kolom binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="44fb4-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="44fb4-249">Query-voorbeeld: bepalen of een waarde is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="44fb4-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="44fb4-250">**Beschrijving**: een vorige waarde toodetermine bekijken als deze verschilt van de huidige waarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="44fb4-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="44fb4-251">Is bijvoorbeeld Hallo vorige auto op Hallo tolstation weg Hallo is die dezelfde als de huidige auto Hallo maken?</span><span class="sxs-lookup"><span data-stu-id="44fb4-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="44fb4-252">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-252">**Input**:</span></span>

| <span data-ttu-id="44fb4-253">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-253">Make</span></span> | <span data-ttu-id="44fb4-254">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-255">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-255">Honda</span></span> |<span data-ttu-id="44fb4-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-257">Toyota</span></span> |<span data-ttu-id="44fb4-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="44fb4-259">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-259">**Output**:</span></span>

| <span data-ttu-id="44fb4-260">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-260">Make</span></span> | <span data-ttu-id="44fb4-261">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-262">Toyota</span></span> |<span data-ttu-id="44fb4-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="44fb4-264">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="44fb4-265">**Uitleg**: Gebruik **LAG** toopeek in Hallo invoer weer in één gebeurtenis stroom en Hallo ophalen **zorg** waarde.</span><span class="sxs-lookup"><span data-stu-id="44fb4-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="44fb4-266">Vergelijk deze toohello **zorg** waarde van de huidige gebeurtenis Hallo en uitvoer Hallo gebeurtenis als deze verschillen.</span><span class="sxs-lookup"><span data-stu-id="44fb4-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="44fb4-267">Query-voorbeeld: zoek Hallo eerste gebeurtenis in een venster</span><span class="sxs-lookup"><span data-stu-id="44fb4-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="44fb4-268">**Beschrijving**: zoeken Hallo eerste auto in een interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="44fb4-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="44fb4-269">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-269">**Input**:</span></span>

| <span data-ttu-id="44fb4-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-270">LicensePlate</span></span> | <span data-ttu-id="44fb4-271">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-271">Make</span></span> | <span data-ttu-id="44fb4-272">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="44fb4-273">DXE 5291</span></span> |<span data-ttu-id="44fb4-274">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-274">Honda</span></span> |<span data-ttu-id="44fb4-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="44fb4-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="44fb4-276">YZK 5704</span></span> |<span data-ttu-id="44fb4-277">Ford</span><span class="sxs-lookup"><span data-stu-id="44fb4-277">Ford</span></span> |<span data-ttu-id="44fb4-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="44fb4-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="44fb4-279">RMV 8282</span></span> |<span data-ttu-id="44fb4-280">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-280">Honda</span></span> |<span data-ttu-id="44fb4-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="44fb4-282">YHN 6970</span></span> |<span data-ttu-id="44fb4-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-283">Toyota</span></span> |<span data-ttu-id="44fb4-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="44fb4-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="44fb4-285">VFE 1616</span></span> |<span data-ttu-id="44fb4-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-286">Toyota</span></span> |<span data-ttu-id="44fb4-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="44fb4-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="44fb4-288">QYF 9358</span></span> |<span data-ttu-id="44fb4-289">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-289">Honda</span></span> |<span data-ttu-id="44fb4-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="44fb4-291">MDR 6128</span></span> |<span data-ttu-id="44fb4-292">BMW</span><span class="sxs-lookup"><span data-stu-id="44fb4-292">BMW</span></span> |<span data-ttu-id="44fb4-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="44fb4-294">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-294">**Output**:</span></span>

| <span data-ttu-id="44fb4-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-295">LicensePlate</span></span> | <span data-ttu-id="44fb4-296">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-296">Make</span></span> | <span data-ttu-id="44fb4-297">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="44fb4-298">DXE 5291</span></span> |<span data-ttu-id="44fb4-299">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-299">Honda</span></span> |<span data-ttu-id="44fb4-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="44fb4-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="44fb4-301">QYF 9358</span></span> |<span data-ttu-id="44fb4-302">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-302">Honda</span></span> |<span data-ttu-id="44fb4-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="44fb4-304">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="44fb4-305">Nu gaan we wijziging Hallo probleem en zoeken Hallo eerste auto's van een bepaald interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="44fb4-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="44fb4-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-306">LicensePlate</span></span> | <span data-ttu-id="44fb4-307">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-307">Make</span></span> | <span data-ttu-id="44fb4-308">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="44fb4-309">DXE 5291</span></span> |<span data-ttu-id="44fb4-310">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-310">Honda</span></span> |<span data-ttu-id="44fb4-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="44fb4-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="44fb4-312">YZK 5704</span></span> |<span data-ttu-id="44fb4-313">Ford</span><span class="sxs-lookup"><span data-stu-id="44fb4-313">Ford</span></span> |<span data-ttu-id="44fb4-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="44fb4-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="44fb4-315">YHN 6970</span></span> |<span data-ttu-id="44fb4-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-316">Toyota</span></span> |<span data-ttu-id="44fb4-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="44fb4-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="44fb4-318">QYF 9358</span></span> |<span data-ttu-id="44fb4-319">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-319">Honda</span></span> |<span data-ttu-id="44fb4-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="44fb4-321">MDR 6128</span></span> |<span data-ttu-id="44fb4-322">BMW</span><span class="sxs-lookup"><span data-stu-id="44fb4-322">BMW</span></span> |<span data-ttu-id="44fb4-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="44fb4-324">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="44fb4-325">Query-voorbeeld: zoek Hallo laatste gebeurtenis in een venster</span><span class="sxs-lookup"><span data-stu-id="44fb4-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="44fb4-326">**Beschrijving**: zoeken Hallo laatste auto in een interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="44fb4-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="44fb4-327">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-327">**Input**:</span></span>

| <span data-ttu-id="44fb4-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-328">LicensePlate</span></span> | <span data-ttu-id="44fb4-329">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-329">Make</span></span> | <span data-ttu-id="44fb4-330">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="44fb4-331">DXE 5291</span></span> |<span data-ttu-id="44fb4-332">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-332">Honda</span></span> |<span data-ttu-id="44fb4-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="44fb4-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="44fb4-334">YZK 5704</span></span> |<span data-ttu-id="44fb4-335">Ford</span><span class="sxs-lookup"><span data-stu-id="44fb4-335">Ford</span></span> |<span data-ttu-id="44fb4-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="44fb4-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="44fb4-337">RMV 8282</span></span> |<span data-ttu-id="44fb4-338">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-338">Honda</span></span> |<span data-ttu-id="44fb4-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="44fb4-340">YHN 6970</span></span> |<span data-ttu-id="44fb4-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-341">Toyota</span></span> |<span data-ttu-id="44fb4-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="44fb4-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="44fb4-343">VFE 1616</span></span> |<span data-ttu-id="44fb4-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-344">Toyota</span></span> |<span data-ttu-id="44fb4-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="44fb4-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="44fb4-346">QYF 9358</span></span> |<span data-ttu-id="44fb4-347">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-347">Honda</span></span> |<span data-ttu-id="44fb4-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="44fb4-349">MDR 6128</span></span> |<span data-ttu-id="44fb4-350">BMW</span><span class="sxs-lookup"><span data-stu-id="44fb4-350">BMW</span></span> |<span data-ttu-id="44fb4-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="44fb4-352">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-352">**Output**:</span></span>

| <span data-ttu-id="44fb4-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-353">LicensePlate</span></span> | <span data-ttu-id="44fb4-354">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-354">Make</span></span> | <span data-ttu-id="44fb4-355">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="44fb4-356">VFE 1616</span></span> |<span data-ttu-id="44fb4-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-357">Toyota</span></span> |<span data-ttu-id="44fb4-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="44fb4-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="44fb4-359">MDR 6128</span></span> |<span data-ttu-id="44fb4-360">BMW</span><span class="sxs-lookup"><span data-stu-id="44fb4-360">BMW</span></span> |<span data-ttu-id="44fb4-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="44fb4-362">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-362">**Solution**:</span></span>

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

<span data-ttu-id="44fb4-363">**Uitleg**: Er zijn twee stappen in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="44fb4-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="44fb4-364">Hallo eerste één vindt Hallo nieuwste tijdstempel in windows 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="44fb4-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="44fb4-365">de tweede stap joins Hallo Hallo resultaten van de eerste query Hallo met Hallo oorspronkelijke stroom toofind Hallo gebeurtenissen die overeenkomen met de Hallo laatste tijdstempels in elk venster.</span><span class="sxs-lookup"><span data-stu-id="44fb4-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="44fb4-366">Query-voorbeeld: Hallo afwezigheid van gebeurtenissen detecteren</span><span class="sxs-lookup"><span data-stu-id="44fb4-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="44fb4-367">**Beschrijving**: Controleer of er een stroom geen waarde die overeenkomt met een bepaald criterium.</span><span class="sxs-lookup"><span data-stu-id="44fb4-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="44fb4-368">Bijvoorbeeld 2 opeenvolgende auto's uit dezelfde maken Hallo ingevoerde Hallo tolstation weg op Hallo laatste 90 seconden?</span><span class="sxs-lookup"><span data-stu-id="44fb4-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="44fb4-369">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-369">**Input**:</span></span>

| <span data-ttu-id="44fb4-370">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-370">Make</span></span> | <span data-ttu-id="44fb4-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-371">LicensePlate</span></span> | <span data-ttu-id="44fb4-372">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-373">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-373">Honda</span></span> |<span data-ttu-id="44fb4-374">ABC 123</span><span class="sxs-lookup"><span data-stu-id="44fb4-374">ABC-123</span></span> |<span data-ttu-id="44fb4-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="44fb4-376">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-376">Honda</span></span> |<span data-ttu-id="44fb4-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="44fb4-377">AAA-999</span></span> |<span data-ttu-id="44fb4-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="44fb4-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-379">Toyota</span></span> |<span data-ttu-id="44fb4-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="44fb4-380">DEF-987</span></span> |<span data-ttu-id="44fb4-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="44fb4-382">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-382">Honda</span></span> |<span data-ttu-id="44fb4-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="44fb4-383">GHI-345</span></span> |<span data-ttu-id="44fb4-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="44fb4-385">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-385">**Output**:</span></span>

| <span data-ttu-id="44fb4-386">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-386">Make</span></span> | <span data-ttu-id="44fb4-387">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-387">Time</span></span> | <span data-ttu-id="44fb4-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="44fb4-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="44fb4-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="44fb4-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="44fb4-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="44fb4-391">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-391">Honda</span></span> |<span data-ttu-id="44fb4-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="44fb4-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="44fb4-393">AAA-999</span></span> |<span data-ttu-id="44fb4-394">ABC 123</span><span class="sxs-lookup"><span data-stu-id="44fb4-394">ABC-123</span></span> |<span data-ttu-id="44fb4-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="44fb4-396">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-396">**Solution**:</span></span>

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

<span data-ttu-id="44fb4-397">**Uitleg**: Gebruik **LAG** toopeek in Hallo invoer weer in één gebeurtenis stroom en Hallo ophalen **zorg** waarde.</span><span class="sxs-lookup"><span data-stu-id="44fb4-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="44fb4-398">Vergelijk deze toohello **zorg** waarde in de huidige gebeurtenis Hallo en uitvoer Hallo gebeurtenis als ze zijn dezelfde Hallo.</span><span class="sxs-lookup"><span data-stu-id="44fb4-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="44fb4-399">U kunt ook **LAG** tooget gegevens over Hallo vorige auto.</span><span class="sxs-lookup"><span data-stu-id="44fb4-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="44fb4-400">Query-voorbeeld: Hallo duur tussen gebeurtenissen detecteren</span><span class="sxs-lookup"><span data-stu-id="44fb4-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="44fb4-401">**Beschrijving**: Hallo duur van een bepaalde gebeurtenis vinden.</span><span class="sxs-lookup"><span data-stu-id="44fb4-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="44fb4-402">Bijvoorbeeld een web-clickstream gezien, bepalen Hallo tijd besteed aan een functie.</span><span class="sxs-lookup"><span data-stu-id="44fb4-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="44fb4-403">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-403">**Input**:</span></span>  

| <span data-ttu-id="44fb4-404">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="44fb4-404">User</span></span> | <span data-ttu-id="44fb4-405">Functie</span><span class="sxs-lookup"><span data-stu-id="44fb4-405">Feature</span></span> | <span data-ttu-id="44fb4-406">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="44fb4-406">Event</span></span> | <span data-ttu-id="44fb4-407">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="44fb4-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="44fb4-408">RightMenu</span></span> |<span data-ttu-id="44fb4-409">Starten</span><span class="sxs-lookup"><span data-stu-id="44fb4-409">Start</span></span> |<span data-ttu-id="44fb4-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="44fb4-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="44fb4-411">RightMenu</span></span> |<span data-ttu-id="44fb4-412">Einde</span><span class="sxs-lookup"><span data-stu-id="44fb4-412">End</span></span> |<span data-ttu-id="44fb4-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="44fb4-414">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-414">**Output**:</span></span>  

| <span data-ttu-id="44fb4-415">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="44fb4-415">User</span></span> | <span data-ttu-id="44fb4-416">Functie</span><span class="sxs-lookup"><span data-stu-id="44fb4-416">Feature</span></span> | <span data-ttu-id="44fb4-417">Duur</span><span class="sxs-lookup"><span data-stu-id="44fb4-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="44fb4-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="44fb4-418">RightMenu</span></span> |<span data-ttu-id="44fb4-419">7</span><span class="sxs-lookup"><span data-stu-id="44fb4-419">7</span></span> |

<span data-ttu-id="44fb4-420">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="44fb4-421">**Uitleg**: gebruik Hallo **laatste** tooretrieve Hallo laatste werken **tijd** waarde indien Hallo gebeurtenistype is **Start**.</span><span class="sxs-lookup"><span data-stu-id="44fb4-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="44fb4-422">Hallo **laatste** functie maakt gebruik van **PARTITION BY [gebruiker]** tooindicate die Hallo resultaat wordt berekend per unieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="44fb4-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="44fb4-423">Hallo-query heeft een maximale drempelwaarde 1 uur voor Hallo tijdverschil **Start** en **stoppen** gebeurtenissen, maar is configureerbaar naar behoefte **(LIMIET DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="44fb4-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="44fb4-424">Query-voorbeeld: Hallo duur van een voorwaarde detecteren</span><span class="sxs-lookup"><span data-stu-id="44fb4-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="44fb4-425">**Beschrijving**: vinden out hoe lang een voorwaarde is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="44fb4-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="44fb4-426">Stel dat een fout heeft geresulteerd in alle auto's met een onjuiste gewicht (meer dan 20.000 pond).</span><span class="sxs-lookup"><span data-stu-id="44fb4-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="44fb4-427">We willen toocompute Hallo duur van Hallo-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="44fb4-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="44fb4-428">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-428">**Input**:</span></span>

| <span data-ttu-id="44fb4-429">Maken</span><span class="sxs-lookup"><span data-stu-id="44fb4-429">Make</span></span> | <span data-ttu-id="44fb4-430">Time</span><span class="sxs-lookup"><span data-stu-id="44fb4-430">Time</span></span> | <span data-ttu-id="44fb4-431">Gewicht</span><span class="sxs-lookup"><span data-stu-id="44fb4-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-432">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-432">Honda</span></span> |<span data-ttu-id="44fb4-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="44fb4-434">2000</span><span class="sxs-lookup"><span data-stu-id="44fb4-434">2000</span></span> |
| <span data-ttu-id="44fb4-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-435">Toyota</span></span> |<span data-ttu-id="44fb4-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="44fb4-437">25000</span><span class="sxs-lookup"><span data-stu-id="44fb4-437">25000</span></span> |
| <span data-ttu-id="44fb4-438">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-438">Honda</span></span> |<span data-ttu-id="44fb4-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="44fb4-440">26000</span><span class="sxs-lookup"><span data-stu-id="44fb4-440">26000</span></span> |
| <span data-ttu-id="44fb4-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-441">Toyota</span></span> |<span data-ttu-id="44fb4-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="44fb4-443">25000</span><span class="sxs-lookup"><span data-stu-id="44fb4-443">25000</span></span> |
| <span data-ttu-id="44fb4-444">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-444">Honda</span></span> |<span data-ttu-id="44fb4-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="44fb4-446">26000</span><span class="sxs-lookup"><span data-stu-id="44fb4-446">26000</span></span> |
| <span data-ttu-id="44fb4-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-447">Toyota</span></span> |<span data-ttu-id="44fb4-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="44fb4-449">25000</span><span class="sxs-lookup"><span data-stu-id="44fb4-449">25000</span></span> |
| <span data-ttu-id="44fb4-450">Honda</span><span class="sxs-lookup"><span data-stu-id="44fb4-450">Honda</span></span> |<span data-ttu-id="44fb4-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="44fb4-452">26000</span><span class="sxs-lookup"><span data-stu-id="44fb4-452">26000</span></span> |
| <span data-ttu-id="44fb4-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="44fb4-453">Toyota</span></span> |<span data-ttu-id="44fb4-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="44fb4-455">2000</span><span class="sxs-lookup"><span data-stu-id="44fb4-455">2000</span></span> |

<span data-ttu-id="44fb4-456">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-456">**Output**:</span></span>

| <span data-ttu-id="44fb4-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="44fb4-457">StartFault</span></span> | <span data-ttu-id="44fb4-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="44fb4-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="44fb4-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="44fb4-461">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-461">**Solution**:</span></span>

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

<span data-ttu-id="44fb4-462">**Uitleg**: Gebruik **LAG** tooview Hallo invoerstroom 24 uur en zoek exemplaren waar **StartFault** en **StopFault** zijn omspannen door Hallo < 20000 gewicht.</span><span class="sxs-lookup"><span data-stu-id="44fb4-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="44fb4-463">Query-voorbeeld: Vul ontbrekende waarden</span><span class="sxs-lookup"><span data-stu-id="44fb4-463">Query example: Fill missing values</span></span>
<span data-ttu-id="44fb4-464">**Beschrijving**: produceren voor Hallo stroom van gebeurtenissen met ontbrekende waarden, een reeks gebeurtenissen met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="44fb4-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="44fb4-465">Bijvoorbeeld, een gebeurtenis om de vijf seconden Hallo laatst gezien gegevenspunt rapporten genereren.</span><span class="sxs-lookup"><span data-stu-id="44fb4-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="44fb4-466">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-466">**Input**:</span></span>

| <span data-ttu-id="44fb4-467">T</span><span class="sxs-lookup"><span data-stu-id="44fb4-467">t</span></span> | <span data-ttu-id="44fb4-468">waarde</span><span class="sxs-lookup"><span data-stu-id="44fb4-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="44fb4-469">' 2014-01-01T06:01:00 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="44fb4-470">1</span><span class="sxs-lookup"><span data-stu-id="44fb4-470">1</span></span> |
| <span data-ttu-id="44fb4-471">' 2014-01-01T06:01:05 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="44fb4-472">2</span><span class="sxs-lookup"><span data-stu-id="44fb4-472">2</span></span> |
| <span data-ttu-id="44fb4-473">' 2014-01-01T06:01:10 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="44fb4-474">3</span><span class="sxs-lookup"><span data-stu-id="44fb4-474">3</span></span> |
| <span data-ttu-id="44fb4-475">' 2014-01-01T06:01:15 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="44fb4-476">4</span><span class="sxs-lookup"><span data-stu-id="44fb4-476">4</span></span> |
| <span data-ttu-id="44fb4-477">' 2014-01-01T06:01:30 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="44fb4-478">5</span><span class="sxs-lookup"><span data-stu-id="44fb4-478">5</span></span> |
| <span data-ttu-id="44fb4-479">' 2014-01-01T06:01:35 '</span><span class="sxs-lookup"><span data-stu-id="44fb4-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="44fb4-480">6</span><span class="sxs-lookup"><span data-stu-id="44fb4-480">6</span></span> |

<span data-ttu-id="44fb4-481">**Uitvoer (eerste 10 rijen)**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="44fb4-482">windowend</span><span class="sxs-lookup"><span data-stu-id="44fb4-482">windowend</span></span> | <span data-ttu-id="44fb4-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="44fb4-483">lastevent.t</span></span> | <span data-ttu-id="44fb4-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="44fb4-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44fb4-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="44fb4-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="44fb4-487">1</span><span class="sxs-lookup"><span data-stu-id="44fb4-487">1</span></span> |
| <span data-ttu-id="44fb4-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="44fb4-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="44fb4-490">2</span><span class="sxs-lookup"><span data-stu-id="44fb4-490">2</span></span> |
| <span data-ttu-id="44fb4-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="44fb4-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="44fb4-493">3</span><span class="sxs-lookup"><span data-stu-id="44fb4-493">3</span></span> |
| <span data-ttu-id="44fb4-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="44fb4-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="44fb4-496">4</span><span class="sxs-lookup"><span data-stu-id="44fb4-496">4</span></span> |
| <span data-ttu-id="44fb4-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="44fb4-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="44fb4-499">4</span><span class="sxs-lookup"><span data-stu-id="44fb4-499">4</span></span> |
| <span data-ttu-id="44fb4-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="44fb4-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="44fb4-502">4</span><span class="sxs-lookup"><span data-stu-id="44fb4-502">4</span></span> |
| <span data-ttu-id="44fb4-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="44fb4-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="44fb4-505">5</span><span class="sxs-lookup"><span data-stu-id="44fb4-505">5</span></span> |
| <span data-ttu-id="44fb4-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="44fb4-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="44fb4-508">6</span><span class="sxs-lookup"><span data-stu-id="44fb4-508">6</span></span> |
| <span data-ttu-id="44fb4-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="44fb4-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="44fb4-511">6</span><span class="sxs-lookup"><span data-stu-id="44fb4-511">6</span></span> |
| <span data-ttu-id="44fb4-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="44fb4-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="44fb4-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="44fb4-514">6</span><span class="sxs-lookup"><span data-stu-id="44fb4-514">6</span></span> |

<span data-ttu-id="44fb4-515">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="44fb4-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="44fb4-516">**Uitleg**: deze query gebeurtenissen worden gegenereerd om de vijf seconden en uitvoer Hallo laatste gebeurtenis dat u eerder hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="44fb4-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="44fb4-517">Hallo [Hopping venster](https://msdn.microsoft.com/library/dn835041.aspx "Hopping venster--Azure Stream Analytics") duur bepaalt hoe ver terug Hallo query eruitziet voor toofind Hallo laatste gebeurtenis (300 seconden in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="44fb4-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="44fb4-518">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="44fb4-518">Get help</span></span>
<span data-ttu-id="44fb4-519">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="44fb4-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44fb4-520">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44fb4-520">Next steps</span></span>
* [<span data-ttu-id="44fb4-521">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44fb4-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="44fb4-522">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44fb4-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="44fb4-523">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="44fb4-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="44fb4-524">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="44fb4-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="44fb4-525">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="44fb4-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

