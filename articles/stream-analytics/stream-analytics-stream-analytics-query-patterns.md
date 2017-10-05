---
title: Voorbeelden van algemene gebruikspatronen in Stream Analytics query | Microsoft Docs
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="11799-104">Voorbeelden van algemene gebruikspatronen van de Stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="11799-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="11799-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="11799-105">Introduction</span></span>
<span data-ttu-id="11799-106">Query's in Azure Stream Analytics worden uitgedrukt in een SQL-achtige querytaal.</span><span class="sxs-lookup"><span data-stu-id="11799-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="11799-107">Deze query's worden beschreven in de [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) handleiding.</span><span class="sxs-lookup"><span data-stu-id="11799-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="11799-108">In dit artikel bevat een overzicht van oplossingen voor enkele veelvoorkomende querypatronen, op basis van praktijkscenario's.</span><span class="sxs-lookup"><span data-stu-id="11799-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="11799-109">Het is een onderhanden werk en met nieuwe patronen voortdurend wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="11799-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="11799-110">Query-voorbeeld: gegevenstypen converteren</span><span class="sxs-lookup"><span data-stu-id="11799-110">Query example: Convert data types</span></span>
<span data-ttu-id="11799-111">**Beschrijving**: het definiëren van de typen eigenschappen voor de invoerstroom.</span><span class="sxs-lookup"><span data-stu-id="11799-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="11799-112">Bijvoorbeeld: het gewicht auto is afkomstig uit de invoerstroom als tekenreeksen en moet worden geconverteerd naar **INT** om uit te voeren **som** het.</span><span class="sxs-lookup"><span data-stu-id="11799-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="11799-113">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-113">**Input**:</span></span>

| <span data-ttu-id="11799-114">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-114">Make</span></span> | <span data-ttu-id="11799-115">Time</span><span class="sxs-lookup"><span data-stu-id="11799-115">Time</span></span> | <span data-ttu-id="11799-116">Gewicht</span><span class="sxs-lookup"><span data-stu-id="11799-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-117">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-117">Honda</span></span> |<span data-ttu-id="11799-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="11799-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="11799-119">"1000"</span></span> |
| <span data-ttu-id="11799-120">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-120">Honda</span></span> |<span data-ttu-id="11799-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="11799-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="11799-122">"2000"</span></span> |

<span data-ttu-id="11799-123">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-123">**Output**:</span></span>

| <span data-ttu-id="11799-124">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-124">Make</span></span> | <span data-ttu-id="11799-125">Gewicht</span><span class="sxs-lookup"><span data-stu-id="11799-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="11799-126">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-126">Honda</span></span> |<span data-ttu-id="11799-127">3000</span><span class="sxs-lookup"><span data-stu-id="11799-127">3000</span></span> |

<span data-ttu-id="11799-128">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="11799-129">**Uitleg**: gebruik een **CAST** -instructie in de **gewicht** aan te geven van het gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="11799-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="11799-130">Zie de lijst met ondersteunde gegevenstypen in [gegevenstypen (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="11799-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="11799-131">Query-voorbeeld: gebruik achtige/niet wilt patroon die overeenkomt met</span><span class="sxs-lookup"><span data-stu-id="11799-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="11799-132">**Beschrijving**: controleert of de waarde van een veld van de gebeurtenis overeenkomt met een bepaald patroon.</span><span class="sxs-lookup"><span data-stu-id="11799-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="11799-133">Bijvoorbeeld, Controleer het resultaat overschrijven die beginnen met A en eindigen met 9.</span><span class="sxs-lookup"><span data-stu-id="11799-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="11799-134">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-134">**Input**:</span></span>

| <span data-ttu-id="11799-135">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-135">Make</span></span> | <span data-ttu-id="11799-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-136">LicensePlate</span></span> | <span data-ttu-id="11799-137">Time</span><span class="sxs-lookup"><span data-stu-id="11799-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-138">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-138">Honda</span></span> |<span data-ttu-id="11799-139">ABC 123</span><span class="sxs-lookup"><span data-stu-id="11799-139">ABC-123</span></span> |<span data-ttu-id="11799-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-141">Toyota</span></span> |<span data-ttu-id="11799-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="11799-142">AAA-999</span></span> |<span data-ttu-id="11799-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="11799-144">Nissan</span></span> |<span data-ttu-id="11799-145">ABC 369</span><span class="sxs-lookup"><span data-stu-id="11799-145">ABC-369</span></span> |<span data-ttu-id="11799-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-147">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-147">**Output**:</span></span>

