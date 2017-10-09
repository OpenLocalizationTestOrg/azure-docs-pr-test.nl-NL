---
title: Service Fabric-prestatiecontrole aaaAzure | Microsoft Docs
description: Meer informatie over prestatiemeteritems voor controle en diagnostische gegevens van Azure Service Fabric-clusters.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="51fda-103">Maatstaven voor prestaties</span><span class="sxs-lookup"><span data-stu-id="51fda-103">Performance metrics</span></span>

<span data-ttu-id="51fda-104">Metrische gegevens moet worden verzameld toounderstand Hallo prestaties van uw cluster, evenals Hallo-toepassingen die erin worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51fda-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="51fda-105">Voor Service Fabric-clusters, wordt u aangeraden verzamelen Hallo prestatiemeteritems te volgen.</span><span class="sxs-lookup"><span data-stu-id="51fda-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="51fda-106">Knooppunten</span><span class="sxs-lookup"><span data-stu-id="51fda-106">Nodes</span></span>

<span data-ttu-id="51fda-107">Voor Hallo-machines in het cluster, kunt verzamelen van Hallo toobetter begrijpen Hallo belasting op elke machine en controleer juiste cluster schalen beslissingen prestatiemeteritems te volgen.</span><span class="sxs-lookup"><span data-stu-id="51fda-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="51fda-108">Prestatiemeteritem-categorie</span><span class="sxs-lookup"><span data-stu-id="51fda-108">Counter Category</span></span> | <span data-ttu-id="51fda-109">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="51fda-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="51fda-110">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-111">Gem. Wachtrijlengte voor schijf lezen</span><span class="sxs-lookup"><span data-stu-id="51fda-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="51fda-112">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-113">Gem. Wachtrijlengte voor schijf schrijven</span><span class="sxs-lookup"><span data-stu-id="51fda-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="51fda-114">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-115">Gem. Leestijd schijf</span><span class="sxs-lookup"><span data-stu-id="51fda-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="51fda-116">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-117">Gem. Schrijftijd schijf</span><span class="sxs-lookup"><span data-stu-id="51fda-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="51fda-118">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-119">Schijf lezen per seconde</span><span class="sxs-lookup"><span data-stu-id="51fda-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="51fda-120">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-121">Gelezen Bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="51fda-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="51fda-122">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-123">Schijf schrijven per seconde</span><span class="sxs-lookup"><span data-stu-id="51fda-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="51fda-124">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="51fda-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="51fda-125">Geschreven Bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="51fda-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="51fda-126">Geheugen</span><span class="sxs-lookup"><span data-stu-id="51fda-126">Memory</span></span> | <span data-ttu-id="51fda-127">Beschikbare megabytes (MB)</span><span class="sxs-lookup"><span data-stu-id="51fda-127">Available MBytes</span></span> |
| <span data-ttu-id="51fda-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="51fda-128">PagingFile</span></span> | <span data-ttu-id="51fda-129">% Gebruik</span><span class="sxs-lookup"><span data-stu-id="51fda-129">% Usage</span></span> |
| <span data-ttu-id="51fda-130">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="51fda-130">Process(Total)</span></span> | <span data-ttu-id="51fda-131">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="51fda-131">% Processor Time</span></span> |
| <span data-ttu-id="51fda-132">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-132">Process (per service)</span></span> | <span data-ttu-id="51fda-133">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="51fda-133">% Processor Time</span></span> |
| <span data-ttu-id="51fda-134">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-134">Process (per service)</span></span> | <span data-ttu-id="51fda-135">Proces-ID</span><span class="sxs-lookup"><span data-stu-id="51fda-135">ID Process</span></span> |
| <span data-ttu-id="51fda-136">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-136">Process (per service)</span></span> | <span data-ttu-id="51fda-137">Eigen Bytes</span><span class="sxs-lookup"><span data-stu-id="51fda-137">Private Bytes</span></span> |
| <span data-ttu-id="51fda-138">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-138">Process (per service)</span></span> | <span data-ttu-id="51fda-139">Aantal threads</span><span class="sxs-lookup"><span data-stu-id="51fda-139">Thread Count</span></span> |
| <span data-ttu-id="51fda-140">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-140">Process (per service)</span></span> | <span data-ttu-id="51fda-141">Virtuele Bytes</span><span class="sxs-lookup"><span data-stu-id="51fda-141">Virtual Bytes</span></span> |
| <span data-ttu-id="51fda-142">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-142">Process (per service)</span></span> | <span data-ttu-id="51fda-143">Werkset</span><span class="sxs-lookup"><span data-stu-id="51fda-143">Working Set</span></span> |
| <span data-ttu-id="51fda-144">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-144">Process (per service)</span></span> | <span data-ttu-id="51fda-145">Werkset - privé</span><span class="sxs-lookup"><span data-stu-id="51fda-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="51fda-146">.NET-toepassingen en services</span><span class="sxs-lookup"><span data-stu-id="51fda-146">.NET applications and services</span></span>

