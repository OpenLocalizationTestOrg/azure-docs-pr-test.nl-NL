---
title: aaaScale Stream Analytics-taken tooincrease doorvoer | Microsoft Docs
description: Meer informatie over hoe tooscale Stream Analytics-taken op invoer partities configureren, Hallo querydefinitie afstemmen en instellen van taak streaming-eenheden.
keywords: gegevens streaming afstemmen analytics streaming gegevensverwerking,
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="ee600-104">Scale Azure Stream Analytics-taken tooincrease stroom gegevensverwerking doorvoer</span><span class="sxs-lookup"><span data-stu-id="ee600-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="ee600-105">Dit artikel laat zien hoe tootune een Stream Analytics query tooincrease doorvoer voor Streaming Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="ee600-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="ee600-106">U leert hoe tooscale Stream Analytics taken door invoer partities configureren en berekenen en het instellen van taak afstemmen Hallo analytics querydefinitie *streamingeenheden* (SUs).</span><span class="sxs-lookup"><span data-stu-id="ee600-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="ee600-107">Wat zijn de onderdelen van een Stream Analytics-taak Hallo?</span><span class="sxs-lookup"><span data-stu-id="ee600-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="ee600-108">De definitie van een Stream Analytics-taak bevat invoer, een query- en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="ee600-109">Invoer is waar Hallo taak leest Hallo-gegevensstroom uit.</span><span class="sxs-lookup"><span data-stu-id="ee600-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="ee600-110">Hallo query is gebruikte tootransform Hallo gegevens invoerstroom en Hallo uitvoer is waar Hallo taak Hallo taak resultaten verzendt.</span><span class="sxs-lookup"><span data-stu-id="ee600-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="ee600-111">Een taak vereist ten minste één invoerbron voor het streamen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ee600-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="ee600-112">Hallo kan invoerbron van de gegevensstroom worden opgeslagen in een Azure event hub of in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ee600-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="ee600-113">Zie voor meer informatie [inleiding tooAzure Stream Analytics](stream-analytics-introduction.md) en [aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="ee600-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="ee600-114">Partities in event hubs en Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="ee600-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="ee600-115">Schalen van een Stream Analytics-taak maakt gebruik van partities in Hallo invoer of uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="ee600-116">Hiermee kunt die u gegevens in op basis van een partitiesleutel subsets verdelen partitioneren.</span><span class="sxs-lookup"><span data-stu-id="ee600-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="ee600-117">Een proces dat Hallo-gegevens (zoals een Streaming Analytics-taak verbruikt) kunt gebruiken en het schrijven van verschillende partities parallel verhoogt de doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="ee600-118">Wanneer u met Streaming Analytics werkt, kunt u profiteren van partitionering in event hubs en in de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ee600-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="ee600-119">Zie voor meer informatie over partities Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ee600-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="ee600-120">Overzicht van Event Hubs-functies</span><span class="sxs-lookup"><span data-stu-id="ee600-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="ee600-121">Partitioneren van gegevens</span><span class="sxs-lookup"><span data-stu-id="ee600-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="ee600-122">Streaming-eenheden (SUs)</span><span class="sxs-lookup"><span data-stu-id="ee600-122">Streaming units (SUs)</span></span>
<span data-ttu-id="ee600-123">Streaming-eenheden (SUs) vertegenwoordigen Hallo bronnen en rekenkracht die vereist zijn in volgorde van tooexecute een Azure Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="ee600-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="ee600-124">SUs bieden een manier toodescribe Hallo relatieve gebeurtenisverwerking capaciteit op basis van een gecombineerde meting van CPU, geheugen, en lezen en schrijven tarieven.</span><span class="sxs-lookup"><span data-stu-id="ee600-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="ee600-125">Elke SU overeenkomt met tooroughly 1 MB per seconde van doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="ee600-126">Hoeveel SUs kiezen zijn vereist voor een bepaalde taak is afhankelijk van Hallo partitieconfiguratie voor Hallo invoer en gedefinieerd voor de taak Hallo Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="ee600-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="ee600-127">U kunt selecteren van tooyour quotum in SUs voor een taak.</span><span class="sxs-lookup"><span data-stu-id="ee600-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="ee600-128">Elk Azure-abonnement heeft standaard een quotum van up too50 SUs voor alle Hallo analytics-taken in een specifieke regio.</span><span class="sxs-lookup"><span data-stu-id="ee600-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="ee600-129">tooincrease SUs voor uw abonnementen buiten dit quotum, neem contact op met [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ee600-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="ee600-130">Geldige waarden voor SUs per taak zijn 1, 3, 6, en omhoog in stappen van 6.</span><span class="sxs-lookup"><span data-stu-id="ee600-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="ee600-131">Perfect parallelle taken</span><span class="sxs-lookup"><span data-stu-id="ee600-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="ee600-132">Een *perfect parallelle* taak is de meest schaalbare scenario Hallo we in Azure Stream Analytics hebben.</span><span class="sxs-lookup"><span data-stu-id="ee600-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="ee600-133">Deze verbinding maakt met één partitie van Hallo invoer tooone exemplaar van Hallo query tooone partitie van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="ee600-134">Deze parallelle uitvoering heeft Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="ee600-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="ee600-135">Als uw query logica is afhankelijk van Hallo sleutel wordt verwerkt door Hallo query dezelfde exemplaar, moet u ervoor zorgen dat het Hallo-gebeurtenissen toohello gaan dezelfde partitie van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="ee600-136">Voor event hubs, dit betekent dat de gebeurtenisgegevens Hallo moet Hallo **PartitionKey** waarde ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ee600-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="ee600-137">U kunt ook de gepartitioneerde afzenders gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee600-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="ee600-138">Voor blob-opslag, betekent dit dat dat Hallo gebeurtenissen toohello worden verzonden dezelfde partitie map.</span><span class="sxs-lookup"><span data-stu-id="ee600-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="ee600-139">Als uw query logica vereist geen Hallo sleutel toobe verwerkt door Hallo dezelfde exemplaar opvragen, kunt u deze vereiste negeren.</span><span class="sxs-lookup"><span data-stu-id="ee600-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="ee600-140">Een voorbeeld van deze logica is een eenvoudige select-project-filter-query.</span><span class="sxs-lookup"><span data-stu-id="ee600-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="ee600-141">Zodra het Hallo-gegevens worden verspreid Hallo invoer zijde, moet u ervoor zorgen dat uw query is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="ee600-142">Hiervoor moet u toouse **Partition By** in alle Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="ee600-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="ee600-143">Meerdere stappen zijn toegestaan, maar ze alle moeten worden gepartitioneerd door Hallo dezelfde sleutel.</span><span class="sxs-lookup"><span data-stu-id="ee600-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="ee600-144">Op dit moment Hallo partitiesleutel te moet worden ingesteld**PartitionId** om Hallo taak toobe volledig parallelle.</span><span class="sxs-lookup"><span data-stu-id="ee600-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="ee600-145">Alleen event hubs en blob-opslag ondersteund gepartitioneerde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="ee600-146">Event hub-uitvoer, moet u configureren Hallo partitie sleutel toobe **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="ee600-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="ee600-147">Voor blob storage-uitvoer hebt u geen toodo alles.</span><span class="sxs-lookup"><span data-stu-id="ee600-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="ee600-148">het aantal invoer partities Hallo moet gelijk zijn aan Hallo aantal partities van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="ee600-149">BLOB storage uitvoer ondersteunt momenteel geen partities.</span><span class="sxs-lookup"><span data-stu-id="ee600-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="ee600-150">Maar dat is geen probleem, omdat deze Hallo partitieschema van Hallo upstream-query.</span><span class="sxs-lookup"><span data-stu-id="ee600-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="ee600-151">Hier volgen voorbeelden van waarden van partitie waarmee een volledig parallelle taak:</span><span class="sxs-lookup"><span data-stu-id="ee600-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="ee600-152">8 event hub invoer partities en 8 event hub uitvoer partities</span><span class="sxs-lookup"><span data-stu-id="ee600-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="ee600-153">8 event hub invoer partities en uitvoer van blob-opslag</span><span class="sxs-lookup"><span data-stu-id="ee600-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="ee600-154">8 blob storage invoer partities en uitvoer van blob-opslag</span><span class="sxs-lookup"><span data-stu-id="ee600-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="ee600-155">8 blob-opslag invoer partities en 8 uitvoer partities van de event hub</span><span class="sxs-lookup"><span data-stu-id="ee600-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="ee600-156">Hallo volgende secties worden enkele voorbeeldscenario's die perfect parallelle zijn.</span><span class="sxs-lookup"><span data-stu-id="ee600-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="ee600-157">Eenvoudige query</span><span class="sxs-lookup"><span data-stu-id="ee600-157">Simple query</span></span>

* <span data-ttu-id="ee600-158">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-159">Uitvoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="ee600-160">Query:</span><span class="sxs-lookup"><span data-stu-id="ee600-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="ee600-161">Deze query is een eenvoudige filter.</span><span class="sxs-lookup"><span data-stu-id="ee600-161">This query is a simple filter.</span></span> <span data-ttu-id="ee600-162">We hebben daarom tooworry over partitioneren Hallo invoer die toohello event hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ee600-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="ee600-163">U ziet dat Hallo-query bevat **partitie door PartitionId**, zodat deze voldoet aan vereiste #2 van eerder.</span><span class="sxs-lookup"><span data-stu-id="ee600-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="ee600-164">Hallo-uitvoer moet tooconfigure Hallo event hub-uitvoer in Hallo taak toohave Hallo partitie sleutelset te**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="ee600-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="ee600-165">Een laatste controle is toomake ervoor dat het aantal invoer partities Hallo gelijk toohello aantal partities van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="ee600-166">Query's uitvoeren met een groeperingssleutel</span><span class="sxs-lookup"><span data-stu-id="ee600-166">Query with a grouping key</span></span>

* <span data-ttu-id="ee600-167">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-168">Uitvoer: Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="ee600-168">Output: Blob storage</span></span>

<span data-ttu-id="ee600-169">Query:</span><span class="sxs-lookup"><span data-stu-id="ee600-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="ee600-170">Deze query heeft een groeperingssleutel.</span><span class="sxs-lookup"><span data-stu-id="ee600-170">This query has a grouping key.</span></span> <span data-ttu-id="ee600-171">Daarom Hallo dezelfde sleutel behoeften toobe door Hallo dezelfde query exemplaar, wat betekent dat gebeurtenissen moeten worden verzonden toohello event hub in een gepartitioneerde wijze verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ee600-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="ee600-172">Maar welke sleutel moet worden gebruikt?</span><span class="sxs-lookup"><span data-stu-id="ee600-172">But which key should be used?</span></span> <span data-ttu-id="ee600-173">**PartitionId** een concept taak logica.</span><span class="sxs-lookup"><span data-stu-id="ee600-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="ee600-174">Hallo sleutel daadwerkelijk belangrijk voor ons is **TollBoothId**, dus Hallo **PartitionKey** waarde Hallo gebeurtenisgegevens moet **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="ee600-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="ee600-175">We dit doen in Hallo query door **Partition By** te**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="ee600-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="ee600-176">Omdat Hallo uitvoer blobopslag, moeten we niet tooworry over het configureren van een waarde voor de partitiesleutel, volgens de vereiste #4.</span><span class="sxs-lookup"><span data-stu-id="ee600-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="ee600-177">Meerdere stappen query met een groeperingssleutel</span><span class="sxs-lookup"><span data-stu-id="ee600-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="ee600-178">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-179">Uitvoer: Event hub-instantie met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="ee600-180">Query:</span><span class="sxs-lookup"><span data-stu-id="ee600-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="ee600-181">Deze query heeft een groeperingssleutel, zodat dezelfde sleutel behoeften toobe verwerkt door Hallo Hallo hetzelfde exemplaar van de query.</span><span class="sxs-lookup"><span data-stu-id="ee600-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="ee600-182">We kunnen gebruiken dezelfde strategie zoals in het vorige voorbeeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee600-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="ee600-183">In dit geval heeft Hallo query meerdere stappen.</span><span class="sxs-lookup"><span data-stu-id="ee600-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="ee600-184">Elke stap heeft **partitie door PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="ee600-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="ee600-185">Ja, dus Hallo query voldaan aan de vereiste #3.</span><span class="sxs-lookup"><span data-stu-id="ee600-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="ee600-186">Hallo-uitvoer moet tooset Hallo partitiesleutel te**PartitionId**, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="ee600-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="ee600-187">Ook ziet u dat er Hallo hetzelfde aantal partities als Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="ee600-188">Voorbeeldscenario's die zijn *niet* perfect parallelle</span><span class="sxs-lookup"><span data-stu-id="ee600-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="ee600-189">In de vorige sectie hello bleek we enkele perfect parallelle scenario's.</span><span class="sxs-lookup"><span data-stu-id="ee600-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="ee600-190">In deze sectie bespreken we scenario's die niet voldoen aan vereisten toobe alle Hallo perfect parallelle.</span><span class="sxs-lookup"><span data-stu-id="ee600-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="ee600-191">Aantal niet-overeenkomende partities</span><span class="sxs-lookup"><span data-stu-id="ee600-191">Mismatched partition count</span></span>
* <span data-ttu-id="ee600-192">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-193">Uitvoer: Event hub met 32 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="ee600-194">In dit geval wordt het maakt niet uit welke Hallo-query is.</span><span class="sxs-lookup"><span data-stu-id="ee600-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="ee600-195">Als Hallo invoer partitie aantal komt niet overeen met de Hallo uitvoer partitie count, Hallo topologie niet perfect parallelle.</span><span class="sxs-lookup"><span data-stu-id="ee600-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="ee600-196">Geen gebruikmaakt van event hubs of blob-opslag als uitvoer</span><span class="sxs-lookup"><span data-stu-id="ee600-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="ee600-197">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-198">Uitvoer: Power BI</span><span class="sxs-lookup"><span data-stu-id="ee600-198">Output: PowerBI</span></span>

<span data-ttu-id="ee600-199">Power BI-uitvoer ondersteunt momenteel geen partitioneren.</span><span class="sxs-lookup"><span data-stu-id="ee600-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="ee600-200">Dit scenario is daarom niet perfect parallelle.</span><span class="sxs-lookup"><span data-stu-id="ee600-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="ee600-201">De query meerdere stappen met verschillende waarden voor Partition By</span><span class="sxs-lookup"><span data-stu-id="ee600-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="ee600-202">Invoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="ee600-203">Uitvoer: Event hub, met 8 partities</span><span class="sxs-lookup"><span data-stu-id="ee600-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="ee600-204">Query:</span><span class="sxs-lookup"><span data-stu-id="ee600-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="ee600-205">Zoals u ziet, gebruikmaakt van de tweede stap Hallo **TollBoothId** als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee600-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="ee600-206">Deze stap is dezelfde niet Hallo als eerste stap hello, en daarom vereist ons toodo een willekeurige volgorde.</span><span class="sxs-lookup"><span data-stu-id="ee600-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="ee600-207">Hallo voorgaande voorbeelden ziet u enkele Stream Analytics-taken die een perfect parallelle topologie te voldoen (of niet).</span><span class="sxs-lookup"><span data-stu-id="ee600-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="ee600-208">Als die in overeenstemming zijn, hebben ze Hallo mogelijkheden voor maximale schaal.</span><span class="sxs-lookup"><span data-stu-id="ee600-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="ee600-209">Voor taken die niet voldoen aan een van deze profielen schalen richtlijnen beschikbaar in toekomstige zijn updates.</span><span class="sxs-lookup"><span data-stu-id="ee600-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="ee600-210">Op dit moment gebruiken Hallo algemene richtlijnen in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ee600-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="ee600-211">Hallo maximale streaming-eenheden van een taak berekenen</span><span class="sxs-lookup"><span data-stu-id="ee600-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="ee600-212">Totaal aantal streaming-eenheden die kunnen worden gebruikt door een Stream Analytics-taak Hallo is afhankelijk van Hallo aantal stappen in Hallo query gedefinieerd voor het Hallo-taak en Hallo aantal partities voor elke stap.</span><span class="sxs-lookup"><span data-stu-id="ee600-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="ee600-213">De stappen in een query</span><span class="sxs-lookup"><span data-stu-id="ee600-213">Steps in a query</span></span>
<span data-ttu-id="ee600-214">Een query kan één of meerdere stappen hebben.</span><span class="sxs-lookup"><span data-stu-id="ee600-214">A query can have one or many steps.</span></span> <span data-ttu-id="ee600-215">Elke stap bestaat uit een subquery die zijn gedefinieerd door Hallo **WITH** sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="ee600-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="ee600-216">Hallo-query die buiten Hallo **WITH** sleutelwoord (slechts één query) ook wordt beschouwd als een stap, zoals Hallo **Selecteer** instructie in de volgende query Hallo:</span><span class="sxs-lookup"><span data-stu-id="ee600-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="ee600-217">Deze query bestaat uit twee stappen.</span><span class="sxs-lookup"><span data-stu-id="ee600-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="ee600-218">Deze query wordt later in Hallo artikel nader besproken.</span><span class="sxs-lookup"><span data-stu-id="ee600-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="ee600-219">Een stap partitioneren</span><span class="sxs-lookup"><span data-stu-id="ee600-219">Partition a step</span></span>
<span data-ttu-id="ee600-220">Een stap partitioneren vereist Hallo volgende voorwaarden:</span><span class="sxs-lookup"><span data-stu-id="ee600-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="ee600-221">de invoerbron Hallo moet worden gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="ee600-222">Hallo **Selecteer** -instructie van Hallo query moet lezen van een gepartitioneerde invoerbron.</span><span class="sxs-lookup"><span data-stu-id="ee600-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="ee600-223">Hallo query binnen Hallo stap Hallo moet hebben **Partition By** sleutelwoord.</span><span class="sxs-lookup"><span data-stu-id="ee600-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="ee600-224">Wanneer een query is gepartitioneerd, Hallo invoervelden zijn verwerkt en geaggregeerde in afzonderlijke partitiegroepen en uitvoer gebeurtenissen worden gegenereerd voor elk van de groepen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ee600-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="ee600-225">Als u een gecombineerde aggregaat wilt, moet u een tweede stap niet-gepartitioneerde tooaggregate maken.</span><span class="sxs-lookup"><span data-stu-id="ee600-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="ee600-226">Hallo max streaming-eenheden voor een taak berekenen</span><span class="sxs-lookup"><span data-stu-id="ee600-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="ee600-227">Alle niet-gepartitioneerde stappen kunnen samen opschalen toosix streaming-eenheden (SUs) voor een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="ee600-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="ee600-228">SUs tooadd, een stap moeten worden gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="ee600-229">Elke partitie kan zes SUs hebben.</span><span class="sxs-lookup"><span data-stu-id="ee600-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="ee600-230">Query’s uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ee600-230">Query</span></span></th><th><span data-ttu-id="ee600-231">Maximale SUs voor Hallo-taak</span><span class="sxs-lookup"><span data-stu-id="ee600-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="ee600-232">Hallo-query bevat één stap.</span><span class="sxs-lookup"><span data-stu-id="ee600-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="ee600-233">Hallo stap niet is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="ee600-234">6</span><span class="sxs-lookup"><span data-stu-id="ee600-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="ee600-235">Hallo invoergegevens stream is gepartitioneerd met 3.</span><span class="sxs-lookup"><span data-stu-id="ee600-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="ee600-236">Hallo-query bevat één stap.</span><span class="sxs-lookup"><span data-stu-id="ee600-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="ee600-237">Hallo stap is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="ee600-238">18</span><span class="sxs-lookup"><span data-stu-id="ee600-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="ee600-239">Hallo-query bevat twee stappen.</span><span class="sxs-lookup"><span data-stu-id="ee600-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="ee600-240">Geen van de stappen Hallo is gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="ee600-241">6</span><span class="sxs-lookup"><span data-stu-id="ee600-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="ee600-242">Hallo invoergegevens stream is gepartitioneerd met 3.</span><span class="sxs-lookup"><span data-stu-id="ee600-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="ee600-243">Hallo-query bevat twee stappen.</span><span class="sxs-lookup"><span data-stu-id="ee600-243">hello query contains two steps.</span></span> <span data-ttu-id="ee600-244">Hallo invoer stap is gepartitioneerd en Hallo tweede stap bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="ee600-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="ee600-245">Hallo <strong>Selecteer</strong> instructie leest uit Hallo gepartitioneerd invoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="ee600-246">24 (18 voor gepartitioneerde stappen) + 6 voor niet-gepartitioneerde stappen</span><span class="sxs-lookup"><span data-stu-id="ee600-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="ee600-247">Voorbeelden van schaal</span><span class="sxs-lookup"><span data-stu-id="ee600-247">Examples of scaling</span></span>

<span data-ttu-id="ee600-248">Hallo berekent volgende query Hallo aantal auto's binnen een drie minuten een gratis-station met drie tollbooths doorlopen.</span><span class="sxs-lookup"><span data-stu-id="ee600-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="ee600-249">Deze query kan worden uitgebreid toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="ee600-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="ee600-250">meer toouse SUs voor Hallo query, zowel de stroom inkomende gegevens Hallo en Hallo query moet worden gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="ee600-251">Omdat Hallo gegevensstroom partitie is too3 ingesteld, kan hello volgende gewijzigde query worden uitgebreid too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="ee600-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="ee600-252">Wanneer een query is gepartitioneerd, worden de invoervelden Hallo verwerkt en geaggregeerd in een afzonderlijke partitiegroepen.</span><span class="sxs-lookup"><span data-stu-id="ee600-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="ee600-253">Uitvoergebeurtenissen worden ook gegenereerd voor elk van Hallo groepen.</span><span class="sxs-lookup"><span data-stu-id="ee600-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="ee600-254">Partitioneren kan leiden tot enige onverwachte resultaten hello **GROUP BY** veld is niet de partitiesleutel Hallo in Hallo invoergegevens stroom.</span><span class="sxs-lookup"><span data-stu-id="ee600-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="ee600-255">Bijvoorbeeld, Hallo **TollBoothId** veld in de vorige query Hallo is niet de partitiesleutel Hallo van **Input1**.</span><span class="sxs-lookup"><span data-stu-id="ee600-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="ee600-256">Hallo-resultaat is dat Hallo gegevens van tolhuisje #1 in meerdere partities kunnen worden verspreid.</span><span class="sxs-lookup"><span data-stu-id="ee600-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="ee600-257">Elk Hallo **Input1** partities afzonderlijk wordt verwerkt door de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="ee600-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="ee600-258">Als gevolg hiervan Hallo meerdere records van het Hallo auto aantal voor dezelfde tolhuisje in Hallo dezelfde tumblingvenster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ee600-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="ee600-259">Als de invoer partitiesleutel Hallo kan niet worden gewijzigd, kan dit probleem worden opgelost door een niet-partitie stap, zoals in het volgende voorbeeld Hallo toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="ee600-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="ee600-260">Deze query kan worden geschaald too24 SUs.</span><span class="sxs-lookup"><span data-stu-id="ee600-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="ee600-261">Als u van twee streams samenvoegen, ervoor zorgen dat Hallo stromen worden gepartitioneerd met de partitiesleutel Hallo van Hallo kolom toocreate Hallo joins te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ee600-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="ee600-262">Controleer ook of u hebt Hallo hetzelfde aantal partities in beide stromen.</span><span class="sxs-lookup"><span data-stu-id="ee600-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="ee600-263">Configureren van de Stream Analytics streaming-eenheden</span><span class="sxs-lookup"><span data-stu-id="ee600-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="ee600-264">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee600-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ee600-265">Vinden in de lijst met resources Hallo Hallo Stream Analytics-taak dat u wilt dat tooscale en het open.</span><span class="sxs-lookup"><span data-stu-id="ee600-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="ee600-266">Taak in Hallo blade onder **configureren**, klikt u op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="ee600-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure Stream Analytics-taak Portalconfiguratie][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="ee600-268">Gebruik Hallo schuifregelaar tooset Hallo SUs voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="ee600-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="ee600-269">U ziet dat u beperkte toospecific SU-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ee600-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="ee600-270">Prestaties van de taak controleren</span><span class="sxs-lookup"><span data-stu-id="ee600-270">Monitor job performance</span></span>
<span data-ttu-id="ee600-271">Hello Azure-portal kunt u Hallo doorvoer van een taak volgen:</span><span class="sxs-lookup"><span data-stu-id="ee600-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Azure Stream Analytics-taken voor monitor][img.stream.analytics.monitor.job]

<span data-ttu-id="ee600-273">Hallo verwacht doorvoer van Hallo werkbelasting berekenen.</span><span class="sxs-lookup"><span data-stu-id="ee600-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="ee600-274">Als Hallo doorvoer kleiner is dan verwacht, Hallo invoer partitie afstemmen, Hallo query afstemmen en SUs tooyour taak toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ee600-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="ee600-275">Stream Analytics-doorvoer op grote schaal visualiseren: Hallo frambozen Pi scenario</span><span class="sxs-lookup"><span data-stu-id="ee600-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="ee600-276">toohelp die u begrijpt hoe de Stream Analytics-taken schalen, hebben we een experiment op basis van de invoer van een apparaat frambozen Pi uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="ee600-277">Dit experiment laat ons zien Hallo effect op de doorvoer van meerdere streaming-eenheden en partities.</span><span class="sxs-lookup"><span data-stu-id="ee600-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="ee600-278">In dit scenario wordt met Hallo apparaat sensor gegevens (clients) tooan event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="ee600-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="ee600-279">Streaming Analytics Hallo gegevens verwerkt en verzendt een waarschuwing of -statistieken als een output tooanother event hub.</span><span class="sxs-lookup"><span data-stu-id="ee600-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="ee600-280">Hallo-client verzendt sensorgegevens in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ee600-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="ee600-281">Hallo gegevensuitvoer is ook in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ee600-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="ee600-282">Hallo gegevens ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="ee600-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="ee600-283">Hallo na query is gebruikt toosend een waarschuwing wanneer een licht is uitgeschakeld:</span><span class="sxs-lookup"><span data-stu-id="ee600-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="ee600-284">Meting doorvoer</span><span class="sxs-lookup"><span data-stu-id="ee600-284">Measure throughput</span></span>

<span data-ttu-id="ee600-285">In deze context is doorvoer Hallo hoeveelheid invoergegevens verwerkt door de Stream Analytics in een vaste hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="ee600-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="ee600-286">(We gemeten voor 10 minuten.) invoergegevens tooachieve Hallo best verwerking doorvoer voor hello, beide Hallo gegevensstroom invoer en Hallo query zijn gepartitioneerd.</span><span class="sxs-lookup"><span data-stu-id="ee600-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="ee600-287">We opgenomen **COUNT()** in Hallo query toomeasure hoeveel invoervelden zijn verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ee600-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="ee600-288">toomake ervoor Hallo-taak is gewoon wacht niet invoervelden toocome, elke partitie van Hallo invoer event hub is vooraf geladen met ongeveer 300 MB met invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="ee600-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="ee600-289">Hallo toont volgende tabel Hallo resultaten die hebt gezien wanneer we het aantal streaming-eenheden Hallo verhoogd en de overeenkomstige partitie Hallo in event hubs telt.</span><span class="sxs-lookup"><span data-stu-id="ee600-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="ee600-290">Invoer partities</span><span class="sxs-lookup"><span data-stu-id="ee600-290">Input Partitions</span></span></th><th><span data-ttu-id="ee600-291">Uitvoer partities</span><span class="sxs-lookup"><span data-stu-id="ee600-291">Output Partitions</span></span></th><th><span data-ttu-id="ee600-292">Streamingeenheden</span><span class="sxs-lookup"><span data-stu-id="ee600-292">Streaming Units</span></span></th><th><span data-ttu-id="ee600-293">Volgehouden doorvoer</span><span class="sxs-lookup"><span data-stu-id="ee600-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="ee600-294">12</span><span class="sxs-lookup"><span data-stu-id="ee600-294">12</span></span></td>
<td><span data-ttu-id="ee600-295">12</span><span class="sxs-lookup"><span data-stu-id="ee600-295">12</span></span></td>
<td><span data-ttu-id="ee600-296">6</span><span class="sxs-lookup"><span data-stu-id="ee600-296">6</span></span></td>
<td><span data-ttu-id="ee600-297">4.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="ee600-298">12</span><span class="sxs-lookup"><span data-stu-id="ee600-298">12</span></span></td>
<td><span data-ttu-id="ee600-299">12</span><span class="sxs-lookup"><span data-stu-id="ee600-299">12</span></span></td>
<td><span data-ttu-id="ee600-300">12</span><span class="sxs-lookup"><span data-stu-id="ee600-300">12</span></span></td>
<td><span data-ttu-id="ee600-301">8.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="ee600-302">48</span><span class="sxs-lookup"><span data-stu-id="ee600-302">48</span></span></td>
<td><span data-ttu-id="ee600-303">48</span><span class="sxs-lookup"><span data-stu-id="ee600-303">48</span></span></td>
<td><span data-ttu-id="ee600-304">48</span><span class="sxs-lookup"><span data-stu-id="ee600-304">48</span></span></td>
<td><span data-ttu-id="ee600-305">38.32 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="ee600-306">192</span><span class="sxs-lookup"><span data-stu-id="ee600-306">192</span></span></td>
<td><span data-ttu-id="ee600-307">192</span><span class="sxs-lookup"><span data-stu-id="ee600-307">192</span></span></td>
<td><span data-ttu-id="ee600-308">192</span><span class="sxs-lookup"><span data-stu-id="ee600-308">192</span></span></td>
<td><span data-ttu-id="ee600-309">172.67 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="ee600-310">480</span><span class="sxs-lookup"><span data-stu-id="ee600-310">480</span></span></td>
<td><span data-ttu-id="ee600-311">480</span><span class="sxs-lookup"><span data-stu-id="ee600-311">480</span></span></td>
<td><span data-ttu-id="ee600-312">480</span><span class="sxs-lookup"><span data-stu-id="ee600-312">480</span></span></td>
<td><span data-ttu-id="ee600-313">454.27 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="ee600-314">720</span><span class="sxs-lookup"><span data-stu-id="ee600-314">720</span></span></td>
<td><span data-ttu-id="ee600-315">720</span><span class="sxs-lookup"><span data-stu-id="ee600-315">720</span></span></td>
<td><span data-ttu-id="ee600-316">720</span><span class="sxs-lookup"><span data-stu-id="ee600-316">720</span></span></td>
<td><span data-ttu-id="ee600-317">609.69 MB/s</span><span class="sxs-lookup"><span data-stu-id="ee600-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="ee600-318">En hello volgende grafiek ziet u een visualisatie van Hallo relatie tussen SUs en doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ee600-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![IMG.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="ee600-320">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="ee600-320">Get help</span></span>
<span data-ttu-id="ee600-321">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ee600-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee600-322">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee600-322">Next steps</span></span>
* [<span data-ttu-id="ee600-323">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee600-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ee600-324">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ee600-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ee600-325">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="ee600-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ee600-326">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="ee600-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

