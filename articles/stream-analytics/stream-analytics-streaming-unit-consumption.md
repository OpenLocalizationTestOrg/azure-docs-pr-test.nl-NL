---
title: "Azure Stream Analytics: Uw taak toouse Streaming-eenheden efficiënt optimaliseren | Microsoft Docs"
description: Aanbevolen procedures voor schaalbaarheid en prestaties in Azure Stream Analytics query.
keywords: Streaming-eenheid, de prestaties van query 's
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="da77a-104">Efficiënt optimaliseren van uw taak toouse Streaming-eenheden</span><span class="sxs-lookup"><span data-stu-id="da77a-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="da77a-105">Azure Stream Analytics aggregeert Hallo prestaties 'gewicht' van een taak die worden uitgevoerd in de Streaming-eenheden (SUs).</span><span class="sxs-lookup"><span data-stu-id="da77a-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="da77a-106">SUs vertegenwoordigen Hallo computerbronnen die verbruikte tooexecute een taak.</span><span class="sxs-lookup"><span data-stu-id="da77a-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="da77a-107">SUs bieden een manier toodescribe Hallo relatieve gebeurtenisverwerking capaciteit op basis van een gecombineerde meting van CPU, geheugen, en lezen en schrijven tarieven.</span><span class="sxs-lookup"><span data-stu-id="da77a-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="da77a-108">Met deze capaciteit kunt u zich richten op Hallo query logica en verwijdert u uit prestatieoverwegingen voor tooknow storage-laag, hoeven handmatig geheugen toewijzen voor uw werk en Hallo CPU core-aantal nodig toorun van uw werk tijdig benaderen.</span><span class="sxs-lookup"><span data-stu-id="da77a-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="da77a-109">Hoeveel SUs zijn vereist voor een taak?</span><span class="sxs-lookup"><span data-stu-id="da77a-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="da77a-110">Aantal vereiste SUs voor een bepaalde taak Hallo kiezen, is afhankelijk van Hallo partitieconfiguratie voor Hallo invoer en Hallo-query die gedefinieerd binnen het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="da77a-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="da77a-111">Hallo **Scale** blade kunt u tooset Hallo rechts aantal SUs.</span><span class="sxs-lookup"><span data-stu-id="da77a-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="da77a-112">Het is een best practices tooallocate meer SUs dan nodig.</span><span class="sxs-lookup"><span data-stu-id="da77a-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="da77a-113">Hallo-verwerkingsengine Stream Analytics geoptimaliseerd voor latentie en doorvoer op Hallo kosten voor het toewijzen van extra geheugen.</span><span class="sxs-lookup"><span data-stu-id="da77a-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="da77a-114">Hallo aanbevolen procedure is over het algemeen toostart met 6 SUs voor query's die geen gebruikmaken van *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="da77a-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="da77a-115">Vervolgens Hallo sweet positie vast door een vallen en opstaan methode waarin u het aantal SUs Hallo wijzigen nadat u representatieve hoeveelheden gegevens doorgeven en hello SU % gebruik metrische gegevens bekijkt.</span><span class="sxs-lookup"><span data-stu-id="da77a-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="da77a-116">Azure Stream Analytics houdt gebeurtenissen in een venster Hallo 'opnieuw ordenen buffer' aangeroepen voordat er begonnen wordt met de verwerking.</span><span class="sxs-lookup"><span data-stu-id="da77a-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="da77a-117">Gebeurtenissen binnen Hallo bestellen venster zijn gesorteerd op basis van tijd en verdere bewerkingen worden uitgevoerd op Hallo ondersteuningsbeheerder gesorteerd gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="da77a-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="da77a-118">Volgorde van gebeurtenissen door de tijd, zorgt u ervoor dat Hallo-operator heeft inzicht in alle gebeurtenissen in Hallo Hallo bepaald tijdsbestek.</span><span class="sxs-lookup"><span data-stu-id="da77a-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="da77a-119">U kunt hiermee ook Hallo operator Hallo vereiste bewerkingen uitvoeren en uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="da77a-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="da77a-120">Een neveneffect van deze methode is dat verwerking door de duur Hallo van Hallo bestellen venster wordt vertraagd.</span><span class="sxs-lookup"><span data-stu-id="da77a-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="da77a-121">Hallo geheugengebruik van Hallo taak (die van invloed op een SU verbruik) is een functie van Hallo grootte van deze opnieuw ordenen venster en Hallo aantal gebeurtenissen die hierin zijn opgenomen.</span><span class="sxs-lookup"><span data-stu-id="da77a-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="da77a-122">Wanneer het aantal lezers Hallo tijdens upgrades van de taak wordt gewijzigd, worden waarschuwingen voor tijdelijke tooaudit Logboeken geschreven.</span><span class="sxs-lookup"><span data-stu-id="da77a-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="da77a-123">Stream Analytics-taken worden automatisch herstellen van deze problemen van voorbijgaande aard.</span><span class="sxs-lookup"><span data-stu-id="da77a-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="da77a-124">Algemene high memory oorzaken voor gebruik van hoge SU voor het uitvoeren van taken</span><span class="sxs-lookup"><span data-stu-id="da77a-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="da77a-125">Hoge kardinaliteit voor GROEPEREN op</span><span class="sxs-lookup"><span data-stu-id="da77a-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="da77a-126">Hallo kardinaliteit van binnenkomende gebeurtenissen bepaalt geheugengebruik voor Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="da77a-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="da77a-127">Bijvoorbeeld in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, dat is gekoppeld aan Hallo **geclusterde** Hallo kardinaliteit van Hallo-query is.</span><span class="sxs-lookup"><span data-stu-id="da77a-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="da77a-128">Hallo query toomitigate problemen die worden veroorzaakt door hoge kardinaliteit uitbreiden door te verhogen met partities **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="da77a-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="da77a-129">aantal Hallo *geclusterde* Hallo kardinaliteit van GROUP BY hier is.</span><span class="sxs-lookup"><span data-stu-id="da77a-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="da77a-130">Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="da77a-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="da77a-131">Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer.</span><span class="sxs-lookup"><span data-stu-id="da77a-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="da77a-132">U moet ook de event hub partities partitioneren door partitionid.</span><span class="sxs-lookup"><span data-stu-id="da77a-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="da77a-133">Aantal hoge niet-overeenkomende gebeurtenissen voor de JOIN</span><span class="sxs-lookup"><span data-stu-id="da77a-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="da77a-134">Hallo aantal niet-overeenkomende gebeurtenissen in een JOIN is van invloed op Hallo geheugengebruik van Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="da77a-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="da77a-135">Neem bijvoorbeeld een query die toofind Hallo aantal ad hits die klikken genereert is op zoek:</span><span class="sxs-lookup"><span data-stu-id="da77a-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="da77a-136">In dit scenario is het mogelijk dat veel advertenties worden weergegeven en enkele muisklikken worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="da77a-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="da77a-137">Dergelijke resultaat moet alle Hallo gebeurtenissen binnen tijdvenster Hallo Hallo taak tookeep.</span><span class="sxs-lookup"><span data-stu-id="da77a-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="da77a-138">Hallo hoeveelheid gebruikt geheugen is evenredig toohello venster grootte en gebeurtenis-snelheid.</span><span class="sxs-lookup"><span data-stu-id="da77a-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="da77a-139">toomitigate partities van deze situatie scale-out Hallo query door te verhogen met behulp van PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="da77a-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="da77a-140">Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten van de verwerking.</span><span class="sxs-lookup"><span data-stu-id="da77a-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="da77a-141">Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer.</span><span class="sxs-lookup"><span data-stu-id="da77a-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="da77a-142">Groot aantal gebeurtenissen in andere volgorde</span><span class="sxs-lookup"><span data-stu-id="da77a-142">Large number of out of order events</span></span> 

