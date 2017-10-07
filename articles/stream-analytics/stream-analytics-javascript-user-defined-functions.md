---
title: aaaAzure Stream Analytics JavaScript gebruiker gedefinieerde functies | Microsoft Docs
description: Geavanceerde query mechanisme met de gebruiker gedefinieerde functies van JavaScript uitvoeren
keywords: JavaScript, de gebruiker gedefinieerde functies, udf
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="f8d49-104">Azure Stream Analytics JavaScript gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="f8d49-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="f8d49-105">Azure Stream Analytics ondersteunt de gebruiker gedefinieerde functies die zijn geschreven in JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f8d49-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="f8d49-106">Met uitgebreide set Hallo **tekenreeks**, **RegExp**, **Math**, **matrix**, en **datum** methoden die JavaScript biedt, complexe gegevenstransformaties met Stream Analytics-taken toocreate eenvoudiger geworden.</span><span class="sxs-lookup"><span data-stu-id="f8d49-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="f8d49-107">De gebruiker gedefinieerde functies JavaScript</span><span class="sxs-lookup"><span data-stu-id="f8d49-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="f8d49-108">De gebruiker gedefinieerde functies JavaScript ondersteuning voor stateless, compute-alleen scalaire functies die niet nodig voor externe verbinding hebt.</span><span class="sxs-lookup"><span data-stu-id="f8d49-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="f8d49-109">Hallo retourneren van een functie mag alleen een scalaire waarde (single).</span><span class="sxs-lookup"><span data-stu-id="f8d49-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="f8d49-110">Nadat u een taak JavaScript gebruiker gedefinieerde functie tooa toevoegt, kunt u Hallo functie overal in Hallo query, zoals een ingebouwde scalaire functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8d49-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="f8d49-111">Hier volgen enkele scenario's waar JavaScript gebruiker gedefinieerde functies interessant mogelijk:</span><span class="sxs-lookup"><span data-stu-id="f8d49-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="f8d49-112">Parseren en manipuleren van tekenreeksen die functies van de reguliere expressie, bijvoorbeeld hebben **Regexp_Replace()** en **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="f8d49-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="f8d49-113">Decoderen en gegevens, bijvoorbeeld conversie van binair naar hexadecimale codering</span><span class="sxs-lookup"><span data-stu-id="f8d49-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="f8d49-114">Rekenkundige berekeningen met JavaScript uitvoeren **Math** functies</span><span class="sxs-lookup"><span data-stu-id="f8d49-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="f8d49-115">Uitvoeren van bewerkingen zoals sorteren, join, zoeken en opvulling matrix</span><span class="sxs-lookup"><span data-stu-id="f8d49-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="f8d49-116">Hier volgen enkele dingen die u met een JavaScript gebruiker gedefinieerde functie in Stream Analytics kan niet doen:</span><span class="sxs-lookup"><span data-stu-id="f8d49-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="f8d49-117">Vestigen op externe REST-eindpunten, bijvoorbeeld: uitvoeren van IP-lookup- of opvragen referentiegegevens omkeren van een externe bron</span><span class="sxs-lookup"><span data-stu-id="f8d49-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="f8d49-118">Indeling van aangepaste gebeurtenisserialisatie uitvoeren of deserialiseren van de invoer/uitvoer</span><span class="sxs-lookup"><span data-stu-id="f8d49-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="f8d49-119">Maken van aangepaste statistische functies</span><span class="sxs-lookup"><span data-stu-id="f8d49-119">Create custom aggregates</span></span>

