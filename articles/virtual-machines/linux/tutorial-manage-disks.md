---
title: aaaManage Azure schijven Hello Azure CLI | Microsoft Docs
description: Zelfstudie - schijven van Azure met Azure CLI Hallo beheren
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="fe8d4-103">Azure-schijven Hello Azure CLI beheren</span><span class="sxs-lookup"><span data-stu-id="fe8d4-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="fe8d4-104">Azure virtuele machines gebruiken schijven toostore Hallo VMs-besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="fe8d4-105">Bij het maken van een virtuele machine is het belangrijk toochoose een schijfgrootte en configuratie juiste toohello verwacht werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="fe8d4-106">Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="fe8d4-107">U meer informatie over:</span><span class="sxs-lookup"><span data-stu-id="fe8d4-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe8d4-108">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="fe8d4-109">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-109">Data disks</span></span>
> * <span data-ttu-id="fe8d4-110">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="fe8d4-111">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-111">Disk performance</span></span>
> * <span data-ttu-id="fe8d4-112">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fe8d4-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="fe8d4-113">De schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="fe8d4-113">Resizing disks</span></span>
> * <span data-ttu-id="fe8d4-114">Schijf momentopnamen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fe8d4-115">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fe8d4-116">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fe8d4-117">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fe8d4-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="fe8d4-118">Standaard Azure-schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-118">Default Azure disks</span></span>

<span data-ttu-id="fe8d4-119">Wanneer een virtuele machine van Azure is gemaakt, zijn twee schijven automatisch gekoppelde toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="fe8d4-120">**Besturingssysteemschijf** - besturingssysteem schijven kunnen worden verkleind up too1 terabyte en hosts Hallo VMs-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="fe8d4-121">Hallo OS-schijf is gelabeld */dev/sda* standaard.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="fe8d4-122">configuratie van de besturingssysteemschijf Hallo van de schijfcache Hallo is geoptimaliseerd voor OS-prestaties.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="fe8d4-123">Vanwege deze configuratie Hallo besturingssysteemschijf **beter niet** toepassingen of gegevens hosten.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="fe8d4-124">Gebruik voor toepassingen en gegevens gegevensschijven, verderop in dit artikel worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="fe8d4-125">**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich bevindt op Hallo dezelfde Azure-host als Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="fe8d4-126">Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="fe8d4-127">Als Hallo VM verplaatste tooa nieuwe host is, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="fe8d4-128">Hallo-grootte van de tijdelijke schijf hello wordt bepaald door Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="fe8d4-129">Tijdelijke schijven zijn gelabeld */dev/sdb* en hebben een koppelpunt van *mnt*.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="fe8d4-130">Tijdelijke schijfgrootten</span><span class="sxs-lookup"><span data-stu-id="fe8d4-130">Temporary disk sizes</span></span>

