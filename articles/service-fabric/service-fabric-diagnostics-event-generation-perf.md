---
title: Prestaties van Azure Service Fabric Monitoring | Microsoft Docs
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="37b0c-103">Maatstaven voor prestaties</span><span class="sxs-lookup"><span data-stu-id="37b0c-103">Performance metrics</span></span>

<span data-ttu-id="37b0c-104">Metrische gegevens moeten worden verzameld voor informatie over de prestaties van uw cluster, evenals de toepassingen die erin worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37b0c-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="37b0c-105">Voor Service Fabric-clusters, wordt u aangeraden de volgende prestatiemeteritems verzamelen.</span><span class="sxs-lookup"><span data-stu-id="37b0c-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="37b0c-106">Knooppunten</span><span class="sxs-lookup"><span data-stu-id="37b0c-106">Nodes</span></span>

<span data-ttu-id="37b0c-107">Voor de computers in uw cluster, kunt u het verzamelen van de volgende prestatiemeteritems om beter te begrijpen van de belasting op elke machine en relevante cluster schalen beslissingen maken.</span><span class="sxs-lookup"><span data-stu-id="37b0c-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="37b0c-108">Prestatiemeteritem-categorie</span><span class="sxs-lookup"><span data-stu-id="37b0c-108">Counter Category</span></span> | <span data-ttu-id="37b0c-109">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="37b0c-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="37b0c-110">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-111">Gem.</span><span class="sxs-lookup"><span data-stu-id="37b0c-111">Avg.</span></span> <span data-ttu-id="37b0c-112">Wachtrijlengte voor schijf lezen</span><span class="sxs-lookup"><span data-stu-id="37b0c-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="37b0c-113">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-114">Gem.</span><span class="sxs-lookup"><span data-stu-id="37b0c-114">Avg.</span></span> <span data-ttu-id="37b0c-115">Wachtrijlengte voor schijf schrijven</span><span class="sxs-lookup"><span data-stu-id="37b0c-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="37b0c-116">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-117">Gem.</span><span class="sxs-lookup"><span data-stu-id="37b0c-117">Avg.</span></span> <span data-ttu-id="37b0c-118">Leestijd schijf</span><span class="sxs-lookup"><span data-stu-id="37b0c-118">Disk sec/Read</span></span> |
| <span data-ttu-id="37b0c-119">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-120">Gem.</span><span class="sxs-lookup"><span data-stu-id="37b0c-120">Avg.</span></span> <span data-ttu-id="37b0c-121">Schrijftijd schijf</span><span class="sxs-lookup"><span data-stu-id="37b0c-121">Disk sec/Write</span></span> |
| <span data-ttu-id="37b0c-122">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-123">Schijf lezen per seconde</span><span class="sxs-lookup"><span data-stu-id="37b0c-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="37b0c-124">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-125">Gelezen Bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="37b0c-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="37b0c-126">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-127">Schijf schrijven per seconde</span><span class="sxs-lookup"><span data-stu-id="37b0c-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="37b0c-128">Fysieke schijf (per schijf)</span><span class="sxs-lookup"><span data-stu-id="37b0c-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="37b0c-129">Geschreven Bytes per seconde</span><span class="sxs-lookup"><span data-stu-id="37b0c-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="37b0c-130">Geheugen</span><span class="sxs-lookup"><span data-stu-id="37b0c-130">Memory</span></span> | <span data-ttu-id="37b0c-131">Beschikbare megabytes (MB)</span><span class="sxs-lookup"><span data-stu-id="37b0c-131">Available MBytes</span></span> |
| <span data-ttu-id="37b0c-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="37b0c-132">PagingFile</span></span> | <span data-ttu-id="37b0c-133">% Gebruik</span><span class="sxs-lookup"><span data-stu-id="37b0c-133">% Usage</span></span> |
| <span data-ttu-id="37b0c-134">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="37b0c-134">Process(Total)</span></span> | <span data-ttu-id="37b0c-135">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="37b0c-135">% Processor Time</span></span> |
| <span data-ttu-id="37b0c-136">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-136">Process (per service)</span></span> | <span data-ttu-id="37b0c-137">Percentage processortijd</span><span class="sxs-lookup"><span data-stu-id="37b0c-137">% Processor Time</span></span> |
| <span data-ttu-id="37b0c-138">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-138">Process (per service)</span></span> | <span data-ttu-id="37b0c-139">Proces-ID</span><span class="sxs-lookup"><span data-stu-id="37b0c-139">ID Process</span></span> |
| <span data-ttu-id="37b0c-140">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-140">Process (per service)</span></span> | <span data-ttu-id="37b0c-141">Eigen Bytes</span><span class="sxs-lookup"><span data-stu-id="37b0c-141">Private Bytes</span></span> |
| <span data-ttu-id="37b0c-142">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-142">Process (per service)</span></span> | <span data-ttu-id="37b0c-143">Aantal threads</span><span class="sxs-lookup"><span data-stu-id="37b0c-143">Thread Count</span></span> |
| <span data-ttu-id="37b0c-144">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-144">Process (per service)</span></span> | <span data-ttu-id="37b0c-145">Virtuele Bytes</span><span class="sxs-lookup"><span data-stu-id="37b0c-145">Virtual Bytes</span></span> |
| <span data-ttu-id="37b0c-146">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-146">Process (per service)</span></span> | <span data-ttu-id="37b0c-147">Werkset</span><span class="sxs-lookup"><span data-stu-id="37b0c-147">Working Set</span></span> |
| <span data-ttu-id="37b0c-148">Proces (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-148">Process (per service)</span></span> | <span data-ttu-id="37b0c-149">Werkset - privé</span><span class="sxs-lookup"><span data-stu-id="37b0c-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="37b0c-150">.NET-toepassingen en services</span><span class="sxs-lookup"><span data-stu-id="37b0c-150">.NET applications and services</span></span>

<span data-ttu-id="37b0c-151">De volgende prestatiemeteritems verzamelen als u .NET-services in uw cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="37b0c-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="37b0c-152">Prestatiemeteritem-categorie</span><span class="sxs-lookup"><span data-stu-id="37b0c-152">Counter Category</span></span> | <span data-ttu-id="37b0c-153">Naam van het meteritem</span><span class="sxs-lookup"><span data-stu-id="37b0c-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="37b0c-154">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-155">Proces-ID</span><span class="sxs-lookup"><span data-stu-id="37b0c-155">Process ID</span></span> |
| <span data-ttu-id="37b0c-156">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-157"># Totaal aantal toegewezen Bytes</span><span class="sxs-lookup"><span data-stu-id="37b0c-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="37b0c-158">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-159"># Totaal aantal Bytes gereserveerd</span><span class="sxs-lookup"><span data-stu-id="37b0c-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="37b0c-160">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-161">Aantal bytes in alle Heaps</span><span class="sxs-lookup"><span data-stu-id="37b0c-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="37b0c-162">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-163"># Verzamelingen van generatie 0</span><span class="sxs-lookup"><span data-stu-id="37b0c-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="37b0c-164">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-165"># Generatie 1-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="37b0c-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="37b0c-166">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-167"># Gen 2-verzamelingen</span><span class="sxs-lookup"><span data-stu-id="37b0c-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="37b0c-168">.NET CLR-geheugen (per-service)</span><span class="sxs-lookup"><span data-stu-id="37b0c-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="37b0c-169">% Tijd in %</span><span class="sxs-lookup"><span data-stu-id="37b0c-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="37b0c-170">Aangepaste service-Fabric-prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="37b0c-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="37b0c-171">Service Fabric genereert een aanzienlijke hoeveelheid aangepaste prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="37b0c-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="37b0c-172">Als u de SDK is geïnstalleerd hebt, ziet u de uitgebreide lijst op uw Windows-computer in uw toepassing Prestatiemeter (Start > Prestatiemeter).</span><span class="sxs-lookup"><span data-stu-id="37b0c-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="37b0c-173">In de toepassingen die u implementeert met uw cluster, als u gebruikmaakt van Reliable Actors, het toevoegen van countes van `Service Fabric Actor` en `Service Fabric Actor Method` categorieën (Zie [Service Fabric betrouwbare actoren Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="37b0c-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="37b0c-174">Als u Reliable Services gebruikt, hebben we op dezelfde manier `Service Fabric Service` en `Service Fabric Service Method` categorieën voor prestatiemeteritems die u moet verzamelen van prestatiemeteritems.</span><span class="sxs-lookup"><span data-stu-id="37b0c-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="37b0c-175">Als u betrouwbare verzamelingen gebruikt, raden wij aan toe te voegen de `Avg. Transaction ms/Commit` van de `Service Fabric Transactional Replicator` voor het verzamelen van de gemiddelde doorvoervertraging per transactie metriek.</span><span class="sxs-lookup"><span data-stu-id="37b0c-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="37b0c-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37b0c-176">Next steps</span></span>

* <span data-ttu-id="37b0c-177">Meer informatie over [genereren van gebeurtenissen op het niveau van het platform](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="37b0c-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="37b0c-178">Verzamelen van prestatiegegevens via [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="37b0c-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