<span data-ttu-id="51fda-147">Verzamel Hallo prestatiemeteritems te volgen als u .NET services tooyour cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="51fda-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="51fda-148">Prestatiemeteritem-categorie</span><span class="sxs-lookup"><span data-stu-id="51fda-148">Counter Category</span></span> | <span data-ttu-id="51fda-149">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="51fda-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="51fda-150">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-151">Proces-ID</span><span class="sxs-lookup"><span data-stu-id="51fda-151">Process ID</span></span> |
| <span data-ttu-id="51fda-152">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-153"># Totaal aantal toegewezen Bytes</span><span class="sxs-lookup"><span data-stu-id="51fda-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="51fda-154">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-155"># Totaal aantal Bytes gereserveerd</span><span class="sxs-lookup"><span data-stu-id="51fda-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="51fda-156">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-157">Aantal bytes in alle Heaps</span><span class="sxs-lookup"><span data-stu-id="51fda-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="51fda-158">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-159"># Verzamelingen van generatie 0</span><span class="sxs-lookup"><span data-stu-id="51fda-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="51fda-160">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-161"># Generatie 1-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="51fda-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="51fda-162">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-163"># Gen 2-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="51fda-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="51fda-164">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="51fda-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="51fda-165">% Tijd in %</span><span class="sxs-lookup"><span data-stu-id="51fda-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="51fda-166">Aangepaste service-Fabric-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="51fda-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="51fda-167">Service Fabric genereert een aanzienlijke hoeveelheid aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="51fda-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="51fda-168">Als er Hallo SDK is geïnstalleerd, ziet u uitgebreide lijst Hallo op uw Windows-computer in uw toepassing Prestatiemeter (Start > Prestatiemeter).</span><span class="sxs-lookup"><span data-stu-id="51fda-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="51fda-169">In toepassingen met Hallo u tooyour cluster implementeert, als u Reliable Actors gebruikt, voegt u countes van `Service Fabric Actor` en `Service Fabric Actor Method` categorieën (Zie [Service Fabric betrouwbare actoren Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="51fda-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="51fda-170">Als u Reliable Services gebruikt, hebben we op dezelfde manier `Service Fabric Service` en `Service Fabric Service Method` categorieën voor prestatiemeteritems die u moet verzamelen van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="51fda-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="51fda-171">Als u betrouwbare verzamelingen gebruikt, raden wij aan toe te voegen Hallo `Avg. Transaction ms/Commit` van Hallo `Service Fabric Transactional Replicator` toocollect Hallo gemiddelde doorvoervertraging per transactie metriek.</span><span class="sxs-lookup"><span data-stu-id="51fda-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="51fda-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51fda-172">Next steps</span></span>

* <span data-ttu-id="51fda-173">Meer informatie over [genereren van gebeurtenissen op Hallo platform niveau](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="51fda-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="51fda-174">Verzamelen van prestatiegegevens via [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="51fda-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
