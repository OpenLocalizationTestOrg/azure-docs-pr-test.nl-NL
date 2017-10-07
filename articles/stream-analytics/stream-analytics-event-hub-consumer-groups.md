---
title: Azure Stream Analytics aaaDebug met event hub-ontvangers | Microsoft Docs
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="ea72d-104">Fouten opsporen in Azure Stream Analytics met event hub-ontvangers</span><span class="sxs-lookup"><span data-stu-id="ea72d-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="ea72d-105">U kunt Azure Event Hubs in Azure Stream Analytics tooingest of uitvoer gegevens uit een taak.</span><span class="sxs-lookup"><span data-stu-id="ea72d-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="ea72d-106">Is een best practice voor het gebruik van Event Hubs toouse meerdere consumergroepen, tooensure taak schaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="ea72d-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="ea72d-107">Een reden hiervoor is dat het aantal lezers in Stream Analytics-taak voor een specifieke invoer Hallo Hallo betrekking heeft op Hallo aantal lezers in een enkel consumergroep.</span><span class="sxs-lookup"><span data-stu-id="ea72d-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="ea72d-108">Hallo exacte aantal ontvangers is gebaseerd op interne implementatiedetails voor Hallo scale-out topologie logica.</span><span class="sxs-lookup"><span data-stu-id="ea72d-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="ea72d-109">Hallo aantal ontvangers is extern niet toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="ea72d-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="ea72d-110">het aantal lezers Hallo kunt wijzigen tijdens het Hallo taak starten of tijdens upgrades van de taak.</span><span class="sxs-lookup"><span data-stu-id="ea72d-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="ea72d-111">Wanneer het aantal lezers Hallo gewijzigd tijdens de upgrade van een taak, worden waarschuwingen voor tijdelijke tooaudit Logboeken geschreven.</span><span class="sxs-lookup"><span data-stu-id="ea72d-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="ea72d-112">Stream Analytics-taken worden automatisch herstellen van deze problemen van voorbijgaande aard.</span><span class="sxs-lookup"><span data-stu-id="ea72d-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="ea72d-113">Het aantal lezers per partitie overschrijdt de limiet van vijf Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ea72d-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="ea72d-114">Scenario's in welke Hallo het aantal lezers per partitie Hallo Event Hubs limiet van vijf overschrijdt zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ea72d-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="ea72d-115">Meerdere SELECT-instructies: als u meerdere SELECT-instructies die te verwijzen**dezelfde** event hub-invoer, elke SELECT-instructie zorgt ervoor dat een nieuwe ontvanger toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea72d-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="ea72d-116">UNION: Wanneer u een UNION gebruikt, is het mogelijk toohave meerdere invoerwaarden die toohello verwijzen **dezelfde** event hub- en groep.</span><span class="sxs-lookup"><span data-stu-id="ea72d-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="ea72d-117">SELF-join: Wanneer u een SELF JOIN-bewerking gebruikt, is het mogelijk toorefer toohello **dezelfde** event hub meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="ea72d-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="ea72d-118">Oplossing</span><span class="sxs-lookup"><span data-stu-id="ea72d-118">Solution</span></span>

<span data-ttu-id="ea72d-119">Hallo kunnen volgende best practices verminderen in welke Hallo het aantal lezers per partitie Hallo Event Hubs limiet van vijf overschrijdt scenario's.</span><span class="sxs-lookup"><span data-stu-id="ea72d-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="ea72d-120">Uw query splitsen in meerdere stappen met behulp van een WITH-component</span><span class="sxs-lookup"><span data-stu-id="ea72d-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="ea72d-121">de component WITH Hallo Hiermee geeft u een tijdelijk benoemde resultatenset die kan worden verwezen door een FROM-component in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="ea72d-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="ea72d-122">U definieert Hallo WITH-clausule in Hallo uitvoering bereik van één SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="ea72d-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="ea72d-123">Bijvoorbeeld, in plaats van deze query:</span><span class="sxs-lookup"><span data-stu-id="ea72d-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="ea72d-124">Gebruik deze query:</span><span class="sxs-lookup"><span data-stu-id="ea72d-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="ea72d-125">Zorg ervoor dat de invoer toodifferent consumergroepen binden</span><span class="sxs-lookup"><span data-stu-id="ea72d-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="ea72d-126">Voor query's waarin drie of meer invoerwaarden verbonden toohello zijn dezelfde Event Hubs consumer groep, maakt u afzonderlijke consumer-groepen.</span><span class="sxs-lookup"><span data-stu-id="ea72d-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="ea72d-127">U moet hiervoor Hallo maken van aanvullende Stream Analytics-invoer.</span><span class="sxs-lookup"><span data-stu-id="ea72d-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="ea72d-128">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="ea72d-128">Get help</span></span>
<span data-ttu-id="ea72d-129">Voor meer informatie en ondersteuning kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="ea72d-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea72d-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea72d-130">Next steps</span></span>
* [<span data-ttu-id="ea72d-131">Inleiding tooStream Analytics</span><span class="sxs-lookup"><span data-stu-id="ea72d-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ea72d-132">Aan de slag met Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ea72d-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ea72d-133">Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="ea72d-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ea72d-134">Naslaggids voor stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="ea72d-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ea72d-135">Stream Analytics management REST API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="ea72d-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
