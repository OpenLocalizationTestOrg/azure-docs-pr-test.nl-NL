---
title: Ontwerpen en implementeren van een Oracle-database in Azure | Microsoft Docs
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
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="80510-103">Ontwerpen en implementeren van een Oracle-database in Azure</span><span class="sxs-lookup"><span data-stu-id="80510-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="80510-104">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="80510-104">Assumptions</span></span>

- <span data-ttu-id="80510-105">U bent van plan te migreren van een Oracle-database van on-premises naar Azure.</span><span class="sxs-lookup"><span data-stu-id="80510-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="80510-106">U hebt een goed begrip van de verschillende metrische gegevens in rapporten voor Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="80510-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="80510-107">U hebt een basislijn begrip van de prestaties van toepassingen en platforms te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="80510-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="80510-108">Doelstellingen</span><span class="sxs-lookup"><span data-stu-id="80510-108">Goals</span></span>

- <span data-ttu-id="80510-109">Begrijpen hoe uw implementatie Oracle in Azure te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="80510-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="80510-110">Gebruik de opties voor een Oracle-database in een Azure-omgeving afstemmen van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="80510-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="80510-111">De verschillen tussen een on-premises en Azure-implementatie</span><span class="sxs-lookup"><span data-stu-id="80510-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="80510-112">Hier volgen een aantal belangrijke zaken rekening moet houden wanneer u bij het migreren van on-premises toepassingen naar Azure.</span><span class="sxs-lookup"><span data-stu-id="80510-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="80510-113">Een belangrijk verschil is dat de resources, zoals virtuele machines, schijven en virtuele netwerken in een Azure-implementatie moet worden gedeeld door andere clients.</span><span class="sxs-lookup"><span data-stu-id="80510-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="80510-114">Resources kunnen bovendien worden beperkt op basis van de vereisten.</span><span class="sxs-lookup"><span data-stu-id="80510-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="80510-115">In plaats van te focussen op het voorkomen (MBTF) mislukt, wordt Azure meer gericht op functionerende van de fout (MTTR).</span><span class="sxs-lookup"><span data-stu-id="80510-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="80510-116">De volgende tabel bevat enkele van de verschillen tussen een lokale implementatie en een Azure-implementatie van een Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="80510-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="80510-117">**Lokale implementatie**</span><span class="sxs-lookup"><span data-stu-id="80510-117">**On-premises implementation**</span></span> | <span data-ttu-id="80510-118">**Azure-implementatie**</span><span class="sxs-lookup"><span data-stu-id="80510-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="80510-119">**Netwerken**</span><span class="sxs-lookup"><span data-stu-id="80510-119">**Networking**</span></span> |<span data-ttu-id="80510-120">LAN/WAN</span><span class="sxs-lookup"><span data-stu-id="80510-120">LAN/WAN</span></span>  |<span data-ttu-id="80510-121">SDN (software gedefinieerde netwerken)</span><span class="sxs-lookup"><span data-stu-id="80510-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="80510-122">**Beveiligingsgroep**</span><span class="sxs-lookup"><span data-stu-id="80510-122">**Security group**</span></span> |<span data-ttu-id="80510-123">Hulpprogramma's voor beperking van de IP/poort</span><span class="sxs-lookup"><span data-stu-id="80510-123">IP/port restriction tools</span></span> |[<span data-ttu-id="80510-124">Netwerkbeveiligingsgroep (NSG)</span><span class="sxs-lookup"><span data-stu-id="80510-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="80510-125">**Herstelmogelijkheden**</span><span class="sxs-lookup"><span data-stu-id="80510-125">**Resilience**</span></span> |<span data-ttu-id="80510-126">MBTF (gemiddelde tijd tussen storingen)</span><span class="sxs-lookup"><span data-stu-id="80510-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="80510-127">MTTR (gemiddelde tijd Recovery)</span><span class="sxs-lookup"><span data-stu-id="80510-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="80510-128">**Gepland onderhoud**</span><span class="sxs-lookup"><span data-stu-id="80510-128">**Planned maintenance**</span></span> |<span data-ttu-id="80510-129">Patchen of upgrades worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="80510-129">Patching/upgrades</span></span>|<span data-ttu-id="80510-130">[Beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patchen/upgrades worden beheerd door Azure)</span><span class="sxs-lookup"><span data-stu-id="80510-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="80510-131">**Resource**</span><span class="sxs-lookup"><span data-stu-id="80510-131">**Resource**</span></span> |<span data-ttu-id="80510-132">Toegewezen</span><span class="sxs-lookup"><span data-stu-id="80510-132">Dedicated</span></span>  |<span data-ttu-id="80510-133">Gedeeld met andere clients</span><span class="sxs-lookup"><span data-stu-id="80510-133">Shared with other clients</span></span>|
> | <span data-ttu-id="80510-134">**Regio 's**</span><span class="sxs-lookup"><span data-stu-id="80510-134">**Regions**</span></span> |<span data-ttu-id="80510-135">Datacenters</span><span class="sxs-lookup"><span data-stu-id="80510-135">Datacenters</span></span> |[<span data-ttu-id="80510-136">Regio paren</span><span class="sxs-lookup"><span data-stu-id="80510-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="80510-137">**Storage**</span><span class="sxs-lookup"><span data-stu-id="80510-137">**Storage**</span></span> |<span data-ttu-id="80510-138">SAN of fysieke schijven</span><span class="sxs-lookup"><span data-stu-id="80510-138">SAN/physical disks</span></span> |[<span data-ttu-id="80510-139">Beheerde Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="80510-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="80510-140">**Schalen**</span><span class="sxs-lookup"><span data-stu-id="80510-140">**Scale**</span></span> |<span data-ttu-id="80510-141">Verticale schaal</span><span class="sxs-lookup"><span data-stu-id="80510-141">Vertical scale</span></span> |<span data-ttu-id="80510-142">Horizontaal schalen</span><span class="sxs-lookup"><span data-stu-id="80510-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="80510-143">Vereisten</span><span class="sxs-lookup"><span data-stu-id="80510-143">Requirements</span></span>