| <span data-ttu-id="fe8d4-131">Type</span><span class="sxs-lookup"><span data-stu-id="fe8d4-131">Type</span></span> | <span data-ttu-id="fe8d4-132">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="fe8d4-132">VM Size</span></span> | <span data-ttu-id="fe8d4-133">Maximumgrootte van tijdelijke schijf (GB)</span><span class="sxs-lookup"><span data-stu-id="fe8d4-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="fe8d4-134">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="fe8d4-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="fe8d4-135">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-135">A and D series</span></span> | <span data-ttu-id="fe8d4-136">800</span><span class="sxs-lookup"><span data-stu-id="fe8d4-136">800</span></span> |
| [<span data-ttu-id="fe8d4-137">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="fe8d4-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="fe8d4-138">F-serie</span><span class="sxs-lookup"><span data-stu-id="fe8d4-138">F series</span></span> | <span data-ttu-id="fe8d4-139">800</span><span class="sxs-lookup"><span data-stu-id="fe8d4-139">800</span></span> |
| [<span data-ttu-id="fe8d4-140">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="fe8d4-141">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="fe8d4-141">D and G series</span></span> | <span data-ttu-id="fe8d4-142">6144</span><span class="sxs-lookup"><span data-stu-id="fe8d4-142">6144</span></span> |
| [<span data-ttu-id="fe8d4-143">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="fe8d4-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="fe8d4-144">L-reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-144">L series</span></span> | <span data-ttu-id="fe8d4-145">5630</span><span class="sxs-lookup"><span data-stu-id="fe8d4-145">5630</span></span> |
| [<span data-ttu-id="fe8d4-146">GPU</span><span class="sxs-lookup"><span data-stu-id="fe8d4-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="fe8d4-147">N reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-147">N series</span></span> | <span data-ttu-id="fe8d4-148">1440</span><span class="sxs-lookup"><span data-stu-id="fe8d4-148">1440</span></span> |
| [<span data-ttu-id="fe8d4-149">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="fe8d4-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="fe8d4-150">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-150">A and H series</span></span> | <span data-ttu-id="fe8d4-151">2000</span><span class="sxs-lookup"><span data-stu-id="fe8d4-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="fe8d4-152">Azure gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-152">Azure data disks</span></span>

<span data-ttu-id="fe8d4-153">Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="fe8d4-154">Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="fe8d4-155">Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="fe8d4-156">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven kunnen worden aangesloten tooa VM.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="fe8d4-157">Voor elke VM-core, kunnen twee schijven worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="fe8d4-158">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="fe8d4-158">Max data disks per VM</span></span>

| <span data-ttu-id="fe8d4-159">Type</span><span class="sxs-lookup"><span data-stu-id="fe8d4-159">Type</span></span> | <span data-ttu-id="fe8d4-160">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="fe8d4-160">VM Size</span></span> | <span data-ttu-id="fe8d4-161">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="fe8d4-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="fe8d4-162">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="fe8d4-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="fe8d4-163">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-163">A and D series</span></span> | <span data-ttu-id="fe8d4-164">32</span><span class="sxs-lookup"><span data-stu-id="fe8d4-164">32</span></span> |
| [<span data-ttu-id="fe8d4-165">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="fe8d4-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="fe8d4-166">F-serie</span><span class="sxs-lookup"><span data-stu-id="fe8d4-166">F series</span></span> | <span data-ttu-id="fe8d4-167">32</span><span class="sxs-lookup"><span data-stu-id="fe8d4-167">32</span></span> |
| [<span data-ttu-id="fe8d4-168">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="fe8d4-169">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="fe8d4-169">D and G series</span></span> | <span data-ttu-id="fe8d4-170">64</span><span class="sxs-lookup"><span data-stu-id="fe8d4-170">64</span></span> |
| [<span data-ttu-id="fe8d4-171">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="fe8d4-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="fe8d4-172">L-reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-172">L series</span></span> | <span data-ttu-id="fe8d4-173">64</span><span class="sxs-lookup"><span data-stu-id="fe8d4-173">64</span></span> |
| [<span data-ttu-id="fe8d4-174">GPU</span><span class="sxs-lookup"><span data-stu-id="fe8d4-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="fe8d4-175">N reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-175">N series</span></span> | <span data-ttu-id="fe8d4-176">48</span><span class="sxs-lookup"><span data-stu-id="fe8d4-176">48</span></span> |
| [<span data-ttu-id="fe8d4-177">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="fe8d4-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="fe8d4-178">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="fe8d4-178">A and H series</span></span> | <span data-ttu-id="fe8d4-179">32</span><span class="sxs-lookup"><span data-stu-id="fe8d4-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="fe8d4-180">VM-schijftypen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-180">VM disk types</span></span>

<span data-ttu-id="fe8d4-181">Azure biedt twee typen van de schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="fe8d4-182">Standard-schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-182">Standard disk</span></span>

<span data-ttu-id="fe8d4-183">Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="fe8d4-184">Standaardschijven zijn ideaal voor een voordelige ontwikkelen en testen werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="fe8d4-185">Premium-schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-185">Premium disk</span></span>

<span data-ttu-id="fe8d4-186">Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="fe8d4-187">Ideaal voor virtuele machines met productie werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="fe8d4-188">Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="fe8d4-189">Premium-schijven zijn drie typen (P10, P20, P30), Hallo grootte van Hallo schijf Hallo schijftype bepaalt.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="fe8d4-190">Wanneer u selecteert, wordt de waarde van een schijf grootte Hallo toohello volgende type afgerond.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="fe8d4-191">Als de schijfgrootte Hallo minder dan 128 GB is, is het schijftype Hallo P10.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="fe8d4-192">Als de schijfgrootte Hallo tussen 129 en 512 GB, is Hallo grootte een P20.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="fe8d4-193">Meer dan 512 GB Hallo grootte is een P30.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="fe8d4-194">Premium-schijfprestaties</span><span class="sxs-lookup"><span data-stu-id="fe8d4-194">Premium disk performance</span></span>

|<span data-ttu-id="fe8d4-195">Premium-opslag schijftype</span><span class="sxs-lookup"><span data-stu-id="fe8d4-195">Premium storage disk type</span></span> | <span data-ttu-id="fe8d4-196">P10</span><span class="sxs-lookup"><span data-stu-id="fe8d4-196">P10</span></span> | <span data-ttu-id="fe8d4-197">P20</span><span class="sxs-lookup"><span data-stu-id="fe8d4-197">P20</span></span> | <span data-ttu-id="fe8d4-198">P30</span><span class="sxs-lookup"><span data-stu-id="fe8d4-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fe8d4-199">Grootte van de schijf (afronden)</span><span class="sxs-lookup"><span data-stu-id="fe8d4-199">Disk size (round up)</span></span> | <span data-ttu-id="fe8d4-200">128 GB</span><span class="sxs-lookup"><span data-stu-id="fe8d4-200">128 GB</span></span> | <span data-ttu-id="fe8d4-201">512 GB</span><span class="sxs-lookup"><span data-stu-id="fe8d4-201">512 GB</span></span> | <span data-ttu-id="fe8d4-202">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="fe8d4-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="fe8d4-203">Max. aantal IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-203">Max IOPS per disk</span></span> | <span data-ttu-id="fe8d4-204">500</span><span class="sxs-lookup"><span data-stu-id="fe8d4-204">500</span></span> | <span data-ttu-id="fe8d4-205">2,300</span><span class="sxs-lookup"><span data-stu-id="fe8d4-205">2,300</span></span> | <span data-ttu-id="fe8d4-206">5,000</span><span class="sxs-lookup"><span data-stu-id="fe8d4-206">5,000</span></span> |
<span data-ttu-id="fe8d4-207">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-207">Throughput per disk</span></span> | <span data-ttu-id="fe8d4-208">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="fe8d4-208">100 MB/s</span></span> | <span data-ttu-id="fe8d4-209">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="fe8d4-209">150 MB/s</span></span> | <span data-ttu-id="fe8d4-210">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="fe8d4-210">200 MB/s</span></span> |

<span data-ttu-id="fe8d4-211">Tijdens het Hallo boven tabel identificeert max. IOP's per schijf, kan een hoger niveau van de prestaties van worden bereikt door meerdere gegevensschijven te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="fe8d4-212">Een VM Standard_GS5 kunt bijvoorbeeld een maximumaantal IOPS 80.000 bereiken.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="fe8d4-213">Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fe8d4-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="fe8d4-214">Maken en koppelen van schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-214">Create and attach disks</span></span>

<span data-ttu-id="fe8d4-215">Gegevensschijven worden gemaakt en gekoppeld op tijd voor het maken van VM of tooan bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="fe8d4-216">Schijf bij het maken van de virtuele machine koppelen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-216">Attach disk at VM creation</span></span>

<span data-ttu-id="fe8d4-217">Een resourcegroep maken met de Hallo [az groep maken](https://docs.microsoft.com/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="fe8d4-218">Een virtuele machine maken met Hallo [az vm maken]( /cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="fe8d4-219">Hallo `--datadisk-sizes-gb` argument gebruikte toospecify dat een extra schijf moet worden gemaakt en gekoppeld toohello virtuele machine is.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="fe8d4-220">toocreate en meer dan één schijf koppelen, voert u een door spaties gescheiden lijst met grootten van de schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="fe8d4-221">In Hallo voorbeeld te volgen, wordt een virtuele machine gemaakt met twee gegevensschijven, beide 128 GB.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="fe8d4-222">Omdat de schijfgrootten Hallo 128 GB, zijn deze schijven geconfigureerd als P10s waarmee maximaal 500 IOP's per schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="fe8d4-223">Schijf tooexisting VM koppelen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="fe8d4-224">toocreate en koppelen van een nieuwe schijf tooan bestaande virtuele machine, gebruikt u Hallo [az vm schijf koppelen](/cli/azure/vm/disk#attach) opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="fe8d4-225">Hallo volgende voorbeeld wordt een premium-schijf 128 GB in grootte, en wordt deze toohello die VM in de laatste stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="fe8d4-226">Gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fe8d4-226">Prepare data disks</span></span>

<span data-ttu-id="fe8d4-227">Als een schijf is aangesloten toohello virtuele machine, moet Hallo besturingssysteem geconfigureerd toobe toouse Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="fe8d4-228">Hallo volgende voorbeeld ziet u hoe toomanually configureren voor een schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="fe8d4-229">Dit proces kan ook worden geautomatiseerd met behulp van cloud-init, die wordt beschreven in een [hoger zelfstudie](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fe8d4-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="fe8d4-230">Handmatige configuratie</span><span class="sxs-lookup"><span data-stu-id="fe8d4-230">Manual configuration</span></span>

<span data-ttu-id="fe8d4-231">Een SSH-verbinding maken met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="fe8d4-232">Hallo voorbeeld IP-adres vervangen door Hallo openbare IP-adres van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="fe8d4-233">Hallo schijf partitioneren met `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="fe8d4-234">Een partitie bestandssysteem toohello schrijven met behulp van Hallo `mkfs` opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="fe8d4-235">Hallo nieuwe schijf koppelen zodat deze toegankelijk is in Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="fe8d4-236">Hallo schijf kan nu worden geopend via Hallo *datadrive* koppelpunt die kan worden gecontroleerd door het uitvoeren van Hallo `df -h` opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="fe8d4-237">Hallo uitvoer toont Hallo nieuw station gekoppeld aan */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="fe8d4-238">tooensure dat station Hallo opnieuw na opnieuw opstarten is gekoppeld, moet deze worden toegevoegd toohello */etc/fstab* bestand.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="fe8d4-239">toodo ophalen dus Hallo UUID van de schijf Hallo Hello `blkid` hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="fe8d4-240">Hallo-uitvoer geeft Hallo UUID van Hallo-station `/dev/sdc1` in dit geval.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="fe8d4-241">Toevoegen van een regel vergelijkbaar toohello na toohello */etc/fstab* bestand.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="fe8d4-242">Ook dat barrières schrijven kan worden uitgeschakeld met *blokkade = 0*, deze configuratie kan de schijf worden verbeterd.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="fe8d4-243">Nu dat hello schijf is geconfigureerd, sluit u Hallo SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="fe8d4-244">Formaat van VM-schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-244">Resize VM disk</span></span>

<span data-ttu-id="fe8d4-245">Wanneer een virtuele machine is geïmplementeerd, kunnen Hallo besturingssysteemschijf of schijven bijgesloten gegevens worden vergroot.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="fe8d4-246">Hallo vergroten met een schijf is handig wanneer hoeven meer opslagruimte of een hoger niveau van de prestaties (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="fe8d4-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="fe8d4-247">Houd er rekening mee schijven in grootte kunnen niet worden verhoogd.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="fe8d4-248">Voordat u voor de grootte van de schijf, Hallo Id of naam van Hallo schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="fe8d4-249">Gebruik Hallo [az Schijflijst](/cli/azure/vm/disk#list) opdracht tooreturn alle schijven in een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="fe8d4-250">Noteer de naam van de schijf Hallo dat u tooresize wilt.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="fe8d4-251">Er moet ook Hallo VM toewijzing ongedaan is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="fe8d4-252">Gebruik Hallo [az vm ongedaan]( /cli/azure/vm#deallocate) opdracht toostop en Hallo VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fe8d4-253">Gebruik Hallo [az schijf update](/cli/azure/vm/disk#update) opdracht tooresize Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="fe8d4-254">In dit voorbeeld wordt een schijf met de naam het formaat *myDataDisk* too1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="fe8d4-255">Nadat de bewerking formaat Hallo is voltooid, start u Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fe8d4-256">Als u het formaat Hallo systeemschijf besturingssysteem hebt gewijzigd, wordt automatisch Hallo partitie worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="fe8d4-257">Als u het formaat van een gegevensschijf hebt gewijzigd, moeten alle huidige partities toobe uitgevouwen in Hallo VMs-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="fe8d4-258">Momentopname maken van Azure-schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-258">Snapshot Azure disks</span></span>

<span data-ttu-id="fe8d4-259">Maken van een momentopname van de schijf, maakt een lezen alleen, punt in tijd kopie van Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="fe8d4-260">Azure VM-momentopnamen zijn handig voor het snel Hallo status van een virtuele machine opslaan voordat u configuratiewijzigingen in.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="fe8d4-261">In Hallo gebeurtenis hello configuratiewijzigingen bewijzen toobe ongewenste, status virtuele machine kan worden hersteld met een Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="fe8d4-262">Wanneer een virtuele machine meer dan één schijf heeft, een momentopname wordt gemaakt van elke schijf onafhankelijk van Hallo anderen.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="fe8d4-263">Overweeg Hallo VM stoppen voordat het maken van momentopnamen van de schijf voor het maken van de toepassing consistente back-ups.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="fe8d4-264">Ook gebruiken Hallo [Azure Backup-service](/azure/backup/), zodat u tooperform automatische back-ups tijdens het Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="fe8d4-265">Momentopname maken</span><span class="sxs-lookup"><span data-stu-id="fe8d4-265">Create snapshot</span></span>

<span data-ttu-id="fe8d4-266">Voordat u een momentopname van de virtuele machine schijf maakt, Hallo-Id of naam van de schijf Hallo is vereist.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="fe8d4-267">Gebruik Hallo [az vm weergeven](https://docs.microsoft.com/en-us/cli/azure/vm#show) opdracht tooreturn Hallo schijf-id. In dit voorbeeld Hallo schijf-id in een variabele opgeslagen, zodat deze kan worden gebruikt in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="fe8d4-268">Nu dat u Hallo-id van de schijf van de virtuele machine hello hebt, hello volgende opdracht maakt een momentopname van Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="fe8d4-269">Schijf maken vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-269">Create disk from snapshot</span></span>

<span data-ttu-id="fe8d4-270">Deze momentopname kan vervolgens worden geconverteerd naar een schijf, wat kan gebruikte toorecreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="fe8d4-271">Virtuele machine herstellen vanuit een momentopname.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="fe8d4-272">toodemonstrate virtuele machine is hersteld, delete Hallo bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fe8d4-273">Maak een nieuwe virtuele machine van Hallo momentopname schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="fe8d4-274">Gegevensschijf opnieuw koppelen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-274">Reattach data disk</span></span>

<span data-ttu-id="fe8d4-275">Alle gegevensschijven moeten toobe opnieuw gekoppeld toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="fe8d4-276">Zoek eerst Hallo schijfnaam voor gegevens met behulp van Hallo [az Schijflijst](https://docs.microsoft.com/cli/azure/disk#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="fe8d4-277">In dit voorbeeld plaatsen Hallo naam van de schijf Hallo in een variabele met de naam *datadisk*, die wordt gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="fe8d4-278">Gebruik Hallo [az vm schijf koppelen](https://docs.microsoft.com/cli/azure/vm/disk#attach) opdracht tooattach Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="fe8d4-279">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-279">Next steps</span></span>

<span data-ttu-id="fe8d4-280">In deze zelfstudie hebt u geleerd over VM schijven onderwerpen, zoals:</span><span class="sxs-lookup"><span data-stu-id="fe8d4-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe8d4-281">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="fe8d4-282">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-282">Data disks</span></span>
> * <span data-ttu-id="fe8d4-283">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="fe8d4-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="fe8d4-284">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="fe8d4-284">Disk performance</span></span>
> * <span data-ttu-id="fe8d4-285">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fe8d4-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="fe8d4-286">De schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="fe8d4-286">Resizing disks</span></span>
> * <span data-ttu-id="fe8d4-287">Schijf momentopnamen</span><span class="sxs-lookup"><span data-stu-id="fe8d4-287">Disk snapshots</span></span>

<span data-ttu-id="fe8d4-288">Ga toohello volgende zelfstudie toolearn over het automatiseren van VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="fe8d4-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe8d4-289">VM-configuratie automatiseren</span><span class="sxs-lookup"><span data-stu-id="fe8d4-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