| <span data-ttu-id="11799-148">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-148">Make</span></span> | <span data-ttu-id="11799-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-149">LicensePlate</span></span> | <span data-ttu-id="11799-150">Time</span><span class="sxs-lookup"><span data-stu-id="11799-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-151">Toyota</span></span> |<span data-ttu-id="11799-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="11799-152">AAA-999</span></span> |<span data-ttu-id="11799-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="11799-154">Nissan</span></span> |<span data-ttu-id="11799-155">ABC 369</span><span class="sxs-lookup"><span data-stu-id="11799-155">ABC-369</span></span> |<span data-ttu-id="11799-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-157">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="11799-158">**Uitleg**: Gebruik de **zoals** instructie om te controleren de **LicensePlate** veld waarde.</span><span class="sxs-lookup"><span data-stu-id="11799-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="11799-159">Deze moet beginnen met een A, en vervolgens hebt een willekeurige tekenreeks van nul of meer tekens en vervolgens eindigen met een 9.</span><span class="sxs-lookup"><span data-stu-id="11799-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="11799-160">Query-voorbeeld: Geef de logica voor andere gevallen en-waarden (CASE-instructies)</span><span class="sxs-lookup"><span data-stu-id="11799-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="11799-161">**Beschrijving**: Geef een andere berekeningen voor het veld, op basis van een bepaald criterium.</span><span class="sxs-lookup"><span data-stu-id="11799-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="11799-162">Geef bijvoorbeeld een beschrijving van de tekenreeks voor het maken van het aantal auto's van dezelfde doorgegeven met een speciaal geval voor 1.</span><span class="sxs-lookup"><span data-stu-id="11799-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="11799-163">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-163">**Input**:</span></span>

| <span data-ttu-id="11799-164">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-164">Make</span></span> | <span data-ttu-id="11799-165">Time</span><span class="sxs-lookup"><span data-stu-id="11799-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-166">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-166">Honda</span></span> |<span data-ttu-id="11799-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-168">Toyota</span></span> |<span data-ttu-id="11799-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-170">Toyota</span></span> |<span data-ttu-id="11799-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-172">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-172">**Output**:</span></span>

| <span data-ttu-id="11799-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="11799-173">CarsPassed</span></span> | <span data-ttu-id="11799-174">Time</span><span class="sxs-lookup"><span data-stu-id="11799-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="11799-175">1 Honda</span></span> |<span data-ttu-id="11799-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="11799-177">2 Toyotas</span><span class="sxs-lookup"><span data-stu-id="11799-177">2 Toyotas</span></span> |<span data-ttu-id="11799-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="11799-179">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-179">**Solution**:</span></span>

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