<span data-ttu-id="f8d49-120">Hoewel u functies zoals **Date.GetDate()** of **Math.random()** worden niet geblokkeerd in definitie van de functies van Hallo Vermijd het gebruik ervan.</span><span class="sxs-lookup"><span data-stu-id="f8d49-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="f8d49-121">Deze functies **niet** return Hallo dezelfde leiden telkens wanneer u deze aanroept en hello Azure Stream Analytics-service geen logboek van de functie aanroepen houdt en resultaten geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f8d49-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="f8d49-122">Als een functie verschillende resultaten op Hallo dezelfde gebeurtenissen retourneert, herhaalbaarheid niet worden gegarandeerd wanneer een taak opnieuw wordt gestart door u of door Hallo Stream Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="f8d49-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="f8d49-123">Toevoegen van een gebruiker gedefinieerde functie van JavaScript in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="f8d49-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="f8d49-124">een eenvoudige op JavaScript gebruiker gedefinieerde functie onder een bestaande Stream Analytics-taak toocreate Voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f8d49-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="f8d49-125">Zoek in hello Azure-portal, Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="f8d49-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="f8d49-126">Onder **taak TOPOLOGIE**, selecteert u de functie.</span><span class="sxs-lookup"><span data-stu-id="f8d49-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="f8d49-127">Een lege lijst met functies wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f8d49-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="f8d49-128">Selecteer een nieuwe gebruiker gedefinieerde functie toocreate **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="f8d49-129">Op Hallo **nieuwe functie** blade voor **functietype**, selecteer **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="f8d49-130">Een standaardsjabloon voor de functie wordt weergegeven in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="f8d49-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="f8d49-131">Voor Hallo **UDF alias**, voer **hex2Int**, en implementatie van de functie Hallo als volgt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f8d49-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="f8d49-132">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-132">Select **Save**.</span></span> <span data-ttu-id="f8d49-133">De functie wordt weergegeven in de lijst met functies Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8d49-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="f8d49-134">Selecteer nieuwe Hallo **hex2Int** functioneren en controleren van de functiedefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8d49-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="f8d49-135">Alle functies een **UDF** voorvoegsel toegevoegde toohello functie alias.</span><span class="sxs-lookup"><span data-stu-id="f8d49-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="f8d49-136">U moet te*Hallo voorvoegsel* wanneer u Hallo functie aanroepen in de Stream Analytics-query.</span><span class="sxs-lookup"><span data-stu-id="f8d49-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="f8d49-137">In dit geval u aanroepen **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="f8d49-138">Een gebruiker gedefinieerde functie van JavaScript-aanroep in een query</span><span class="sxs-lookup"><span data-stu-id="f8d49-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="f8d49-139">In Hallo-query-editor, onder **taak TOPOLOGIE**, selecteer **Query**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="f8d49-140">Uw query bewerken en vervolgens Hallo gebruiker gedefinieerde functie aanroept als volgt:</span><span class="sxs-lookup"><span data-stu-id="f8d49-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="f8d49-141">tooupload hello voorbeeldgegevensbestand, klik met de rechtermuisknop Hallo taak invoer.</span><span class="sxs-lookup"><span data-stu-id="f8d49-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="f8d49-142">tootest uw query, selecteer **Test**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="f8d49-143">Ondersteunde JavaScript-objecten</span><span class="sxs-lookup"><span data-stu-id="f8d49-143">Supported JavaScript objects</span></span>
<span data-ttu-id="f8d49-144">Azure Stream Analytics JavaScript gebruiker gedefinieerde functies ondersteuning voor ingebouwde JavaScript-objecten.</span><span class="sxs-lookup"><span data-stu-id="f8d49-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="f8d49-145">Zie voor een lijst van deze objecten [globale objecten](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="f8d49-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="f8d49-146">Conversie van stream Analytics en JavaScript</span><span class="sxs-lookup"><span data-stu-id="f8d49-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="f8d49-147">Er zijn verschillen in Hallo-typen die ondersteuning bieden voor Hallo Stream Analytics query language- en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f8d49-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="f8d49-148">Deze tabel bevat Hallo conversie toewijzingen tussen Hallo twee:</span><span class="sxs-lookup"><span data-stu-id="f8d49-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="f8d49-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8d49-149">Stream Analytics</span></span> | <span data-ttu-id="f8d49-150">Javascript</span><span class="sxs-lookup"><span data-stu-id="f8d49-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="f8d49-151">bigint</span><span class="sxs-lookup"><span data-stu-id="f8d49-151">bigint</span></span> | <span data-ttu-id="f8d49-152">Nummer (JavaScript kan alleen bestaan uit gehele getallen up tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="f8d49-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="f8d49-153">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f8d49-153">DateTime</span></span> | <span data-ttu-id="f8d49-154">Datum (JavaScript alleen ondersteund in milliseconden)</span><span class="sxs-lookup"><span data-stu-id="f8d49-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="f8d49-155">dubbele</span><span class="sxs-lookup"><span data-stu-id="f8d49-155">double</span></span> | <span data-ttu-id="f8d49-156">Aantal</span><span class="sxs-lookup"><span data-stu-id="f8d49-156">Number</span></span>
<span data-ttu-id="f8d49-157">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="f8d49-157">nvarchar(MAX)</span></span> | <span data-ttu-id="f8d49-158">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f8d49-158">String</span></span>
<span data-ttu-id="f8d49-159">Record</span><span class="sxs-lookup"><span data-stu-id="f8d49-159">Record</span></span> | <span data-ttu-id="f8d49-160">Object</span><span class="sxs-lookup"><span data-stu-id="f8d49-160">Object</span></span>
<span data-ttu-id="f8d49-161">Matrix</span><span class="sxs-lookup"><span data-stu-id="f8d49-161">Array</span></span> | <span data-ttu-id="f8d49-162">Matrix</span><span class="sxs-lookup"><span data-stu-id="f8d49-162">Array</span></span>
<span data-ttu-id="f8d49-163">NULL</span><span class="sxs-lookup"><span data-stu-id="f8d49-163">NULL</span></span> | <span data-ttu-id="f8d49-164">Null</span><span class="sxs-lookup"><span data-stu-id="f8d49-164">Null</span></span>


