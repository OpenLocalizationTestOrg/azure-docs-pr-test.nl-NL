---
title: Azure Batch pool formaat start gebeurtenis | Microsoft Docs
description: Verwijzing voor Batch-pool formaat start-gebeurtenis.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="48786-103">Gebeurtenissen voor het starten van toepassingen formaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="48786-103">Pool resize start event</span></span>

 <span data-ttu-id="48786-104">Deze gebeurtenis wordt verzonden wanneer het formaat van een groep van toepassingen is gestart.</span><span class="sxs-lookup"><span data-stu-id="48786-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="48786-105">Aangezien het formaat van de groep van toepassingen een asynchrone gebeurtenis is, kunt u verwachten groep complete gebeurtenis resize om te worden verzonden wanneer de bewerking formaat is voltooid.</span><span class="sxs-lookup"><span data-stu-id="48786-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="48786-106">Het volgende voorbeeld ziet de hoofdtekst van de groep van toepassingen startgebeurtenis resize voor een groep van toepassingen vergroten of verkleinen van 0 voor 2 knooppunten met een handmatige formaat.</span><span class="sxs-lookup"><span data-stu-id="48786-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="48786-107">Element</span><span class="sxs-lookup"><span data-stu-id="48786-107">Element</span></span>|<span data-ttu-id="48786-108">Type</span><span class="sxs-lookup"><span data-stu-id="48786-108">Type</span></span>|<span data-ttu-id="48786-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="48786-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="48786-110">poolId</span><span class="sxs-lookup"><span data-stu-id="48786-110">poolId</span></span>|<span data-ttu-id="48786-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="48786-111">String</span></span>|<span data-ttu-id="48786-112">De id van de groep.</span><span class="sxs-lookup"><span data-stu-id="48786-112">The id of the pool.</span></span>|
|<span data-ttu-id="48786-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="48786-113">nodeDeallocationOption</span></span>|<span data-ttu-id="48786-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="48786-114">String</span></span>|<span data-ttu-id="48786-115">Geeft aan wanneer knooppunten kunnen worden verwijderd uit de groep als de poolgrootte afneemt.</span><span class="sxs-lookup"><span data-stu-id="48786-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="48786-116">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="48786-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="48786-117">**requeue** : Beëindig actieve taken en requeue ze.</span><span class="sxs-lookup"><span data-stu-id="48786-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="48786-118">De taken wordt opnieuw uitgevoerd wanneer de taak is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="48786-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="48786-119">Knooppunten verwijderen zodra taken zijn beëindigd.</span><span class="sxs-lookup"><span data-stu-id="48786-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="48786-120">**beëindigen** – actieve taken beëindigen.</span><span class="sxs-lookup"><span data-stu-id="48786-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="48786-121">De taken worden niet opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="48786-121">The tasks will not run again.</span></span> <span data-ttu-id="48786-122">Knooppunten verwijderen zodra taken zijn beëindigd.</span><span class="sxs-lookup"><span data-stu-id="48786-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="48786-123">**taskcompletion** : toestaan dat actieve taken te voltooien.</span><span class="sxs-lookup"><span data-stu-id="48786-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="48786-124">Er zijn geen nieuwe taken tijdens het wachten plannen.</span><span class="sxs-lookup"><span data-stu-id="48786-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="48786-125">Verwijder de knooppunten wanneer alle taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="48786-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="48786-126">**Retaineddata** -Sta toe dat actieve taken uit om te voltooien en wacht vervolgens tot alle bewaarperioden om te verlopen.</span><span class="sxs-lookup"><span data-stu-id="48786-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="48786-127">Er zijn geen nieuwe taken tijdens het wachten plannen.</span><span class="sxs-lookup"><span data-stu-id="48786-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="48786-128">Verwijder de knooppunten wanneer alle bewaarperioden voor taken zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="48786-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="48786-129">De standaardwaarde is requeue.</span><span class="sxs-lookup"><span data-stu-id="48786-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="48786-130">Als de poolgrootte toeneemt, wordt de waarde is ingesteld op **ongeldig**.</span><span class="sxs-lookup"><span data-stu-id="48786-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="48786-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="48786-131">currentDedicated</span></span>|<span data-ttu-id="48786-132">Int32</span><span class="sxs-lookup"><span data-stu-id="48786-132">Int32</span></span>|<span data-ttu-id="48786-133">Het aantal rekenknooppunten momenteel toegewezen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="48786-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="48786-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="48786-134">targetDedicated</span></span>|<span data-ttu-id="48786-135">Int32</span><span class="sxs-lookup"><span data-stu-id="48786-135">Int32</span></span>|<span data-ttu-id="48786-136">Het aantal rekenknooppunten die zijn aangevraagd voor de groep.</span><span class="sxs-lookup"><span data-stu-id="48786-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="48786-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="48786-137">enableAutoScale</span></span>|<span data-ttu-id="48786-138">BOOL</span><span class="sxs-lookup"><span data-stu-id="48786-138">Bool</span></span>|<span data-ttu-id="48786-139">Hiermee geeft u op of de poolgrootte automatisch wordt aangepast gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="48786-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="48786-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="48786-140">isAutoPool</span></span>|<span data-ttu-id="48786-141">BOOL</span><span class="sxs-lookup"><span data-stu-id="48786-141">Bool</span></span>|<span data-ttu-id="48786-142">Speficies of de groep is gemaakt via een taak AutoPool mechanisme.</span><span class="sxs-lookup"><span data-stu-id="48786-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