- <span data-ttu-id="80510-144">Bepaalt de snelheid van grootte en de groei van de database.</span><span class="sxs-lookup"><span data-stu-id="80510-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="80510-145">Bepaal de vereisten IOP's, die u kunt een schatting maken op basis van Oracle AWR rapporten of andere hulpprogramma's voor Netwerkcontrole.</span><span class="sxs-lookup"><span data-stu-id="80510-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="80510-146">Configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="80510-146">Configuration options</span></span>

<span data-ttu-id="80510-147">Er zijn vier mogelijke gebieden die u afstemmen kunt om de prestaties verbeteren in een Azure-omgeving:</span><span class="sxs-lookup"><span data-stu-id="80510-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="80510-148">Grootte van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="80510-148">Virtual machine size</span></span>
- <span data-ttu-id="80510-149">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="80510-149">Network throughput</span></span>
- <span data-ttu-id="80510-150">Schijftypen en configuraties</span><span class="sxs-lookup"><span data-stu-id="80510-150">Disk types and configurations</span></span>
- <span data-ttu-id="80510-151">Schijf-cache-instellingen</span><span class="sxs-lookup"><span data-stu-id="80510-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="80510-152">Een AWR genereren</span><span class="sxs-lookup"><span data-stu-id="80510-152">Generate an AWR report</span></span>

