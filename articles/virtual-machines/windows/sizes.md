---
title: aaaWindows VM-groottes in Azure | Microsoft Docs
description: Geeft een lijst Hallo verschillende grootten beschikbaar voor Windows virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="f04d3-103">Grootten voor Windows virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="f04d3-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="f04d3-104">Dit artikel beschrijft de beschikbare grootten Hallo en opties voor hello Azure virtuele machines kunt u toorun uw Windows-apps en werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="f04d3-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="f04d3-105">Het bevat ook toobe voor overwegingen met betrekking tot implementatie op de hoogte van wanneer u van plan bent toouse deze resources.</span><span class="sxs-lookup"><span data-stu-id="f04d3-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="f04d3-106">In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f04d3-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="f04d3-107">Type</span><span class="sxs-lookup"><span data-stu-id="f04d3-107">Type</span></span>                     | <span data-ttu-id="f04d3-108">Grootten</span><span class="sxs-lookup"><span data-stu-id="f04d3-108">Sizes</span></span>           |    <span data-ttu-id="f04d3-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f04d3-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="f04d3-110">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="f04d3-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="f04d3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="f04d3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="f04d3-112">Evenwichtige CPU-geheugenverhouding.</span><span class="sxs-lookup"><span data-stu-id="f04d3-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="f04d3-113">Ideaal voor testen en ontwikkeling, kleine toomedium databases en lage toomedium verkeer webservers.</span><span class="sxs-lookup"><span data-stu-id="f04d3-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="f04d3-114">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="f04d3-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="f04d3-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="f04d3-115">Fs, F</span></span>             | <span data-ttu-id="f04d3-116">Hoge CPU-geheugenverhouding.</span><span class="sxs-lookup"><span data-stu-id="f04d3-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="f04d3-117">Goed voor webservers met gemiddeld verkeer, netwerkapparatuur, batchprocessen en toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="f04d3-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="f04d3-118">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="f04d3-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="f04d3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="f04d3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="f04d3-120">Verhouding tussen het hoge geheugen aan CPU.</span><span class="sxs-lookup"><span data-stu-id="f04d3-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="f04d3-121">Ideaal voor relationele database-servers, gemiddeld toolarge caches en in het geheugen analytics.</span><span class="sxs-lookup"><span data-stu-id="f04d3-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="f04d3-122">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="f04d3-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="f04d3-123">Ls</span><span class="sxs-lookup"><span data-stu-id="f04d3-123">Ls</span></span>                | <span data-ttu-id="f04d3-124">Snelle doorvoer van schijfgegevens en IO.</span><span class="sxs-lookup"><span data-stu-id="f04d3-124">High disk throughput and IO.</span></span> <span data-ttu-id="f04d3-125">Ideaal voor big data-, SQL- en NoSQL-databases.</span><span class="sxs-lookup"><span data-stu-id="f04d3-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="f04d3-126">GPU</span><span class="sxs-lookup"><span data-stu-id="f04d3-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="f04d3-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="f04d3-127">NV, NC</span></span>            | <span data-ttu-id="f04d3-128">Gespecialiseerde virtuele machines gericht voor zware grafische weergave en het bewerken van video's.</span><span class="sxs-lookup"><span data-stu-id="f04d3-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="f04d3-129">Beschikbaar met één of meerdere GPU's.</span><span class="sxs-lookup"><span data-stu-id="f04d3-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="f04d3-130">Krachtig rekenvermogen</span><span class="sxs-lookup"><span data-stu-id="f04d3-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="f04d3-131">H, A8 11</span><span class="sxs-lookup"><span data-stu-id="f04d3-131">H, A8-11</span></span>          | <span data-ttu-id="f04d3-132">Onze snelste en krachtigste CPU-virtuele machines met optionele netwerkinterfaces (RDMA) voor hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="f04d3-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="f04d3-133">Zie voor meer informatie over prijzen Hallo verschillende grootten [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="f04d3-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="f04d3-134">algemene beperkingen toosee op Azure Virtual machines, Zie [Azure-abonnement en Servicelimieten, quota's en beperkingen](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f04d3-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="f04d3-135">Opslagkosten zijn berekend afzonderlijk op basis van de gebruikte pagina's in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="f04d3-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="f04d3-136">Voor meer informatie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="f04d3-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="f04d3-137">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="f04d3-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="f04d3-138">Rest-API</span><span class="sxs-lookup"><span data-stu-id="f04d3-138">Rest API</span></span>

<span data-ttu-id="f04d3-139">Zie voor informatie over het gebruik van Hallo REST-API tooquery voor VM-groottes Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f04d3-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="f04d3-140">Lijst met beschikbare virtuele machine grootten voor het vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="f04d3-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="f04d3-141">Lijst met beschikbare virtuele machine grootten voor een abonnement</span><span class="sxs-lookup"><span data-stu-id="f04d3-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="f04d3-142">Grootte van de lijst met beschikbare virtuele machines in een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="f04d3-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="f04d3-143">ACU</span><span class="sxs-lookup"><span data-stu-id="f04d3-143">ACU</span></span>

<span data-ttu-id="f04d3-144">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="f04d3-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f04d3-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f04d3-145">Next steps</span></span>

<span data-ttu-id="f04d3-146">Meer informatie over Hallo andere VM-grootten die beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="f04d3-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="f04d3-147">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="f04d3-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="f04d3-148">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="f04d3-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="f04d3-149">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="f04d3-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="f04d3-150">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="f04d3-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="f04d3-151">Geoptimaliseerde GPU</span><span class="sxs-lookup"><span data-stu-id="f04d3-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="f04d3-152">Krachtig rekenvermogen</span><span class="sxs-lookup"><span data-stu-id="f04d3-152">High performance compute</span></span>](sizes-hpc.md)