<span data-ttu-id="11799-180">**Uitleg**: de **geval** component kan wij verschillende berekeningen, op basis van bepaalde criteria (in ons geval de telling van de auto's in het venster cumulatieve).</span><span class="sxs-lookup"><span data-stu-id="11799-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="11799-181">Query-voorbeeld: gegevens verzenden naar meerdere uitgangen</span><span class="sxs-lookup"><span data-stu-id="11799-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="11799-182">**Beschrijving**: gegevens verzenden naar meerdere doelen van de uitvoer van een enkele taak.</span><span class="sxs-lookup"><span data-stu-id="11799-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="11799-183">Bijvoorbeeld, analyseren van gegevens voor een waarschuwing op basis van drempelwaarden en alle gebeurtenissen naar blob-opslag te archiveren.</span><span class="sxs-lookup"><span data-stu-id="11799-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="11799-184">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-184">**Input**:</span></span>

| <span data-ttu-id="11799-185">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-185">Make</span></span> | <span data-ttu-id="11799-186">Time</span><span class="sxs-lookup"><span data-stu-id="11799-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-187">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-187">Honda</span></span> |<span data-ttu-id="11799-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-189">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-189">Honda</span></span> |<span data-ttu-id="11799-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-191">Toyota</span></span> |<span data-ttu-id="11799-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-193">Toyota</span></span> |<span data-ttu-id="11799-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-195">Toyota</span></span> |<span data-ttu-id="11799-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="11799-197">**Output1**:</span></span>

| <span data-ttu-id="11799-198">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-198">Make</span></span> | <span data-ttu-id="11799-199">Time</span><span class="sxs-lookup"><span data-stu-id="11799-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-200">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-200">Honda</span></span> |<span data-ttu-id="11799-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-202">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-202">Honda</span></span> |<span data-ttu-id="11799-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-204">Toyota</span></span> |<span data-ttu-id="11799-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-206">Toyota</span></span> |<span data-ttu-id="11799-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-208">Toyota</span></span> |<span data-ttu-id="11799-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="11799-210">**Output2**:</span></span>

| <span data-ttu-id="11799-211">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-211">Make</span></span> | <span data-ttu-id="11799-212">Time</span><span class="sxs-lookup"><span data-stu-id="11799-212">Time</span></span> | <span data-ttu-id="11799-213">Count</span><span class="sxs-lookup"><span data-stu-id="11799-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-214">Toyota</span></span> |<span data-ttu-id="11799-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="11799-216">3</span><span class="sxs-lookup"><span data-stu-id="11799-216">3</span></span> |

<span data-ttu-id="11799-217">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-217">**Solution**:</span></span>

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

<span data-ttu-id="11799-218">**Uitleg**: de **INTO** component Stream Analytics wordt uitgelegd welke van de uitvoer schrijven van de gegevens uit deze instructie.</span><span class="sxs-lookup"><span data-stu-id="11799-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="11799-219">Is het doorgeven van de gegevens die we ontvangen op een uitvoer die we met de naam van de eerste query **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="11799-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="11799-220">De tweede query biedt een aantal eenvoudige aggregatie en filteren en deze stuurt de resultaten naar een downstream waarschuwingsmethoden systeem.</span><span class="sxs-lookup"><span data-stu-id="11799-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="11799-221">Opmerking u kunt ook opnieuw gebruiken de resultaten van de algemene tabelexpressies (CTE's) (zoals **WITH** instructies) in meerdere uitvoer-instructies.</span><span class="sxs-lookup"><span data-stu-id="11799-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="11799-222">Deze optie heeft het voordeel van het openen van de invoerbron minder lezers.</span><span class="sxs-lookup"><span data-stu-id="11799-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="11799-223">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="11799-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="11799-224">Voorbeeld van de query: de unieke waarden tellen</span><span class="sxs-lookup"><span data-stu-id="11799-224">Query example: Count unique values</span></span>
<span data-ttu-id="11799-225">**Beschrijving**: het aantal unieke waarden die worden weergegeven in de stroom binnen een tijdvenster tellen.</span><span class="sxs-lookup"><span data-stu-id="11799-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="11799-226">Bijvoorbeeld hoeveel unieke wordt doorgegeven aan de stand tolstation in een venster 2 seconden auto's?</span><span class="sxs-lookup"><span data-stu-id="11799-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="11799-227">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-227">**Input**:</span></span>

| <span data-ttu-id="11799-228">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-228">Make</span></span> | <span data-ttu-id="11799-229">Time</span><span class="sxs-lookup"><span data-stu-id="11799-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-230">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-230">Honda</span></span> |<span data-ttu-id="11799-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-232">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-232">Honda</span></span> |<span data-ttu-id="11799-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-234">Toyota</span></span> |<span data-ttu-id="11799-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-236">Toyota</span></span> |<span data-ttu-id="11799-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-238">Toyota</span></span> |<span data-ttu-id="11799-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="11799-240">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="11799-240">**Output:**</span></span>

| <span data-ttu-id="11799-241">Count</span><span class="sxs-lookup"><span data-stu-id="11799-241">Count</span></span> | <span data-ttu-id="11799-242">Time</span><span class="sxs-lookup"><span data-stu-id="11799-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-243">2</span><span class="sxs-lookup"><span data-stu-id="11799-243">2</span></span> |<span data-ttu-id="11799-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="11799-245">1</span><span class="sxs-lookup"><span data-stu-id="11799-245">1</span></span> |<span data-ttu-id="11799-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="11799-247">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="11799-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="11799-248">**Uitleg:**
**COUNT (afzonderlijke zorg)** retourneert het aantal afzonderlijke waarden in de **zorg** kolom binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="11799-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="11799-249">Query-voorbeeld: bepalen of een waarde is gewijzigd</span><span class="sxs-lookup"><span data-stu-id="11799-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="11799-250">**Beschrijving**: kijken naar een vorige waarde om te bepalen of anders is dan de huidige waarde.</span><span class="sxs-lookup"><span data-stu-id="11799-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="11799-251">Bijvoorbeeld, is de vorige auto tolstation onderweg de dezelfde maken als de huidige auto?</span><span class="sxs-lookup"><span data-stu-id="11799-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="11799-252">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-252">**Input**:</span></span>

| <span data-ttu-id="11799-253">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-253">Make</span></span> | <span data-ttu-id="11799-254">Time</span><span class="sxs-lookup"><span data-stu-id="11799-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-255">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-255">Honda</span></span> |<span data-ttu-id="11799-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-257">Toyota</span></span> |<span data-ttu-id="11799-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="11799-259">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-259">**Output**:</span></span>

| <span data-ttu-id="11799-260">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-260">Make</span></span> | <span data-ttu-id="11799-261">Time</span><span class="sxs-lookup"><span data-stu-id="11799-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="11799-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-262">Toyota</span></span> |<span data-ttu-id="11799-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="11799-264">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="11799-265">**Uitleg**: Gebruik **LAG** als u wilt bekijken in de invoerstroom één gebeurtenis terug en de **zorg** waarde.</span><span class="sxs-lookup"><span data-stu-id="11799-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="11799-266">Vergelijk deze naar de **zorg** -waarde op de huidige gebeurtenis en de uitvoer van de gebeurtenis als deze verschillen.</span><span class="sxs-lookup"><span data-stu-id="11799-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="11799-267">Voorbeeld van de query: de eerste gebeurtenis niet vinden in een venster</span><span class="sxs-lookup"><span data-stu-id="11799-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="11799-268">**Beschrijving**: de eerste auto niet vinden in het interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="11799-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="11799-269">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-269">**Input**:</span></span>

| <span data-ttu-id="11799-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-270">LicensePlate</span></span> | <span data-ttu-id="11799-271">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-271">Make</span></span> | <span data-ttu-id="11799-272">Time</span><span class="sxs-lookup"><span data-stu-id="11799-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="11799-273">DXE 5291</span></span> |<span data-ttu-id="11799-274">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-274">Honda</span></span> |<span data-ttu-id="11799-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="11799-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="11799-276">YZK 5704</span></span> |<span data-ttu-id="11799-277">Ford</span><span class="sxs-lookup"><span data-stu-id="11799-277">Ford</span></span> |<span data-ttu-id="11799-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="11799-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="11799-279">RMV 8282</span></span> |<span data-ttu-id="11799-280">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-280">Honda</span></span> |<span data-ttu-id="11799-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="11799-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="11799-282">YHN 6970</span></span> |<span data-ttu-id="11799-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-283">Toyota</span></span> |<span data-ttu-id="11799-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="11799-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="11799-285">VFE 1616</span></span> |<span data-ttu-id="11799-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-286">Toyota</span></span> |<span data-ttu-id="11799-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="11799-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="11799-288">QYF 9358</span></span> |<span data-ttu-id="11799-289">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-289">Honda</span></span> |<span data-ttu-id="11799-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="11799-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="11799-291">MDR 6128</span></span> |<span data-ttu-id="11799-292">BMW</span><span class="sxs-lookup"><span data-stu-id="11799-292">BMW</span></span> |<span data-ttu-id="11799-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="11799-294">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-294">**Output**:</span></span>

| <span data-ttu-id="11799-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-295">LicensePlate</span></span> | <span data-ttu-id="11799-296">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-296">Make</span></span> | <span data-ttu-id="11799-297">Time</span><span class="sxs-lookup"><span data-stu-id="11799-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="11799-298">DXE 5291</span></span> |<span data-ttu-id="11799-299">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-299">Honda</span></span> |<span data-ttu-id="11799-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="11799-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="11799-301">QYF 9358</span></span> |<span data-ttu-id="11799-302">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-302">Honda</span></span> |<span data-ttu-id="11799-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="11799-304">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="11799-305">Nu gaan we het probleem wijzigen en de eerste auto van een bepaalde merk niet vinden in het interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="11799-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="11799-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-306">LicensePlate</span></span> | <span data-ttu-id="11799-307">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-307">Make</span></span> | <span data-ttu-id="11799-308">Time</span><span class="sxs-lookup"><span data-stu-id="11799-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="11799-309">DXE 5291</span></span> |<span data-ttu-id="11799-310">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-310">Honda</span></span> |<span data-ttu-id="11799-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="11799-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="11799-312">YZK 5704</span></span> |<span data-ttu-id="11799-313">Ford</span><span class="sxs-lookup"><span data-stu-id="11799-313">Ford</span></span> |<span data-ttu-id="11799-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="11799-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="11799-315">YHN 6970</span></span> |<span data-ttu-id="11799-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-316">Toyota</span></span> |<span data-ttu-id="11799-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="11799-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="11799-318">QYF 9358</span></span> |<span data-ttu-id="11799-319">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-319">Honda</span></span> |<span data-ttu-id="11799-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="11799-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="11799-321">MDR 6128</span></span> |<span data-ttu-id="11799-322">BMW</span><span class="sxs-lookup"><span data-stu-id="11799-322">BMW</span></span> |<span data-ttu-id="11799-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="11799-324">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="11799-325">Voorbeeld van de query: de laatste gebeurtenis niet vinden in een venster</span><span class="sxs-lookup"><span data-stu-id="11799-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="11799-326">**Beschrijving**: de laatste auto niet vinden in het interval van elke 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="11799-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="11799-327">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-327">**Input**:</span></span>

| <span data-ttu-id="11799-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-328">LicensePlate</span></span> | <span data-ttu-id="11799-329">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-329">Make</span></span> | <span data-ttu-id="11799-330">Time</span><span class="sxs-lookup"><span data-stu-id="11799-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="11799-331">DXE 5291</span></span> |<span data-ttu-id="11799-332">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-332">Honda</span></span> |<span data-ttu-id="11799-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="11799-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="11799-334">YZK 5704</span></span> |<span data-ttu-id="11799-335">Ford</span><span class="sxs-lookup"><span data-stu-id="11799-335">Ford</span></span> |<span data-ttu-id="11799-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="11799-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="11799-337">RMV 8282</span></span> |<span data-ttu-id="11799-338">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-338">Honda</span></span> |<span data-ttu-id="11799-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="11799-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="11799-340">YHN 6970</span></span> |<span data-ttu-id="11799-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-341">Toyota</span></span> |<span data-ttu-id="11799-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="11799-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="11799-343">VFE 1616</span></span> |<span data-ttu-id="11799-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-344">Toyota</span></span> |<span data-ttu-id="11799-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="11799-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="11799-346">QYF 9358</span></span> |<span data-ttu-id="11799-347">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-347">Honda</span></span> |<span data-ttu-id="11799-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="11799-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="11799-349">MDR 6128</span></span> |<span data-ttu-id="11799-350">BMW</span><span class="sxs-lookup"><span data-stu-id="11799-350">BMW</span></span> |<span data-ttu-id="11799-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="11799-352">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-352">**Output**:</span></span>

| <span data-ttu-id="11799-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-353">LicensePlate</span></span> | <span data-ttu-id="11799-354">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-354">Make</span></span> | <span data-ttu-id="11799-355">Time</span><span class="sxs-lookup"><span data-stu-id="11799-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="11799-356">VFE 1616</span></span> |<span data-ttu-id="11799-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-357">Toyota</span></span> |<span data-ttu-id="11799-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="11799-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="11799-359">MDR 6128</span></span> |<span data-ttu-id="11799-360">BMW</span><span class="sxs-lookup"><span data-stu-id="11799-360">BMW</span></span> |<span data-ttu-id="11799-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="11799-362">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-362">**Solution**:</span></span>

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

<span data-ttu-id="11799-363">**Uitleg**: Er zijn twee stappen in de query.</span><span class="sxs-lookup"><span data-stu-id="11799-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="11799-364">Het eerste beheerpunt vindt de meest recente tijdstempel in windows 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="11799-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="11799-365">De tweede stap koppelt de resultaten van de eerste query met de oorspronkelijke stroom vinden van de gebeurtenissen die overeenkomen met de laatste tijdstempels in elk venster.</span><span class="sxs-lookup"><span data-stu-id="11799-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="11799-366">Voorbeeld van de query: de afwezigheid van gebeurtenissen detecteren</span><span class="sxs-lookup"><span data-stu-id="11799-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="11799-367">**Beschrijving**: Controleer of er een stroom geen waarde die overeenkomt met een bepaald criterium.</span><span class="sxs-lookup"><span data-stu-id="11799-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="11799-368">Bijvoorbeeld: hebt 2 opeenvolgende auto's uit hetzelfde merk onderweg tolstation ingevoerd gedurende de laatste 90 seconden</span><span class="sxs-lookup"><span data-stu-id="11799-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="11799-369">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-369">**Input**:</span></span>

| <span data-ttu-id="11799-370">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-370">Make</span></span> | <span data-ttu-id="11799-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-371">LicensePlate</span></span> | <span data-ttu-id="11799-372">Time</span><span class="sxs-lookup"><span data-stu-id="11799-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-373">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-373">Honda</span></span> |<span data-ttu-id="11799-374">ABC 123</span><span class="sxs-lookup"><span data-stu-id="11799-374">ABC-123</span></span> |<span data-ttu-id="11799-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="11799-376">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-376">Honda</span></span> |<span data-ttu-id="11799-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="11799-377">AAA-999</span></span> |<span data-ttu-id="11799-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="11799-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-379">Toyota</span></span> |<span data-ttu-id="11799-380">DEF 987</span><span class="sxs-lookup"><span data-stu-id="11799-380">DEF-987</span></span> |<span data-ttu-id="11799-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="11799-382">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-382">Honda</span></span> |<span data-ttu-id="11799-383">GHI 345</span><span class="sxs-lookup"><span data-stu-id="11799-383">GHI-345</span></span> |<span data-ttu-id="11799-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="11799-385">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-385">**Output**:</span></span>

| <span data-ttu-id="11799-386">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-386">Make</span></span> | <span data-ttu-id="11799-387">Time</span><span class="sxs-lookup"><span data-stu-id="11799-387">Time</span></span> | <span data-ttu-id="11799-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="11799-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="11799-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="11799-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="11799-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="11799-391">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-391">Honda</span></span> |<span data-ttu-id="11799-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="11799-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="11799-393">AAA-999</span></span> |<span data-ttu-id="11799-394">ABC 123</span><span class="sxs-lookup"><span data-stu-id="11799-394">ABC-123</span></span> |<span data-ttu-id="11799-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="11799-396">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-396">**Solution**:</span></span>

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

<span data-ttu-id="11799-397">**Uitleg**: Gebruik **LAG** als u wilt bekijken in de invoerstroom één gebeurtenis terug en de **zorg** waarde.</span><span class="sxs-lookup"><span data-stu-id="11799-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="11799-398">Vergelijk deze met de **zorg** waarde in de huidige gebeurtenis en de gebeurtenis vervolgens uitvoer als ze hetzelfde zijn.</span><span class="sxs-lookup"><span data-stu-id="11799-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="11799-399">U kunt ook **LAG** ophalen van gegevens over de vorige auto.</span><span class="sxs-lookup"><span data-stu-id="11799-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="11799-400">Voorbeeld van de query: de tijd tussen gebeurtenissen detecteren</span><span class="sxs-lookup"><span data-stu-id="11799-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="11799-401">**Beschrijving**: de duur van een bepaalde gebeurtenis vinden.</span><span class="sxs-lookup"><span data-stu-id="11799-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="11799-402">Bijvoorbeeld: een web-clickstream gezien, bepalen de tijd die op een functie.</span><span class="sxs-lookup"><span data-stu-id="11799-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="11799-403">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-403">**Input**:</span></span>  

| <span data-ttu-id="11799-404">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="11799-404">User</span></span> | <span data-ttu-id="11799-405">Functie</span><span class="sxs-lookup"><span data-stu-id="11799-405">Feature</span></span> | <span data-ttu-id="11799-406">Gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="11799-406">Event</span></span> | <span data-ttu-id="11799-407">Time</span><span class="sxs-lookup"><span data-stu-id="11799-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="11799-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="11799-408">RightMenu</span></span> |<span data-ttu-id="11799-409">Starten</span><span class="sxs-lookup"><span data-stu-id="11799-409">Start</span></span> |<span data-ttu-id="11799-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="11799-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="11799-411">RightMenu</span></span> |<span data-ttu-id="11799-412">Einde</span><span class="sxs-lookup"><span data-stu-id="11799-412">End</span></span> |<span data-ttu-id="11799-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="11799-414">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-414">**Output**:</span></span>  

| <span data-ttu-id="11799-415">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="11799-415">User</span></span> | <span data-ttu-id="11799-416">Functie</span><span class="sxs-lookup"><span data-stu-id="11799-416">Feature</span></span> | <span data-ttu-id="11799-417">Duur</span><span class="sxs-lookup"><span data-stu-id="11799-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="11799-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="11799-418">RightMenu</span></span> |<span data-ttu-id="11799-419">7</span><span class="sxs-lookup"><span data-stu-id="11799-419">7</span></span> |

<span data-ttu-id="11799-420">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="11799-421">**Uitleg**: Gebruik de **laatste** functie voor het ophalen van de laatste **tijd** waarde wanneer het gebeurtenistype is **Start**.</span><span class="sxs-lookup"><span data-stu-id="11799-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="11799-422">De **laatste** functie maakt gebruik van **PARTITION BY [gebruiker]** om aan te geven dat het resultaat wordt berekend per unieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="11799-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="11799-423">De query heeft een 1 uur maximale drempelwaarde voor het tijdsverschil tussen **Start** en **stoppen** gebeurtenissen, maar is configureerbaar naar behoefte **(LIMIET DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="11799-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="11799-424">Voorbeeld van de query: de duur van een voorwaarde detecteren</span><span class="sxs-lookup"><span data-stu-id="11799-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="11799-425">**Beschrijving**: vinden out hoe lang een voorwaarde is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="11799-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="11799-426">Stel dat een fout heeft geresulteerd in alle auto's met een onjuiste gewicht (meer dan 20.000 pond).</span><span class="sxs-lookup"><span data-stu-id="11799-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="11799-427">We willen berekenen van de duur van de fout.</span><span class="sxs-lookup"><span data-stu-id="11799-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="11799-428">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-428">**Input**:</span></span>

| <span data-ttu-id="11799-429">Maken</span><span class="sxs-lookup"><span data-stu-id="11799-429">Make</span></span> | <span data-ttu-id="11799-430">Time</span><span class="sxs-lookup"><span data-stu-id="11799-430">Time</span></span> | <span data-ttu-id="11799-431">Gewicht</span><span class="sxs-lookup"><span data-stu-id="11799-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-432">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-432">Honda</span></span> |<span data-ttu-id="11799-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="11799-434">2000</span><span class="sxs-lookup"><span data-stu-id="11799-434">2000</span></span> |
| <span data-ttu-id="11799-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-435">Toyota</span></span> |<span data-ttu-id="11799-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="11799-437">25000</span><span class="sxs-lookup"><span data-stu-id="11799-437">25000</span></span> |
| <span data-ttu-id="11799-438">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-438">Honda</span></span> |<span data-ttu-id="11799-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="11799-440">26000</span><span class="sxs-lookup"><span data-stu-id="11799-440">26000</span></span> |
| <span data-ttu-id="11799-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-441">Toyota</span></span> |<span data-ttu-id="11799-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="11799-443">25000</span><span class="sxs-lookup"><span data-stu-id="11799-443">25000</span></span> |
| <span data-ttu-id="11799-444">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-444">Honda</span></span> |<span data-ttu-id="11799-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="11799-446">26000</span><span class="sxs-lookup"><span data-stu-id="11799-446">26000</span></span> |
| <span data-ttu-id="11799-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-447">Toyota</span></span> |<span data-ttu-id="11799-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="11799-449">25000</span><span class="sxs-lookup"><span data-stu-id="11799-449">25000</span></span> |
| <span data-ttu-id="11799-450">Honda</span><span class="sxs-lookup"><span data-stu-id="11799-450">Honda</span></span> |<span data-ttu-id="11799-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="11799-452">26000</span><span class="sxs-lookup"><span data-stu-id="11799-452">26000</span></span> |
| <span data-ttu-id="11799-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="11799-453">Toyota</span></span> |<span data-ttu-id="11799-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="11799-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="11799-455">2000</span><span class="sxs-lookup"><span data-stu-id="11799-455">2000</span></span> |

<span data-ttu-id="11799-456">**Uitvoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-456">**Output**:</span></span>

| <span data-ttu-id="11799-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="11799-457">StartFault</span></span> | <span data-ttu-id="11799-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="11799-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="11799-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="11799-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="11799-461">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-461">**Solution**:</span></span>

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

<span data-ttu-id="11799-462">**Uitleg**: Gebruik **LAG** weergeven van de invoerstroom 24 uur en zoek naar waar u exemplaren **StartFault** en **StopFault** door het gewicht < 20000 zijn omspannen.</span><span class="sxs-lookup"><span data-stu-id="11799-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="11799-463">Query-voorbeeld: Vul ontbrekende waarden</span><span class="sxs-lookup"><span data-stu-id="11799-463">Query example: Fill missing values</span></span>
<span data-ttu-id="11799-464">**Beschrijving**: voor de stroom van gebeurtenissen met ontbrekende waarden produceren van een stream van gebeurtenissen met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="11799-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="11799-465">Bijvoorbeeld, een gebeurtenis om de vijf seconden die het meest recent waargenomen gegevenspunt rapporten genereren.</span><span class="sxs-lookup"><span data-stu-id="11799-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="11799-466">**Invoer**:</span><span class="sxs-lookup"><span data-stu-id="11799-466">**Input**:</span></span>

| <span data-ttu-id="11799-467">T</span><span class="sxs-lookup"><span data-stu-id="11799-467">t</span></span> | <span data-ttu-id="11799-468">waarde</span><span class="sxs-lookup"><span data-stu-id="11799-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="11799-469">' 2014-01-01T06:01:00 '</span><span class="sxs-lookup"><span data-stu-id="11799-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="11799-470">1</span><span class="sxs-lookup"><span data-stu-id="11799-470">1</span></span> |
| <span data-ttu-id="11799-471">' 2014-01-01T06:01:05 '</span><span class="sxs-lookup"><span data-stu-id="11799-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="11799-472">2</span><span class="sxs-lookup"><span data-stu-id="11799-472">2</span></span> |
| <span data-ttu-id="11799-473">' 2014-01-01T06:01:10 '</span><span class="sxs-lookup"><span data-stu-id="11799-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="11799-474">3</span><span class="sxs-lookup"><span data-stu-id="11799-474">3</span></span> |
| <span data-ttu-id="11799-475">' 2014-01-01T06:01:15 '</span><span class="sxs-lookup"><span data-stu-id="11799-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="11799-476">4</span><span class="sxs-lookup"><span data-stu-id="11799-476">4</span></span> |
| <span data-ttu-id="11799-477">' 2014-01-01T06:01:30 '</span><span class="sxs-lookup"><span data-stu-id="11799-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="11799-478">5</span><span class="sxs-lookup"><span data-stu-id="11799-478">5</span></span> |
| <span data-ttu-id="11799-479">' 2014-01-01T06:01:35 '</span><span class="sxs-lookup"><span data-stu-id="11799-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="11799-480">6</span><span class="sxs-lookup"><span data-stu-id="11799-480">6</span></span> |

<span data-ttu-id="11799-481">**Uitvoer (eerste 10 rijen)**:</span><span class="sxs-lookup"><span data-stu-id="11799-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="11799-482">windowend</span><span class="sxs-lookup"><span data-stu-id="11799-482">windowend</span></span> | <span data-ttu-id="11799-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="11799-483">lastevent.t</span></span> | <span data-ttu-id="11799-484">lastevent.Value</span><span class="sxs-lookup"><span data-stu-id="11799-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11799-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="11799-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="11799-487">1</span><span class="sxs-lookup"><span data-stu-id="11799-487">1</span></span> |
| <span data-ttu-id="11799-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="11799-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="11799-490">2</span><span class="sxs-lookup"><span data-stu-id="11799-490">2</span></span> |
| <span data-ttu-id="11799-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="11799-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="11799-493">3</span><span class="sxs-lookup"><span data-stu-id="11799-493">3</span></span> |
| <span data-ttu-id="11799-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="11799-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="11799-496">4</span><span class="sxs-lookup"><span data-stu-id="11799-496">4</span></span> |
| <span data-ttu-id="11799-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="11799-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="11799-499">4</span><span class="sxs-lookup"><span data-stu-id="11799-499">4</span></span> |
| <span data-ttu-id="11799-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="11799-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="11799-502">4</span><span class="sxs-lookup"><span data-stu-id="11799-502">4</span></span> |
| <span data-ttu-id="11799-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="11799-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="11799-505">5</span><span class="sxs-lookup"><span data-stu-id="11799-505">5</span></span> |
| <span data-ttu-id="11799-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="11799-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="11799-508">6</span><span class="sxs-lookup"><span data-stu-id="11799-508">6</span></span> |
| <span data-ttu-id="11799-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="11799-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="11799-511">6</span><span class="sxs-lookup"><span data-stu-id="11799-511">6</span></span> |
| <span data-ttu-id="11799-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="11799-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="11799-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="11799-514">6</span><span class="sxs-lookup"><span data-stu-id="11799-514">6</span></span> |

<span data-ttu-id="11799-515">**Oplossing**:</span><span class="sxs-lookup"><span data-stu-id="11799-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="11799-516">**Uitleg**: deze query gebeurtenissen genereert elke vijf seconden en levert de laatste gebeurtenis dat u eerder hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="11799-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="11799-517">De [Hopping venster](https://msdn.microsoft.com/library/dn835041.aspx "Hopping venster--Azure Stream Analytics") duur bepaalt hoe ver terug de query ziet er als u wilt zoeken naar de nieuwste gebeurtenis (300 seconden in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="11799-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="11799-518">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="11799-518">Get help</span></span>
<span data-ttu-id="11799-519">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="11799-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11799-520">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11799-520">Next steps</span></span>
* [<span data-ttu-id="11799-521">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11799-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="11799-522">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11799-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="11799-523">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="11799-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="11799-524">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="11799-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="11799-525">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="11799-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

