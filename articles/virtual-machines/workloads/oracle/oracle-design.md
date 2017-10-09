---
title: aaaDesign en implementeer een Oracle-database in Azure | Microsoft Docs
description: Ontwerpen en implementeren van een Oracle-database in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 8fa1207458695df1c7330ec626888b1b6b8d8939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="4be9a-103">Ontwerpen en implementeren van een Oracle-database in Azure</span><span class="sxs-lookup"><span data-stu-id="4be9a-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="4be9a-104">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="4be9a-104">Assumptions</span></span>

- <span data-ttu-id="4be9a-105">U bent van plan een Oracle-database van de lokale tooAzure toomigrate.</span><span class="sxs-lookup"><span data-stu-id="4be9a-105">You're planning toomigrate an Oracle database from on-premises tooAzure.</span></span>
- <span data-ttu-id="4be9a-106">U hebt een goed begrip van Hallo verschillende metrische gegevens in rapporten voor Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="4be9a-106">You have an understanding of hello various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="4be9a-107">U hebt een basislijn begrip van de prestaties van toepassingen en platforms te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4be9a-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="4be9a-108">Doelstellingen</span><span class="sxs-lookup"><span data-stu-id="4be9a-108">Goals</span></span>

- <span data-ttu-id="4be9a-109">Begrijpen hoe toooptimize uw Oracle-implementatie in Azure.</span><span class="sxs-lookup"><span data-stu-id="4be9a-109">Understand how toooptimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="4be9a-110">Gebruik de opties voor een Oracle-database in een Azure-omgeving afstemmen van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="4be9a-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="hello-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="4be9a-111">Hallo verschillen tussen een on-premises en Azure-implementatie</span><span class="sxs-lookup"><span data-stu-id="4be9a-111">hello differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="4be9a-112">Hieronder volgen enkele belangrijke dingen tookeep rekening moet houden bij waarnaar u migreert lokale toepassingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4be9a-112">Following are some important things tookeep in mind when you're migrating on-premises applications tooAzure.</span></span> 

<span data-ttu-id="4be9a-113">Een belangrijk verschil is dat de resources, zoals virtuele machines, schijven en virtuele netwerken in een Azure-implementatie moet worden gedeeld door andere clients.</span><span class="sxs-lookup"><span data-stu-id="4be9a-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="4be9a-114">Resources kunnen bovendien worden beperkt op basis van Hallo vereisten.</span><span class="sxs-lookup"><span data-stu-id="4be9a-114">In addition, resources can be throttled based on hello requirements.</span></span> <span data-ttu-id="4be9a-115">In plaats van te focussen op het voorkomen (MBTF) mislukt, wordt Azure meer gericht op functionerende hallo-fout (MTTR).</span><span class="sxs-lookup"><span data-stu-id="4be9a-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving hello failure (MTTR).</span></span>

