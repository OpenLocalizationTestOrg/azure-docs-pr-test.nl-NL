---
title: aaa "Azure Batch pool formaat start gebeurtenis | Microsoft Docs'
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="b357c-103">Gebeurtenissen voor het starten van toepassingen formaat wijzigen</span><span class="sxs-lookup"><span data-stu-id="b357c-103">Pool resize start event</span></span>

 <span data-ttu-id="b357c-104">Deze gebeurtenis wordt verzonden wanneer het formaat van een groep van toepassingen is gestart.</span><span class="sxs-lookup"><span data-stu-id="b357c-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="b357c-105">Aangezien Hallo groep formaat een asynchrone gebeurtenis is, kunt u verwachten een pool formaat gebeurtenis toobe verzonden zodra Hallo vergroten of verkleinen van de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b357c-105">Since hello pool resize is an asynchronous event, you can expect a pool resize complete event toobe emitted once hello resize operation completes.</span></span>

 <span data-ttu-id="b357c-106">Hallo volgende voorbeeld toont de hoofdtekst van de groep van toepassingen startgebeurtenis resize voor een groep van toepassingen vergroten of verkleinen van 0 too2 knooppunten met een handmatige Hallo vergroten of verkleinen.</span><span class="sxs-lookup"><span data-stu-id="b357c-106">hello following example shows hello body of a pool resize start event for a pool resizing from 0 too2 nodes with a manual resize.</span></span>

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

|<span data-ttu-id="b357c-107">Element</span><span class="sxs-lookup"><span data-stu-id="b357c-107">Element</span></span>|<span data-ttu-id="b357c-108">Type</span><span class="sxs-lookup"><span data-stu-id="b357c-108">Type</span></span>|<span data-ttu-id="b357c-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="b357c-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b357c-110">poolId</span><span class="sxs-lookup"><span data-stu-id="b357c-110">poolId</span></span>|<span data-ttu-id="b357c-111">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b357c-111">String</span></span>|<span data-ttu-id="b357c-112">Hallo-id van Hallo pool.</span><span class="sxs-lookup"><span data-stu-id="b357c-112">hello id of hello pool.</span></span>|
|<span data-ttu-id="b357c-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="b357c-113">nodeDeallocationOption</span></span>|<span data-ttu-id="b357c-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b357c-114">String</span></span>|<span data-ttu-id="b357c-115">Geeft aan wanneer knooppunten kunnen worden verwijderd uit groep hello, als Hallo poolgrootte afneemt.</span><span class="sxs-lookup"><span data-stu-id="b357c-115">Specifies when nodes may be removed from hello pool, if hello pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="b357c-116">Mogelijke waarden zijn:</span><span class="sxs-lookup"><span data-stu-id="b357c-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="b357c-117">**requeue** : Beëindig actieve taken en requeue ze.</span><span class="sxs-lookup"><span data-stu-id="b357c-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="b357c-118">Hallo taken wordt opnieuw uitgevoerd wanneer de taak Hallo is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b357c-118">hello tasks will run again when hello job is enabled.</span></span> <span data-ttu-id="b357c-119">Knooppunten verwijderen zodra taken zijn beëindigd.</span><span class="sxs-lookup"><span data-stu-id="b357c-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b357c-120">**beëindigen** – actieve taken beëindigen.</span><span class="sxs-lookup"><span data-stu-id="b357c-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="b357c-121">Hallo-taken worden niet opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b357c-121">hello tasks will not run again.</span></span> <span data-ttu-id="b357c-122">Knooppunten verwijderen zodra taken zijn beëindigd.</span><span class="sxs-lookup"><span data-stu-id="b357c-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="b357c-123">**taskcompletion** : toestaan dat taken toocomplete momenteel wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b357c-123">**taskcompletion** – Allow currently running tasks toocomplete.</span></span> <span data-ttu-id="b357c-124">Er zijn geen nieuwe taken tijdens het wachten plannen.</span><span class="sxs-lookup"><span data-stu-id="b357c-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b357c-125">Verwijder de knooppunten wanneer alle taken zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="b357c-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="b357c-126">**Retaineddata** - Sta toe dat actieve taken toocomplete en wacht vervolgens tot alle gegevens bewaren perioden tooexpire taken.</span><span class="sxs-lookup"><span data-stu-id="b357c-126">**Retaineddata** - Allow currently running tasks toocomplete, then wait for all task data retention periods tooexpire.</span></span> <span data-ttu-id="b357c-127">Er zijn geen nieuwe taken tijdens het wachten plannen.</span><span class="sxs-lookup"><span data-stu-id="b357c-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="b357c-128">Verwijder de knooppunten wanneer alle bewaarperioden voor taken zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="b357c-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="b357c-129">de standaardwaarde Hallo is requeue.</span><span class="sxs-lookup"><span data-stu-id="b357c-129">hello default value is requeue.</span></span><br /><br /> <span data-ttu-id="b357c-130">Als de poolgrootte Hallo toeneemt wordt Hallo waarde te ingesteld**ongeldig**.</span><span class="sxs-lookup"><span data-stu-id="b357c-130">If hello pool size is increasing then hello value is set too**invalid**.</span></span>|
|<span data-ttu-id="b357c-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="b357c-131">currentDedicated</span></span>|<span data-ttu-id="b357c-132">Int32</span><span class="sxs-lookup"><span data-stu-id="b357c-132">Int32</span></span>|<span data-ttu-id="b357c-133">het aantal rekenknooppunten Hallo momenteel toohello groep toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b357c-133">hello number of compute nodes currently assigned toohello pool.</span></span>|
|<span data-ttu-id="b357c-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="b357c-134">targetDedicated</span></span>|<span data-ttu-id="b357c-135">Int32</span><span class="sxs-lookup"><span data-stu-id="b357c-135">Int32</span></span>|<span data-ttu-id="b357c-136">Hallo aantal rekenknooppunten die zijn aangevraagd voor Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b357c-136">hello number of compute nodes that are requested for hello pool.</span></span>|
|<span data-ttu-id="b357c-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="b357c-137">enableAutoScale</span></span>|<span data-ttu-id="b357c-138">BOOL</span><span class="sxs-lookup"><span data-stu-id="b357c-138">Bool</span></span>|<span data-ttu-id="b357c-139">Hiermee geeft u op of Hallo groepsgrootte automatisch wordt aangepast gedurende een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="b357c-139">Specifies whether hello pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="b357c-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="b357c-140">isAutoPool</span></span>|<span data-ttu-id="b357c-141">BOOL</span><span class="sxs-lookup"><span data-stu-id="b357c-141">Bool</span></span>|<span data-ttu-id="b357c-142">Speficies of Hallo van toepassingen via een taak AutoPool mechanisme is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b357c-142">Speficies whether hello pool was created via a job's AutoPool mechanism.</span></span>|
