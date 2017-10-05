---
title: Fouten opsporen in Azure Stream Analytics met event hub-ontvangers | Microsoft Docs
description: Aanbevolen procedures voor het overwegen van Event Hubs consumer-groepen in de Stream Analytics-taken opvragen.
keywords: limiet van Event hub, klantengroep
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
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="8f801-104">Fouten opsporen in Azure Stream Analytics met event hub-ontvangers</span><span class="sxs-lookup"><span data-stu-id="8f801-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="8f801-105">U kunt Azure Event Hubs in Azure Stream Analytics opnemen of gegevens uit een taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8f801-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="8f801-106">Er is een best practice voor het gebruik van Event Hubs meerdere consumergroepen gebruiken om te controleren of de taak schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="8f801-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="8f801-107">Een reden hiervoor is dat het aantal lezers in de Stream Analytics-taak voor een specifieke invoer betrekking heeft op het aantal lezers in een enkel consumergroep.</span><span class="sxs-lookup"><span data-stu-id="8f801-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="8f801-108">Het exacte aantal ontvangers is gebaseerd op interne implementatiedetails voor de scale-out-topologie-logica.</span><span class="sxs-lookup"><span data-stu-id="8f801-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="8f801-109">Het aantal ontvangers is extern niet toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="8f801-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="8f801-110">Het aantal lezers kunt wijzigen op de begintijd van taak of tijdens upgrades van de taak.</span><span class="sxs-lookup"><span data-stu-id="8f801-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="8f801-111">Wanneer het aantal lezers gewijzigd tijdens de upgrade van een taak, worden naar het controlelogboeken tijdelijke waarschuwingen geschreven.</span><span class="sxs-lookup"><span data-stu-id="8f801-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="8f801-112">Stream Analytics-taken worden automatisch herstellen van deze problemen van voorbijgaande aard.</span><span class="sxs-lookup"><span data-stu-id="8f801-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="8f801-113">Het aantal lezers per partitie overschrijdt de limiet van vijf Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8f801-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="8f801-114">Scenario's waarin het aantal lezers per partitie de Event Hubs-limiet van vijf overschrijdt omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="8f801-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="8f801-115">Meerdere SELECT-instructies: als u meerdere SELECT-instructies die naar verwijzen **dezelfde** event hub-invoer, elke SELECT-instructie zorgt ervoor dat een nieuwe ontvanger worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f801-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="8f801-116">UNION: Wanneer u een UNION, het is mogelijk om meerdere invoerwaarden die naar verwijzen de **dezelfde** event hub- en groep.</span><span class="sxs-lookup"><span data-stu-id="8f801-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="8f801-117">SELF-join: Bij gebruik van een SELF JOIN-bewerking is het mogelijk om te verwijzen naar de **dezelfde** event hub meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="8f801-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="8f801-118">Oplossing</span><span class="sxs-lookup"><span data-stu-id="8f801-118">Solution</span></span>

<span data-ttu-id="8f801-119">De volgende aanbevolen procedures verminderen scenario's waarin het aantal lezers per partitie de limiet van vijf voor Event Hubs overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="8f801-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="8f801-120">Uw query splitsen in meerdere stappen met behulp van een WITH-component</span><span class="sxs-lookup"><span data-stu-id="8f801-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="8f801-121">De component WITH Hiermee geeft u een tijdelijk benoemde resultatenset die door een FROM-component in de query kan worden verwezen.</span><span class="sxs-lookup"><span data-stu-id="8f801-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="8f801-122">De component WITH wordt gedefinieerd in het bereik van de uitvoering van één SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="8f801-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="8f801-123">Bijvoorbeeld, in plaats van deze query:</span><span class="sxs-lookup"><span data-stu-id="8f801-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="8f801-124">Gebruik deze query:</span><span class="sxs-lookup"><span data-stu-id="8f801-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="8f801-125">Zorg ervoor dat de invoer aan verschillende groepen consumenten binden</span><span class="sxs-lookup"><span data-stu-id="8f801-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="8f801-126">Voor query's waarin drie of meer invoerwaarden zijn verbonden met de dezelfde consumergroep van Event Hubs, afzonderlijke consumergroepen te maken.</span><span class="sxs-lookup"><span data-stu-id="8f801-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="8f801-127">Dit is vereist voor het maken van aanvullende Stream Analytics-invoer.</span><span class="sxs-lookup"><span data-stu-id="8f801-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="8f801-128">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="8f801-128">Get help</span></span>
<span data-ttu-id="8f801-129">Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8f801-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f801-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f801-130">Next steps</span></span>
* [<span data-ttu-id="8f801-131">Inleiding tot Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8f801-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8f801-132">Aan de slag met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8f801-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8f801-133">Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="8f801-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8f801-134">Naslaggids voor stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="8f801-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8f801-135">Stream Analytics management REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="8f801-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