<span data-ttu-id="4be9a-116">Hallo volgende tabel bevat enkele van Hallo verschillen tussen een lokale implementatie en een Azure-implementatie van een Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="4be9a-116">hello following table lists some of hello differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="4be9a-117">**Lokale implementatie**</span><span class="sxs-lookup"><span data-stu-id="4be9a-117">**On-premises implementation**</span></span> | <span data-ttu-id="4be9a-118">**Azure-implementatie**</span><span class="sxs-lookup"><span data-stu-id="4be9a-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="4be9a-119">**Netwerken**</span><span class="sxs-lookup"><span data-stu-id="4be9a-119">**Networking**</span></span> |<span data-ttu-id="4be9a-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="4be9a-120">LAN/WAN</span></span>  |<span data-ttu-id="4be9a-121">SDN (software gedefinieerde netwerken)</span><span class="sxs-lookup"><span data-stu-id="4be9a-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="4be9a-122">**Beveiligingsgroep**</span><span class="sxs-lookup"><span data-stu-id="4be9a-122">**Security group**</span></span> |<span data-ttu-id="4be9a-123">Hulpprogramma's voor beperking van de IP/poort</span><span class="sxs-lookup"><span data-stu-id="4be9a-123">IP/port restriction tools</span></span> |[<span data-ttu-id="4be9a-124">Netwerkbeveiligingsgroep (NSG)</span><span class="sxs-lookup"><span data-stu-id="4be9a-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="4be9a-125">**Herstelmogelijkheden**</span><span class="sxs-lookup"><span data-stu-id="4be9a-125">**Resilience**</span></span> |<span data-ttu-id="4be9a-126">MBTF (gemiddelde tijd tussen storingen)</span><span class="sxs-lookup"><span data-stu-id="4be9a-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="4be9a-127">MTTR (tussentijd toorecovery)</span><span class="sxs-lookup"><span data-stu-id="4be9a-127">MTTR (mean time toorecovery)</span></span>|
> | <span data-ttu-id="4be9a-128">**Gepland onderhoud**</span><span class="sxs-lookup"><span data-stu-id="4be9a-128">**Planned maintenance**</span></span> |<span data-ttu-id="4be9a-129">Patchen of upgrades worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="4be9a-129">Patching/upgrades</span></span>|<span data-ttu-id="4be9a-130">[Beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patchen/upgrades worden beheerd door Azure)</span><span class="sxs-lookup"><span data-stu-id="4be9a-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="4be9a-131">**Resource**</span><span class="sxs-lookup"><span data-stu-id="4be9a-131">**Resource**</span></span> |<span data-ttu-id="4be9a-132">Toegewezen</span><span class="sxs-lookup"><span data-stu-id="4be9a-132">Dedicated</span></span>  |<span data-ttu-id="4be9a-133">Gedeeld met andere clients</span><span class="sxs-lookup"><span data-stu-id="4be9a-133">Shared with other clients</span></span>|
> | <span data-ttu-id="4be9a-134">**Regio 's**</span><span class="sxs-lookup"><span data-stu-id="4be9a-134">**Regions**</span></span> |<span data-ttu-id="4be9a-135">Datacenters</span><span class="sxs-lookup"><span data-stu-id="4be9a-135">Datacenters</span></span> |[<span data-ttu-id="4be9a-136">Regio paren</span><span class="sxs-lookup"><span data-stu-id="4be9a-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="4be9a-137">**Storage**</span><span class="sxs-lookup"><span data-stu-id="4be9a-137">**Storage**</span></span> |<span data-ttu-id="4be9a-138">SAN of fysieke schijven</span><span class="sxs-lookup"><span data-stu-id="4be9a-138">SAN/physical disks</span></span> |[<span data-ttu-id="4be9a-139">Beheerde Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="4be9a-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="4be9a-140">**Schalen**</span><span class="sxs-lookup"><span data-stu-id="4be9a-140">**Scale**</span></span> |<span data-ttu-id="4be9a-141">Verticale schaal</span><span class="sxs-lookup"><span data-stu-id="4be9a-141">Vertical scale</span></span> |<span data-ttu-id="4be9a-142">Horizontaal schalen</span><span class="sxs-lookup"><span data-stu-id="4be9a-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="4be9a-143">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4be9a-143">Requirements</span></span>

- <span data-ttu-id="4be9a-144">Hallo database grootte en groei snelheid bepalen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-144">Determine hello database size and growth rate.</span></span>
- <span data-ttu-id="4be9a-145">Hallo IOPS vereisten, kunt u schatten op basis van Oracle AWR rapporten of andere hulpprogramma's voor Netwerkcontrole bepalen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-145">Determine hello IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="4be9a-146">Configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="4be9a-146">Configuration options</span></span>

<span data-ttu-id="4be9a-147">Er zijn vier mogelijke gebieden dat kunt u de afstemmen tooimprove prestaties in een Azure-omgeving:</span><span class="sxs-lookup"><span data-stu-id="4be9a-147">There are four potential areas that you can tune tooimprove performance in an Azure environment:</span></span>

- <span data-ttu-id="4be9a-148">Grootte van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4be9a-148">Virtual machine size</span></span>
- <span data-ttu-id="4be9a-149">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="4be9a-149">Network throughput</span></span>
- <span data-ttu-id="4be9a-150">Schijftypen en configuraties</span><span class="sxs-lookup"><span data-stu-id="4be9a-150">Disk types and configurations</span></span>
- <span data-ttu-id="4be9a-151">Schijf-cache-instellingen</span><span class="sxs-lookup"><span data-stu-id="4be9a-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="4be9a-152">Een AWR genereren</span><span class="sxs-lookup"><span data-stu-id="4be9a-152">Generate an AWR report</span></span>

