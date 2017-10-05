---
title: Grootten van virtuele Windows-machine in Azure | Microsoft Docs
description: Hier worden de verschillende grootten beschikbaar voor Windows virtuele machines in Azure.
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
ms.openlocfilehash: b3a674137ed3dd47188d4af0bc845104eabc885e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="29956-103">Grootten voor Windows virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="29956-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="29956-104">In dit artikel beschrijft de beschikbare grootten en opties voor de virtuele machines van Azure die kunt u uw Windows-apps en werkbelastingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="29956-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="29956-105">Het biedt tevens overwegingen voor de implementatie moet letten wanneer u van plan bent om deze bronnen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29956-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="29956-106">In dit artikel is ook beschikbaar voor [virtuele Linux-machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29956-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="29956-107">Type</span><span class="sxs-lookup"><span data-stu-id="29956-107">Type</span></span>                     | <span data-ttu-id="29956-108">Grootten</span><span class="sxs-lookup"><span data-stu-id="29956-108">Sizes</span></span>           |    <span data-ttu-id="29956-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="29956-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="29956-110">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="29956-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="29956-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0 7</span><span class="sxs-lookup"><span data-stu-id="29956-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="29956-112">Evenwichtige CPU-geheugenverhouding.</span><span class="sxs-lookup"><span data-stu-id="29956-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="29956-113">Ideaal voor testen en ontwikkelen, kleine tot middelgrote databases en webservers met weinig of gemiddeld verkeer.</span><span class="sxs-lookup"><span data-stu-id="29956-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="29956-114">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="29956-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="29956-115">FS, F</span><span class="sxs-lookup"><span data-stu-id="29956-115">Fs, F</span></span>             | <span data-ttu-id="29956-116">Hoge CPU-geheugenverhouding.</span><span class="sxs-lookup"><span data-stu-id="29956-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="29956-117">Goed voor webservers met gemiddeld verkeer, netwerkapparatuur, batchprocessen en toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="29956-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="29956-118">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="29956-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="29956-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="29956-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="29956-120">Verhouding tussen het hoge geheugen aan CPU.</span><span class="sxs-lookup"><span data-stu-id="29956-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="29956-121">Uiterst geschikt voor relationele-databaseservers, middelgrote tot grote caches en analysefuncties in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="29956-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="29956-122">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="29956-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="29956-123">Ls</span><span class="sxs-lookup"><span data-stu-id="29956-123">Ls</span></span>                | <span data-ttu-id="29956-124">Snelle doorvoer van schijfgegevens en IO.</span><span class="sxs-lookup"><span data-stu-id="29956-124">High disk throughput and IO.</span></span> <span data-ttu-id="29956-125">Ideaal voor big data-, SQL- en NoSQL-databases.</span><span class="sxs-lookup"><span data-stu-id="29956-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="29956-126">GPU</span><span class="sxs-lookup"><span data-stu-id="29956-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="29956-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="29956-127">NV, NC</span></span>            | <span data-ttu-id="29956-128">Gespecialiseerde virtuele machines gericht voor zware grafische weergave en het bewerken van video's.</span><span class="sxs-lookup"><span data-stu-id="29956-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="29956-129">Beschikbaar met één of meerdere GPU's.</span><span class="sxs-lookup"><span data-stu-id="29956-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="29956-130">Krachtig rekenvermogen</span><span class="sxs-lookup"><span data-stu-id="29956-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="29956-131">H, A8 11</span><span class="sxs-lookup"><span data-stu-id="29956-131">H, A8-11</span></span>          | <span data-ttu-id="29956-132">Onze snelste en krachtigste CPU-virtuele machines met optionele netwerkinterfaces (RDMA) voor hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="29956-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="29956-133">Zie voor meer informatie over prijzen van de verschillende grootten [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="29956-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="29956-134">Zie voor algemene limieten op Azure Virtual machines [Azure-abonnement en Servicelimieten, quota's en beperkingen](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="29956-134">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="29956-135">Opslagkosten worden afzonderlijk berekend op basis van het aantal pagina's dat in het opslagaccount is gebruikt.</span><span class="sxs-lookup"><span data-stu-id="29956-135">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="29956-136">Voor meer informatie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="29956-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="29956-137">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="29956-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="29956-138">Rest-API</span><span class="sxs-lookup"><span data-stu-id="29956-138">Rest API</span></span>

<span data-ttu-id="29956-139">Zie de volgende onderwerpen voor informatie over het gebruik van de REST-API aan query voor VM-grootten:</span><span class="sxs-lookup"><span data-stu-id="29956-139">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="29956-140">Lijst met beschikbare virtuele machine grootten voor het vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="29956-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="29956-141">Lijst met beschikbare virtuele machine grootten voor een abonnement</span><span class="sxs-lookup"><span data-stu-id="29956-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="29956-142">Grootte van de lijst met beschikbare virtuele machines in een beschikbaarheidsset</span><span class="sxs-lookup"><span data-stu-id="29956-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="29956-143">ACU</span><span class="sxs-lookup"><span data-stu-id="29956-143">ACU</span></span>

<span data-ttu-id="29956-144">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="29956-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29956-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29956-145">Next steps</span></span>

<span data-ttu-id="29956-146">Meer informatie over de verschillende grootten voor virtuele machine die beschikbaar zijn:</span><span class="sxs-lookup"><span data-stu-id="29956-146">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="29956-147">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="29956-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="29956-148">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="29956-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="29956-149">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="29956-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="29956-150">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="29956-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="29956-151">Geoptimaliseerde GPU</span><span class="sxs-lookup"><span data-stu-id="29956-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="29956-152">Krachtig rekenvermogen</span><span class="sxs-lookup"><span data-stu-id="29956-152">High performance compute</span></span>](sizes-hpc.md)



