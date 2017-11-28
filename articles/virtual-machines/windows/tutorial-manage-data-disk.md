---
title: aaaManage Azure schijven Hello Azure PowerShell | Microsoft Docs
description: Zelfstudie - Azure-schijven Hello Azure PowerShell beheren
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="6fd3f-103">Azure-schijven met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="6fd3f-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="6fd3f-104">Azure virtuele machines gebruiken schijven toostore Hallo VMs-besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="6fd3f-105">Bij het maken van een virtuele machine is het belangrijk toochoose een schijfgrootte en configuratie juiste toohello verwacht werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="6fd3f-106">Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="6fd3f-107">U meer informatie over:</span><span class="sxs-lookup"><span data-stu-id="6fd3f-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6fd3f-108">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6fd3f-109">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-109">Data disks</span></span>
> * <span data-ttu-id="6fd3f-110">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="6fd3f-111">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="6fd3f-111">Disk performance</span></span>
> * <span data-ttu-id="6fd3f-112">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6fd3f-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="6fd3f-113">Deze zelfstudie vereist hello Azure PowerShell-moduleversie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6fd3f-114">Voer ` Get-Module -ListAvailable AzureRM` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="6fd3f-115">Als u tooupgrade moet, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="6fd3f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="6fd3f-116">Standaard Azure-schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-116">Default Azure disks</span></span>

<span data-ttu-id="6fd3f-117">Wanneer een virtuele machine van Azure is gemaakt, zijn twee schijven automatisch gekoppelde toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="6fd3f-118">**Besturingssysteemschijf** - besturingssysteem schijven kunnen worden verkleind up too1 terabyte en hosts Hallo VMs-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="6fd3f-119">Hallo OS-schijf is toegewezen stationsletter van *c:* standaard.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="6fd3f-120">configuratie van de besturingssysteemschijf Hallo van de schijfcache Hallo is geoptimaliseerd voor OS-prestaties.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="6fd3f-121">Hallo OS-schijf **beter niet** toepassingen of gegevens hosten.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="6fd3f-122">Gebruik een gegevensschijf, die verderop in dit artikel wordt beschreven voor toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="6fd3f-123">**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich bevindt op Hallo dezelfde Azure-host als Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="6fd3f-124">Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="6fd3f-125">Als Hallo VM verplaatste tooa nieuwe host is, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="6fd3f-126">Hallo-grootte van de tijdelijke schijf hello wordt bepaald door Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="6fd3f-127">Tijdelijke schijven zijn toegewezen stationsletter van *d:* standaard.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="6fd3f-128">Tijdelijke schijfgrootten</span><span class="sxs-lookup"><span data-stu-id="6fd3f-128">Temporary disk sizes</span></span>