<span data-ttu-id="f8d49-165">Hier volgen JavaScript aan Stream Analytics-conversies:</span><span class="sxs-lookup"><span data-stu-id="f8d49-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="f8d49-166">Javascript</span><span class="sxs-lookup"><span data-stu-id="f8d49-166">JavaScript</span></span> | <span data-ttu-id="f8d49-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8d49-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="f8d49-168">Aantal</span><span class="sxs-lookup"><span data-stu-id="f8d49-168">Number</span></span> | <span data-ttu-id="f8d49-169">Bigint (als Hallo getal ronde en tussen lang is. MinValue en een lange. MaxValue; anders is de dubbele)</span><span class="sxs-lookup"><span data-stu-id="f8d49-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="f8d49-170">Date</span><span class="sxs-lookup"><span data-stu-id="f8d49-170">Date</span></span> | <span data-ttu-id="f8d49-171">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f8d49-171">DateTime</span></span>
<span data-ttu-id="f8d49-172">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="f8d49-172">String</span></span> | <span data-ttu-id="f8d49-173">nvarchar(max)</span><span class="sxs-lookup"><span data-stu-id="f8d49-173">nvarchar(MAX)</span></span>
<span data-ttu-id="f8d49-174">Object</span><span class="sxs-lookup"><span data-stu-id="f8d49-174">Object</span></span> | <span data-ttu-id="f8d49-175">Record</span><span class="sxs-lookup"><span data-stu-id="f8d49-175">Record</span></span>
<span data-ttu-id="f8d49-176">Matrix</span><span class="sxs-lookup"><span data-stu-id="f8d49-176">Array</span></span> | <span data-ttu-id="f8d49-177">Matrix</span><span class="sxs-lookup"><span data-stu-id="f8d49-177">Array</span></span>
<span data-ttu-id="f8d49-178">Null is en niet-gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="f8d49-178">Null, Undefined</span></span> | <span data-ttu-id="f8d49-179">NULL</span><span class="sxs-lookup"><span data-stu-id="f8d49-179">NULL</span></span>
<span data-ttu-id="f8d49-180">Een ander type (bijvoorbeeld, een functie of fout)</span><span class="sxs-lookup"><span data-stu-id="f8d49-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="f8d49-181">Niet ondersteund (resulteert in een runtime-fout)</span><span class="sxs-lookup"><span data-stu-id="f8d49-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f8d49-182">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f8d49-182">Troubleshooting</span></span>
<span data-ttu-id="f8d49-183">JavaScript-runtime-fouten worden beschouwd als onherstelbare en via het activiteitenlogboek Hallo worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f8d49-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="f8d49-184">tooretrieve hello log in hello Azure-portal, Ga tooyour taak en selecteert u **activiteitenlogboek**.</span><span class="sxs-lookup"><span data-stu-id="f8d49-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="f8d49-185">Andere patronen van de gebruiker gedefinieerde functie JavaScript</span><span class="sxs-lookup"><span data-stu-id="f8d49-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="f8d49-186">Geneste JSON toooutput schrijven</span><span class="sxs-lookup"><span data-stu-id="f8d49-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="f8d49-187">Als er een vervolgactie verwerkingsstap die gebruikmaakt van een Stream Analytics-taak uitvoer als invoer en hiervoor een JSON-indeling, kunt u een JSON-tekenreeks toooutput schrijven.</span><span class="sxs-lookup"><span data-stu-id="f8d49-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="f8d49-188">het volgende voorbeeld Hallo Hallo roept **JSON.stringify()** werken toopack alle naam/waarde-paren Hallo invoer en vervolgens als één enkele tekenreekswaarde in de uitvoer geschreven.</span><span class="sxs-lookup"><span data-stu-id="f8d49-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="f8d49-189">**Definitie van de gebruiker gedefinieerde functie JavaScript:**</span><span class="sxs-lookup"><span data-stu-id="f8d49-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="f8d49-190">**Voorbeeldquery:**</span><span class="sxs-lookup"><span data-stu-id="f8d49-190">**Sample query:**</span></span>
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a><span data-ttu-id="f8d49-191">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="f8d49-191">Get help</span></span>
<span data-ttu-id="f8d49-192">Voor aanvullende hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f8d49-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8d49-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8d49-193">Next steps</span></span>
* [<span data-ttu-id="f8d49-194">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8d49-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f8d49-195">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f8d49-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f8d49-196">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="f8d49-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f8d49-197">Azure Stream Analytics query language reference</span><span class="sxs-lookup"><span data-stu-id="f8d49-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f8d49-198">Azure Stream Analytics management REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="f8d49-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
