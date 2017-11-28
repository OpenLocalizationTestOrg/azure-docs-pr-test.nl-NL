---
title: Migreren virtuele machines naar Azure Premium-opslag | Microsoft Docs
description: Uw bestaande virtuele machines migreren naar Azure Premium-opslag. Premium-opslag biedt ondersteuning voor schijven voor hoge prestaties, lage latentie voor I/O-intensieve werkbelastingen die worden uitgevoerd op Azure Virtual Machines.
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 645b37fff2dd6a12114719bac66a937cf8e8ffaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="69cdf-104">Migreren naar Azure Premium-opslag (niet-beheerde schijven)</span><span class="sxs-lookup"><span data-stu-id="69cdf-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-105">Dit artikel wordt beschreven hoe u migreert van een virtuele machine die gebruikmaakt van niet-beheerde standaardschijven voor een virtuele machine die gebruikmaakt van niet-beheerde premium-schijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="69cdf-106">U wordt aangeraden dat u Azure beheerd schijven gebruikt voor nieuwe virtuele machines en u uw vorige niet-beheerde schijven converteren naar beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="69cdf-107">Beheerde schijven ingang onderliggende storage-accounts, zodat u niet te hoeft.</span><span class="sxs-lookup"><span data-stu-id="69cdf-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="69cdf-108">Zie voor meer informatie onze [schijven overzicht beheerde](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-108">For more information, please see our [Managed Disks Overview](storage-managed-disks-overview.md).</span></span>
>

