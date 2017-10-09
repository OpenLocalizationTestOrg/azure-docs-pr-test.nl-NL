---
title: een klassieke VM tooan ARM beheerd schijf VM aaaMigrate | Microsoft Docs
description: "Migreren van één Azure VM van Hallo-classic deployment model tooManaged schijven Hallo Resource Manager-implementatiemodel."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="2f82c-103">Handmatig migreren van een klassieke VM tooa nieuwe ARM beheerd schijf VM van Hallo VHD</span><span class="sxs-lookup"><span data-stu-id="2f82c-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="2f82c-104">Deze sectie helpt u toomigrate uw bestaande Azure VM's vanuit het klassieke implementatiemodel hello te[schijven beheerd](managed-disks-overview.md) Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2f82c-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="2f82c-105">Hallo-migratie plannen tooManaged schijven</span><span class="sxs-lookup"><span data-stu-id="2f82c-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="2f82c-106">Deze sectie helpt u bij toomake Hallo beste beslissing op schijf en VM-typen.</span><span class="sxs-lookup"><span data-stu-id="2f82c-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="2f82c-107">Locatie</span><span class="sxs-lookup"><span data-stu-id="2f82c-107">Location</span></span>

<span data-ttu-id="2f82c-108">Kies een locatie waar Azure beheerd schijven beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="2f82c-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="2f82c-109">Als u tooPremium beheerd schijven migreert, zorg er ook voor Premium-opslag is beschikbaar in Hallo regio waar u van plan bent toomigrate aan.</span><span class="sxs-lookup"><span data-stu-id="2f82c-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="2f82c-110">Zie [Azure Services byRegion](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="2f82c-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="2f82c-111">Formaten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="2f82c-111">VM sizes</span></span>

<span data-ttu-id="2f82c-112">Als u tooPremium beheerd schijven migreert, hebt u tooupdate Hallo grootte van Hallo VM tooPremium kan grootte van de opslagruimte beschikbaar is in Hallo regio waar de VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="2f82c-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="2f82c-113">Bekijk Hallo VM-grootten die Premium-opslag die geschikt zijn.</span><span class="sxs-lookup"><span data-stu-id="2f82c-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="2f82c-114">Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2f82c-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="2f82c-115">Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="2f82c-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="2f82c-116">Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.</span><span class="sxs-lookup"><span data-stu-id="2f82c-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="2f82c-117">Schijfformaten</span><span class="sxs-lookup"><span data-stu-id="2f82c-117">Disk sizes</span></span>

<span data-ttu-id="2f82c-118">**Premium beheerde schijven**</span><span class="sxs-lookup"><span data-stu-id="2f82c-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="2f82c-119">Er zijn zeven typen premium-beheerde schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten.</span><span class="sxs-lookup"><span data-stu-id="2f82c-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="2f82c-120">Houd rekening met deze limieten bij het kiezen van Hallo Premium schijftype voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek worden geladen.</span><span class="sxs-lookup"><span data-stu-id="2f82c-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="2f82c-121">Premium-schijven Type</span><span class="sxs-lookup"><span data-stu-id="2f82c-121">Premium Disks Type</span></span>  | <span data-ttu-id="2f82c-122">P4</span><span class="sxs-lookup"><span data-stu-id="2f82c-122">P4</span></span>    | <span data-ttu-id="2f82c-123">P6</span><span class="sxs-lookup"><span data-stu-id="2f82c-123">P6</span></span>    | <span data-ttu-id="2f82c-124">P10</span><span class="sxs-lookup"><span data-stu-id="2f82c-124">P10</span></span>   | <span data-ttu-id="2f82c-125">P20</span><span class="sxs-lookup"><span data-stu-id="2f82c-125">P20</span></span>   | <span data-ttu-id="2f82c-126">P30</span><span class="sxs-lookup"><span data-stu-id="2f82c-126">P30</span></span>   | <span data-ttu-id="2f82c-127">P40</span><span class="sxs-lookup"><span data-stu-id="2f82c-127">P40</span></span>   | <span data-ttu-id="2f82c-128">P50</span><span class="sxs-lookup"><span data-stu-id="2f82c-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="2f82c-129">Schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="2f82c-129">Disk size</span></span>           | <span data-ttu-id="2f82c-130">128 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-130">128 GB</span></span>| <span data-ttu-id="2f82c-131">512 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-131">512 GB</span></span>| <span data-ttu-id="2f82c-132">128 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-132">128 GB</span></span>| <span data-ttu-id="2f82c-133">512 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-133">512 GB</span></span>            | <span data-ttu-id="2f82c-134">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="2f82c-135">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="2f82c-136">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="2f82c-137">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="2f82c-137">IOPS per disk</span></span>       | <span data-ttu-id="2f82c-138">120</span><span class="sxs-lookup"><span data-stu-id="2f82c-138">120</span></span>   | <span data-ttu-id="2f82c-139">240</span><span class="sxs-lookup"><span data-stu-id="2f82c-139">240</span></span>   | <span data-ttu-id="2f82c-140">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-140">500</span></span>   | <span data-ttu-id="2f82c-141">2300</span><span class="sxs-lookup"><span data-stu-id="2f82c-141">2300</span></span>              | <span data-ttu-id="2f82c-142">5000</span><span class="sxs-lookup"><span data-stu-id="2f82c-142">5000</span></span>              | <span data-ttu-id="2f82c-143">7500</span><span class="sxs-lookup"><span data-stu-id="2f82c-143">7500</span></span>              | <span data-ttu-id="2f82c-144">7500</span><span class="sxs-lookup"><span data-stu-id="2f82c-144">7500</span></span>              | 
| <span data-ttu-id="2f82c-145">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="2f82c-145">Throughput per disk</span></span> | <span data-ttu-id="2f82c-146">25 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-146">25 MB per second</span></span>  | <span data-ttu-id="2f82c-147">50 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-147">50 MB per second</span></span>  | <span data-ttu-id="2f82c-148">100 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-148">100 MB per second</span></span> | <span data-ttu-id="2f82c-149">150 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-149">150 MB per second</span></span> | <span data-ttu-id="2f82c-150">200 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-150">200 MB per second</span></span> | <span data-ttu-id="2f82c-151">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-151">250 MB per second</span></span> | <span data-ttu-id="2f82c-152">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-152">250 MB per second</span></span> | 

<span data-ttu-id="2f82c-153">**Beheerde standaardschijven**</span><span class="sxs-lookup"><span data-stu-id="2f82c-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="2f82c-154">Er zijn zeven soorten Standard-beheerde schijven die kunnen worden gebruikt met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f82c-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="2f82c-155">Elk van deze andere capaciteit hebben maar dezelfde IOPS en doorvoerlimieten hebben.</span><span class="sxs-lookup"><span data-stu-id="2f82c-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="2f82c-156">Standard-beheerde schijven op basis van de capaciteitsbehoeften Hallo van uw toepassing hello type kiezen.</span><span class="sxs-lookup"><span data-stu-id="2f82c-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="2f82c-157">Standard-schijftype</span><span class="sxs-lookup"><span data-stu-id="2f82c-157">Standard Disk Type</span></span>  | <span data-ttu-id="2f82c-158">S4</span><span class="sxs-lookup"><span data-stu-id="2f82c-158">S4</span></span>               | <span data-ttu-id="2f82c-159">S6</span><span class="sxs-lookup"><span data-stu-id="2f82c-159">S6</span></span>               | <span data-ttu-id="2f82c-160">S10</span><span class="sxs-lookup"><span data-stu-id="2f82c-160">S10</span></span>              | <span data-ttu-id="2f82c-161">S20</span><span class="sxs-lookup"><span data-stu-id="2f82c-161">S20</span></span>              | <span data-ttu-id="2f82c-162">S30</span><span class="sxs-lookup"><span data-stu-id="2f82c-162">S30</span></span>              | <span data-ttu-id="2f82c-163">S40</span><span class="sxs-lookup"><span data-stu-id="2f82c-163">S40</span></span>              | <span data-ttu-id="2f82c-164">S50</span><span class="sxs-lookup"><span data-stu-id="2f82c-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="2f82c-165">Schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="2f82c-165">Disk size</span></span>           | <span data-ttu-id="2f82c-166">30 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-166">30 GB</span></span>            | <span data-ttu-id="2f82c-167">64 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-167">64 GB</span></span>            | <span data-ttu-id="2f82c-168">128 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-168">128 GB</span></span>           | <span data-ttu-id="2f82c-169">512 GB</span><span class="sxs-lookup"><span data-stu-id="2f82c-169">512 GB</span></span>           | <span data-ttu-id="2f82c-170">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="2f82c-171">2048 GB (2TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="2f82c-172">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="2f82c-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="2f82c-173">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="2f82c-173">IOPS per disk</span></span>       | <span data-ttu-id="2f82c-174">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-174">500</span></span>              | <span data-ttu-id="2f82c-175">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-175">500</span></span>              | <span data-ttu-id="2f82c-176">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-176">500</span></span>              | <span data-ttu-id="2f82c-177">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-177">500</span></span>              | <span data-ttu-id="2f82c-178">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-178">500</span></span>              | <span data-ttu-id="2f82c-179">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-179">500</span></span>             | <span data-ttu-id="2f82c-180">500</span><span class="sxs-lookup"><span data-stu-id="2f82c-180">500</span></span>              | 
| <span data-ttu-id="2f82c-181">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="2f82c-181">Throughput per disk</span></span> | <span data-ttu-id="2f82c-182">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-182">60 MB per second</span></span> | <span data-ttu-id="2f82c-183">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-183">60 MB per second</span></span> | <span data-ttu-id="2f82c-184">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-184">60 MB per second</span></span> | <span data-ttu-id="2f82c-185">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-185">60 MB per second</span></span> | <span data-ttu-id="2f82c-186">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-186">60 MB per second</span></span> | <span data-ttu-id="2f82c-187">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-187">60 MB per second</span></span> | <span data-ttu-id="2f82c-188">60 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="2f82c-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="2f82c-189">Het beleid voor schijf</span><span class="sxs-lookup"><span data-stu-id="2f82c-189">Disk caching policy</span></span> 

<span data-ttu-id="2f82c-190">**Premium beheerde schijven**</span><span class="sxs-lookup"><span data-stu-id="2f82c-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="2f82c-191">Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2f82c-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="2f82c-192">Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs.</span><span class="sxs-lookup"><span data-stu-id="2f82c-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="2f82c-193">Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.</span><span class="sxs-lookup"><span data-stu-id="2f82c-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="2f82c-194">Prijzen</span><span class="sxs-lookup"><span data-stu-id="2f82c-194">Pricing</span></span>

<span data-ttu-id="2f82c-195">Bekijk Hallo [prijzen voor schijven beheerd](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="2f82c-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="2f82c-196">Prijzen van beheerde Premium-schijven is hetzelfde als Hallo onbeheerde Premium-schijven.</span><span class="sxs-lookup"><span data-stu-id="2f82c-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="2f82c-197">Maar prijzen voor beheerde standaardschijven is anders dan standaardschijven zonder begeleiding.</span><span class="sxs-lookup"><span data-stu-id="2f82c-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="2f82c-198">Controlelijst</span><span class="sxs-lookup"><span data-stu-id="2f82c-198">Checklist</span></span>

1.  <span data-ttu-id="2f82c-199">Als u tooPremium beheerd schijven migreert, zorg er dan voor dat deze beschikbaar is in Hallo regio die u naar migreert.</span><span class="sxs-lookup"><span data-stu-id="2f82c-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="2f82c-200">Bepaal Hallo nieuwe VM-reeks die u gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f82c-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="2f82c-201">Deze moet een Premium-opslag geschikt als u tooPremium beheerd schijven migreert.</span><span class="sxs-lookup"><span data-stu-id="2f82c-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="2f82c-202">Bepaal Hallo exacte VM-grootte u wilt gebruiken die beschikbaar zijn in Hallo regio die u migreert naar.</span><span class="sxs-lookup"><span data-stu-id="2f82c-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="2f82c-203">VM-grootte moet toobe groot genoeg toosupport Hallo aantal gegevensschijven dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="2f82c-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="2f82c-204">Als u vier gegevensschijven hebt, moet Hallo VM twee of meer kernen hebben.</span><span class="sxs-lookup"><span data-stu-id="2f82c-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="2f82c-205">Houd ook rekening met verwerkingskracht, geheugen en netwerkbandbreedte moet.</span><span class="sxs-lookup"><span data-stu-id="2f82c-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="2f82c-206">Informatie over een Hallo huidige VM handige, inclusief Hallo-lijst van schijven en de bijbehorende VHD-blobs.</span><span class="sxs-lookup"><span data-stu-id="2f82c-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="2f82c-207">Bereid uw toepassing uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="2f82c-207">Prepare your application for downtime.</span></span> <span data-ttu-id="2f82c-208">toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f82c-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="2f82c-209">Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform.</span><span class="sxs-lookup"><span data-stu-id="2f82c-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="2f82c-210">Duur van uitvaltijd is afhankelijk van Hallo hoeveelheid gegevens in Hallo schijven toomigrate.</span><span class="sxs-lookup"><span data-stu-id="2f82c-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="2f82c-211">Hallo VM migreren</span><span class="sxs-lookup"><span data-stu-id="2f82c-211">Migrate hello VM</span></span>

<span data-ttu-id="2f82c-212">Bereid uw toepassing uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="2f82c-212">Prepare your application for downtime.</span></span> <span data-ttu-id="2f82c-213">toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f82c-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="2f82c-214">Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform.</span><span class="sxs-lookup"><span data-stu-id="2f82c-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="2f82c-215">Duur van uitvaltijd is afhankelijk van de hoeveelheid gegevens in Hallo schijven toomigrate Hallo.</span><span class="sxs-lookup"><span data-stu-id="2f82c-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="2f82c-216">Stel eerst Hallo algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="2f82c-216">First, set hello common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="2f82c-217">Maak een beheerde OS-schijf met Hallo VHD van Hallo klassieke VM.</span><span class="sxs-lookup"><span data-stu-id="2f82c-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="2f82c-218">Zorg ervoor dat u hebt opgegeven Hallo URI Hallo OS VHD toohello $osVhdUri parameter voltooien.</span><span class="sxs-lookup"><span data-stu-id="2f82c-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="2f82c-219">Typ ook **- AccountType** als **PremiumLRS** of **StandardLRS** op basis van het type schijven (Premium of Standard) u migreert naar.</span><span class="sxs-lookup"><span data-stu-id="2f82c-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="2f82c-220">Hallo OS schijf toohello koppelen nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f82c-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="2f82c-221">Een beheerde gegevensschijf van Hallo gegevens VHD-bestand maken en toe te voegen toohello nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f82c-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="2f82c-222">Maken van nieuwe virtuele machine Hallo door in te stellen van openbare IP-, virtueel netwerk en NIC.</span><span class="sxs-lookup"><span data-stu-id="2f82c-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="2f82c-223">Mogelijk zijn er extra stappen nodig toosupport uw toepassing die niet worden gedekt door deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="2f82c-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2f82c-224">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f82c-224">Next steps</span></span>

- <span data-ttu-id="2f82c-225">Verbinding maken met toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f82c-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="2f82c-226">Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f82c-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

