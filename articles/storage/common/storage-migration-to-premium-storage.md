---
title: aaaMigrating VMs tooAzure Premium-opslag | Microsoft Docs
description: Migreer uw bestaande virtuele machines tooAzure Premium-opslag. Premium-opslag biedt ondersteuning voor schijven voor hoge prestaties, lage latentie voor I/O-intensieve werkbelastingen die worden uitgevoerd op Azure Virtual Machines.
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
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="752be-104">Migreren tooAzure Premium-opslag (niet-beheerde schijven)</span><span class="sxs-lookup"><span data-stu-id="752be-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="752be-105">Dit artikel wordt beschreven hoe een virtuele machine die gebruikmaakt van niet-beheerde standaardschijven tooa VM die gebruikmaakt van toomigrate zonder begeleiding premium-schijven.</span><span class="sxs-lookup"><span data-stu-id="752be-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="752be-106">U wordt aangeraden dat u Azure beheerd schijven gebruikt voor nieuwe virtuele machines en dat u uw vorige niet-beheerde schijven toomanaged schijven converteren.</span><span class="sxs-lookup"><span data-stu-id="752be-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="752be-107">Schijven ingang Hallo onderliggende storage-accounts zodat u niet te hoeft worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="752be-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="752be-108">Zie voor meer informatie onze [schijven overzicht beheerde](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="752be-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="752be-109">Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines met I/O-intensieve werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="752be-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="752be-110">U kunt profiteren van Hallo snelheid en prestaties van deze schijven nemen door te migreren van uw toepassing VM schijven tooAzure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="752be-111">Hallo-doel van deze handleiding is toohelp nieuwe gebruikers van betere Azure Premium-opslag voorbereiden toomake een overgang van hun huidige systeem tooPremium opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="752be-112">Hallo handleiding biedt drie van de belangrijke onderdelen Hallo in dit proces:</span><span class="sxs-lookup"><span data-stu-id="752be-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="752be-113">Hallo migratie tooPremium opslag plannen</span><span class="sxs-lookup"><span data-stu-id="752be-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="752be-114">Voorbereiden en kopieer virtuele harde schijven (VHD's) tooPremium opslag</span><span class="sxs-lookup"><span data-stu-id="752be-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="752be-115">Premium-opslag met van Azure virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="752be-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="752be-116">U kunt virtuele machines migreren van andere platforms tooAzure Premium-opslag of bestaande Azure-virtuele machines migreren van standaardopslag tooPremium opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="752be-117">Deze handleiding worden de stappen beschreven voor beide twee scenario's.</span><span class="sxs-lookup"><span data-stu-id="752be-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="752be-118">Hallo stappen opgegeven in de relevante sectie hello, afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="752be-119">U vindt een overzicht van functies en prijzen van Premium-opslag in Premium-opslag: [krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="752be-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="752be-120">Het is raadzaam om een hoge IOPS tooAzure Premium-opslag voor de beste prestaties voor uw toepassing hello vereisen schijf voor de virtuele machine migreren.</span><span class="sxs-lookup"><span data-stu-id="752be-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="752be-121">Als de schijf niet hoge IOPS vereist, kunt u kosten beperken door handhaven standaardopslag die schijfgegevens voor virtuele machine op de harde schijven (HDD's) in plaats van SSD's opslaat.</span><span class="sxs-lookup"><span data-stu-id="752be-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="752be-122">Voltooien van het migratieproces Hallo in zijn geheel moet mogelijk extra acties vóór en na Hallo stappen in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="752be-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="752be-123">Voorbeelden zijn virtuele netwerken of eindpunten configureren of u wijzigingen aanbrengt code vanuit Hallo toepassing zelf, waarin u mogelijk de enige downtime in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="752be-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="752be-124">Deze acties zijn unieke tooeach toepassing en u ze samen met de stappen in deze handleiding toomake Hallo volledige overgang tooPremium opslag zo weinig mogelijk Hallo moet voltooien.</span><span class="sxs-lookup"><span data-stu-id="752be-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="752be-125"><a name="plan-the-migration-to-premium-storage"></a>Hallo migratie tooPremium opslag plannen</span><span class="sxs-lookup"><span data-stu-id="752be-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="752be-126">Deze sectie zorgt ervoor dat u gereed toofollow Hallo migratiestappen in dit artikel, en u bij toomake Hallo beste beslissing op schijf en VM-typen helpt.</span><span class="sxs-lookup"><span data-stu-id="752be-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="752be-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="752be-127">Prerequisites</span></span>
* <span data-ttu-id="752be-128">U moet een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="752be-128">You will need an Azure subscription.</span></span> <span data-ttu-id="752be-129">Als u niet hebt, kunt u één maand [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/) abonnement of gaat u naar [prijzen van Azure](https://azure.microsoft.com/pricing/) voor meer opties.</span><span class="sxs-lookup"><span data-stu-id="752be-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="752be-130">tooexecute PowerShell-cmdlets, moet u Hallo Microsoft Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="752be-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="752be-131">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) installeren voor Hallo installatiepunt en de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="752be-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="752be-132">Wanneer u van plan toouse Azure VM's uitgevoerd op de Premium-opslag bent, moet u toouse Hallo Premium-opslag kunnen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="752be-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="752be-133">Standaard- en Premium-opslag-schijven kunt u met Premium-opslag kunnen virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="752be-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="752be-134">Premium-opslag-schijven zijn beschikbaar met meer VM-typen in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="752be-135">Zie voor meer informatie over alle beschikbare virtuele machine van Azure schijftypen en groottes [grootten voor virtuele machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [grootten voor Cloudservices](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="752be-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="752be-136">Overwegingen</span><span class="sxs-lookup"><span data-stu-id="752be-136">Considerations</span></span>
<span data-ttu-id="752be-137">Een virtuele machine van Azure ondersteunt meerdere schijven met Premium-opslag koppelen zodat uw toepassingen van too256 TB opslagruimte per virtuele machine kunnen hebben.</span><span class="sxs-lookup"><span data-stu-id="752be-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="752be-138">Met de Premium-opslag, kunnen uw toepassingen 80.000 IOP's (i/o-bewerkingen per seconde) per VM en 2000 MB per tweede schijfdoorvoer per virtuele machine met zeer lage latentie voor leesbewerkingen bereiken.</span><span class="sxs-lookup"><span data-stu-id="752be-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="752be-139">Hebt u opties in tal van virtuele machines en de schijven.</span><span class="sxs-lookup"><span data-stu-id="752be-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="752be-140">Deze sectie is toohelp toofind een optie die het beste past bij uw workload.</span><span class="sxs-lookup"><span data-stu-id="752be-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="752be-141">Formaten van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="752be-141">VM sizes</span></span>
<span data-ttu-id="752be-142">Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="752be-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="752be-143">Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="752be-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="752be-144">Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.</span><span class="sxs-lookup"><span data-stu-id="752be-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="752be-145">Schijfformaten</span><span class="sxs-lookup"><span data-stu-id="752be-145">Disk sizes</span></span>
<span data-ttu-id="752be-146">Er zijn vijf typen schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten.</span><span class="sxs-lookup"><span data-stu-id="752be-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="752be-147">In overweging nemen deze limieten wanneer Hallo schijftype kiezen voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="752be-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="752be-148">Premium-schijven Type</span><span class="sxs-lookup"><span data-stu-id="752be-148">Premium Disks Type</span></span>  | <span data-ttu-id="752be-149">P10</span><span class="sxs-lookup"><span data-stu-id="752be-149">P10</span></span>   | <span data-ttu-id="752be-150">P20</span><span class="sxs-lookup"><span data-stu-id="752be-150">P20</span></span>   | <span data-ttu-id="752be-151">P30</span><span class="sxs-lookup"><span data-stu-id="752be-151">P30</span></span>            | <span data-ttu-id="752be-152">P40</span><span class="sxs-lookup"><span data-stu-id="752be-152">P40</span></span>            | <span data-ttu-id="752be-153">P50</span><span class="sxs-lookup"><span data-stu-id="752be-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="752be-154">Schijfgrootte</span><span class="sxs-lookup"><span data-stu-id="752be-154">Disk size</span></span>           | <span data-ttu-id="752be-155">128 GB</span><span class="sxs-lookup"><span data-stu-id="752be-155">128 GB</span></span>| <span data-ttu-id="752be-156">512 GB</span><span class="sxs-lookup"><span data-stu-id="752be-156">512 GB</span></span>| <span data-ttu-id="752be-157">1024 GB (1 TB)</span><span class="sxs-lookup"><span data-stu-id="752be-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="752be-158">2048 GB (2 TB)</span><span class="sxs-lookup"><span data-stu-id="752be-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="752be-159">4095 GB (4 TB)</span><span class="sxs-lookup"><span data-stu-id="752be-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="752be-160">IOP's per schijf</span><span class="sxs-lookup"><span data-stu-id="752be-160">IOPS per disk</span></span>       | <span data-ttu-id="752be-161">500</span><span class="sxs-lookup"><span data-stu-id="752be-161">500</span></span>   | <span data-ttu-id="752be-162">2300</span><span class="sxs-lookup"><span data-stu-id="752be-162">2300</span></span>  | <span data-ttu-id="752be-163">5000</span><span class="sxs-lookup"><span data-stu-id="752be-163">5000</span></span>           | <span data-ttu-id="752be-164">7500</span><span class="sxs-lookup"><span data-stu-id="752be-164">7500</span></span>           | <span data-ttu-id="752be-165">7500</span><span class="sxs-lookup"><span data-stu-id="752be-165">7500</span></span>           | 
| <span data-ttu-id="752be-166">Doorvoer per schijf</span><span class="sxs-lookup"><span data-stu-id="752be-166">Throughput per disk</span></span> | <span data-ttu-id="752be-167">100 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="752be-167">100 MB per second</span></span> | <span data-ttu-id="752be-168">150 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="752be-168">150 MB per second</span></span> | <span data-ttu-id="752be-169">200 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="752be-169">200 MB per second</span></span> | <span data-ttu-id="752be-170">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="752be-170">250 MB per second</span></span> | <span data-ttu-id="752be-171">250 MB per seconde</span><span class="sxs-lookup"><span data-stu-id="752be-171">250 MB per second</span></span> |

<span data-ttu-id="752be-172">Bepalen of extra gegevensschijven nodig zijn voor uw virtuele machine zijn afhankelijk van uw workload.</span><span class="sxs-lookup"><span data-stu-id="752be-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="752be-173">U kunt verschillende permanente gegevens schijven tooyour VM koppelen.</span><span class="sxs-lookup"><span data-stu-id="752be-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="752be-174">Indien nodig, kunt u via Hallo schijven tooincrease Hallo capaciteit en prestaties van Hallo volume stripe.</span><span class="sxs-lookup"><span data-stu-id="752be-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="752be-175">(Zie Wat is er schijf Striping [hier](storage-premium-storage-performance.md#disk-striping).) Als u Premium-opslag gegevensschijven met stripe [opslagruimten][4], moet u deze configureren met één kolom voor elke schijf die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="752be-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="752be-176">Anders hello algehele prestaties van Hallo striped volume mogelijk lager is dan verwacht vanwege toouneven distributie van verkeer over Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="752be-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="752be-177">Voor Linux VM's kunt u Hallo *mdadm* hulpprogramma tooachieve Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="752be-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="752be-178">Zie het artikel [Software-RAID configureren op Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="752be-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="752be-179">Schaalbaarheidsdoelen van Storage-account</span><span class="sxs-lookup"><span data-stu-id="752be-179">Storage account scalability targets</span></span>
<span data-ttu-id="752be-180">Premium-opslagaccounts hebben Hallo na schaalbaarheidsdoelen in toevoeging toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="752be-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="752be-181">Als uw toepassingsvereisten Hallo schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt, bouwen van uw toepassing toouse meerdere opslagaccounts en partitioneren van uw gegevens over de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="752be-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="752be-182">Capaciteit van de totale Account</span><span class="sxs-lookup"><span data-stu-id="752be-182">Total Account Capacity</span></span> | <span data-ttu-id="752be-183">Totale bandbreedte voor een Account met lokaal redundante opslag</span><span class="sxs-lookup"><span data-stu-id="752be-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="752be-184">Schijf capaciteit: 35TB</span><span class="sxs-lookup"><span data-stu-id="752be-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="752be-185">Momentopname maken van capaciteit: 10 TB</span><span class="sxs-lookup"><span data-stu-id="752be-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="752be-186">Up too50 gigabits per seconde voor inkomend en uitgaand</span><span class="sxs-lookup"><span data-stu-id="752be-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="752be-187">Hallo voor meer informatie over specificaties voor Premium-opslag, Bekijk [Scalability and Performance Targets wanneer u Premium-opslag](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="752be-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="752be-188">Het beleid voor schijf</span><span class="sxs-lookup"><span data-stu-id="752be-188">Disk caching policy</span></span>
<span data-ttu-id="752be-189">Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM.</span><span class="sxs-lookup"><span data-stu-id="752be-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="752be-190">Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs.</span><span class="sxs-lookup"><span data-stu-id="752be-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="752be-191">Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken.</span><span class="sxs-lookup"><span data-stu-id="752be-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="752be-192">Hallo-cache-instellingen voor bestaande gegevensschijven kunnen worden bijgewerkt met behulp van [Azure Portal](https://portal.azure.com) of Hallo *- HostCaching* parameter Hallo *Set AzureDataDisk* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="752be-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="752be-193">Locatie</span><span class="sxs-lookup"><span data-stu-id="752be-193">Location</span></span>
<span data-ttu-id="752be-194">Kies een locatie waar Azure Premium-opslag beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="752be-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="752be-195">Zie [Azure-Services per regio](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="752be-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="752be-196">Virtuele machines zich bevinden in Hallo dezelfde regio als Hallo Storage-account dat winkels schijven Hallo voor Hallo VM u veel betere prestaties krijgt dan als ze zich in afzonderlijke regio's.</span><span class="sxs-lookup"><span data-stu-id="752be-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="752be-197">Andere Azure VM-configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="752be-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="752be-198">Wanneer u een virtuele machine in Azure maakt, zult u gevraagd tooconfigure bepaalde instellingen voor virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="752be-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="752be-199">Denk eraan dat enkele instellingen vast voor Hallo levensduur van Hallo VM, terwijl u kunt wijzigen of anderen later toevoegen.</span><span class="sxs-lookup"><span data-stu-id="752be-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="752be-200">Deze configuratie-instellingen voor virtuele machine van Azure controleren en zorg ervoor dat ze zijn geconfigureerd op de juiste wijze toomatch de vereisten van uw werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="752be-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="752be-201">Optimalisatie</span><span class="sxs-lookup"><span data-stu-id="752be-201">Optimization</span></span>
<span data-ttu-id="752be-202">[Azure Premium-opslag: Ontwerpen voor hoge prestaties](storage-premium-storage-performance.md) biedt richtlijnen voor het bouwen van krachtige toepassingen met behulp van Azure Premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="752be-203">Hallo richtlijnen gecombineerd met de prestaties van best practices van toepassing tootechnologies gebruikt door de toepassing, kunt u volgen.</span><span class="sxs-lookup"><span data-stu-id="752be-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="752be-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Voorbereiden en virtuele harde schijven (VHD's) tooPremium opslag kopiëren</span><span class="sxs-lookup"><span data-stu-id="752be-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="752be-205">Hallo volgende sectie bevat richtlijnen voor het voorbereiden van VHD's van uw virtuele machine en VHD's tooAzure Storage kopiëren.</span><span class="sxs-lookup"><span data-stu-id="752be-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="752be-206">Scenario 1: 'Ik ben migreren van bestaande virtuele machines in Azure tooAzure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="752be-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="752be-207">Scenario 2: 'Ik ben migreren VM's van andere platforms tooAzure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="752be-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="752be-208">Vereisten</span><span class="sxs-lookup"><span data-stu-id="752be-208">Prerequisites</span></span>
<span data-ttu-id="752be-209">tooprepare hello VHD's voor migratie, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="752be-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="752be-210">Een Azure-abonnement, een opslagaccount en een container in dat storage account toowhich kunt u uw VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="752be-211">Houd er rekening mee dat Hallo doelopslagaccount kan bestaan uit een Standard of Premium-opslag-account, afhankelijk van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="752be-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="752be-212">Een hulpprogramma toogeneralize hello VHD als u van plan toocreate meerdere VM-exemplaren van deze bent.</span><span class="sxs-lookup"><span data-stu-id="752be-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="752be-213">Bijvoorbeeld: sysprep voor Windows of virt-sysprep voor Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="752be-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="752be-214">Een hulpprogramma tooupload Hallo VHD-bestand toohello Storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="752be-215">Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) of gebruik een [Azure Opslagverkenner](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="752be-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="752be-216">Deze handleiding beschrijft de VHD met Hallo AzCopy hulpprogramma kopieert.</span><span class="sxs-lookup"><span data-stu-id="752be-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="752be-217">Als u ervoor de optie synchrone kopiëren met AzCopy, voor optimale prestaties kiest Kopieer uw VHD door een van deze hulpprogramma's van een Azure-virtuele machine die zich in Hallo dezelfde regio als doelopslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="752be-218">Als u een VHD van een Azure-virtuele machine in een andere regio kopieert, kan de prestaties van uw trager worden.</span><span class="sxs-lookup"><span data-stu-id="752be-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="752be-219">Voor het kopiëren een grote hoeveelheid gegevens over beperkte bandbreedte, kunt u overwegen [hello Azure Import/Export-service tootransfer gegevens tooBlob opslag met](../storage-import-export-service.md); Hiermee kunt u tootransfer uw gegevens door back-ups van harde schijf tooan Azure-schijven Datacenter.</span><span class="sxs-lookup"><span data-stu-id="752be-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="752be-220">U kunt hello Azure Import/Export-toocopy gegevens tooa standaardopslag serviceaccount alleen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="752be-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="752be-221">Nadat Hallo gegevens uw account standard-opslag is, kunt u beide Hallo [kopie Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) of AzCopy tootransfer Hallo gegevens tooyour premium storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="752be-222">Houd er rekening mee dat Microsoft Azure biedt alleen ondersteuning voor VHD-bestanden van vaste grootte.</span><span class="sxs-lookup"><span data-stu-id="752be-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="752be-223">VHDX-bestanden of dynamische virtuele harde schijven worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="752be-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="752be-224">Als u een dynamische VHD hebt, kunt u deze converteren toofixed grootte Hallo met [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="752be-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="752be-225"><a name="scenario1"></a>Scenario 1: 'Ik ben migreren van bestaande virtuele machines in Azure tooAzure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="752be-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="752be-226">Als u migreert Azure virtuele machines, stop Hallo VM, bestaande virtuele harde schijven per Hallo type VHD die u wilt voorbereiden en kopieert u Hallo VHD met AzCopy of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="752be-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="752be-227">Hallo VM moet toobe volledig omlaag toomigrate een oude toestand.</span><span class="sxs-lookup"><span data-stu-id="752be-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="752be-228">Er zijn een uitvaltijd totdat Hallo migratie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="752be-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="752be-229">Step 1.</span><span class="sxs-lookup"><span data-stu-id="752be-229">Step 1.</span></span> <span data-ttu-id="752be-230">VHD's voorbereiden voor migratie</span><span class="sxs-lookup"><span data-stu-id="752be-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="752be-231">Als u een bestaande virtuele Azure-machines tooPremium opslag migreert, is uw VHD mogelijk:</span><span class="sxs-lookup"><span data-stu-id="752be-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="752be-232">De installatiekopie van een gegeneraliseerde besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="752be-232">A generalized operating system image</span></span>
* <span data-ttu-id="752be-233">Een unieke besturingssysteemschijf</span><span class="sxs-lookup"><span data-stu-id="752be-233">A unique operating system disk</span></span>
* <span data-ttu-id="752be-234">Een gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="752be-234">A data disk</span></span>

<span data-ttu-id="752be-235">Hieronder doorlopen we deze 3 scenario's voor het voorbereiden van uw VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="752be-236">Gebruik een gegeneraliseerde besturingssysteem-VHD toocreate meerdere VM-exemplaren</span><span class="sxs-lookup"><span data-stu-id="752be-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="752be-237">Als u een VHD die gebruikt toocreate worden uploadt meerdere algemene Azure VM-instanties, moet u eerst de VHD met een hulpprogramma sysprep generalize.</span><span class="sxs-lookup"><span data-stu-id="752be-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="752be-238">Dit geldt tooa VHD on-premises of in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="752be-239">Sysprep verwijdert alle systeemspecifieke gegevens uit Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="752be-240">Een momentopname of back-up van uw VM voordat deze het generaliseren.</span><span class="sxs-lookup"><span data-stu-id="752be-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="752be-241">Sysprep uitgevoerd worden gestopt en VM-instantie Hallo ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="752be-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="752be-242">Volg de stappen hieronder toosysprep een Windows-besturingssysteem-VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="752be-243">Houd er rekening mee dat Hallo Sysprep opdracht uit te voeren u tooshut omlaag Hallo virtuele machine moet.</span><span class="sxs-lookup"><span data-stu-id="752be-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="752be-244">Zie voor meer informatie over Sysprep [Sysprep overzicht](http://technet.microsoft.com/library/hh825209.aspx) of [technische documentatie van Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="752be-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="752be-245">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="752be-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="752be-246">Voer Hallo opdracht tooopen Sysprep te volgen:</span><span class="sxs-lookup"><span data-stu-id="752be-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="752be-247">Selecteer in het hulpprogramma voor systeemvoorbereiding Hallo, selecteer System Voer Out of Box Experience (OOBE), selecteer Hallo Generalize of u het selectievakje **afsluiten**, en klik vervolgens op **OK**, zoals wordt weergegeven in onderstaande Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="752be-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="752be-248">Sysprep wordt generalize Hallo-besturingssysteem en Hallo-systeem afsluiten.</span><span class="sxs-lookup"><span data-stu-id="752be-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="752be-249">Voor een VM Ubuntu Hallo gebruik virt sysprep tooachieve dezelfde.</span><span class="sxs-lookup"><span data-stu-id="752be-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="752be-250">Zie [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="752be-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="752be-251">Zie ook een aantal van de open source Hallo [inrichten van Linux-servers software](http://www.cyberciti.biz/tips/server-provisioning-software.html) voor andere Linux-besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="752be-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="752be-252">Gebruik een unieke besturingssysteem-VHD toocreate één VM-exemplaar</span><span class="sxs-lookup"><span data-stu-id="752be-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="752be-253">Als u een toepassing die wordt uitgevoerd op Hallo VM waarvoor Hallo machine specifieke gegevens hebt, niet generalize Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="752be-254">Een VHD niet gegeneraliseerd mag gebruikte toocreate een uniek exemplaar van de virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="752be-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="752be-255">Bijvoorbeeld, als u een domeincontroller op uw VHD hebt, maakt sysprep wordt uitgevoerd het niet effectief als een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="752be-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="752be-256">Bekijk Hallo toepassingen die worden uitgevoerd op uw virtuele machine en Hallo gevolgen van het sysprep erop worden uitgevoerd voordat het generaliseren van Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="752be-257">Gegevensschijf VHD registreren</span><span class="sxs-lookup"><span data-stu-id="752be-257">Register data disk VHD</span></span>
<span data-ttu-id="752be-258">Als u gegevensschijven in Azure toobe gemigreerd, moet u ervoor dat Hallo virtuele machines die gebruikmaken van deze schijven worden afgesloten gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="752be-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="752be-259">Volg de stappen Hallo hieronder toocopy VHD tooAzure Premium-opslag en registreren als een ingerichte gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="752be-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="752be-260">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="752be-260">Step 2.</span></span> <span data-ttu-id="752be-261">Hallo-doel voor de VHD maken</span><span class="sxs-lookup"><span data-stu-id="752be-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="752be-262">Een opslagaccount voor het onderhouden van uw VHD's maken.</span><span class="sxs-lookup"><span data-stu-id="752be-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="752be-263">Hallo volgende punten bij het plannen van waar u rekening houden toostore uw VHD's:</span><span class="sxs-lookup"><span data-stu-id="752be-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="752be-264">Hallo-doel Premium storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="752be-265">Hallo opslagaccountlocatie moet hetzelfde zijn als Premium-opslag kunnen Azure virtuele machines in de laatste fase hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="752be-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="752be-266">U kan kopiëren tooa nieuw opslagaccount of plan toouse Hallo hetzelfde opslagaccount op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="752be-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="752be-267">Kopieer en sla de opslagaccountsleutel van doelopslagaccount Hallo Hallo voor de volgende fase Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="752be-268">Voor gegevensschijven, kunt u tookeep sommige gegevensschijven in een standard-opslagaccount (bijvoorbeeld schijven die koelervoorbeeld opslag), maar wij raden u alle gegevens voor productie werkbelasting toouse premium-opslag te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="752be-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="752be-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Stap 3.</span><span class="sxs-lookup"><span data-stu-id="752be-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="752be-270">Kopieer de VHD met AzCopy of PowerShell</span><span class="sxs-lookup"><span data-stu-id="752be-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="752be-271">U moet toofind uw containerpad en storage account key tooprocess een van deze twee opties.</span><span class="sxs-lookup"><span data-stu-id="752be-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="752be-272">Container pad en de opslagruimte accountsleutel vindt u in **Azure Portal** > **opslag**.</span><span class="sxs-lookup"><span data-stu-id="752be-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="752be-273">URL van de opslagcontainer Hallo worden zoals 'https://myaccount.blob.core.windows.net/mycontainer/'.</span><span class="sxs-lookup"><span data-stu-id="752be-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="752be-274">Optie 1: Kopieer geen VHD met AzCopy (asynchrone kopiëren)</span><span class="sxs-lookup"><span data-stu-id="752be-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="752be-275">AzCopy gebruikt, kunt u eenvoudig uploaden Hallo VHD via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="752be-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="752be-276">Dit kan tijd duren, afhankelijk van de grootte van de Hallo Hallo VHD's.</span><span class="sxs-lookup"><span data-stu-id="752be-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="752be-277">Houd er rekening mee toocheck Hallo inkomend en uitgaand opslagaccountlimieten wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="752be-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="752be-278">Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="752be-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="752be-279">Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="752be-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="752be-280">Open Azure PowerShell en ga toohello-map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="752be-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="752be-281">Gebruik Hallo volgende opdracht toocopy Hallo VHD-bestand van 'Bron' te 'Bestemming'.</span><span class="sxs-lookup"><span data-stu-id="752be-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="752be-282">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="752be-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="752be-283">Hier volgen beschrijvingen van Hallo parameters gebruikt in Hallo AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="752be-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="752be-284">**/ Bron:  *&lt;bron&gt;:***  locatie van het Hallo-map of URL van de opslagcontainer waarin Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="752be-285">**/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van Hallo bron storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="752be-286">**/ Dest:  *&lt;bestemming&gt;:***  opslag container URL toocopy Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="752be-287">**/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van Hallo doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="752be-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="752be-288">**/ Patroon:  *&lt;bestandsnaam&gt;:***  het Hallo-bestandsnaam opgeven van Hallo VHD toocopy.</span><span class="sxs-lookup"><span data-stu-id="752be-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="752be-289">Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="752be-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="752be-290">Optie 2: Kopieer geen VHD met PowerShell (Synchronized kopiëren)</span><span class="sxs-lookup"><span data-stu-id="752be-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="752be-291">U kunt ook Hallo VHD-bestand met Hallo PowerShell-cmdlet Start-AzureStorageBlobCopy kopiëren.</span><span class="sxs-lookup"><span data-stu-id="752be-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="752be-292">Hallo volgende opdracht op Azure PowerShell toocopy VHD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="752be-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="752be-293">Hallo-waarden in <> vervangen door een overeenkomende waarden uit de bron- en storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="752be-294">toouse dit uitvoert, moet u een zogenaamd VHD's in uw doelopslagaccount hebben.</span><span class="sxs-lookup"><span data-stu-id="752be-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="752be-295">Als het Hallo-container bestaat niet, maken voordat Hallo opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="752be-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="752be-296">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="752be-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="752be-297"><a name="scenario2"></a>Scenario 2: 'Ik ben migreren VM's van andere platforms tooAzure Premium-opslag."</span><span class="sxs-lookup"><span data-stu-id="752be-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="752be-298">Als u een VHD van niet - Azure-Cloud-opslag tooAzure migreert, moet u eerst Hallo VHD tooa lokale directory te exporteren.</span><span class="sxs-lookup"><span data-stu-id="752be-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="752be-299">Hallo voltooid bronpad van de lokale map Hallo waar VHD wordt opgeslagen bij de hand hebben en met behulp van AzCopy tooupload het tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="752be-300">Step 1.</span><span class="sxs-lookup"><span data-stu-id="752be-300">Step 1.</span></span> <span data-ttu-id="752be-301">Exporteren van VHD tooa lokale directory</span><span class="sxs-lookup"><span data-stu-id="752be-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="752be-302">Kopieer geen VHD van AWS</span><span class="sxs-lookup"><span data-stu-id="752be-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="752be-303">Als u van AWS gebruikmaakt, exporteert u Hallo EC2 exemplaar tooa VHD in een Amazon S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="752be-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="752be-304">Volg de stappen Hallo in Hallo Amazon-documentatie voor exporteren Amazon EC2 exemplaren tooinstall Hallo Amazon EC2 opdrachtregelinterface (CLI) hulpprogramma en Hallo-exemplaar-export-taak maken opdracht tooexport Hallo EC2 exemplaar tooa VHD-bestand uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="752be-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="752be-305">Ervoor toouse worden **VHD** voor Hallo schijf &#95; INSTALLATIEKOPIE &#95; INDELING variabele bij het uitvoeren van Hallo **-exemplaar-export-taak maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="752be-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="752be-306">Hallo wordt geëxporteerde VHD-bestand opgeslagen in Hallo Amazon S3-bucket die u tijdens dat proces opgeeft.</span><span class="sxs-lookup"><span data-stu-id="752be-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="752be-307">Hallo VHD-bestand downloaden van Hallo S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="752be-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="752be-308">Selecteer Hallo VHD-bestand, klikt u vervolgens **acties** > **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="752be-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="752be-309">Kopieer geen VHD van andere niet-Azure-cloud</span><span class="sxs-lookup"><span data-stu-id="752be-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="752be-310">Als u een VHD van niet - Azure-Cloud-opslag tooAzure migreert, moet u eerst Hallo VHD tooa lokale directory te exporteren.</span><span class="sxs-lookup"><span data-stu-id="752be-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="752be-311">Kopieer Hallo voltooid bronpad van de lokale map Hallo waar de VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="752be-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="752be-312">Kopieer geen VHD van on-premises</span><span class="sxs-lookup"><span data-stu-id="752be-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="752be-313">Als u een VHD van een on-premises omgeving migreert, moet u volledige bronpad Hallo waar de VHD wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="752be-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="752be-314">Hallo bronpad kan een server of bestandsshare worden.</span><span class="sxs-lookup"><span data-stu-id="752be-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="752be-315">Stap 2.</span><span class="sxs-lookup"><span data-stu-id="752be-315">Step 2.</span></span> <span data-ttu-id="752be-316">Hallo-doel voor de VHD maken</span><span class="sxs-lookup"><span data-stu-id="752be-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="752be-317">Een opslagaccount voor het onderhouden van uw VHD's maken.</span><span class="sxs-lookup"><span data-stu-id="752be-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="752be-318">Hallo volgende punten bij het plannen van waar u rekening houden toostore uw VHD's:</span><span class="sxs-lookup"><span data-stu-id="752be-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="752be-319">Hallo doel storage-account kan worden standaard of premium-opslag, afhankelijk van uw vereisten voor toepassingsimplementatie.</span><span class="sxs-lookup"><span data-stu-id="752be-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="752be-320">Hallo storage accountregio moet hetzelfde zijn als Premium-opslag kunnen Azure virtuele machines in de laatste fase hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="752be-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="752be-321">U kan kopiëren tooa nieuw opslagaccount of plan toouse Hallo hetzelfde opslagaccount op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="752be-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="752be-322">Kopieer en sla de opslagaccountsleutel van doelopslagaccount Hallo Hallo voor de volgende fase Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="752be-323">Wij raden u alle gegevens voor productie werkbelasting toouse premium-opslag te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="752be-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="752be-324">Stap 3.</span><span class="sxs-lookup"><span data-stu-id="752be-324">Step 3.</span></span> <span data-ttu-id="752be-325">Hallo VHD tooAzure opslag uploaden</span><span class="sxs-lookup"><span data-stu-id="752be-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="752be-326">Nu dat u uw VHD in de lokale directory Hallo hebt, kunt u AzCopy of AzurePowerShell tooupload Hallo .vhd-bestand tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="752be-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="752be-327">Beide opties vindt u hier:</span><span class="sxs-lookup"><span data-stu-id="752be-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="752be-328">Optie 1: Met behulp van Azure PowerShell Add-AzureVhd tooupload Hallo .vhd-bestand</span><span class="sxs-lookup"><span data-stu-id="752be-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="752be-329">Een voorbeeld <Uri> mogelijk ***'https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd'***.</span><span class="sxs-lookup"><span data-stu-id="752be-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="752be-330">Een voorbeeld <FileInfo> mogelijk ***'C:\path\to\upload.vhd'***.</span><span class="sxs-lookup"><span data-stu-id="752be-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="752be-331">Optie 2: Met behulp van AzCopy tooupload Hallo .vhd-bestand</span><span class="sxs-lookup"><span data-stu-id="752be-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="752be-332">AzCopy gebruikt, kunt u eenvoudig uploaden Hallo VHD via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="752be-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="752be-333">Dit kan tijd duren, afhankelijk van de grootte van de Hallo Hallo VHD's.</span><span class="sxs-lookup"><span data-stu-id="752be-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="752be-334">Houd er rekening mee toocheck Hallo inkomend en uitgaand opslagaccountlimieten wanneer u deze optie.</span><span class="sxs-lookup"><span data-stu-id="752be-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="752be-335">Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="752be-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="752be-336">Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="752be-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="752be-337">Open Azure PowerShell en ga toohello-map waarin AzCopy is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="752be-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="752be-338">Gebruik Hallo volgende opdracht toocopy Hallo VHD-bestand van 'Bron' te 'Bestemming'.</span><span class="sxs-lookup"><span data-stu-id="752be-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="752be-339">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="752be-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="752be-340">Hier volgen beschrijvingen van Hallo parameters gebruikt in Hallo AzCopy-opdracht:</span><span class="sxs-lookup"><span data-stu-id="752be-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="752be-341">**/ Bron:  *&lt;bron&gt;:***  locatie van het Hallo-map of URL van de opslagcontainer waarin Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="752be-342">**/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van Hallo bron storage-account.</span><span class="sxs-lookup"><span data-stu-id="752be-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="752be-343">**/ Dest:  *&lt;bestemming&gt;:***  opslag container URL toocopy Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="752be-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="752be-344">**/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van Hallo doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="752be-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="752be-345">**/ BlobType: pagina:** geeft aan dat Hallo-doel is een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="752be-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="752be-346">**/ Patroon:  *&lt;bestandsnaam&gt;:***  het Hallo-bestandsnaam opgeven van Hallo VHD toocopy.</span><span class="sxs-lookup"><span data-stu-id="752be-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="752be-347">Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="752be-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="752be-348">Andere opties voor het uploaden van een VHD</span><span class="sxs-lookup"><span data-stu-id="752be-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="752be-349">U kunt ook een VHD tooyour storage-account met behulp van een Hallo na betekent uploaden:</span><span class="sxs-lookup"><span data-stu-id="752be-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="752be-350">API voor Azure Storage kopiëren-Blob</span><span class="sxs-lookup"><span data-stu-id="752be-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="752be-351">Azure Storage Explorer uploaden van BLOB 's</span><span class="sxs-lookup"><span data-stu-id="752be-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="752be-352">Opslag voor importeren/exporteren Service REST API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="752be-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="752be-353">U kunt het beste Import/Export-Service gebruikt als de geschatte tijd uploaden is langer dan zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="752be-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="752be-354">U kunt [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate Hallo tijd van de grootte en de overdracht van gegevenseenheid.</span><span class="sxs-lookup"><span data-stu-id="752be-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="752be-355">Import/Export kan worden gebruikt toocopy tooa standard-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="752be-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="752be-356">U moet toocopy van standaardopslag toopremium storage-account met behulp van een hulpprogramma zoals AzCopy.</span><span class="sxs-lookup"><span data-stu-id="752be-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="752be-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Azure virtuele machines met Premium-opslag maken</span><span class="sxs-lookup"><span data-stu-id="752be-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="752be-358">Nadat Hallo VHD geüpload of gekopieerde toohello gewenst storage-account is, Hallo-instructies in deze sectie tooregister Hallo VHD volgen als een installatiekopie van het besturingssysteem, of de besturingssysteemschijf afhankelijk van uw scenario en maak een VM-instantie uit.</span><span class="sxs-lookup"><span data-stu-id="752be-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="752be-359">Hallo gegevensschijf VHD kan worden aangesloten toohello VM zodra deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="752be-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="752be-360">Een migratie voorbeeldscript wordt verstrekt aan Hallo einde van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="752be-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="752be-361">Dit eenvoudige script komt niet overeen met alle scenario's.</span><span class="sxs-lookup"><span data-stu-id="752be-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="752be-362">U moet mogelijk tooupdate Hallo script toomatch met uw specifieke scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="752be-363">Hieronder vindt u de toosee als dit script geldt tooyour scenario [A migratie voorbeeldscript](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="752be-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="752be-364">Controlelijst</span><span class="sxs-lookup"><span data-stu-id="752be-364">Checklist</span></span>
1. <span data-ttu-id="752be-365">Wacht totdat alle Hallo VHD schijven kopiëren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="752be-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="752be-366">Zorg ervoor dat de dat Premium-opslag is beschikbaar in Hallo-regio die u naar migreert.</span><span class="sxs-lookup"><span data-stu-id="752be-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="752be-367">Bepaal Hallo nieuwe VM-reeks die u gaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="752be-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="752be-368">Dit moet een compatibele Premium-opslag en Hallo grootte moet zijn afhankelijk van beschikbaarheid in regio Hallo Hallo en op basis van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="752be-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="752be-369">Bepaal Hallo exacte VM-grootte die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="752be-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="752be-370">VM-grootte moet toobe groot genoeg toosupport Hallo aantal gegevensschijven dat u hebt.</span><span class="sxs-lookup"><span data-stu-id="752be-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="752be-371">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="752be-371">E.g.</span></span> <span data-ttu-id="752be-372">Als u 4 gegevensschijven hebt, moet Hallo VM 2 of hoger kernen hebben.</span><span class="sxs-lookup"><span data-stu-id="752be-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="752be-373">Houd ook rekening met verwerkingskracht, geheugen en netwerkbandbreedte moet.</span><span class="sxs-lookup"><span data-stu-id="752be-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="752be-374">Hallo doelregio een Premium-opslag-account maken.</span><span class="sxs-lookup"><span data-stu-id="752be-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="752be-375">Dit is Hallo account u voor Hallo gebruiken wilt nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="752be-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="752be-376">Informatie over een Hallo huidige VM handige, inclusief Hallo-lijst van schijven en de bijbehorende VHD-blobs.</span><span class="sxs-lookup"><span data-stu-id="752be-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="752be-377">Bereid uw toepassing uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="752be-377">Prepare your application for downtime.</span></span> <span data-ttu-id="752be-378">toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="752be-379">Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform.</span><span class="sxs-lookup"><span data-stu-id="752be-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="752be-380">Duur van uitvaltijd afhankelijk Hallo hoeveelheid gegevens in Hallo schijven toomigrate.</span><span class="sxs-lookup"><span data-stu-id="752be-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="752be-381">Als u een Azure Resource Manager VM vanaf een speciale VHD schijf maakt, Raadpleeg te[deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) voor de implementatie van Resource Manager-VM met bestaande schijf.</span><span class="sxs-lookup"><span data-stu-id="752be-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="752be-382">Registreren van uw VHD</span><span class="sxs-lookup"><span data-stu-id="752be-382">Register your VHD</span></span>
<span data-ttu-id="752be-383">een virtuele machine van het besturingssysteem-VHD- of tooattach een schijf gegevens tooa toocreate nieuwe virtuele machine, moet u eerst registreren ze.</span><span class="sxs-lookup"><span data-stu-id="752be-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="752be-384">Voer onderstaande stappen, afhankelijk van uw VHD-scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="752be-385">Besturingssysteem-VHD toocreate gegeneraliseerd meerdere exemplaren van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="752be-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="752be-386">Nadat gegeneraliseerde installatiekopie van het besturingssysteem VHD is geüpload toohello storage-account, registreert u dit als een **Azure VM-installatiekopie** zodat u een of meer VM-exemplaren van deze maken kunt.</span><span class="sxs-lookup"><span data-stu-id="752be-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="752be-387">Hallo volgende PowerShell-cmdlets tooregister uw VHD als de installatiekopie van een Azure VM-OS gebruiken.</span><span class="sxs-lookup"><span data-stu-id="752be-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="752be-388">Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.</span><span class="sxs-lookup"><span data-stu-id="752be-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="752be-389">Kopieer en sla Hallo-naam van deze nieuwe Azure VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="752be-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="752be-390">In Hallo bovenstaande voorbeeld is het *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="752be-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="752be-391">Unieke besturingssysteem-VHD toocreate slechts één exemplaar van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="752be-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="752be-392">Na het Hallo unieke OS VHD geüploade toohello opslag is account, registreert u dit als een **Azure Besturingssysteemschijf** zodat u een VM-exemplaar van deze maken kunt.</span><span class="sxs-lookup"><span data-stu-id="752be-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="752be-393">Gebruik deze PowerShell-cmdlets tooregister uw VHD als een Besturingssysteemschijf Azure.</span><span class="sxs-lookup"><span data-stu-id="752be-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="752be-394">Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.</span><span class="sxs-lookup"><span data-stu-id="752be-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="752be-395">Kopieer en Hallo-naam van deze nieuwe OS-schijf van Azure worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="752be-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="752be-396">In Hallo bovenstaande voorbeeld is het *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="752be-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="752be-397">Gegevens schijf VHD toobe toonew Azure VM-exemplaren die zijn gekoppeld</span><span class="sxs-lookup"><span data-stu-id="752be-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="752be-398">Nadat hello gegevensschijf VHD is geüpload toostorage account, registreren als een Azure-gegevensschijf zodat deze aangesloten tooyour worden kan nieuwe DS-serie DSv2 reeks of GS-serie Azure VM-instantie.</span><span class="sxs-lookup"><span data-stu-id="752be-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="752be-399">Gebruik deze PowerShell-cmdlets tooregister uw VHD als een Azure-gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="752be-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="752be-400">Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.</span><span class="sxs-lookup"><span data-stu-id="752be-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="752be-401">Kopieer en Hallo-naam van deze nieuwe Azure-gegevensschijf worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="752be-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="752be-402">In Hallo bovenstaande voorbeeld is het *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="752be-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="752be-403">Maak een geschikt VM voor Premium-opslag</span><span class="sxs-lookup"><span data-stu-id="752be-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="752be-404">Eenmaal Hallo installatiekopie van het besturingssysteem of besturingssysteemschijf zijn geregistreerd, maakt u een nieuwe Active Directory-serie, DSv2-serie- of GS-serie VM.</span><span class="sxs-lookup"><span data-stu-id="752be-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="752be-405">U gaat gebruiken de besturingssysteemkopie Hallo of naam van een besturingssysteem schijf die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="752be-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="752be-406">Selecteer Hallo VM in Hallo Premium Storage-laag.</span><span class="sxs-lookup"><span data-stu-id="752be-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="752be-407">In onderstaand voorbeeld gebruiken we Hallo *Standard_DS2* VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="752be-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="752be-408">Hallo schijf grootte toomake zeker van te zijn dat deze overeenkomt met de capaciteit en prestatie-eisen en hello Azure schijfgrootten beschikbaar bijwerken.</span><span class="sxs-lookup"><span data-stu-id="752be-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="752be-409">Volg Hallo stapsgewijze PowerShell-cmdlets hieronder toocreate Hallo nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="752be-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="752be-410">Stel eerst Hallo algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="752be-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="752be-411">Maak eerst een cloudservice waarin u uw nieuwe virtuele machines worden gehost.</span><span class="sxs-lookup"><span data-stu-id="752be-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="752be-412">Maak vervolgens hello Azure VM-instantie van Hallo installatiekopie van het besturingssysteem of Besturingssysteemschijf die u hebt geregistreerd, afhankelijk van uw scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="752be-413">Besturingssysteem-VHD toocreate gegeneraliseerd meerdere exemplaren van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="752be-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="752be-414">Hallo maken een of meer nieuwe DS reeks Azure VM-instanties met Hallo **installatiekopie van het besturingssysteem Azure** die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="752be-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="752be-415">Geef de naam van deze installatiekopie van het besturingssysteem in Hallo VM-configuratie bij het maken van nieuwe virtuele machine, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="752be-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="752be-416">Unieke besturingssysteem-VHD toocreate slechts één exemplaar van de virtuele machine in Azure</span><span class="sxs-lookup"><span data-stu-id="752be-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="752be-417">Maak een nieuw Azure VM exemplaar voor DS reeks met behulp van Hallo **Besturingssysteemschijf Azure** die u hebt geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="752be-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="752be-418">Geef de naam van deze Besturingssysteemschijf Hallo VM-configuratie bij het maken van nieuwe virtuele machine Hallo zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="752be-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="752be-419">Geef andere Azure VM-informatie, zoals een cloudservice, regio, storage-account, beschikbaarheidsset en het beleid.</span><span class="sxs-lookup"><span data-stu-id="752be-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="752be-420">Houd er rekening mee dat Hallo VM-instantie geplaatst met bijbehorende besturingssysteem worden moet of gegevensschijven zodat Hallo geselecteerd cloud-service, regio en storage-account moet zich in dezelfde locatie als onderliggende VHD's van deze schijven Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="752be-421">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="752be-421">Attach data disk</span></span>
<span data-ttu-id="752be-422">Ten slotte, als u hebt geregistreerd gegevens schijf VHD's, koppelt u ze toohello nieuwe Premium-opslag kan virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="752be-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="752be-423">Gebruikt u de volgende PowerShell-cmdlet tooattach gegevens schijf toohello nieuwe virtuele machine en Hallo cachebeleid opgeven.</span><span class="sxs-lookup"><span data-stu-id="752be-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="752be-424">In het voorbeeld hieronder Hallo cachebeleid is ingesteld te*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="752be-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="752be-425">Mogelijk zijn er extra stappen nodig toosupport uw toepassing die niet worden gedekt door deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="752be-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="752be-426">Controleren en back-up plannen</span><span class="sxs-lookup"><span data-stu-id="752be-426">Checking and plan backup</span></span>
<span data-ttu-id="752be-427">Eenmaal Hallo nieuwe virtuele machine actief is en die wordt uitgevoerd, toegang met behulp van dezelfde gebruikersnaam en wachtwoord Hallo is als de oorspronkelijke VM Hallo en controleren of alles werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="752be-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="752be-428">Alle Hallo-instellingen, inclusief Hallo striped volumes, moeten aanwezig zijn in Hallo van nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="752be-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="752be-429">de laatste stap Hallo is tooplan back-up en onderhoud planning voor de nieuwe virtuele machine op basis van de behoeften van de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="752be-430"><a name="a-sample-migration-script"></a>Een voorbeeldscript voor migratie</span><span class="sxs-lookup"><span data-stu-id="752be-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="752be-431">Als u meerdere virtuele machines toomigrate hebt, wordt de automation via PowerShell-scripts nuttig zijn.</span><span class="sxs-lookup"><span data-stu-id="752be-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="752be-432">Hier volgt een voorbeeld van een script waarmee Hallo migratie van een virtuele machine worden geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="752be-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="752be-433">Opmerking die onderstaand script is slechts een voorbeeld en er zijn enkele veronderstellingen over Hallo huidige VM-schijven.</span><span class="sxs-lookup"><span data-stu-id="752be-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="752be-434">U moet mogelijk tooupdate Hallo script toomatch met uw specifieke scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="752be-435">Hallo veronderstellingen zijn:</span><span class="sxs-lookup"><span data-stu-id="752be-435">hello assumptions are:</span></span>

* <span data-ttu-id="752be-436">Klassieke Azure-VM's die u maakt.</span><span class="sxs-lookup"><span data-stu-id="752be-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="752be-437">Uw bron OS schijven en de gegevensschijven van de bron zich in hetzelfde opslagaccount en in dezelfde container.</span><span class="sxs-lookup"><span data-stu-id="752be-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="752be-438">Als de OS-schijven en de gegevensschijven zich niet op dezelfde Hallo plaatst, kunt u AzCopy of Azure PowerShell toocopy VHD's via de storage-accounts en containers.</span><span class="sxs-lookup"><span data-stu-id="752be-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="752be-439">Raadpleeg de vorige stap toohello: [kopie VHD met AzCopy of PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="752be-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="752be-440">Dit script toomeet bewerken uw scenario is een andere keuze, maar we raden via AzCopy of PowerShell nadat het is eenvoudiger en sneller.</span><span class="sxs-lookup"><span data-stu-id="752be-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="752be-441">Hieronder vindt u Hallo automatiseringsscript.</span><span class="sxs-lookup"><span data-stu-id="752be-441">hello automation script is provided below.</span></span> <span data-ttu-id="752be-442">Tekst vervangen door uw gegevens en Hallo script toomatch werk met uw specifieke scenario.</span><span class="sxs-lookup"><span data-stu-id="752be-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="752be-443">Met behulp van de bestaande script Hallo behoudt niet Hallo netwerkconfiguratie van de bron-VM.</span><span class="sxs-lookup"><span data-stu-id="752be-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="752be-444">U moet toore-config Hallo netwerkinstellingen op de gemigreerde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="752be-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="752be-445"><a name="optimization"></a>Optimalisatie</span><span class="sxs-lookup"><span data-stu-id="752be-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="752be-446">Uw huidige configuratie van de virtuele machine kan worden aangepast specifiek toowork goed met standaardschijven.</span><span class="sxs-lookup"><span data-stu-id="752be-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="752be-447">Bijvoorbeeld: tooincrease Hallo prestaties met behulp van veel schijven in striped volumes.</span><span class="sxs-lookup"><span data-stu-id="752be-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="752be-448">Bijvoorbeeld, in plaats van 4 schijven afzonderlijk op Premium-opslag, mogelijk kunnen toooptimize Hallo kosten doordat één schijf.</span><span class="sxs-lookup"><span data-stu-id="752be-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="752be-449">Optimalisaties zoals dit moet toobe verwerkt op basis van geval tot geval en aangepaste stappen na de migratie Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="752be-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="752be-450">Merk ook op dit proces werkt niet goed voor databases en toepassingen die afhankelijk van Hallo schijfindeling gedefinieerd in het Hallo-installatieprogramma zijn.</span><span class="sxs-lookup"><span data-stu-id="752be-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="752be-451">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="752be-451">Preparation</span></span>
1. <span data-ttu-id="752be-452">Volledige Hallo eenvoudige migratie, zoals beschreven in Hallo eerder gedeelte.</span><span class="sxs-lookup"><span data-stu-id="752be-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="752be-453">Optimalisaties wordt uitgevoerd op Hallo nieuwe virtuele machine na migratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="752be-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="752be-454">Definieer Hallo nieuwe schijfgrootten nodig voor de configuratie van Hallo geoptimaliseerd.</span><span class="sxs-lookup"><span data-stu-id="752be-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="752be-455">Toewijzing van Hallo huidige schijven/volumes toohello nieuwe schijf specificaties bepalen.</span><span class="sxs-lookup"><span data-stu-id="752be-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="752be-456">De stappen worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="752be-456">Execution steps</span></span>
1. <span data-ttu-id="752be-457">Hallo nieuwe schijven met de juiste Hallo grootte op Hallo VM voor Premium-opslag beschikbaar maken.</span><span class="sxs-lookup"><span data-stu-id="752be-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="752be-458">Aanmelding toohello VM en Hallo gegevens kopiëren van Hallo huidige volume toohello nieuwe schijf die is toegewezen toothat volume.</span><span class="sxs-lookup"><span data-stu-id="752be-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="752be-459">Doe dit voor alle Hallo huidige volumes die toomap tooa nieuwe schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="752be-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="752be-460">Vervolgens wijzigen Hallo toepassing instellingen tooswitch toohello nieuwe schijven en Hallo oude volumes loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="752be-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="752be-461">Voor het afstemmen Hallo-toepassing voor betere prestaties van de schijf, Raadpleeg te[toepassingsprestaties optimaliseren](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="752be-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="752be-462">Migraties van toepassing</span><span class="sxs-lookup"><span data-stu-id="752be-462">Application migrations</span></span>
<span data-ttu-id="752be-463">Databases en andere complexe toepassingen mogelijk speciale stappen zoals gedefinieerd door Hallo toepassingsprovider voor Hallo-migratie.</span><span class="sxs-lookup"><span data-stu-id="752be-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="752be-464">Raadpleeg de documentatie van de toepassing toorespective.</span><span class="sxs-lookup"><span data-stu-id="752be-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="752be-465">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="752be-465">E.g.</span></span> <span data-ttu-id="752be-466">doorgaans databases kunnen worden gemigreerd door middel van de back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="752be-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="752be-467">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="752be-467">Next steps</span></span>
<span data-ttu-id="752be-468">Zie Hallo resources voor specifieke scenario's voor het migreren van virtuele machines te volgen:</span><span class="sxs-lookup"><span data-stu-id="752be-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="752be-469">Azure virtuele Machines tussen Opslagaccounts migreren</span><span class="sxs-lookup"><span data-stu-id="752be-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="752be-470">Maken en uploaden van een Windows Server-VHD tooAzure.</span><span class="sxs-lookup"><span data-stu-id="752be-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="752be-471">Maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="752be-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="752be-472">Migreren van virtuele Machines van Amazon AWS tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="752be-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="752be-473">Zie ook Hallo resources toolearn meer informatie over Azure Storage en Azure Virtual Machines te volgen:</span><span class="sxs-lookup"><span data-stu-id="752be-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="752be-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="752be-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="752be-475">Virtuele Machines in Azure</span><span class="sxs-lookup"><span data-stu-id="752be-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="752be-476">Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines</span><span class="sxs-lookup"><span data-stu-id="752be-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