<span data-ttu-id="80510-153">Als u een bestaande een Oracle-database en u van plan bent om te migreren naar Azure, hebt u verschillende mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="80510-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="80510-154">U kunt het rapport Oracle AWR ophalen van de metrische gegevens (IOP's, Mbps, GiBs, enzovoort) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="80510-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="80510-155">Kies vervolgens de virtuele machine op basis van de metrische gegevens die u hebt verzameld.</span><span class="sxs-lookup"><span data-stu-id="80510-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="80510-156">Of u kunt contact opnemen met uw team voor infrastructuur voor vergelijkbare informatie.</span><span class="sxs-lookup"><span data-stu-id="80510-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="80510-157">U kunt uw rapport AWR uitvoeren tijdens normale en piekuren werkbelastingen, zodat u kunt vergelijken.</span><span class="sxs-lookup"><span data-stu-id="80510-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="80510-158">Op basis van deze rapporten, kunt u de virtuele machines op basis van de gemiddelde werkbelasting of de maximale werkbelasting groot.</span><span class="sxs-lookup"><span data-stu-id="80510-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="80510-159">Hieronder volgt een voorbeeld van hoe u een rapport AWR genereren:</span><span class="sxs-lookup"><span data-stu-id="80510-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="80510-160">De belangrijkste metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="80510-160">Key metrics</span></span>