<span data-ttu-id="4be9a-153">Als u een bestaande een Oracle-database en toomigrate tooAzure van plan bent, hebt u verschillende mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="4be9a-153">If you have an existing an Oracle database and are planning toomigrate tooAzure, you have several options.</span></span> <span data-ttu-id="4be9a-154">U kunt uitvoeren Hallo Oracle AWR rapport tooget Hallo metrische gegevens (IOP's, Mbps, GiBs, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="4be9a-154">You can run hello Oracle AWR report tooget hello metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="4be9a-155">Kies vervolgens Hallo die VM op basis van Hallo metrische gegevens die u hebt verzameld.</span><span class="sxs-lookup"><span data-stu-id="4be9a-155">Then choose hello VM based on hello metrics that you collected.</span></span> <span data-ttu-id="4be9a-156">Of u kunt contact opnemen met uw team tooget vergelijkbare informatie over de infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="4be9a-156">Or you can contact your infrastructure team tooget similar information.</span></span>

<span data-ttu-id="4be9a-157">U kunt uw rapport AWR uitvoeren tijdens normale en piekuren werkbelastingen, zodat u kunt vergelijken.</span><span class="sxs-lookup"><span data-stu-id="4be9a-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="4be9a-158">Op basis van deze rapporten, kunt u virtuele machines op basis van gemiddelde werkbelasting Hallo of de maximale werkbelasting Hallo Hallo groot.</span><span class="sxs-lookup"><span data-stu-id="4be9a-158">Based on these reports, you can size hello VMs based on either hello average workload or hello maximum workload.</span></span>

<span data-ttu-id="4be9a-159">Hieronder volgt een voorbeeld van hoe u een rapport AWR toogenerate:</span><span class="sxs-lookup"><span data-stu-id="4be9a-159">Following is an example of how toogenerate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="4be9a-160">De belangrijkste metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="4be9a-160">Key metrics</span></span>

<span data-ttu-id="4be9a-161">Hieronder vindt u Hallo metrische gegevens die u van Hallo AWR rapport verkrijgen kunt:</span><span class="sxs-lookup"><span data-stu-id="4be9a-161">Following are hello metrics that you can obtain from hello AWR report:</span></span>

- <span data-ttu-id="4be9a-162">Totaal aantal kernen</span><span class="sxs-lookup"><span data-stu-id="4be9a-162">Total number of cores</span></span>
- <span data-ttu-id="4be9a-163">CPU-kloksnelheid</span><span class="sxs-lookup"><span data-stu-id="4be9a-163">CPU clock speed</span></span>
- <span data-ttu-id="4be9a-164">Totale geheugen in GB</span><span class="sxs-lookup"><span data-stu-id="4be9a-164">Total memory in GB</span></span>
- <span data-ttu-id="4be9a-165">CPU-gebruik</span><span class="sxs-lookup"><span data-stu-id="4be9a-165">CPU utilization</span></span>
- <span data-ttu-id="4be9a-166">Overdrachtssnelheid piek</span><span class="sxs-lookup"><span data-stu-id="4be9a-166">Peak data transfer rate</span></span>
- <span data-ttu-id="4be9a-167">Het aantal i/o-wijzigingen (lezen/schrijven)</span><span class="sxs-lookup"><span data-stu-id="4be9a-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="4be9a-168">Opnieuw logboek snelheid (MBPs)</span><span class="sxs-lookup"><span data-stu-id="4be9a-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="4be9a-169">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="4be9a-169">Network throughput</span></span>
- <span data-ttu-id="4be9a-170">Netwerk latentie snelheid (laag/hoog)</span><span class="sxs-lookup"><span data-stu-id="4be9a-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="4be9a-171">Databasegrootte in GB</span><span class="sxs-lookup"><span data-stu-id="4be9a-171">Database size in GB</span></span>
- <span data-ttu-id="4be9a-172">Bytes ontvangen via SQL * Net van / tooclient</span><span class="sxs-lookup"><span data-stu-id="4be9a-172">Bytes received via SQL*Net from/tooclient</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="4be9a-173">Grootte van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4be9a-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-hello-awr-report"></a><span data-ttu-id="4be9a-174">1. Schatting maken van VM-grootte op basis van CPU, geheugen en i/o-gebruik van Hallo AWR rapport</span><span class="sxs-lookup"><span data-stu-id="4be9a-174">1. Estimate VM size based on CPU, memory, and I/O usage from hello AWR report</span></span>

<span data-ttu-id="4be9a-175">Wat die u mogelijk bekijkt is hello bovenste vijf is een time-out opgetreden voor gebeurtenissen die aangeven waar knelpunten in het systeem Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="4be9a-175">One thing you might look at is hello top five timed foreground events that indicate where hello system bottlenecks are.</span></span>

<span data-ttu-id="4be9a-176">Bijvoorbeeld in Hallo diagram te volgen, Hallo log-bestand synchronisatie wordt Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-176">For example, in hello following diagram, hello log file sync is at hello top.</span></span> <span data-ttu-id="4be9a-177">Hiermee wordt aangegeven Hallo aantal wacht die vereist zijn voordat Hallo LGWR Hallo buffer toohello opnieuw logboek logboekbestand worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-177">It indicates hello number of waits that are required before hello LGWR writes hello log buffer toohello redo log file.</span></span> <span data-ttu-id="4be9a-178">Deze resultaten blijkt dat beter presterende opslag of schijven vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="4be9a-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="4be9a-179">Hallo diagram toont bovendien ook Hallo aantal CPU (kernen) en Hallo en de hoeveelheid geheugen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-179">In addition, hello diagram also shows hello number of CPU (cores) and hello amount of memory.</span></span>

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="4be9a-181">Hallo toont volgende diagram Hallo totale i/o lezen en schrijven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-181">hello following diagram shows hello total I/O of read and write.</span></span> <span data-ttu-id="4be9a-182">Er zijn 59 lezen en 247.3 GB tijdens Hallo van Hallo rapport geschreven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-182">There were 59 GB read and 247.3 GB written during hello time of hello report.</span></span>

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="4be9a-184">2. Kies een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4be9a-184">2. Choose a VM</span></span>

<span data-ttu-id="4be9a-185">Op basis van het Hallo-informatie die u hebt verzameld van Hallo AWR rapport, is de volgende stap Hallo toochoose een virtuele machine met een vergelijkbare grootte die voldoet aan uw.</span><span class="sxs-lookup"><span data-stu-id="4be9a-185">Based on hello information that you collected from hello AWR report, hello next step is toochoose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="4be9a-186">U vindt een lijst met beschikbare virtuele machines in Hallo artikel [geoptimaliseerd voor geheugen](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="4be9a-186">You can find a list of available VMs in hello article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-hello-vm-sizing-with-a-similar-vm-series-based-on-hello-acu"></a><span data-ttu-id="4be9a-187">3. Hallo VM sizing stemmen met een vergelijkbare VM-reeks op basis van Hallo ACU</span><span class="sxs-lookup"><span data-stu-id="4be9a-187">3. Fine-tune hello VM sizing with a similar VM series based on hello ACU</span></span>

<span data-ttu-id="4be9a-188">Nadat u hebt gekozen Hallo VM, betaalt u aandacht toohello ACU voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="4be9a-188">After you've chosen hello VM, pay attention toohello ACU for hello VM.</span></span> <span data-ttu-id="4be9a-189">U kunt een andere virtuele machine op basis van Hallo ACU-waarde die beter aansluit bij uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="4be9a-189">You might choose a different VM based on hello ACU value that better suits your requirements.</span></span> <span data-ttu-id="4be9a-190">Zie voor meer informatie [Azure compute eenheid](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="4be9a-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Schermafbeelding van Hallo ACU eenheden-pagina](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="4be9a-192">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="4be9a-192">Network throughput</span></span>

<span data-ttu-id="4be9a-193">Hallo volgende diagram ziet u Hallo relatie tussen de doorvoer en IOP's:</span><span class="sxs-lookup"><span data-stu-id="4be9a-193">hello following diagram shows hello relation between throughput and IOPS:</span></span>

![Schermopname van doorvoer](./media/oracle-design/throughput.png)

<span data-ttu-id="4be9a-195">de totale netwerkdoorvoer Hallo geschat op basis van de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="4be9a-195">hello total network throughput is estimated based on hello following information:</span></span>
- <span data-ttu-id="4be9a-196">SQL * Net verkeer</span><span class="sxs-lookup"><span data-stu-id="4be9a-196">SQL*Net traffic</span></span>
- <span data-ttu-id="4be9a-197">MBps x het aantal servers (uitgaande stream zoals Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="4be9a-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="4be9a-198">Andere factoren, zoals toepassing replicatie</span><span class="sxs-lookup"><span data-stu-id="4be9a-198">Other factors, such as application replication</span></span>

![Schermopname van Hallo SQL * Net doorvoer](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="4be9a-200">Op basis van de vereisten van uw netwerkbandbreedte, zijn er verschillende gatewaytypen voor toochoose van.</span><span class="sxs-lookup"><span data-stu-id="4be9a-200">Based on your network bandwidth requirements, there are various gateway types for you toochoose from.</span></span> <span data-ttu-id="4be9a-201">Het gaat hierbij om basic, VpnGw en Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4be9a-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="4be9a-202">Zie voor meer informatie, Hallo [VPN-gateway pagina met prijzen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="4be9a-202">For more information, see hello [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="4be9a-203">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="4be9a-203">**Recommendations**</span></span>

- <span data-ttu-id="4be9a-204">Netwerklatentie is hoger dan tooan on-premises implementatie.</span><span class="sxs-lookup"><span data-stu-id="4be9a-204">Network latency is higher compared tooan on-premises deployment.</span></span> <span data-ttu-id="4be9a-205">Netwerk ronde reizen kan aanzienlijk verminderen, de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="4be9a-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="4be9a-206">tooreduce retourbewerkingen, consolideren toepassingen met hoge transacties of 'chatty' apps op Hallo dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4be9a-206">tooreduce round-trips, consolidate applications that have high transactions or “chatty” apps on hello same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="4be9a-207">Schijftypen en configuraties</span><span class="sxs-lookup"><span data-stu-id="4be9a-207">Disk types and configurations</span></span>

- <span data-ttu-id="4be9a-208">*Standaard OS schijven*: deze schijftypen bieden permanente gegevens en opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="4be9a-209">Ze zijn geoptimaliseerd voor OS toegang bij het opstarten en zijn niet bedoeld voor transactionele of datawarehouse-werkbelastingen (analytische).</span><span class="sxs-lookup"><span data-stu-id="4be9a-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="4be9a-210">*Schijven zonder begeleiding*: met deze schijftypen die u beheert Hallo storage-accounts die Hallo virtuele harde schijf (VHD)-bestanden die overeenkomen met tooyour VM schijven opslaan.</span><span class="sxs-lookup"><span data-stu-id="4be9a-210">*Unmanaged disks*: With these disk types, you manage hello storage accounts that store hello virtual hard disk (VHD) files that correspond tooyour VM disks.</span></span> <span data-ttu-id="4be9a-211">VHD-bestanden worden opgeslagen als pagina-blobs in Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="4be9a-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="4be9a-212">*Schijven die worden beheerd*: Azure beheert Hallo storage-accounts die u voor uw VM-schijven gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-212">*Managed disks*: Azure manages hello storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="4be9a-213">U geeft Hallo schijftype (premium of standaard) en Hallo grootte van Hallo-schijf die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-213">You specify hello disk type (premium or standard) and hello size of hello disk that you need.</span></span> <span data-ttu-id="4be9a-214">Azure maakt en beheert de Hallo schijf voor u.</span><span class="sxs-lookup"><span data-stu-id="4be9a-214">Azure creates and manages hello disk for you.</span></span>

- <span data-ttu-id="4be9a-215">*Premium-opslag-schijven*: deze schijftypen geschikt zijn voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="4be9a-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="4be9a-216">Premium-opslag ondersteunt het VM-schijven die kunnen worden gekoppeld toospecific grootte-serie VM's, zoals Active Directory, DSv2 GS en F-serie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4be9a-216">Premium storage supports VM disks that can be attached toospecific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="4be9a-217">Hallo premium schijf is voorzien van verschillende grootte en kunt u kiezen tussen schijven variërend van 32 GB too4, 096 GB.</span><span class="sxs-lookup"><span data-stu-id="4be9a-217">hello premium disk comes with different sizes, and you can choose between disks ranging from 32 GB too4,096 GB.</span></span> <span data-ttu-id="4be9a-218">De grootte van elke schijf heeft zijn eigen prestatiespecificaties.</span><span class="sxs-lookup"><span data-stu-id="4be9a-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="4be9a-219">Afhankelijk van uw toepassing, kunt u een of meer schijven tooyour VM koppelen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-219">Depending on your application requirements, you can attach one or more disks tooyour VM.</span></span>

<span data-ttu-id="4be9a-220">Wanneer u een nieuwe beheerde schijf vanuit Hallo portal maakt, kunt u Hallo **accounttype** Hallo type schijf dat u wilt toouse.</span><span class="sxs-lookup"><span data-stu-id="4be9a-220">When you create a new managed disk from hello portal, you can choose hello **Account type** for hello type of disk you want toouse.</span></span> <span data-ttu-id="4be9a-221">Houd er rekening mee dat niet alle beschikbare schijven in de vervolgkeuzelijst Hallo worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-221">Keep in mind that not all available disks are shown in hello drop-down menu.</span></span> <span data-ttu-id="4be9a-222">Nadat u een bepaalde VM-grootte hebt gekozen, ziet u Hallo menu alleen Hallo beschikbaar premium-opslag SKU's die zijn gebaseerd op deze VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="4be9a-222">After you choose a particular VM size, hello menu shows only hello available premium storage SKUs that are based on that VM size.</span></span>

![Schermafbeelding van pagina met Hallo-beheerde schijven](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="4be9a-224">Zie voor meer informatie [beheerde schijven voor virtuele machines en hoge prestaties Premium-opslag](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="4be9a-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="4be9a-225">Nadat u uw opslag op een virtuele machine hebt geconfigureerd, kunt u tooload test Hallo schijven hebben voordat u een database maakt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-225">After you configure your storage on a VM, you might want tooload test hello disks before creating a database.</span></span> <span data-ttu-id="4be9a-226">Doorvoer latentie doelen weten Hallo i/o-snelheid in termen van de latentie en de doorvoer kan u helpen bepalen als Hallo VM's Hallo ondersteunen worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="4be9a-226">Knowing hello I/O rate in terms of both latency and throughput can help you determine if hello VMs support hello expected throughput with latency targets.</span></span>

<span data-ttu-id="4be9a-227">Er zijn een aantal hulpprogramma's voor de toepassing werklast testen, zoals Oracle Orion Sysbench en Fio.</span><span class="sxs-lookup"><span data-stu-id="4be9a-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="4be9a-228">Hallo load test opnieuw uitgevoerd nadat u een Oracle-database hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4be9a-228">Run hello load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="4be9a-229">Start de werkbelasting van uw normale en piekuren en Hallo resultaten weergeven Hallo van basislijn van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="4be9a-229">Start your regular and peak workloads, and hello results show you hello baseline of your environment.</span></span>

<span data-ttu-id="4be9a-230">Belangrijker toosize Hallo opslag op basis van Hallo IOPS snelheid in plaats van Hallo opslaggrootte mogelijk.</span><span class="sxs-lookup"><span data-stu-id="4be9a-230">It might be more important toosize hello storage based on hello IOPS rate rather than hello storage size.</span></span> <span data-ttu-id="4be9a-231">Bijvoorbeeld als Hallo vereist IOPS 5.000 is, maar hoeft u alleen 200 GB, u mogelijk alsnog Hallo P30 klasse premium schijf ook al beschikt u over meer dan 200 GB aan opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="4be9a-231">For example, if hello required IOPS is 5,000, but you only need 200 GB, you might still get hello P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="4be9a-232">Hallo IOPS snelheid kan worden verkregen van Hallo AWR rapport.</span><span class="sxs-lookup"><span data-stu-id="4be9a-232">hello IOPS rate can be obtained from hello AWR report.</span></span> <span data-ttu-id="4be9a-233">Dit wordt bepaald door Hallo opnieuw logboek, fysieke leesbewerkingen en snelheid van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-233">It's determined by hello redo log, physical reads, and writes rate.</span></span>

![Schermafbeelding van pagina Hallo AWR-rapport](./media/oracle-design/awr_report.png)

<span data-ttu-id="4be9a-235">Hallo opnieuw grootte is bijvoorbeeld 12,200,000 bytes per seconde, wat gelijk too11.63 MBPs.</span><span class="sxs-lookup"><span data-stu-id="4be9a-235">For example, hello redo size is 12,200,000 bytes per second, which is equal too11.63 MBPs.</span></span>
<span data-ttu-id="4be9a-236">Hallo IOPS is 12.200.000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="4be9a-236">hello IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="4be9a-237">Nadat u een duidelijk beeld van Hallo i/o-vereisten hebt, kunt u een combinatie van stations die het beste geschikt toomeet zijn deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="4be9a-237">After you have a clear picture of hello I/O requirements, you can choose a combination of drives that are best suited toomeet those requirements.</span></span>

<span data-ttu-id="4be9a-238">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="4be9a-238">**Recommendations**</span></span>

- <span data-ttu-id="4be9a-239">Voor gegevens tabelruimte, verdeeld over Hallo i/o-werkbelasting een aantal schijven met behulp van beheerde opslaggroep of Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="4be9a-239">For data tablespace, spread hello I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="4be9a-240">Als Hallo i/o-blokgrootte voor lees-intensieve en write-intensieve bewerkingen toeneemt, kunt u meer gegevensschijven toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-240">As hello I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="4be9a-241">Hallo blokgrootte voor grote opeenvolgende processen verhogen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-241">Increase hello block size for large sequential processes.</span></span>
- <span data-ttu-id="4be9a-242">Gebruik gegevens compressie tooreduce i/o (voor gegevens en indexen).</span><span class="sxs-lookup"><span data-stu-id="4be9a-242">Use data compression tooreduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="4be9a-243">Afzonderlijke opnieuw Logboeken, systeem en temps en ongedaan maken van TS op afzonderlijke gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="4be9a-244">Niet alle toepassingsbestanden op standaard OS-schijven (/ dev/sda) plaatsen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="4be9a-245">Deze schijven worden niet geoptimaliseerd voor snelle VM opstarttijden, en ze bieden geen goede prestaties voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="4be9a-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="4be9a-246">Schijf-cache-instellingen</span><span class="sxs-lookup"><span data-stu-id="4be9a-246">Disk cache settings</span></span>

<span data-ttu-id="4be9a-247">Er zijn drie opties voor hostcaching:</span><span class="sxs-lookup"><span data-stu-id="4be9a-247">There are three options for host caching:</span></span>

- <span data-ttu-id="4be9a-248">*Alleen-lezen*: alle aanvragen in cache zijn opgeslagen voor toekomstige leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="4be9a-249">Alle schrijfbewerkingen worden persistent rechtstreeks tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="4be9a-249">All writes are persisted directly tooAzure Blob storage.</span></span>

- <span data-ttu-id="4be9a-250">*Lezen / schrijven*: dit is een 'read-ahead' algoritme.</span><span class="sxs-lookup"><span data-stu-id="4be9a-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="4be9a-251">Hallo leest en schrijft in cache zijn opgeslagen voor toekomstige leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-251">hello reads and writes are cached for future reads.</span></span> <span data-ttu-id="4be9a-252">Niet-write-through schrijfbewerkingen zijn eerst toohello lokale cache bewaard.</span><span class="sxs-lookup"><span data-stu-id="4be9a-252">Non-write-through writes are persisted toohello local cache first.</span></span> <span data-ttu-id="4be9a-253">Schrijfbewerkingen zijn persistente tooAzure opslag voor SQL Server, omdat deze write-through gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4be9a-253">For SQL Server, writes are persisted tooAzure Storage because it uses write-through.</span></span> <span data-ttu-id="4be9a-254">Het bevat ook Hallo laagste schijf latentie voor lichte werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="4be9a-254">It also provides hello lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="4be9a-255">*Geen* (uitgeschakeld): deze optie gebruikt, kunt u Hallo cache overslaan.</span><span class="sxs-lookup"><span data-stu-id="4be9a-255">*None* (disabled): By using this option, you can bypass hello cache.</span></span> <span data-ttu-id="4be9a-256">Alle Hallo-gegevens worden overgebracht toodisk en persistent tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="4be9a-256">All hello data is transferred toodisk and persisted tooAzure Storage.</span></span> <span data-ttu-id="4be9a-257">Deze methode kunt u Hallo hoogste i/o-snelheid voor i/o-intensieve werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-257">This method gives you hello highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="4be9a-258">Tootake 'transactiekosten' moet u ook rekening.</span><span class="sxs-lookup"><span data-stu-id="4be9a-258">You also need tootake “transaction cost” into consideration.</span></span>

<span data-ttu-id="4be9a-259">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="4be9a-259">**Recommendations**</span></span>

<span data-ttu-id="4be9a-260">toomaximize hello doorvoer, het is raadzaam dat u met begint **geen** voor hostcaching.</span><span class="sxs-lookup"><span data-stu-id="4be9a-260">toomaximize hello throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="4be9a-261">Voor Premium-opslag, houd er rekening mee moet u Hallo 'barrières"uitschakelen wanneer u Hallo bestandssysteem Hello koppelt **ReadOnly** of **geen** opties.</span><span class="sxs-lookup"><span data-stu-id="4be9a-261">For Premium Storage, keep in mind that you must disable hello "barriers" when you mount hello file system with hello **ReadOnly** or **None** options.</span></span> <span data-ttu-id="4be9a-262">Hallo /etc/fstab bestand bijwerken met Hallo UUID toohello schijven.</span><span class="sxs-lookup"><span data-stu-id="4be9a-262">Update hello /etc/fstab file with hello UUID toohello disks.</span></span>

<span data-ttu-id="4be9a-263">Zie voor meer informatie [Premium-opslag voor virtuele Linux-machines](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="4be9a-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Schermafbeelding van pagina met Hallo-beheerde schijven](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="4be9a-265">Voor OS-schijven, gebruikt u de standaard **lezen/schrijven** opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="4be9a-266">Gebruik voor het systeem, TEMP en ongedaan maken **geen** voor opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="4be9a-267">Gebruik voor gegevens, **geen** voor opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="4be9a-268">Maar als de database alleen-lezen of lees-intensieve is, gebruikt u **alleen-lezen** opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="4be9a-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="4be9a-269">Nadat de instelling van de schijf gegevens zijn opgeslagen, kunt u Hallo host cache-instelling niet wijzigen, tenzij u het Hallo-station op Hallo OS niveau ontkoppelen en koppel deze het vervolgens opnieuw nadat u hebt aangebracht Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4be9a-269">After your data disk setting is saved, you can't change hello host cache setting unless you unmount hello drive at hello OS level and then remount it after you've made hello change.</span></span>


## <a name="security"></a><span data-ttu-id="4be9a-270">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="4be9a-270">Security</span></span>

<span data-ttu-id="4be9a-271">Nadat u hebt ingesteld en geconfigureerd van uw Azure-omgeving, de volgende stap Hallo toosecure is uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="4be9a-271">After you have set up and configured your Azure environment, hello next step is toosecure your network.</span></span> <span data-ttu-id="4be9a-272">Hier volgen enkele aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="4be9a-272">Here are some recommendations:</span></span>

- <span data-ttu-id="4be9a-273">*NSG-beleid*: NSG worden gedefinieerd met een subnet of NIC.</span><span class="sxs-lookup"><span data-stu-id="4be9a-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="4be9a-274">Het is eenvoudiger toocontrol toegang op Hallo subnetniveau voor beveiliging en werking routering voor dingen zoals firewalls, toepassing.</span><span class="sxs-lookup"><span data-stu-id="4be9a-274">It's simpler toocontrol access at hello subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="4be9a-275">*Jumpbox*: voor een beter beveiligde toegang beheerders moeten niet rechtstreeks toegang toohello toepassingsservice of database.</span><span class="sxs-lookup"><span data-stu-id="4be9a-275">*Jumpbox*: For more secure access, administrators should not directly connect toohello application service or database.</span></span> <span data-ttu-id="4be9a-276">Een jumpbox wordt gebruikt als een medium tussen Hallo beheerder machine en de Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="4be9a-276">A jumpbox is used as a media between hello administrator machine and Azure resources.</span></span>
<span data-ttu-id="4be9a-277">![Schermafbeelding van pagina met Hallo Jumpbox-topologie](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="4be9a-277">![Screenshot of hello Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="4be9a-278">Hallo beheerder machine moet IP beperkte toegang toohello jumpbox alleen aanbieden.</span><span class="sxs-lookup"><span data-stu-id="4be9a-278">hello administrator machine should offer IP-restricted access toohello jumpbox only.</span></span> <span data-ttu-id="4be9a-279">Hallo jumpbox moet hebben toegang toohello toepassing en -database.</span><span class="sxs-lookup"><span data-stu-id="4be9a-279">hello jumpbox should have access toohello application and database.</span></span>

- <span data-ttu-id="4be9a-280">*Particulier netwerk* (subnetten): We raden u aan Hallo toepassings-service en de database op afzonderlijke subnetten, zodat betere controle kan worden ingesteld door het NSG-beleid.</span><span class="sxs-lookup"><span data-stu-id="4be9a-280">*Private network* (subnets): We recommend that you have hello application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="4be9a-281">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="4be9a-281">Additional reading</span></span>

- [<span data-ttu-id="4be9a-282">Oracle ASM configureren</span><span class="sxs-lookup"><span data-stu-id="4be9a-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="4be9a-283">Oracle Data Guard configureren</span><span class="sxs-lookup"><span data-stu-id="4be9a-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="4be9a-284">Oracle Golden Gate configureren</span><span class="sxs-lookup"><span data-stu-id="4be9a-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="4be9a-285">Oracle back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="4be9a-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="4be9a-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4be9a-286">Next steps</span></span>

- [<span data-ttu-id="4be9a-287">Zelfstudie: Een maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="4be9a-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="4be9a-288">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="4be9a-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