<span data-ttu-id="da77a-143">Een groot aantal gebeurtenissen in andere volgorde binnen een grote tijdvenster zorgt ervoor dat Hallo grootte van Hallo 'rangschikken buffer' toobe groter.</span><span class="sxs-lookup"><span data-stu-id="da77a-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="da77a-144">toomitigate partities van deze situatie scale Hallo query door te verhogen met behulp van PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="da77a-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="da77a-145">Nadat het Hallo-query is gepartitioneerd, wordt deze zich verdeeld over meerdere knooppunten.</span><span class="sxs-lookup"><span data-stu-id="da77a-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="da77a-146">Als gevolg hiervan Hallo aantal gebeurtenissen die afkomstig zijn in elk knooppunt verminderd die op zijn beurt verkleint Hallo Hallo bestellen buffer.</span><span class="sxs-lookup"><span data-stu-id="da77a-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="da77a-147">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="da77a-147">Get help</span></span>
<span data-ttu-id="da77a-148">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="da77a-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da77a-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da77a-149">Next steps</span></span>
* [<span data-ttu-id="da77a-150">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="da77a-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="da77a-151">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="da77a-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="da77a-152">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="da77a-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="da77a-153">Azure Stream Analytics query language reference</span><span class="sxs-lookup"><span data-stu-id="da77a-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="da77a-154">Naslaginformatie over Azure Stream Analytics Management REST-API</span><span class="sxs-lookup"><span data-stu-id="da77a-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