<span data-ttu-id="80510-161">Hieronder volgen de metrische gegevens die u kunt het rapport AWR ophalen:</span><span class="sxs-lookup"><span data-stu-id="80510-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="80510-162">Totaal aantal kernen</span><span class="sxs-lookup"><span data-stu-id="80510-162">Total number of cores</span></span>
- <span data-ttu-id="80510-163">CPU-kloksnelheid</span><span class="sxs-lookup"><span data-stu-id="80510-163">CPU clock speed</span></span>
- <span data-ttu-id="80510-164">Totale geheugen in GB</span><span class="sxs-lookup"><span data-stu-id="80510-164">Total memory in GB</span></span>
- <span data-ttu-id="80510-165">CPU-gebruik</span><span class="sxs-lookup"><span data-stu-id="80510-165">CPU utilization</span></span>
- <span data-ttu-id="80510-166">Overdrachtssnelheid piek</span><span class="sxs-lookup"><span data-stu-id="80510-166">Peak data transfer rate</span></span>
- <span data-ttu-id="80510-167">Het aantal i/o-wijzigingen (lezen/schrijven)</span><span class="sxs-lookup"><span data-stu-id="80510-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="80510-168">Opnieuw logboek snelheid (MBPs)</span><span class="sxs-lookup"><span data-stu-id="80510-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="80510-169">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="80510-169">Network throughput</span></span>
- <span data-ttu-id="80510-170">Netwerk latentie snelheid (laag/hoog)</span><span class="sxs-lookup"><span data-stu-id="80510-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="80510-171">Databasegrootte in GB</span><span class="sxs-lookup"><span data-stu-id="80510-171">Database size in GB</span></span>
- <span data-ttu-id="80510-172">Bytes ontvangen via SQL * Net van/naar client</span><span class="sxs-lookup"><span data-stu-id="80510-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="80510-173">Grootte van virtuele machine</span><span class="sxs-lookup"><span data-stu-id="80510-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="80510-174">1. VM-grootte van een schatting op basis van CPU, geheugen en i/o-gebruik van het rapport AWR</span><span class="sxs-lookup"><span data-stu-id="80510-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="80510-175">U kunt bekijken wat is de bovenste vijf is een time-out opgetreden voor gebeurtenissen die aangeven waar de knelpunten in het systeem zijn.</span><span class="sxs-lookup"><span data-stu-id="80510-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="80510-176">In het volgende diagram wordt is de synchronisatie log-bestand bijvoorbeeld aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="80510-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="80510-177">Dit geeft het aantal wacht die vereist zijn voordat de LGWR de logboekbuffer naar het logboekbestand opnieuw schrijft.</span><span class="sxs-lookup"><span data-stu-id="80510-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="80510-178">Deze resultaten blijkt dat beter presterende opslag of schijven vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="80510-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="80510-179">Het diagram toont bovendien ook het aantal CPU (kernen) en de hoeveelheid geheugen.</span><span class="sxs-lookup"><span data-stu-id="80510-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![Schermafbeelding van de rapportpagina AWR](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="80510-181">Het volgende diagram toont het totale aantal i/o lezen en schrijven.</span><span class="sxs-lookup"><span data-stu-id="80510-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="80510-182">Er zijn 59 lezen en 247.3 GB geschreven tijdens de periode van het rapport.</span><span class="sxs-lookup"><span data-stu-id="80510-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![Schermafbeelding van de rapportpagina AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="80510-184">2. Kies een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="80510-184">2. Choose a VM</span></span>

<span data-ttu-id="80510-185">Op basis van de informatie die u uit het rapport AWR hebt verzameld, is de volgende stap om te kiezen van een virtuele machine met een vergelijkbare grootte die voldoet aan uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="80510-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="80510-186">U vindt een lijst met beschikbare virtuele machines in het artikel [geoptimaliseerd voor geheugen](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="80510-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="80510-187">3. De grootte van de virtuele machine met een vergelijkbare VM-reeks op basis van de ACU stemmen</span><span class="sxs-lookup"><span data-stu-id="80510-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="80510-188">Nadat u de virtuele machine hebt gekozen, moet u aandacht schenken aan de ACU voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="80510-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="80510-189">U kunt een andere virtuele machine op basis van de waarde ACU dat beter past bij uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="80510-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="80510-190">Zie voor meer informatie [Azure compute eenheid](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="80510-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Schermafbeelding van de pagina ACU-eenheden](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="80510-192">Netwerkdoorvoer</span><span class="sxs-lookup"><span data-stu-id="80510-192">Network throughput</span></span>

<span data-ttu-id="80510-193">Het volgende diagram toont de relatie tussen de doorvoer en IOP's:</span><span class="sxs-lookup"><span data-stu-id="80510-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![Schermopname van doorvoer](./media/oracle-design/throughput.png)

<span data-ttu-id="80510-195">De totale netwerkdoorvoer geschat op basis van de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="80510-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="80510-196">SQL * Net verkeer</span><span class="sxs-lookup"><span data-stu-id="80510-196">SQL*Net traffic</span></span>
- <span data-ttu-id="80510-197">MBps x het aantal servers (uitgaande stream zoals Oracle Data Guard)</span><span class="sxs-lookup"><span data-stu-id="80510-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="80510-198">Andere factoren, zoals toepassing replicatie</span><span class="sxs-lookup"><span data-stu-id="80510-198">Other factors, such as application replication</span></span>

![Schermafbeelding van de SQL * Net doorvoer](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="80510-200">Op basis van de vereisten van uw netwerkbandbreedte, zijn er verschillende gatewaytypen waarmee u kunt kiezen uit.</span><span class="sxs-lookup"><span data-stu-id="80510-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="80510-201">Het gaat hierbij om basic, VpnGw en Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="80510-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="80510-202">Zie voor meer informatie de [VPN-gateway pagina met prijzen](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="80510-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="80510-203">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="80510-203">**Recommendations**</span></span>

- <span data-ttu-id="80510-204">Netwerklatentie hoger vergeleken met een on-premises implementatie.</span><span class="sxs-lookup"><span data-stu-id="80510-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="80510-205">Netwerk ronde reizen kan aanzienlijk verminderen, de prestaties verbeteren.</span><span class="sxs-lookup"><span data-stu-id="80510-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="80510-206">Als u retourbewerkingen, worden geconsolideerd toepassingen met hoge transacties of 'chatty' apps op dezelfde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="80510-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="80510-207">Schijftypen en configuraties</span><span class="sxs-lookup"><span data-stu-id="80510-207">Disk types and configurations</span></span>

- <span data-ttu-id="80510-208">*Standaard OS schijven*: deze schijftypen bieden permanente gegevens en opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="80510-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="80510-209">Ze zijn geoptimaliseerd voor OS toegang bij het opstarten en zijn niet bedoeld voor transactionele of datawarehouse-werkbelastingen (analytische).</span><span class="sxs-lookup"><span data-stu-id="80510-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="80510-210">*Schijven zonder begeleiding*: met deze schijftypen die u beheert de opslagaccounts die voor het opslaan van de virtuele harde schijf (VHD)-bestanden die met uw VM-schijven overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="80510-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="80510-211">VHD-bestanden worden opgeslagen als pagina-blobs in Azure storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="80510-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="80510-212">*Schijven die worden beheerd*: Azure beheert de storage-accounts die u voor uw VM-schijven gebruikt.</span><span class="sxs-lookup"><span data-stu-id="80510-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="80510-213">U geeft het schijftype (premium of standaard) en de grootte van de schijf die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="80510-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="80510-214">Azure maakt en beheert de schijf voor u.</span><span class="sxs-lookup"><span data-stu-id="80510-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="80510-215">*Premium-opslag-schijven*: deze schijftypen geschikt zijn voor productieworkloads.</span><span class="sxs-lookup"><span data-stu-id="80510-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="80510-216">Premium-opslag biedt ondersteuning voor VM-schijven die kunnen worden bijgevoegd aan een specifieke grootte-serie-VM's, zoals Active Directory, DSv2 GS en F-serie virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="80510-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="80510-217">De premium-schijf is voorzien van verschillende grootte en kunt u kiezen tussen schijven variërend van 32 GB tot 4096 GB.</span><span class="sxs-lookup"><span data-stu-id="80510-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="80510-218">De grootte van elke schijf heeft zijn eigen prestatiespecificaties.</span><span class="sxs-lookup"><span data-stu-id="80510-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="80510-219">Afhankelijk van uw toepassing, kunt u een of meer schijven aan uw virtuele machine te koppelen.</span><span class="sxs-lookup"><span data-stu-id="80510-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="80510-220">Wanneer u een nieuwe beheerde schijf van de portal maakt, kunt u de **accounttype** voor het type schijf dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="80510-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="80510-221">Houd er rekening mee dat niet alle beschikbare schijven worden weergegeven in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="80510-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="80510-222">Nadat u een bepaalde VM-grootte hebt gekozen, ziet u het menu alleen de beschikbare premium-opslag SKU's die zijn gebaseerd op deze VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="80510-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![Schermafbeelding van de beheerde schijfpagina](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="80510-224">Zie voor meer informatie [beheerde schijven voor virtuele machines en hoge prestaties Premium-opslag](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="80510-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="80510-225">Nadat u uw opslag op een virtuele machine hebt geconfigureerd, kunt u laden van de schijven te testen voordat u een database te maken.</span><span class="sxs-lookup"><span data-stu-id="80510-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="80510-226">De i/o-snelheid in termen van de latentie en de doorvoer weten, kunt u bepalen of de VM's de verwachte doorvoer latentie doelen ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="80510-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="80510-227">Er zijn een aantal hulpprogramma's voor de toepassing werklast testen, zoals Oracle Orion Sysbench en Fio.</span><span class="sxs-lookup"><span data-stu-id="80510-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="80510-228">Voer de test load opnieuw uit nadat u een Oracle-database hebt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="80510-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="80510-229">Start de werkbelasting van uw normale en piekuren en de resultaten staat dat u de basislijn van uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="80510-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="80510-230">Kan het zijn belangrijker grootte van de opslag op basis van de snelheid van de IOPS in plaats van de grootte van de opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="80510-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="80510-231">Bijvoorbeeld, als het aantal IOPS dat vereist 5.000 is, maar u alleen 200 GB hoeft, u mogelijk nog steeds de P30 klasse premium schijf ook al beschikt u over meer dan 200 GB aan opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="80510-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="80510-232">De snelheid IOP's kan worden verkregen van het rapport AWR.</span><span class="sxs-lookup"><span data-stu-id="80510-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="80510-233">Dit wordt bepaald door het logboek opnieuw, fysieke leesbewerkingen en snelheid van schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="80510-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![Schermafbeelding van de rapportpagina AWR](./media/oracle-design/awr_report.png)

<span data-ttu-id="80510-235">Bijvoorbeeld, is de grootte van de opnieuw 12,200,000 bytes per seconde die gelijk aan 11.63 MBPs is.</span><span class="sxs-lookup"><span data-stu-id="80510-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="80510-236">Het aantal IOPS dat is 12.200.000 / 2,358 = 5,174.</span><span class="sxs-lookup"><span data-stu-id="80510-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="80510-237">Nadat u een duidelijk beeld van de i/o-vereisten hebt, kunt u een combinatie van stations die geschikt zijn om te voldoen aan deze vereisten zijn.</span><span class="sxs-lookup"><span data-stu-id="80510-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="80510-238">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="80510-238">**Recommendations**</span></span>

- <span data-ttu-id="80510-239">Voor gegevens verdeeld tabelruimte, de i/o-werkbelasting over een aantal schijven met behulp van beheerde opslaggroep of Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="80510-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="80510-240">Als de blokgrootte van i/o-voor lees-intensieve en write-intensieve bewerkingen toeneemt, Voeg meer gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="80510-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="80510-241">Vergroot de blokgrootte voor grote opeenvolgende processen.</span><span class="sxs-lookup"><span data-stu-id="80510-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="80510-242">Gegevenscompressie gebruiken om te beperken van i/o (voor gegevens en indexen).</span><span class="sxs-lookup"><span data-stu-id="80510-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="80510-243">Afzonderlijke opnieuw Logboeken, systeem en temps en ongedaan maken van TS op afzonderlijke gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="80510-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="80510-244">Niet alle toepassingsbestanden op standaard OS-schijven (/ dev/sda) plaatsen.</span><span class="sxs-lookup"><span data-stu-id="80510-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="80510-245">Deze schijven worden niet geoptimaliseerd voor snelle VM opstarttijden, en ze bieden geen goede prestaties voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="80510-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="80510-246">Schijf-cache-instellingen</span><span class="sxs-lookup"><span data-stu-id="80510-246">Disk cache settings</span></span>

<span data-ttu-id="80510-247">Er zijn drie opties voor hostcaching:</span><span class="sxs-lookup"><span data-stu-id="80510-247">There are three options for host caching:</span></span>

- <span data-ttu-id="80510-248">*Alleen-lezen*: alle aanvragen in cache zijn opgeslagen voor toekomstige leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="80510-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="80510-249">Alle schrijfbewerkingen worden vastgehouden rechtstreeks naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="80510-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="80510-250">*Lezen / schrijven*: dit is een 'read-ahead' algoritme.</span><span class="sxs-lookup"><span data-stu-id="80510-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="80510-251">Lees- en schrijfbewerkingen in cache zijn opgeslagen voor toekomstige leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="80510-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="80510-252">Niet-write-through schrijfbewerkingen worden eerst naar de lokale cache persistent.</span><span class="sxs-lookup"><span data-stu-id="80510-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="80510-253">Voor SQL Server, schrijfbewerkingen naar Azure Storage vastgehouden omdat deze write-through gebruikt.</span><span class="sxs-lookup"><span data-stu-id="80510-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="80510-254">Het bevat ook de laagste latentie voor de schijf voor lichte werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="80510-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="80510-255">*Geen* (uitgeschakeld): deze optie gebruikt, kunt u de cache overslaan.</span><span class="sxs-lookup"><span data-stu-id="80510-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="80510-256">Alle gegevens is overgebracht naar de schijf en opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="80510-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="80510-257">Deze methode biedt u de hoogste i/o-snelheid voor i/o-intensieve werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="80510-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="80510-258">U moet ook rekening te houden 'transactiekosten'.</span><span class="sxs-lookup"><span data-stu-id="80510-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="80510-259">**Aanbevelingen**</span><span class="sxs-lookup"><span data-stu-id="80510-259">**Recommendations**</span></span>

<span data-ttu-id="80510-260">Als u wilt de doorvoer maximaliseren, wordt aangeraden dat u met begint **geen** voor hostcaching.</span><span class="sxs-lookup"><span data-stu-id="80510-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="80510-261">Voor Premium-opslag, houd er rekening mee moet u de 'barrières"uitschakelen wanneer u het bestandssysteem met koppelt de **ReadOnly** of **geen** opties.</span><span class="sxs-lookup"><span data-stu-id="80510-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="80510-262">Het bestand /etc/fstab bijwerken met de UUID aan de schijven.</span><span class="sxs-lookup"><span data-stu-id="80510-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="80510-263">Zie voor meer informatie [Premium-opslag voor virtuele Linux-machines](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="80510-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Schermafbeelding van de beheerde schijfpagina](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="80510-265">Voor OS-schijven, gebruikt u de standaard **lezen/schrijven** opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="80510-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="80510-266">Gebruik voor het systeem, TEMP en ongedaan maken **geen** voor opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="80510-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="80510-267">Gebruik voor gegevens, **geen** voor opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="80510-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="80510-268">Maar als de database alleen-lezen of lees-intensieve is, gebruikt u **alleen-lezen** opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="80510-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="80510-269">Nadat de instelling van de schijf gegevens zijn opgeslagen, kunt u de host-cache-instelling niet wijzigen, tenzij u ontkoppelen van het station op het niveau van het besturingssysteem en koppel deze het vervolgens opnieuw nadat u de wijziging hebt aangebracht.</span><span class="sxs-lookup"><span data-stu-id="80510-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="80510-270">Beveiliging</span><span class="sxs-lookup"><span data-stu-id="80510-270">Security</span></span>

<span data-ttu-id="80510-271">Nadat u hebt ingesteld en geconfigureerd van uw Azure-omgeving, wordt de volgende stap is om uw netwerk te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="80510-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="80510-272">Hier volgen enkele aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="80510-272">Here are some recommendations:</span></span>

- <span data-ttu-id="80510-273">*NSG-beleid*: NSG worden gedefinieerd met een subnet of NIC.</span><span class="sxs-lookup"><span data-stu-id="80510-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="80510-274">Het is eenvoudiger om toegang te controleren op subnetniveau zowel voor beveiliging en werking routering voor dingen zoals firewalls, toepassing.</span><span class="sxs-lookup"><span data-stu-id="80510-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="80510-275">*Jumpbox*: voor een beter beveiligde toegang beheerders moeten niet rechtstreeks toegang tot de toepassingsservice of de database.</span><span class="sxs-lookup"><span data-stu-id="80510-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="80510-276">Een jumpbox wordt gebruikt als een medium tussen de administrator-machine en de Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="80510-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="80510-277">![Schermafbeelding van de topologie Jumpbox pagina](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="80510-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="80510-278">De beheerder machine moet IP beperkte toegang tot de jumpbox alleen aanbieden.</span><span class="sxs-lookup"><span data-stu-id="80510-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="80510-279">De jumpbox moet toegang hebben tot de toepassing en de database.</span><span class="sxs-lookup"><span data-stu-id="80510-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="80510-280">*Particulier netwerk* (subnetten): We raden u aan de toepassingsservice en de database op afzonderlijke subnetten, zodat betere controle kan worden ingesteld door het NSG-beleid.</span><span class="sxs-lookup"><span data-stu-id="80510-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="80510-281">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="80510-281">Additional reading</span></span>

- [<span data-ttu-id="80510-282">Oracle ASM configureren</span><span class="sxs-lookup"><span data-stu-id="80510-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="80510-283">Oracle Data Guard configureren</span><span class="sxs-lookup"><span data-stu-id="80510-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="80510-284">Oracle Golden Gate configureren</span><span class="sxs-lookup"><span data-stu-id="80510-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="80510-285">Oracle back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="80510-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="80510-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80510-286">Next steps</span></span>

- [<span data-ttu-id="80510-287">Zelfstudie: Een maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="80510-287">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="80510-288">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="80510-288">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
