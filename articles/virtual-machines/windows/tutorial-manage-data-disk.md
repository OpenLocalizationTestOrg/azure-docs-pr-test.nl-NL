---
title: Azure-schijven met de Azure PowerShell beheren | Microsoft Docs
description: Zelfstudie - schijven van Azure met Azure PowerShell beheren
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
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="1037c-103">Azure-schijven met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="1037c-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="1037c-104">Virtuele machines in Azure schijven gebruiken voor het opslaan van het besturingssysteem, toepassingen en gegevens van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1037c-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="1037c-105">Bij het maken van een virtuele machine is het van belang dat u kiest een grootte van de schijf en de configuratie geschikt is voor de verwachte werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="1037c-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="1037c-106">Deze zelfstudie bevat informatie over het implementeren en beheren van VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="1037c-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="1037c-107">U meer informatie over:</span><span class="sxs-lookup"><span data-stu-id="1037c-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1037c-108">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="1037c-109">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="1037c-109">Data disks</span></span>
> * <span data-ttu-id="1037c-110">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="1037c-111">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="1037c-111">Disk performance</span></span>
> * <span data-ttu-id="1037c-112">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="1037c-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="1037c-113">Voor deze zelfstudie is moduleversie 3,6 of hoger van Azure PowerShell vereist.</span><span class="sxs-lookup"><span data-stu-id="1037c-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1037c-114">Voer ` Get-Module -ListAvailable AzureRM` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="1037c-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="1037c-115">Als u upgraden wilt, Zie [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1037c-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="1037c-116">Standaard Azure-schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-116">Default Azure disks</span></span>

<span data-ttu-id="1037c-117">Wanneer een virtuele machine van Azure is gemaakt, worden twee schijven automatisch gekoppeld aan de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1037c-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="1037c-118">**Besturingssysteemschijf** -systeemschijven kan worden verkleind tot 1 terabyte is, en fungeert als host voor het besturingssysteem van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1037c-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="1037c-119">De besturingssysteemschijf is toegewezen stationsletter van *c:* standaard.</span><span class="sxs-lookup"><span data-stu-id="1037c-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="1037c-120">De configuratie van de besturingssysteemschijf van de schijfcache is geoptimaliseerd voor OS-prestaties.</span><span class="sxs-lookup"><span data-stu-id="1037c-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="1037c-121">De besturingssysteemschijf **beter niet** toepassingen of gegevens hosten.</span><span class="sxs-lookup"><span data-stu-id="1037c-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="1037c-122">Gebruik een gegevensschijf, die verderop in dit artikel wordt beschreven voor toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="1037c-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="1037c-123">**Tijdelijke schijf** -tijdelijke schijven gebruiken een SSD-schijf die zich op dezelfde Azure host als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1037c-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="1037c-124">Tijdelijke schijven zijn maximaal zodat en kunnen worden gebruikt voor bewerkingen, zoals tijdelijke gegevensverwerking.</span><span class="sxs-lookup"><span data-stu-id="1037c-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="1037c-125">Als de virtuele machine wordt verplaatst naar een nieuwe host, wordt echter gegevens die zijn opgeslagen op een tijdelijke schijf verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1037c-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="1037c-126">De grootte van de tijdelijke schijf wordt bepaald door de VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="1037c-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="1037c-127">Tijdelijke schijven zijn toegewezen stationsletter van *d:* standaard.</span><span class="sxs-lookup"><span data-stu-id="1037c-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="1037c-128">Tijdelijke schijfgrootten</span><span class="sxs-lookup"><span data-stu-id="1037c-128">Temporary disk sizes</span></span>

| <span data-ttu-id="1037c-129">Type</span><span class="sxs-lookup"><span data-stu-id="1037c-129">Type</span></span> | <span data-ttu-id="1037c-130">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="1037c-130">VM Size</span></span> | <span data-ttu-id="1037c-131">Maximumgrootte van tijdelijke schijf (GB)</span><span class="sxs-lookup"><span data-stu-id="1037c-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="1037c-132">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="1037c-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="1037c-133">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-133">A and D series</span></span> | <span data-ttu-id="1037c-134">800</span><span class="sxs-lookup"><span data-stu-id="1037c-134">800</span></span> |
| [<span data-ttu-id="1037c-135">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="1037c-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="1037c-136">F-serie</span><span class="sxs-lookup"><span data-stu-id="1037c-136">F series</span></span> | <span data-ttu-id="1037c-137">800</span><span class="sxs-lookup"><span data-stu-id="1037c-137">800</span></span> |
| [<span data-ttu-id="1037c-138">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="1037c-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="1037c-139">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="1037c-139">D and G series</span></span> | <span data-ttu-id="1037c-140">6144</span><span class="sxs-lookup"><span data-stu-id="1037c-140">6144</span></span> |
| [<span data-ttu-id="1037c-141">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="1037c-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="1037c-142">L-reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-142">L series</span></span> | <span data-ttu-id="1037c-143">5630</span><span class="sxs-lookup"><span data-stu-id="1037c-143">5630</span></span> |
| [<span data-ttu-id="1037c-144">GPU</span><span class="sxs-lookup"><span data-stu-id="1037c-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="1037c-145">N reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-145">N series</span></span> | <span data-ttu-id="1037c-146">1440</span><span class="sxs-lookup"><span data-stu-id="1037c-146">1440</span></span> |
| [<span data-ttu-id="1037c-147">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="1037c-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="1037c-148">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-148">A and H series</span></span> | <span data-ttu-id="1037c-149">2000</span><span class="sxs-lookup"><span data-stu-id="1037c-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="1037c-150">Azure gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="1037c-150">Azure data disks</span></span>

<span data-ttu-id="1037c-151">Extra gegevensschijven kunnen worden toegevoegd voor het installeren van toepassingen en gegevens op te slaan.</span><span class="sxs-lookup"><span data-stu-id="1037c-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="1037c-152">Gegevensschijven moeten worden gebruikt in een situatie waarin de opslag van gegevens duurzaam en responsief gewenst is.</span><span class="sxs-lookup"><span data-stu-id="1037c-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="1037c-153">Elke gegevensschijf heeft een maximale capaciteit van 1 terabyte.</span><span class="sxs-lookup"><span data-stu-id="1037c-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="1037c-154">De grootte van de virtuele machine bepaalt hoeveel gegevensschijven kunnen worden gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1037c-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="1037c-155">Voor elke VM-core, kunnen twee schijven worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1037c-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="1037c-156">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="1037c-156">Max data disks per VM</span></span>

| <span data-ttu-id="1037c-157">Type</span><span class="sxs-lookup"><span data-stu-id="1037c-157">Type</span></span> | <span data-ttu-id="1037c-158">VM-grootte</span><span class="sxs-lookup"><span data-stu-id="1037c-158">VM Size</span></span> | <span data-ttu-id="1037c-159">Maximum aantal gegevensschijven per VM</span><span class="sxs-lookup"><span data-stu-id="1037c-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="1037c-160">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="1037c-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="1037c-161">A en D-reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-161">A and D series</span></span> | <span data-ttu-id="1037c-162">32</span><span class="sxs-lookup"><span data-stu-id="1037c-162">32</span></span> |
| [<span data-ttu-id="1037c-163">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="1037c-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="1037c-164">F-serie</span><span class="sxs-lookup"><span data-stu-id="1037c-164">F series</span></span> | <span data-ttu-id="1037c-165">32</span><span class="sxs-lookup"><span data-stu-id="1037c-165">32</span></span> |
| [<span data-ttu-id="1037c-166">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="1037c-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="1037c-167">D en G-serie</span><span class="sxs-lookup"><span data-stu-id="1037c-167">D and G series</span></span> | <span data-ttu-id="1037c-168">64</span><span class="sxs-lookup"><span data-stu-id="1037c-168">64</span></span> |
| [<span data-ttu-id="1037c-169">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="1037c-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="1037c-170">L-reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-170">L series</span></span> | <span data-ttu-id="1037c-171">64</span><span class="sxs-lookup"><span data-stu-id="1037c-171">64</span></span> |
| [<span data-ttu-id="1037c-172">GPU</span><span class="sxs-lookup"><span data-stu-id="1037c-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="1037c-173">N reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-173">N series</span></span> | <span data-ttu-id="1037c-174">48</span><span class="sxs-lookup"><span data-stu-id="1037c-174">48</span></span> |
| [<span data-ttu-id="1037c-175">Hoge prestaties</span><span class="sxs-lookup"><span data-stu-id="1037c-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="1037c-176">A en H reeks</span><span class="sxs-lookup"><span data-stu-id="1037c-176">A and H series</span></span> | <span data-ttu-id="1037c-177">32</span><span class="sxs-lookup"><span data-stu-id="1037c-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="1037c-178">VM-schijftypen</span><span class="sxs-lookup"><span data-stu-id="1037c-178">VM disk types</span></span>

<span data-ttu-id="1037c-179">Azure biedt twee typen van de schijf.</span><span class="sxs-lookup"><span data-stu-id="1037c-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="1037c-180">Standard-schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-180">Standard disk</span></span>

<span data-ttu-id="1037c-181">Standard Storage wordt ondersteund door HDD's en biedt voordelige en hoogwaardige opslag.</span><span class="sxs-lookup"><span data-stu-id="1037c-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="1037c-182">Standaardschijven zijn ideaal voor een voordelige ontwikkelen en testen werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="1037c-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="1037c-183">Premium-schijf</span><span class="sxs-lookup"><span data-stu-id="1037c-183">Premium disk</span></span>

<span data-ttu-id="1037c-184">Premium-schijven worden ondersteund door de hoge prestaties, lage latentie SSD-schijf.</span><span class="sxs-lookup"><span data-stu-id="1037c-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="1037c-185">Ideaal voor virtuele machines met productie werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="1037c-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="1037c-186">Premium-opslag ondersteunt DS-serie, DSv2-serie GS-serie en virtuele machines FS-serie.</span><span class="sxs-lookup"><span data-stu-id="1037c-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="1037c-187">Premium-schijven zijn drie typen (P10, P20, P30), de grootte van de schijf bepaalt het schijftype.</span><span class="sxs-lookup"><span data-stu-id="1037c-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="1037c-188">Wanneer u selecteert, wordt de een de waarde van de schijfgrootte afgerond naar het volgende type.</span><span class="sxs-lookup"><span data-stu-id="1037c-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="1037c-189">Bijvoorbeeld, als de grootte lager dan 128 GB is wordt het schijftype P10, worden tussen 129 512 P20 en meer dan 512 P30.</span><span class="sxs-lookup"><span data-stu-id="1037c-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="1037c-190">Premium-schijfprestaties</span><span class="sxs-lookup"><span data-stu-id="1037c-190">Premium disk performance</span></span>

|<span data-ttu-id="1037c-191">Premium-opslag schijftype</span><span class="sxs-lookup"><span data-stu-id="1037c-191">Premium storage disk type</span></span> | <span data-ttu-id="1037c-192">P10</span><span class="sxs-lookup"><span data-stu-id="1037c-192">P10</span></span> | <span data-ttu-id="1037c-193">P20</span><span class="sxs-lookup"><span data-stu-id="1037c-193">P20</span></span> | <span data-ttu-id="1037c-194">P30</span><span class="sxs-lookup"><span data-stu-id="1037c-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1037c-195">Grootte van de schijf (afronden)</span><span class="sxs-lookup"><span data-stu-id="1037c-195">Disk size (round up)</span></span> | <span data-ttu-id="1037c-196">128 GB</span><span class="sxs-lookup"><span data-stu-id="1037c-196">128 GB</span></span> | <span data-ttu-id="1037c-197">512 GB</span><span class="sxs-lookup"><span data-stu-id="1037c-197">512 GB</span></span> | <span data-ttu-id="1037c-198">1.024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="1037c-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="1037c-199">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="1037c-199">IOPS per disk</span></span> | <span data-ttu-id="1037c-200">500</span><span class="sxs-lookup"><span data-stu-id="1037c-200">500</span></span> | <span data-ttu-id="1037c-201">2,300</span><span class="sxs-lookup"><span data-stu-id="1037c-201">2,300</span></span> | <span data-ttu-id="1037c-202">5,000</span><span class="sxs-lookup"><span data-stu-id="1037c-202">5,000</span></span> |
<span data-ttu-id="1037c-203">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="1037c-203">Throughput per disk</span></span> | <span data-ttu-id="1037c-204">100 MB/s</span><span class="sxs-lookup"><span data-stu-id="1037c-204">100 MB/s</span></span> | <span data-ttu-id="1037c-205">150 MB/s</span><span class="sxs-lookup"><span data-stu-id="1037c-205">150 MB/s</span></span> | <span data-ttu-id="1037c-206">200 MB/s</span><span class="sxs-lookup"><span data-stu-id="1037c-206">200 MB/s</span></span> |

<span data-ttu-id="1037c-207">Terwijl de bovenstaande tabel max. IOP's per schijf identificeert, kan een hoger niveau van de prestaties worden bereikt door meerdere gegevensschijven te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1037c-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="1037c-208">64 gegevensschijven kunnen bijvoorbeeld worden gekoppeld aan Standard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="1037c-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="1037c-209">Als u elk van deze schijven worden aangepast als een P30, kan een maximum van 80.000 IOP's kan worden bereikt.</span><span class="sxs-lookup"><span data-stu-id="1037c-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="1037c-210">Zie voor gedetailleerde informatie over max. IOP's per VM [Linux VM-grootten](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1037c-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="1037c-211">Maken en koppelen van schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-211">Create and attach disks</span></span>

<span data-ttu-id="1037c-212">Als u het voorbeeld in deze zelfstudie, moet u een bestaande virtuele machine hebben.</span><span class="sxs-lookup"><span data-stu-id="1037c-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="1037c-213">Indien nodig, dit [voorbeeldscript](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) kunt maken voor u.</span><span class="sxs-lookup"><span data-stu-id="1037c-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="1037c-214">Wanneer het uitvoeren van de zelfstudie vervangt benoemt de resourcegroep en de virtuele machine waar nodig.</span><span class="sxs-lookup"><span data-stu-id="1037c-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="1037c-215">Maken van de eerste configuratie met [nieuw AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="1037c-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="1037c-216">Het volgende voorbeeld wordt een schijf die 128 GB groot is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1037c-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="1037c-217">Maken van de gegevensschijf met de [nieuw AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1037c-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="1037c-218">Ophalen van de virtuele machine die u wilt toevoegen de gegevensschijf aan met de [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1037c-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="1037c-219">De gegevensschijf toevoegen aan de virtuele-machineconfiguratie met de [toevoegen AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1037c-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="1037c-220">Werk de virtuele machine met de [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) opdracht.</span><span class="sxs-lookup"><span data-stu-id="1037c-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="1037c-221">Gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="1037c-221">Prepare data disks</span></span>

<span data-ttu-id="1037c-222">Zodra een schijf is gekoppeld aan de virtuele machine, moet het besturingssysteem worden geconfigureerd voor gebruik van de schijf.</span><span class="sxs-lookup"><span data-stu-id="1037c-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="1037c-223">Het volgende voorbeeld laat zien hoe de eerste schijf die is toegevoegd aan de virtuele machine handmatig configureren.</span><span class="sxs-lookup"><span data-stu-id="1037c-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="1037c-224">Dit proces kan ook worden geautomatiseerd met behulp van de [extensie voor aangepaste scripts](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1037c-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="1037c-225">Handmatige configuratie</span><span class="sxs-lookup"><span data-stu-id="1037c-225">Manual configuration</span></span>

<span data-ttu-id="1037c-226">Een RDP-verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1037c-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="1037c-227">Opent u PowerShell en voer dit script.</span><span class="sxs-lookup"><span data-stu-id="1037c-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="1037c-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1037c-228">Next steps</span></span>

<span data-ttu-id="1037c-229">In deze zelfstudie hebt u geleerd over VM schijven onderwerpen, zoals:</span><span class="sxs-lookup"><span data-stu-id="1037c-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1037c-230">OS-schijven en tijdelijke schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="1037c-231">Gegevensschijven</span><span class="sxs-lookup"><span data-stu-id="1037c-231">Data disks</span></span>
> * <span data-ttu-id="1037c-232">Standard en Premium-schijven</span><span class="sxs-lookup"><span data-stu-id="1037c-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="1037c-233">Prestaties van de schijf</span><span class="sxs-lookup"><span data-stu-id="1037c-233">Disk performance</span></span>
> * <span data-ttu-id="1037c-234">Koppelen en gegevensschijven voorbereiden</span><span class="sxs-lookup"><span data-stu-id="1037c-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="1037c-235">Ga naar de volgende zelfstudie voor meer informatie over het automatiseren van VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="1037c-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1037c-236">VM-configuratie automatiseren</span><span class="sxs-lookup"><span data-stu-id="1037c-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