<span data-ttu-id="69cdf-109">Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines met I/O-intensieve werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="69cdf-110">U kunt profiteren van de snelheid en prestaties van deze schijven nemen door te migreren van uw toepassing VM schijven naar Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="69cdf-111">Het doel van deze handleiding is om nieuwe gebruikers van betere Azure Premium-opslag voorbereiden voor een goede overgang van hun huidige systeem naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="69cdf-112">De handleiding biedt drie van de belangrijkste onderdelen van dit proces:</span><span class="sxs-lookup"><span data-stu-id="69cdf-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="69cdf-113">Plannen voor de migratie naar Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="69cdf-114">Voorbereiden en virtuele harde schijven (VHD's) te kopiëren naar Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="69cdf-115">Premium-opslag met van Azure virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="69cdf-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="69cdf-116">U kunt virtuele machines migreren van andere platforms naar Azure Premium-opslag of migreren van bestaande Azure-virtuele machines van de Standard-opslag naar Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="69cdf-117">Deze handleiding worden de stappen beschreven voor beide twee scenario's.</span><span class="sxs-lookup"><span data-stu-id="69cdf-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="69cdf-118">Volg de stappen die zijn opgegeven in de relevante sectie afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="69cdf-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-119">U vindt een overzicht van functies en prijzen van Premium-opslag in Premium-opslag: [krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="69cdf-120">Het is raadzaam om een hoge IOPS naar Azure Premium-opslag voor de beste prestaties voor uw toepassing vereisen schijf voor de virtuele machine migreren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="69cdf-121">Als de schijf niet hoge IOPS vereist, kunt u kosten beperken door handhaven standaardopslag die schijfgegevens voor virtuele machine op de harde schijven (HDD's) in plaats van SSD's opslaat.</span><span class="sxs-lookup"><span data-stu-id="69cdf-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="69cdf-122">De migratie voltooien in zijn geheel moet mogelijk extra acties vóór en na de stappen in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="69cdf-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="69cdf-123">Voorbeelden zijn virtuele netwerken of eindpunten configureren of u code wijzigingen aanbrengt in de toepassing zelf waarin u mogelijk de enige downtime in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="69cdf-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="69cdf-124">Deze acties zijn uniek voor elke toepassing en u ze samen met de stappen in deze handleiding voor de volledige overgang naar Premium-opslag zo weinig mogelijk moet voltooien.</span><span class="sxs-lookup"><span data-stu-id="69cdf-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="69cdf-125"><a name="plan-the-migration-to-premium-storage"></a>Plannen voor de migratie naar Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="69cdf-126">In deze sectie zorgt ervoor dat u bent klaar om de migratie stappen in dit artikel helpt u bij het maken van de beste beslissing op schijf en VM-typen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="69cdf-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="69cdf-127">Prerequisites</span></span>
* <span data-ttu-id="69cdf-128">U moet een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="69cdf-128">You will need an Azure subscription.</span></span> <span data-ttu-id="69cdf-129">Als u niet hebt, kunt u één maand [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/) abonnement of gaat u naar [prijzen van Azure](https://azure.microsoft.com/pricing/) voor meer opties.</span><span class="sxs-lookup"><span data-stu-id="69cdf-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="69cdf-130">Voor het uitvoeren van PowerShell-cmdlets, moet u de Microsoft Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="69cdf-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="69cdf-131">Zie [How to install and configure Azure PowerShell](/powershell/azure/overview) (Azure PowerShell installeren en configureren) voor het installatiepunt en de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="69cdf-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="69cdf-132">Wanneer u van plan bent te gebruiken van Azure VM's uitgevoerd op de Premium-opslag, moet u de compatibele virtuele machines voor een Premium-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="69cdf-133">Standaard- en Premium-opslag-schijven kunt u met Premium-opslag kunnen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="69cdf-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="69cdf-134">Premium-schijven voor opslag zijn in de toekomst meer VM-typen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="69cdf-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="69cdf-135">Zie voor meer informatie over alle beschikbare virtuele machine van Azure schijftypen en groottes [grootten voor virtuele machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [grootten voor Cloudservices](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="69cdf-136">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="69cdf-136">Considerations</span></span>
<span data-ttu-id="69cdf-137">Een virtuele machine van Azure ondersteunt meerdere schijven met Premium-opslag koppelen zodat uw toepassingen kunnen maximaal 256 TB aan opslag per VM hebben.</span><span class="sxs-lookup"><span data-stu-id="69cdf-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="69cdf-138">Met de Premium-opslag, kunnen uw toepassingen 80.000 IOP's (i/o-bewerkingen per seconde) per VM en 2000 MB per tweede schijfdoorvoer per virtuele machine met zeer lage latentie voor leesbewerkingen bereiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="69cdf-139">Hebt u opties in tal van virtuele machines en de schijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="69cdf-140">Deze sectie is om te zoeken naar een optie die het beste past bij uw workload.</span><span class="sxs-lookup"><span data-stu-id="69cdf-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="69cdf-141">Formaten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="69cdf-141">VM sizes</span></span>
<span data-ttu-id="69cdf-142">De Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69cdf-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="69cdf-143">Bekijk de prestatiekenmerken van virtuele machines die geschikt is voor Premium-opslag en kiest u de meest geschikte VM-grootte die het beste past bij uw workload.</span><span class="sxs-lookup"><span data-stu-id="69cdf-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="69cdf-144">Zorg ervoor dat er voldoende bandbreedte beschikbaar op de virtuele machine is om het verkeer van de schijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="69cdf-145">Schijfformaten</span><span class="sxs-lookup"><span data-stu-id="69cdf-145">Disk sizes</span></span>
<span data-ttu-id="69cdf-146">Er zijn vijf typen schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten.</span><span class="sxs-lookup"><span data-stu-id="69cdf-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="69cdf-147">In overweging nemen deze limieten bij het kiezen van het schijftype voor de virtuele machine op basis van de behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek worden geladen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="69cdf-148">Premium-schijven Type</span><span class="sxs-lookup"><span data-stu-id="69cdf-148">Premium Disks Type</span></span>  | <span data-ttu-id="69cdf-149">P10</span><span class="sxs-lookup"><span data-stu-id="69cdf-149">P10</span></span>   | <span data-ttu-id="69cdf-150">P20</span><span class="sxs-lookup"><span data-stu-id="69cdf-150">P20</span></span>   | <span data-ttu-id="69cdf-151">P30</span><span class="sxs-lookup"><span data-stu-id="69cdf-151">P30</span></span>            | <span data-ttu-id="69cdf-152">P40</span><span class="sxs-lookup"><span data-stu-id="69cdf-152">P40</span></span>            | <span data-ttu-id="69cdf-153">P50</span><span class="sxs-lookup"><span data-stu-id="69cdf-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="69cdf-154">Schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="69cdf-154">Disk size</span></span>           | <span data-ttu-id="69cdf-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="69cdf-155">128 GB</span></span>| <span data-ttu-id="69cdf-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="69cdf-156">512 GB</span></span>| <span data-ttu-id="69cdf-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="69cdf-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="69cdf-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="69cdf-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="69cdf-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="69cdf-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="69cdf-160">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="69cdf-160">IOPS per disk</span></span>       | <span data-ttu-id="69cdf-161">500</span><span class="sxs-lookup"><span data-stu-id="69cdf-161">500</span></span>   | <span data-ttu-id="69cdf-162">2300</span><span class="sxs-lookup"><span data-stu-id="69cdf-162">2300</span></span>  | <span data-ttu-id="69cdf-163">5000</span><span class="sxs-lookup"><span data-stu-id="69cdf-163">5000</span></span>           | <span data-ttu-id="69cdf-164">7500</span><span class="sxs-lookup"><span data-stu-id="69cdf-164">7500</span></span>           | <span data-ttu-id="69cdf-165">7500</span><span class="sxs-lookup"><span data-stu-id="69cdf-165">7500</span></span>           | 
| <span data-ttu-id="69cdf-166">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="69cdf-166">Throughput per disk</span></span> | <span data-ttu-id="69cdf-167">100 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="69cdf-167">100 MB per second</span></span> | <span data-ttu-id="69cdf-168">150 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="69cdf-168">150 MB per second</span></span> | <span data-ttu-id="69cdf-169">200 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="69cdf-169">200 MB per second</span></span> | <span data-ttu-id="69cdf-170">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="69cdf-170">250 MB per second</span></span> | <span data-ttu-id="69cdf-171">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="69cdf-171">250 MB per second</span></span> |

<span data-ttu-id="69cdf-172">Bepalen of extra gegevensschijven nodig zijn voor uw virtuele machine zijn afhankelijk van uw workload.</span><span class="sxs-lookup"><span data-stu-id="69cdf-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="69cdf-173">U kunt meerdere permanente gegevensschijven koppelen aan uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69cdf-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="69cdf-174">Indien nodig, kunt u op de schijven te verhogen van de capaciteit en prestaties van het volume stripe.</span><span class="sxs-lookup"><span data-stu-id="69cdf-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="69cdf-175">(Zie Wat is er schijf Striping [hier](storage-premium-storage-performance.md#disk-striping).) Als u Premium-opslag gegevensschijven met stripe [opslagruimten][4], moet u deze configureren met één kolom voor elke schijf die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="69cdf-176">Anders wordt de algehele prestaties van de striped volumes mogelijk lager dan verwacht vanwege ongelijke verdeling van het verkeer op de schijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="69cdf-177">Voor Linux VM's kunt u de *mdadm* hulpprogramma dezelfde bereiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="69cdf-178">Zie het artikel [Software-RAID configureren op Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-178">See article [Configure Software RAID on Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="69cdf-179">Schaalbaarheidsdoelen van Storage-account</span><span class="sxs-lookup"><span data-stu-id="69cdf-179">Storage account scalability targets</span></span>
<span data-ttu-id="69cdf-180">Premium-opslagaccounts hebben het volgende schaalbaarheidsdoelen naast de [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="69cdf-181">Als uw toepassingsvereisten de schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt, bouwen van uw toepassing gebruik van meerdere opslagaccounts en partitioneren van uw gegevens over de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="69cdf-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="69cdf-182">Capaciteit van de totale Account</span><span class="sxs-lookup"><span data-stu-id="69cdf-182">Total Account Capacity</span></span> | <span data-ttu-id="69cdf-183">Totale bandbreedte voor een Account met lokaal redundante opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="69cdf-184">Schijf capaciteit: 35TB</span><span class="sxs-lookup"><span data-stu-id="69cdf-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="69cdf-185">Momentopname maken van capaciteit: 10 TB</span><span class="sxs-lookup"><span data-stu-id="69cdf-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="69cdf-186">Maximaal 50 gigabits per seconde voor inkomend en uitgaand</span><span class="sxs-lookup"><span data-stu-id="69cdf-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="69cdf-187">Bekijk voor meer informatie op Premium-opslag-specificaties [Scalability and Performance Targets wanneer u Premium-opslag](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="69cdf-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="69cdf-188">Het beleid voor schijf</span><span class="sxs-lookup"><span data-stu-id="69cdf-188">Disk caching policy</span></span>
<span data-ttu-id="69cdf-189">Beleid voor de schijfcache is standaard *alleen-lezen* voor alle Premium gegevensschijven, en *lezen-schrijven* voor de Premium-schijf is gekoppeld aan de VM.</span><span class="sxs-lookup"><span data-stu-id="69cdf-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="69cdf-190">Deze configuratieinstelling wordt aanbevolen de optimale prestaties voor uw toepassing IOs bereiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="69cdf-191">Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="69cdf-192">De cache-instellingen voor bestaande gegevensschijven kunnen worden bijgewerkt met behulp van [Azure Portal](https://portal.azure.com) of de *- HostCaching* parameter van de *Set AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="69cdf-193">Locatie</span><span class="sxs-lookup"><span data-stu-id="69cdf-193">Location</span></span>
<span data-ttu-id="69cdf-194">Kies een locatie waar Azure Premium-opslag beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="69cdf-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="69cdf-195">Zie [Azure-Services per regio](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="69cdf-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="69cdf-196">Virtuele machines zich in dezelfde regio bevinden als het opslagaccount dat slaat de schijven voor de virtuele machine u veel betere prestaties krijgt dan als ze zich in afzonderlijke regio's.</span><span class="sxs-lookup"><span data-stu-id="69cdf-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="69cdf-197">Andere Azure VM-configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="69cdf-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="69cdf-198">Wanneer u een virtuele machine in Azure maakt, wordt u gevraagd om bepaalde VM-instellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="69cdf-199">Denk eraan dat enkele instellingen vast voor de levensduur van de virtuele machine, terwijl u kunt wijzigen of anderen later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="69cdf-200">Deze configuratie-instellingen voor virtuele machine van Azure controleren en zorg ervoor dat deze overeenkomen met de vereisten van uw werkbelasting op de juiste wijze zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="69cdf-201">Optimalisatie</span><span class="sxs-lookup"><span data-stu-id="69cdf-201">Optimization</span></span>
<span data-ttu-id="69cdf-202">[Azure Premium-opslag: Ontwerpen voor hoge prestaties](storage-premium-storage-performance.md) biedt richtlijnen voor het bouwen van krachtige toepassingen met behulp van Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="69cdf-203">Volg de richtlijnen in combinatie met aanbevolen procedures voor prestaties van toepassing op de technologieën die worden gebruikt door uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="69cdf-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="69cdf-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Voorbereiden en virtuele harde schijven (VHD's) te kopiëren naar Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="69cdf-205">De volgende sectie bevat richtlijnen voor het voorbereiden van VHD's van uw virtuele machine en VHD's kopiëren naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="69cdf-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="69cdf-206">Scenario 1: 'Ik ben migreren van bestaande Azure virtuele machines naar Azure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="69cdf-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="69cdf-207">Scenario 2: 'Ik ben migreren VM's van andere platforms naar Azure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="69cdf-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="69cdf-208">Vereisten</span><span class="sxs-lookup"><span data-stu-id="69cdf-208">Prerequisites</span></span>
<span data-ttu-id="69cdf-209">Als u de VHD's voorbereiden voor migratie, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="69cdf-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="69cdf-210">Een Azure-abonnement, een opslagaccount en een container in dat storage-account waarmee u uw VHD kunt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="69cdf-211">Houd er rekening mee dat het doelopslagaccount kan een Standard of Premium-opslag-account, afhankelijk van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="69cdf-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="69cdf-212">Een hulpprogramma voor de VHD generalize als u wilt maken van meerdere exemplaren van de virtuele machine uit.</span><span class="sxs-lookup"><span data-stu-id="69cdf-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="69cdf-213">Bijvoorbeeld: sysprep voor Windows of virt-sysprep voor Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="69cdf-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="69cdf-214">Een hulpprogramma voor het uploaden van het VHD-bestand naar de Storage-account.</span><span class="sxs-lookup"><span data-stu-id="69cdf-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="69cdf-215">Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md) of gebruik een [Azure Opslagverkenner](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="69cdf-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="69cdf-216">Deze handleiding beschrijft de VHD met het AzCopy-hulpprogramma kopieert.</span><span class="sxs-lookup"><span data-stu-id="69cdf-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-217">Als u de optie synchrone kopiëren met AzCopy, kiest voor optimale prestaties, kopieert u uw VHD door een van deze hulpprogramma's van een Azure-virtuele machine die zich in dezelfde regio bevinden als het doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69cdf-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="69cdf-218">Als u een VHD van een Azure-virtuele machine in een andere regio kopieert, kan de prestaties van uw trager worden.</span><span class="sxs-lookup"><span data-stu-id="69cdf-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="69cdf-219">Voor het kopiëren een grote hoeveelheid gegevens over beperkte bandbreedte, kunt u overwegen [via de Azure Import/Export-service gegevens overdraagt naar Blob Storage](storage-import-export-service.md); Hiermee kunt u uw gegevens overbrengen back-upfunctie harde schijven naar een Azure-datacenter.</span><span class="sxs-lookup"><span data-stu-id="69cdf-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="69cdf-220">U kunt de Azure Import/Export-service gebruiken om gegevens te kopiëren naar een standard-opslagaccount alleen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="69cdf-221">Nadat de gegevens uw account standard-opslag is, kunt u ofwel de [kopie Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) of AzCopy voor de gegevensoverdracht naar uw premium-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69cdf-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="69cdf-222">Houd er rekening mee dat Microsoft Azure biedt alleen ondersteuning voor VHD-bestanden van vaste grootte.</span><span class="sxs-lookup"><span data-stu-id="69cdf-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="69cdf-223">VHDX-bestanden of dynamische virtuele harde schijven worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="69cdf-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="69cdf-224">Als u een dynamische VHD hebt, kunt u deze converteren naar vaste grootte met behulp van de [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="69cdf-225"><a name="scenario1"></a>Scenario 1: 'Ik ben migreren van bestaande Azure virtuele machines naar Azure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="69cdf-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="69cdf-226">Als u bestaande Azure-virtuele machines migreert, stop de virtuele machine, virtuele harde schijven per het type VHD die u wilt voorbereiden en kopieer de VHD met AzCopy of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69cdf-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="69cdf-227">De virtuele machine moet volledig omlaag voor het migreren van een oude toestand.</span><span class="sxs-lookup"><span data-stu-id="69cdf-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="69cdf-228">Er zijn een uitvaltijd totdat de migratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="69cdf-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="69cdf-229">Step 1.</span><span class="sxs-lookup"><span data-stu-id="69cdf-229">Step 1.</span></span> <span data-ttu-id="69cdf-230">VHD's voorbereiden voor migratie</span><span class="sxs-lookup"><span data-stu-id="69cdf-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="69cdf-231">Als u bestaande Azure-virtuele machines naar Premium-opslag migreert, mogelijk uw VHD:</span><span class="sxs-lookup"><span data-stu-id="69cdf-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="69cdf-232">De installatiekopie van een gegeneraliseerde besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="69cdf-232">A generalized operating system image</span></span>
* <span data-ttu-id="69cdf-233">Een unieke besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="69cdf-233">A unique operating system disk</span></span>
* <span data-ttu-id="69cdf-234">Een gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="69cdf-234">A data disk</span></span>

<span data-ttu-id="69cdf-235">Hieronder doorlopen we deze 3 scenario's voor het voorbereiden van uw VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="69cdf-236">Een gegeneraliseerde besturingssysteem-VHD gebruiken voor het maken van meerdere VM-exemplaren</span><span class="sxs-lookup"><span data-stu-id="69cdf-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="69cdf-237">Als u een VHD die wordt gebruikt voor het maken van meerdere algemene Azure VM-exemplaren uploaden wilt, moet u eerst de VHD met een hulpprogramma sysprep generalize.</span><span class="sxs-lookup"><span data-stu-id="69cdf-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="69cdf-238">Dit geldt voor een VHD die on-premises of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="69cdf-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="69cdf-239">Sysprep verwijdert alle systeemspecifieke gegevens uit de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69cdf-240">Een momentopname of back-up van uw VM voordat deze het generaliseren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="69cdf-241">Sysprep uitgevoerd worden gestopt en toewijzing van de VM-instantie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="69cdf-242">Volg onderstaande stappen om sysprep een Windows-besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="69cdf-243">Houd er rekening mee dat de opdracht Sysprep uit te voeren, moet u de virtuele machine afgesloten.</span><span class="sxs-lookup"><span data-stu-id="69cdf-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="69cdf-244">Zie voor meer informatie over Sysprep [Sysprep overzicht](http://technet.microsoft.com/library/hh825209.aspx) of [technische documentatie van Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="69cdf-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="69cdf-245">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="69cdf-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="69cdf-246">Voer de volgende opdracht Sysprep openen:</span><span class="sxs-lookup"><span data-stu-id="69cdf-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="69cdf-247">Selecteer in het hulpprogramma voor systeemvoorbereiding, voer System Out-of-Box Experience (OOBE), schakel het selectievakje Generalize, selecteert u **afsluiten**, en klik vervolgens op **OK**, zoals wordt weergegeven in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="69cdf-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="69cdf-248">Sysprep wordt generalize van het besturingssysteem en het systeem afsluiten.</span><span class="sxs-lookup"><span data-stu-id="69cdf-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="69cdf-249">Voor een VM Ubuntu virt-sysprep te gebruiken als u dezelfde.</span><span class="sxs-lookup"><span data-stu-id="69cdf-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="69cdf-250">Zie [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="69cdf-251">Zie ook enkele van de open source [inrichten van Linux-servers software](http://www.cyberciti.biz/tips/server-provisioning-software.html) voor andere Linux-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="69cdf-252">Een unieke besturingssysteem-VHD gebruiken voor het maken van een enkel VM-exemplaar</span><span class="sxs-lookup"><span data-stu-id="69cdf-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="69cdf-253">Als u een toepassing die wordt uitgevoerd op de virtuele machine waarvoor u de specifieke gegevens van de machine hebt, niet generalize voor de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="69cdf-254">Een niet-gegeneraliseerd VHD kan worden gebruikt voor het maken van een uniek exemplaar van de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="69cdf-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="69cdf-255">Bijvoorbeeld, als u een domeincontroller op uw VHD hebt, maakt sysprep wordt uitgevoerd het niet effectief als een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="69cdf-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="69cdf-256">Bekijk de toepassingen die worden uitgevoerd op uw virtuele machine en de impact van sysprep erop worden uitgevoerd voordat het generaliseren van de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="69cdf-257">Gegevensschijf VHD registreren</span><span class="sxs-lookup"><span data-stu-id="69cdf-257">Register data disk VHD</span></span>
<span data-ttu-id="69cdf-258">Hebt u gegevensschijven in Azure worden gemigreerd, moet u ervoor zorgen dat de virtuele machines die gebruikmaken van de gegevensschijven van deze worden afgesloten.</span><span class="sxs-lookup"><span data-stu-id="69cdf-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="69cdf-259">Volg de stappen die hieronder worden beschreven op de VHD naar Azure Premium-opslag te kopiëren en registreren als een ingerichte gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="69cdf-260">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="69cdf-260">Step 2.</span></span> <span data-ttu-id="69cdf-261">Het doel voor de VHD maken</span><span class="sxs-lookup"><span data-stu-id="69cdf-261">Create the destination for your VHD</span></span>
<span data-ttu-id="69cdf-262">Een opslagaccount voor het onderhouden van uw VHD's maken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="69cdf-263">Houd rekening met de volgende punten bij het plannen waar uw VHD's wordt opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="69cdf-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="69cdf-264">Het doel van Premium storage-account.</span><span class="sxs-lookup"><span data-stu-id="69cdf-264">The target Premium storage account.</span></span>
* <span data-ttu-id="69cdf-265">De opslaglocatie voor de account moet hetzelfde als de Premium-opslag kunnen virtuele Azure-machines in de laatste fase wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="69cdf-266">U kan kopiëren naar een nieuw opslagaccount of wilt gebruiken hetzelfde opslagaccount op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="69cdf-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="69cdf-267">Kopieer en sla de opslagaccountsleutel van het opslagaccount voor de bestemming voor de volgende fase.</span><span class="sxs-lookup"><span data-stu-id="69cdf-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="69cdf-268">Voor gegevensschijven, kunt u een aantal gegevensschijven in een standard-opslagaccount (bijvoorbeeld schijven die koelervoorbeeld opslag) behouden, maar wij raden u alle gegevens voor de werkbelasting van de productie te gebruiken van premium-opslag te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="69cdf-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Stap 3.</span><span class="sxs-lookup"><span data-stu-id="69cdf-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="69cdf-270">Kopieer de VHD met AzCopy of PowerShell</span><span class="sxs-lookup"><span data-stu-id="69cdf-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="69cdf-271">U moet uw container pad en de opslagruimte accountsleutel vinden voor het verwerken van een van deze twee opties.</span><span class="sxs-lookup"><span data-stu-id="69cdf-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="69cdf-272">Container pad en de opslagruimte accountsleutel vindt u in **Azure Portal** > **opslag**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="69cdf-273">De container-URL worden zoals 'https://myaccount.blob.core.windows.net/mycontainer/'.</span><span class="sxs-lookup"><span data-stu-id="69cdf-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="69cdf-274">Optie 1: Kopieer geen VHD met AzCopy (asynchrone kopiëren)</span><span class="sxs-lookup"><span data-stu-id="69cdf-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="69cdf-275">AzCopy gebruikt, kunt u eenvoudig uploaden de VHD via Internet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="69cdf-276">Dit kan tijd duren, afhankelijk van de grootte van de VHD's.</span><span class="sxs-lookup"><span data-stu-id="69cdf-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="69cdf-277">Vergeet niet om te controleren limieten inkomend en uitgaand van het opslagaccount wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="69cdf-278">Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="69cdf-279">Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="69cdf-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="69cdf-280">Open Azure PowerShell en Ga naar de map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="69cdf-281">Gebruik de volgende opdracht om te kopiëren van de VHD-bestand van 'Bron' naar 'Bestemming'.</span><span class="sxs-lookup"><span data-stu-id="69cdf-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="69cdf-282">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69cdf-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="69cdf-283">Hier volgen beschrijvingen van de parameters gebruikt in de AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="69cdf-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="69cdf-284">**/ Bron:  *&lt;bron&gt;:***  locatie van de map of URL van de opslagcontainer die de VHD bevat.</span><span class="sxs-lookup"><span data-stu-id="69cdf-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="69cdf-285">**/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van het opslagaccount van de bron.</span><span class="sxs-lookup"><span data-stu-id="69cdf-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="69cdf-286">**/ Dest:  *&lt;bestemming&gt;:***  URL van de opslagcontainer voor het kopiëren van de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="69cdf-287">**/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van het doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69cdf-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="69cdf-288">**/ Patroon:  *&lt;bestandsnaam&gt;:***  Geef de bestandsnaam van de VHD te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="69cdf-289">Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="69cdf-290">Optie 2: Kopieer geen VHD met PowerShell (Synchronized kopiëren)</span><span class="sxs-lookup"><span data-stu-id="69cdf-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="69cdf-291">U kunt ook het VHD-bestand met de PowerShell-cmdlet Start-AzureStorageBlobCopy kopiëren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="69cdf-292">Gebruik de volgende opdracht op Azure PowerShell te kopiëren van de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="69cdf-293">Vervang de waarden in <> met overeenkomende waarden uit de bron- en storage-account.</span><span class="sxs-lookup"><span data-stu-id="69cdf-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="69cdf-294">Voor het gebruik van deze opdracht moet u een zogenaamd VHD's in uw doelopslagaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="69cdf-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="69cdf-295">Als de container niet bestaat, maken voordat de opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="69cdf-296">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69cdf-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="69cdf-297"><a name="scenario2"></a>Scenario 2: 'Ik ben migreren VM's van andere platforms naar Azure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="69cdf-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="69cdf-298">Als u VHD van niet - Azure Cloud-opslag naar Azure migreert, moet u eerst de VHD exporteren naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="69cdf-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="69cdf-299">Het pad van de volledige broncode van de lokale map waar de VHD handige wordt opgeslagen en vervolgens met behulp van AzCopy te uploaden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="69cdf-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="69cdf-300">Step 1.</span><span class="sxs-lookup"><span data-stu-id="69cdf-300">Step 1.</span></span> <span data-ttu-id="69cdf-301">Exporteren van VHD naar een lokale map</span><span class="sxs-lookup"><span data-stu-id="69cdf-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="69cdf-302">Kopieer geen VHD van AWS</span><span class="sxs-lookup"><span data-stu-id="69cdf-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="69cdf-303">Als u van AWS gebruikmaakt, moet u het exemplaar EC2 exporteren naar een VHD in een Amazon S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="69cdf-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="69cdf-304">Volg de stappen beschreven in de Amazon-documentatie voor Amazon EC2 exemplaren voor het installeren van het hulpprogramma EC2 Amazon-opdrachtregelinterface (CLI) en voer de opdracht create-exemplaar-export-taak het exemplaar EC2 exporteren naar een VHD-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="69cdf-305">Zorg ervoor dat u **VHD** voor de schijf &#95; INSTALLATIEKOPIE &#95; INDELING variabele bij het uitvoeren van de **-exemplaar-export-taak maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="69cdf-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="69cdf-306">Het geëxporteerde VHD-bestand wordt opgeslagen in de Amazon S3-bucket die u tijdens dat proces opgeeft.</span><span class="sxs-lookup"><span data-stu-id="69cdf-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="69cdf-307">Download het VHD-bestand van de S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="69cdf-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="69cdf-308">Selecteer vervolgens het VHD-bestand **acties** > **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="69cdf-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="69cdf-309">Kopieer geen VHD van andere niet-Azure-cloud</span><span class="sxs-lookup"><span data-stu-id="69cdf-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="69cdf-310">Als u VHD van niet - Azure Cloud-opslag naar Azure migreert, moet u eerst de VHD exporteren naar een lokale map.</span><span class="sxs-lookup"><span data-stu-id="69cdf-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="69cdf-311">Kopieer het pad van de volledige broncode van de lokale map waar de VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="69cdf-312">Kopieer geen VHD van on-premises</span><span class="sxs-lookup"><span data-stu-id="69cdf-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="69cdf-313">Als u een VHD van een on-premises omgeving migreert, moet u de volledige broncode pad op waar de VHD is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="69cdf-314">Het bronpad kan een server of bestandsshare worden.</span><span class="sxs-lookup"><span data-stu-id="69cdf-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="69cdf-315">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="69cdf-315">Step 2.</span></span> <span data-ttu-id="69cdf-316">Het doel voor de VHD maken</span><span class="sxs-lookup"><span data-stu-id="69cdf-316">Create the destination for your VHD</span></span>
<span data-ttu-id="69cdf-317">Een opslagaccount voor het onderhouden van uw VHD's maken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="69cdf-318">Houd rekening met de volgende punten bij het plannen waar uw VHD's wordt opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="69cdf-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="69cdf-319">Het doel storage-account kan worden standaard of premium-opslag, afhankelijk van uw vereisten voor toepassingsimplementatie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="69cdf-320">Regio van het opslagaccount moet hetzelfde zijn als Premium-opslag kunnen Azure virtuele machines in de laatste fase wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="69cdf-321">U kan kopiëren naar een nieuw opslagaccount of wilt gebruiken hetzelfde opslagaccount op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="69cdf-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="69cdf-322">Kopieer en sla de opslagaccountsleutel van het opslagaccount voor de bestemming voor de volgende fase.</span><span class="sxs-lookup"><span data-stu-id="69cdf-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="69cdf-323">Wij raden u alle gegevens voor de werkbelasting van de productie te gebruiken van premium-opslag te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="69cdf-324">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="69cdf-324">Step 3.</span></span> <span data-ttu-id="69cdf-325">De VHD te uploaden naar Azure Storage</span><span class="sxs-lookup"><span data-stu-id="69cdf-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="69cdf-326">Nu dat u uw VHD in de lokale directory hebt, kunt u AzCopy of AzurePowerShell het VHD-bestand uploaden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="69cdf-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="69cdf-327">Beide opties vindt u hier:</span><span class="sxs-lookup"><span data-stu-id="69cdf-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="69cdf-328">Optie 1: Met behulp van Azure PowerShell Add-AzureVhd het .vhd-bestand te uploaden</span><span class="sxs-lookup"><span data-stu-id="69cdf-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="69cdf-329">Een voorbeeld <Uri> mogelijk ***'https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd'***.</span><span class="sxs-lookup"><span data-stu-id="69cdf-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="69cdf-330">Een voorbeeld <FileInfo> mogelijk ***'C:\path\to\upload.vhd'***.</span><span class="sxs-lookup"><span data-stu-id="69cdf-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="69cdf-331">Optie 2: Upload het .vhd-bestand met behulp van AzCopy</span><span class="sxs-lookup"><span data-stu-id="69cdf-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="69cdf-332">AzCopy gebruikt, kunt u eenvoudig uploaden de VHD via Internet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="69cdf-333">Dit kan tijd duren, afhankelijk van de grootte van de VHD's.</span><span class="sxs-lookup"><span data-stu-id="69cdf-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="69cdf-334">Vergeet niet om te controleren limieten inkomend en uitgaand van het opslagaccount wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="69cdf-335">Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="69cdf-336">Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="69cdf-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="69cdf-337">Open Azure PowerShell en Ga naar de map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="69cdf-338">Gebruik de volgende opdracht om te kopiëren van de VHD-bestand van 'Bron' naar 'Bestemming'.</span><span class="sxs-lookup"><span data-stu-id="69cdf-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="69cdf-339">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="69cdf-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="69cdf-340">Hier volgen beschrijvingen van de parameters gebruikt in de AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="69cdf-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="69cdf-341">**/ Bron:  *&lt;bron&gt;:***  locatie van de map of URL van de opslagcontainer die de VHD bevat.</span><span class="sxs-lookup"><span data-stu-id="69cdf-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="69cdf-342">**/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van het opslagaccount van de bron.</span><span class="sxs-lookup"><span data-stu-id="69cdf-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="69cdf-343">**/ Dest:  *&lt;bestemming&gt;:***  URL van de opslagcontainer voor het kopiëren van de VHD.</span><span class="sxs-lookup"><span data-stu-id="69cdf-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="69cdf-344">**/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van het doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69cdf-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="69cdf-345">**/ BlobType: pagina:** geeft aan dat de bestemming een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="69cdf-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="69cdf-346">**/ Patroon:  *&lt;bestandsnaam&gt;:***  Geef de bestandsnaam van de VHD te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="69cdf-347">Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="69cdf-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="69cdf-348">Andere opties voor het uploaden van een VHD</span><span class="sxs-lookup"><span data-stu-id="69cdf-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="69cdf-349">U kunt ook een VHD uploaden naar uw storage-account met behulp van een van de volgende wijzen:</span><span class="sxs-lookup"><span data-stu-id="69cdf-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="69cdf-350">API voor Azure Storage kopiëren-Blob</span><span class="sxs-lookup"><span data-stu-id="69cdf-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="69cdf-351">Azure Storage Explorer uploaden van BLOB 's</span><span class="sxs-lookup"><span data-stu-id="69cdf-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="69cdf-352">Opslag voor importeren/exporteren Service REST API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="69cdf-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="69cdf-353">U kunt het beste Import/Export-Service gebruikt als de geschatte tijd uploaden is langer dan zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="69cdf-354">U kunt [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) om in te schatten het tijdstip in gegevenseenheid grootte en de overdracht.</span><span class="sxs-lookup"><span data-stu-id="69cdf-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="69cdf-355">Import/Export kan worden gebruikt om te kopiëren naar een standard-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="69cdf-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="69cdf-356">U wilt kopiëren van de standard-opslag naar premium storage-account met behulp van een hulpprogramma zoals AzCopy.</span><span class="sxs-lookup"><span data-stu-id="69cdf-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="69cdf-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Azure virtuele machines met Premium-opslag maken</span><span class="sxs-lookup"><span data-stu-id="69cdf-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="69cdf-358">Nadat de VHD is geüpload of gekopieerd naar het gewenste opslagaccount, volg de instructies in deze sectie om de VHD registreren als een installatiekopie van het besturingssysteem, of de besturingssysteemschijf afhankelijk van uw scenario en maak vervolgens een VM-instantie uit.</span><span class="sxs-lookup"><span data-stu-id="69cdf-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="69cdf-359">De gegevensschijf VHD kan worden gekoppeld aan de virtuele machine nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="69cdf-360">Een migratie voorbeeldscript wordt verstrekt aan het einde van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="69cdf-361">Dit eenvoudige script komt niet overeen met alle scenario's.</span><span class="sxs-lookup"><span data-stu-id="69cdf-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="69cdf-362">Mogelijk moet u het script moet overeenkomen met uw specifieke scenario bijwerken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="69cdf-363">Als dit script wordt toegepast op uw scenario Zie onderstaande [A migratie voorbeeldscript](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="69cdf-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="69cdf-364">Controlelijst</span><span class="sxs-lookup"><span data-stu-id="69cdf-364">Checklist</span></span>
1. <span data-ttu-id="69cdf-365">Wacht totdat alle VHD-schijven kopiëren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="69cdf-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="69cdf-366">Zorg ervoor dat de dat Premium-opslag is beschikbaar in de regio die u naar migreert.</span><span class="sxs-lookup"><span data-stu-id="69cdf-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="69cdf-367">Bepaal de nieuwe VM-reeks die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="69cdf-368">Dit moet een Premium-opslag die geschikt zijn en de grootte moet hangt af van de beschikbaarheid in regio en op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="69cdf-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="69cdf-369">Bepaal de exacte VM-grootte die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="69cdf-370">VM-grootte moet groot genoeg zijn om het aantal gegevensschijven dat u hebt ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="69cdf-371">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="69cdf-371">E.g.</span></span> <span data-ttu-id="69cdf-372">Als u 4 gegevensschijven hebt, moet de virtuele machine 2 of hoger kernen hebben.</span><span class="sxs-lookup"><span data-stu-id="69cdf-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="69cdf-373">Houd ook rekening met verwerkingskracht, geheugen en netwerkbandbreedte moet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="69cdf-374">Premium-opslagaccount maken in de doelregio.</span><span class="sxs-lookup"><span data-stu-id="69cdf-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="69cdf-375">Dit is het account dat u voor de nieuwe virtuele machine gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="69cdf-376">De huidige VM details die handig zijn, met inbegrip van de lijst van schijven en de bijbehorende VHD-blobs hebben.</span><span class="sxs-lookup"><span data-stu-id="69cdf-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="69cdf-377">Bereid uw toepassing uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-377">Prepare your application for downtime.</span></span> <span data-ttu-id="69cdf-378">U hebt hiervoor een schone migratie stoppen van de verwerking in het huidige systeem.</span><span class="sxs-lookup"><span data-stu-id="69cdf-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="69cdf-379">Alleen dan kunt u dit downloaden naar consistente status die u naar het nieuwe platform migreren kunt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="69cdf-380">Duur van uitvaltijd is afhankelijk van de hoeveelheid gegevens op de schijven om te migreren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-381">Als u een Azure Resource Manager VM vanaf een speciale VHD schijf maakt, raadpleegt u [deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) voor de implementatie van Resource Manager-VM met bestaande schijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="69cdf-382">Registreren van uw VHD</span><span class="sxs-lookup"><span data-stu-id="69cdf-382">Register your VHD</span></span>
<span data-ttu-id="69cdf-383">Een virtuele machine van besturingssysteem-VHD maken of een gegevensschijf koppelen aan een nieuwe virtuele machine, moet u deze eerst registreren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="69cdf-384">Voer onderstaande stappen, afhankelijk van uw VHD-scenario.</span><span class="sxs-lookup"><span data-stu-id="69cdf-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="69cdf-385">Besturingssysteem-VHD voor het maken van meerdere exemplaren van de virtuele machine van Azure gegeneraliseerd</span><span class="sxs-lookup"><span data-stu-id="69cdf-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="69cdf-386">Nadat gegeneraliseerde installatiekopie van het besturingssysteem VHD is geüpload naar het opslagaccount, registreert u dit als een **Azure VM-installatiekopie** zodat u een of meer VM-exemplaren van deze maken kunt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="69cdf-387">Gebruik de volgende PowerShell-cmdlets voor het registreren van uw VHD als de installatiekopie van een besturingssysteem van de Azure-virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69cdf-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="69cdf-388">Geef de URL van de volledige container waarnaar de VHD is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="69cdf-389">Kopiëren en opslaan van de naam van deze nieuwe Azure VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="69cdf-390">In het bovenstaande voorbeeld is het *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="69cdf-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="69cdf-391">Unieke besturingssysteem-VHD voor het maken van één exemplaar van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="69cdf-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="69cdf-392">Nadat de unieke OS VHD is geüpload naar het opslagaccount, registreert u dit als een **Azure Besturingssysteemschijf** zodat u een VM-exemplaar van deze maken kunt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="69cdf-393">Deze PowerShell-cmdlets gebruiken om uw VHD registreren als een Besturingssysteemschijf Azure.</span><span class="sxs-lookup"><span data-stu-id="69cdf-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="69cdf-394">Geef de URL van de volledige container waarnaar de VHD is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="69cdf-395">Kopiëren en opslaan van de naam van deze nieuwe Azure OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="69cdf-396">In het bovenstaande voorbeeld is het *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="69cdf-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="69cdf-397">Gegevens schijf VHD moet worden gekoppeld aan de nieuwe virtuele machine van Azure-exemplaren</span><span class="sxs-lookup"><span data-stu-id="69cdf-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="69cdf-398">Nadat de gegevensschijf VHD is geüpload naar storage-account, registreren als een Azure-gegevensschijf zodat deze kan worden gekoppeld aan uw nieuwe DS-serie, DSv2 reeks of GS-serie Azure VM-instantie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="69cdf-399">Deze PowerShell-cmdlets gebruiken om uw VHD registreren als een Azure-gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="69cdf-400">Geef de URL van de volledige container waarnaar de VHD is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="69cdf-401">Kopiëren en opslaan van de naam van deze nieuwe Azure-gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="69cdf-402">In het bovenstaande voorbeeld is het *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="69cdf-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="69cdf-403">Maak een geschikt VM voor Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="69cdf-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="69cdf-404">Eenmaal de installatiekopie van het besturingssysteem of besturingssysteemschijf zijn geregistreerd, maakt u een nieuwe Active Directory-serie, DSv2-serie- of GS-serie VM.</span><span class="sxs-lookup"><span data-stu-id="69cdf-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="69cdf-405">U gaat gebruiken de installatiekopie van besturingssysteem of de naam van een besturingssysteem schijf die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="69cdf-406">Selecteer het VM-type van de laag Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="69cdf-407">In onderstaand voorbeeld gebruiken we de *Standard_DS2* VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="69cdf-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-408">De schijfgrootte om ervoor te zorgen dat deze overeenkomt met de capaciteit en prestatie-eisen en de beschikbare Azure schijfgrootte bijwerken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="69cdf-409">Volg de stapsgewijze PowerShell-cmdlets hieronder om aan te maken van de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69cdf-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="69cdf-410">Stel eerst de algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="69cdf-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="69cdf-411">Maak eerst een cloudservice waarin u uw nieuwe virtuele machines worden gehost.</span><span class="sxs-lookup"><span data-stu-id="69cdf-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="69cdf-412">Maak vervolgens de virtuele machine van Azure-instantie van de installatiekopie van het besturingssysteem of de OS-schijf die u hebt geregistreerd, afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="69cdf-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="69cdf-413">Besturingssysteem-VHD voor het maken van meerdere exemplaren van de virtuele machine van Azure gegeneraliseerd</span><span class="sxs-lookup"><span data-stu-id="69cdf-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="69cdf-414">Maken van een of meer nieuwe DS reeks Azure VM-exemplaren met de **installatiekopie van het besturingssysteem Azure** die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="69cdf-415">Geef de naam van deze installatiekopie van het besturingssysteem in de VM-configuratie bij het maken van nieuwe virtuele machine, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="69cdf-416">Unieke besturingssysteem-VHD voor het maken van één exemplaar van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="69cdf-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="69cdf-417">Maak een nieuw DS reeks Azure VM exemplaar met de **Besturingssysteemschijf Azure** die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="69cdf-418">Bij het maken van de nieuwe virtuele machine zoals hieronder wordt weergegeven, moet u deze naam Besturingssysteemschijf opgeven in de VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="69cdf-419">Geef andere Azure VM-informatie, zoals een cloudservice, regio, storage-account, beschikbaarheidsset en het beleid.</span><span class="sxs-lookup"><span data-stu-id="69cdf-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="69cdf-420">Houd er rekening mee dat de VM-instantie geplaatst met bijbehorende besturingssysteem of gegevensschijven, worden moet zodat de geselecteerde cloud-service, regio en storage-account op dezelfde locatie als de onderliggende virtuele harde schijven van deze schijven zijn moet.</span><span class="sxs-lookup"><span data-stu-id="69cdf-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="69cdf-421">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="69cdf-421">Attach data disk</span></span>
<span data-ttu-id="69cdf-422">Ten slotte, als u de gegevensschijf VHD's hebt geregistreerd, koppel ze aan de nieuwe Premium-opslag compatibele Azure VM.</span><span class="sxs-lookup"><span data-stu-id="69cdf-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="69cdf-423">Gebruikt u de volgende PowerShell-cmdlet gegevensschijf koppelen aan de nieuwe virtuele machine en het cachebeleid opgeven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="69cdf-424">In onderstaand voorbeeld het cachebeleid is ingesteld op *ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="69cdf-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="69cdf-425">Mogelijk zijn er extra stappen die nodig zijn voor ondersteuning van uw toepassing die niet worden gedekt door deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="69cdf-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="69cdf-426">Controleren en back-up plannen</span><span class="sxs-lookup"><span data-stu-id="69cdf-426">Checking and plan backup</span></span>
<span data-ttu-id="69cdf-427">Nadat de nieuwe virtuele machine actief en werkend is, toegang tot dit met behulp van dezelfde aanmeldings-id en wachtwoord is als de oorspronkelijke virtuele machine en controleer of dat alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="69cdf-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="69cdf-428">Alle instellingen, inclusief de striped volumes, zou aanwezig zijn in de nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="69cdf-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="69cdf-429">De laatste stap is het plannen van back-up en -onderhoudsschema voor de nieuwe virtuele machine op basis van de behoeften van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="69cdf-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="69cdf-430"><a name="a-sample-migration-script"></a>Een voorbeeldscript voor migratie</span><span class="sxs-lookup"><span data-stu-id="69cdf-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="69cdf-431">Als er meerdere virtuele machines te migreren, wordt de automation via PowerShell-scripts nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="69cdf-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="69cdf-432">Hier volgt een voorbeeld van een script waarmee de migratie van een virtuele machine worden geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="69cdf-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="69cdf-433">Opmerking die onderstaand script is slechts een voorbeeld en er zijn enkele veronderstellingen over de huidige VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="69cdf-434">Mogelijk moet u het script moet overeenkomen met uw specifieke scenario bijwerken.</span><span class="sxs-lookup"><span data-stu-id="69cdf-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="69cdf-435">Het uitgangspunten zijn:</span><span class="sxs-lookup"><span data-stu-id="69cdf-435">The assumptions are:</span></span>

* <span data-ttu-id="69cdf-436">Klassieke Azure-VM's die u maakt.</span><span class="sxs-lookup"><span data-stu-id="69cdf-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="69cdf-437">Uw bron OS schijven en de gegevensschijven van de bron zich in hetzelfde opslagaccount en in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="69cdf-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="69cdf-438">Als de OS-schijven en de gegevensschijven niet op dezelfde plaats, kunt u AzCopy of Azure PowerShell te kopiëren van VHD's via de storage-accounts en containers.</span><span class="sxs-lookup"><span data-stu-id="69cdf-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="69cdf-439">Raadpleeg de vorige stap: [kopie VHD met AzCopy of PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="69cdf-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="69cdf-440">Het bewerken van dit script om te voldoen aan uw scenario is een andere keuze, maar we raden via AzCopy of PowerShell nadat het is eenvoudiger en sneller.</span><span class="sxs-lookup"><span data-stu-id="69cdf-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="69cdf-441">Hieronder vindt u het automatiseringsscript.</span><span class="sxs-lookup"><span data-stu-id="69cdf-441">The automation script is provided below.</span></span> <span data-ttu-id="69cdf-442">Tekst vervangen door uw gegevens en bijwerken van het script moet overeenkomen met uw specifieke scenario.</span><span class="sxs-lookup"><span data-stu-id="69cdf-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="69cdf-443">Met het bestaande script behoudt niet de netwerkconfiguratie van de bron-VM.</span><span class="sxs-lookup"><span data-stu-id="69cdf-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="69cdf-444">U moet re-config de netwerkinstellingen op de gemigreerde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="69cdf-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="69cdf-445"><a name="optimization"></a>Optimalisatie</span><span class="sxs-lookup"><span data-stu-id="69cdf-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="69cdf-446">Uw huidige configuratie van de virtuele machine kan worden aangepast specifiek werken goed met standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="69cdf-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="69cdf-447">Bijvoorbeeld, de prestaties verbeteren door het gebruik van veel schijven in striped volumes.</span><span class="sxs-lookup"><span data-stu-id="69cdf-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="69cdf-448">Bijvoorbeeld, in plaats van 4 schijven afzonderlijk op Premium-opslag, kunt u mogelijk de kosten optimaliseren door één schijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="69cdf-449">Optimalisaties zoals dit moet worden verwerkt op basis van geval tot geval en aangepaste stappen moeten worden uitgevoerd na de migratie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="69cdf-450">Merk ook op dit proces werkt niet goed voor databases en toepassingen die afhankelijk van de schijfindeling dat is gedefinieerd in de instellingen zijn.</span><span class="sxs-lookup"><span data-stu-id="69cdf-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="69cdf-451">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="69cdf-451">Preparation</span></span>
1. <span data-ttu-id="69cdf-452">De eenvoudige migratie voltooid zoals beschreven in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="69cdf-453">Optimalisaties worden uitgevoerd op de nieuwe virtuele machine na de migratie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="69cdf-454">De nieuwe schijfgrootte die nodig zijn voor de configuratie van de geoptimaliseerde definiëren.</span><span class="sxs-lookup"><span data-stu-id="69cdf-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="69cdf-455">Toewijzing van de huidige schijven/volumes in de nieuwe schijf specificaties bepalen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="69cdf-456">De stappen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="69cdf-456">Execution steps</span></span>
1. <span data-ttu-id="69cdf-457">De nieuwe schijven maken met de juiste grootte beschikbaar op de virtuele machine Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="69cdf-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="69cdf-458">Meld u aan de virtuele machine en kopieer de gegevens van het huidige volume aan de nieuwe schijf die is toegewezen aan dat volume.</span><span class="sxs-lookup"><span data-stu-id="69cdf-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="69cdf-459">Doe dit voor de huidige volumes die moeten worden toegewezen aan een nieuwe schijf.</span><span class="sxs-lookup"><span data-stu-id="69cdf-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="69cdf-460">Vervolgens wijzigt u de toepassingsinstellingen overschakelen naar de nieuwe schijven en de oude volumes loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="69cdf-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="69cdf-461">Voor het afstemmen van de toepassing voor betere prestaties van de schijf, raadpleegt u [toepassingsprestaties optimaliseren](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="69cdf-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="69cdf-462">Migraties van toepassing</span><span class="sxs-lookup"><span data-stu-id="69cdf-462">Application migrations</span></span>
<span data-ttu-id="69cdf-463">Databases en andere complexe toepassingen mogelijk speciale stappen zoals gedefinieerd door de aanbieder van de toepassing voor de migratie.</span><span class="sxs-lookup"><span data-stu-id="69cdf-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="69cdf-464">Raadpleeg de documentatie van de desbetreffende toepassing.</span><span class="sxs-lookup"><span data-stu-id="69cdf-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="69cdf-465">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="69cdf-465">E.g.</span></span> <span data-ttu-id="69cdf-466">doorgaans databases kunnen worden gemigreerd door middel van de back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="69cdf-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69cdf-467">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69cdf-467">Next steps</span></span>
<span data-ttu-id="69cdf-468">Zie de volgende bronnen voor specifieke scenario's voor het migreren van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="69cdf-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="69cdf-469">Azure virtuele Machines tussen Opslagaccounts migreren</span><span class="sxs-lookup"><span data-stu-id="69cdf-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="69cdf-470">Maken en een Windows Server-VHD uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="69cdf-470">Create and upload a Windows Server VHD to Azure.</span></span>](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="69cdf-471">Maakt en uploadt u een virtuele harde schijf met het Linux-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="69cdf-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="69cdf-472">Migreren van virtuele Machines van Amazon AWS naar Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="69cdf-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="69cdf-473">Zie ook de volgende bronnen voor meer informatie over Azure Storage en Azure Virtual Machines:</span><span class="sxs-lookup"><span data-stu-id="69cdf-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="69cdf-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="69cdf-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="69cdf-475">Virtuele Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="69cdf-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="69cdf-476">Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines</span><span class="sxs-lookup"><span data-stu-id="69cdf-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