| <span data-ttu-id="6fd3f-129">Type</span><span class="sxs-lookup"><span data-stu-id="6fd3f-129">Type</span></span> | <span data-ttu-id="6fd3f-130">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="6fd3f-130">VM Size</span></span> | <span data-ttu-id="6fd3f-131">Maximumgrootte van tijdelijke schijf (GB)</span><span class="sxs-lookup"><span data-stu-id="6fd3f-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="6fd3f-132">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="6fd3f-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6fd3f-133">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-133">A and D series</span></span> | <span data-ttu-id="6fd3f-134">800</span><span class="sxs-lookup"><span data-stu-id="6fd3f-134">800</span></span> |
| [<span data-ttu-id="6fd3f-135">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="6fd3f-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6fd3f-136">F-serie</span><span class="sxs-lookup"><span data-stu-id="6fd3f-136">F series</span></span> | <span data-ttu-id="6fd3f-137">800</span><span class="sxs-lookup"><span data-stu-id="6fd3f-137">800</span></span> |
| [<span data-ttu-id="6fd3f-138">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="6fd3f-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6fd3f-139">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="6fd3f-139">D and G series</span></span> | <span data-ttu-id="6fd3f-140">6144</span><span class="sxs-lookup"><span data-stu-id="6fd3f-140">6144</span></span> |
| [<span data-ttu-id="6fd3f-141">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="6fd3f-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6fd3f-142">L-reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-142">L series</span></span> | <span data-ttu-id="6fd3f-143">5630</span><span class="sxs-lookup"><span data-stu-id="6fd3f-143">5630</span></span> |
| [<span data-ttu-id="6fd3f-144">GPU</span><span class="sxs-lookup"><span data-stu-id="6fd3f-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6fd3f-145">N reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-145">N series</span></span> | <span data-ttu-id="6fd3f-146">1440</span><span class="sxs-lookup"><span data-stu-id="6fd3f-146">1440</span></span> |
| [<span data-ttu-id="6fd3f-147">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="6fd3f-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6fd3f-148">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-148">A and H series</span></span> | <span data-ttu-id="6fd3f-149">2000</span><span class="sxs-lookup"><span data-stu-id="6fd3f-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="6fd3f-150">Azure gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-150">Azure data disks</span></span>

<span data-ttu-id="6fd3f-151">Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="6fd3f-152">Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="6fd3f-153">Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="6fd3f-154">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunnen worden aangesloten tooa VM.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="6fd3f-155">Voor elke VM-core, kunnen twee schijven worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="6fd3f-156">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="6fd3f-156">Max data disks per VM</span></span>

| <span data-ttu-id="6fd3f-157">Type</span><span class="sxs-lookup"><span data-stu-id="6fd3f-157">Type</span></span> | <span data-ttu-id="6fd3f-158">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="6fd3f-158">VM Size</span></span> | <span data-ttu-id="6fd3f-159">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="6fd3f-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="6fd3f-160">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="6fd3f-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="6fd3f-161">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-161">A and D series</span></span> | <span data-ttu-id="6fd3f-162">32</span><span class="sxs-lookup"><span data-stu-id="6fd3f-162">32</span></span> |
| [<span data-ttu-id="6fd3f-163">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="6fd3f-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="6fd3f-164">F-serie</span><span class="sxs-lookup"><span data-stu-id="6fd3f-164">F series</span></span> | <span data-ttu-id="6fd3f-165">32</span><span class="sxs-lookup"><span data-stu-id="6fd3f-165">32</span></span> |
| [<span data-ttu-id="6fd3f-166">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="6fd3f-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="6fd3f-167">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="6fd3f-167">D and G series</span></span> | <span data-ttu-id="6fd3f-168">64</span><span class="sxs-lookup"><span data-stu-id="6fd3f-168">64</span></span> |
| [<span data-ttu-id="6fd3f-169">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="6fd3f-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="6fd3f-170">L-reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-170">L series</span></span> | <span data-ttu-id="6fd3f-171">64</span><span class="sxs-lookup"><span data-stu-id="6fd3f-171">64</span></span> |
| [<span data-ttu-id="6fd3f-172">GPU</span><span class="sxs-lookup"><span data-stu-id="6fd3f-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="6fd3f-173">N reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-173">N series</span></span> | <span data-ttu-id="6fd3f-174">48</span><span class="sxs-lookup"><span data-stu-id="6fd3f-174">48</span></span> |
| [<span data-ttu-id="6fd3f-175">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="6fd3f-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="6fd3f-176">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="6fd3f-176">A and H series</span></span> | <span data-ttu-id="6fd3f-177">32</span><span class="sxs-lookup"><span data-stu-id="6fd3f-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="6fd3f-178">VM-schijftypen</span><span class="sxs-lookup"><span data-stu-id="6fd3f-178">VM disk types</span></span>

<span data-ttu-id="6fd3f-179">Azure biedt twee typen van de schijf.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="6fd3f-180">Standard-schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-180">Standard disk</span></span>

<span data-ttu-id="6fd3f-181">Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="6fd3f-182">Standaardschijven zijn ideaal voor een voordelige ontwikkelen en testen werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="6fd3f-183">Premium-schijf</span><span class="sxs-lookup"><span data-stu-id="6fd3f-183">Premium disk</span></span>

<span data-ttu-id="6fd3f-184">Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="6fd3f-185">Ideaal voor virtuele machines met productie werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="6fd3f-186">Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="6fd3f-187">Premium-schijven zijn drie typen (P10, P20, P30), Hallo grootte van Hallo schijf Hallo schijftype bepaalt.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="6fd3f-188">Wanneer u selecteert, wordt de waarde van een schijf grootte Hallo toohello volgende type afgerond.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="6fd3f-189">Bijvoorbeeld, als Hallo grootte lager dan 128 GB Hallo schijftype is worden P10, tussen 129 512 P20 en meer dan 512 P30.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="6fd3f-190">Premium-schijfprestaties</span><span class="sxs-lookup"><span data-stu-id="6fd3f-190">Premium disk performance</span></span>

|<span data-ttu-id="6fd3f-191">Premium-opslag schijftype</span><span class="sxs-lookup"><span data-stu-id="6fd3f-191">Premium storage disk type</span></span> | <span data-ttu-id="6fd3f-192">P10</span><span class="sxs-lookup"><span data-stu-id="6fd3f-192">P10</span></span> | <span data-ttu-id="6fd3f-193">P20</span><span class="sxs-lookup"><span data-stu-id="6fd3f-193">P20</span></span> | <span data-ttu-id="6fd3f-194">P30</span><span class="sxs-lookup"><span data-stu-id="6fd3f-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6fd3f-195">Grootte van de schijf (afronden)</span><span class="sxs-lookup"><span data-stu-id="6fd3f-195">Disk size (round up)</span></span> | <span data-ttu-id="6fd3f-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="6fd3f-196">128 GB</span></span> | <span data-ttu-id="6fd3f-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="6fd3f-197">512 GB</span></span> | <span data-ttu-id="6fd3f-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="6fd3f-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="6fd3f-199">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="6fd3f-199">IOPS per disk</span></span> | <span data-ttu-id="6fd3f-200">500</span><span class="sxs-lookup"><span data-stu-id="6fd3f-200">500</span></span> | <span data-ttu-id="6fd3f-201">2,300</span><span class="sxs-lookup"><span data-stu-id="6fd3f-201">2,300</span></span> | <span data-ttu-id="6fd3f-202">5,000</span><span class="sxs-lookup"><span data-stu-id="6fd3f-202">5,000</span></span> |
<span data-ttu-id="6fd3f-203">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="6fd3f-203">Throughput per disk</span></span> | <span data-ttu-id="6fd3f-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="6fd3f-204">100 MB/s</span></span> | <span data-ttu-id="6fd3f-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="6fd3f-205">150 MB/s</span></span> | <span data-ttu-id="6fd3f-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="6fd3f-206">200 MB/s</span></span> |

<span data-ttu-id="6fd3f-207">Tijdens het Hallo boven tabel identificeert max. IOP's per schijf, kan een hoger niveau van de prestaties van worden bereikt door meerdere gegevensschijven te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="6fd3f-208">64 gegevens schijven kunnen worden gekoppeld voor het exemplaar tooStandard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="6fd3f-209">Als u elk van deze schijven worden aangepast als een P30, kan een maximum van 80.000 IOP's kan worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="6fd3f-210">Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="6fd3f-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="6fd3f-211">Maken en koppelen van schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-211">Create and attach disks</span></span>

<span data-ttu-id="6fd3f-212">toocomplete hello voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="6fd3f-213">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="6fd3f-214">Wanneer werkende Hallo-zelfstudie vervangt benoemt Hallo resourcegroep en de VM waar nodig.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="6fd3f-215">Maken van de eerste configuratie Hallo met [nieuw AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="6fd3f-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="6fd3f-216">Hallo volgt configureert u een schijf die 128 GB groot is.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="6fd3f-217">Hallo gegevensschijf maken met de Hallo [nieuw AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="6fd3f-218">Get Hallo virtuele machine die u wilt dat tooadd Hallo gegevens schijf toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="6fd3f-219">Add Hallo gegevens schijf toohello Virtuele-machineconfiguratie Hello [toevoegen AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="6fd3f-220">Hallo virtuele machine bijwerken met Hallo [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="6fd3f-221">Gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6fd3f-221">Prepare data disks</span></span>

<span data-ttu-id="6fd3f-222">Als een schijf is aangesloten toohello virtuele machine, moet Hallo besturingssysteem geconfigureerd toobe toouse Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="6fd3f-223">Hallo volgende voorbeeld ziet u hoe de eerste Hallo-schijf toegevoegd voor het configureren van toomanually toohello VM.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="6fd3f-224">Dit proces kan ook worden geautomatiseerd met Hallo [extensie voor aangepaste scripts](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6fd3f-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="6fd3f-225">Handmatige configuratie</span><span class="sxs-lookup"><span data-stu-id="6fd3f-225">Manual configuration</span></span>

<span data-ttu-id="6fd3f-226">Maak een RDP-verbinding met de Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="6fd3f-227">Opent u PowerShell en voer dit script.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="6fd3f-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6fd3f-228">Next steps</span></span>

<span data-ttu-id="6fd3f-229">In deze zelfstudie hebt u geleerd over VM schijven onderwerpen, zoals:</span><span class="sxs-lookup"><span data-stu-id="6fd3f-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6fd3f-230">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="6fd3f-231">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-231">Data disks</span></span>
> * <span data-ttu-id="6fd3f-232">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="6fd3f-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="6fd3f-233">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="6fd3f-233">Disk performance</span></span>
> * <span data-ttu-id="6fd3f-234">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="6fd3f-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="6fd3f-235">Ga toohello volgende zelfstudie toolearn over het automatiseren van VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6fd3f-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6fd3f-236">VM-configuratie automatiseren</span><span class="sxs-lookup"><span data-stu-id="6fd3f-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
