---
title: aaaAzure Linux VM-groottes - HPC | Microsoft Docs
description: Geeft een lijst Hallo verschillende grootten beschikbaar voor Linux high performance computing-virtuele machines in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="60fca-103">Hoge prestaties compute Linux VM-grootten</span><span class="sxs-lookup"><span data-stu-id="60fca-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="60fca-104">RDMA-compatibele exemplaren</span><span class="sxs-lookup"><span data-stu-id="60fca-104">RDMA-capable instances</span></span>
<span data-ttu-id="60fca-105">Een netwerkinterface voor remote direct memory access (RDMA) connectiviteit zijn uitgerust met een subset van Hallo rekenintensieve exemplaren (H16mr H16r A8 en A9).</span><span class="sxs-lookup"><span data-stu-id="60fca-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="60fca-106">Deze interface is bovendien toohello standaard Azure-netwerk interface beschikbaar tooother VM-grootten.</span><span class="sxs-lookup"><span data-stu-id="60fca-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="60fca-107">Deze interface kunt Hallo RDMA-compatibele exemplaren toocommunicate via een InfiniBand-netwerk op FDR tarieven voor H16r en H16mr virtuele machines en QDR tarieven voor A8 en A9 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="60fca-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="60fca-108">Deze RDMA-mogelijkheden kunnen verhogen Hallo schaalbaarheid en prestaties van Message Passing Interface (MPI)-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="60fca-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="60fca-109">Zijn de vereisten voor RDMA-compatibele virtuele Linux-machines tooaccess hello Azure RDMA netwerk:</span><span class="sxs-lookup"><span data-stu-id="60fca-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="60fca-110">**Distributies** - moet u virtuele machines van RDMA-compatibele SUSE Linux Enterprise Server (SLES) implementeren of Rogue Wave-Software (voorheen OpenLogic) op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="60fca-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="60fca-111">Hallo volgende Marketplace-installatiekopieën bieden ondersteuning voor RDMA-verbindingen:</span><span class="sxs-lookup"><span data-stu-id="60fca-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="60fca-112">SLES 12 SP1 voor HPC of SLES 12 SP1 voor HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="60fca-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="60fca-113">7.3 HPC op basis van centOS, 7.1 HPC op basis van CentOS, op basis van CentOS 6,8 HPC of 6.5 HPC op basis van CentOS</span><span class="sxs-lookup"><span data-stu-id="60fca-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="60fca-114">Voor virtuele machines H-serie, wordt aangeraden een SLES 12 SP1 voor HPC-installatiekopie of op basis van CentOS 7.1 of hoger HPC-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="60fca-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="60fca-115">Op Hallo op basis van CentOS HPC-installatiekopieën, kernel-updates zijn uitgeschakeld in Hallo **yum** configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="60fca-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="60fca-116">Dit is omdat hello zijn stuurprogramma's Linux RDMA gedistribueerd als een RPM-pakket en updates voor stuurprogramma's niet werken mogelijk als Hallo kernel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="60fca-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="60fca-117">**MPI** -Intel MPI-bibliotheek 5.x</span><span class="sxs-lookup"><span data-stu-id="60fca-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="60fca-118">Afhankelijk van de Marketplace-installatiekopie Hallo u kiest, afzonderlijke licentieverlening, installatie, of de configuratie van Intel MPI kan nodig zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="60fca-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="60fca-119">**SLES 12 SP1 voor HPC-installatiekopie** -Intel MPI-pakketten worden gedistribueerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="60fca-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="60fca-120">Door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="60fca-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="60fca-121">**CentOS HPC-installatiekopieën** -Intel MPI 5.1 is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="60fca-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="60fca-122">Aanvullende configuratie is nodig toorun MPI-taken op geclusterde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="60fca-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="60fca-123">Op een cluster van virtuele machines, moet u bijvoorbeeld tooestablish vertrouwensrelatie tussen Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="60fca-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="60fca-124">Zie voor de gebruikelijke instellingen [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="60fca-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="60fca-125">Aandachtspunten voor topologie netwerk</span><span class="sxs-lookup"><span data-stu-id="60fca-125">Network topology considerations</span></span>
* <span data-ttu-id="60fca-126">Eth1 is op RDMA-functionaliteit Linux virtuele machines in Azure gereserveerd voor RDMA-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="60fca-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="60fca-127">Wijzig de instellingen Eth1 of gegevens in het configuratiebestand Hallo toothis netwerk verwijst niet.</span><span class="sxs-lookup"><span data-stu-id="60fca-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="60fca-128">Eth0 is gereserveerd voor reguliere Azure-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="60fca-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="60fca-129">IP via InfiniBand (IB) wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="60fca-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="60fca-130">Alleen RDMA over IB wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="60fca-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="60fca-131">Met behulp van HPC Pack</span><span class="sxs-lookup"><span data-stu-id="60fca-131">Using HPC Pack</span></span>
<span data-ttu-id="60fca-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak beheeroplossing, is een optie voor u toouse Hallo rekenintensieve exemplaren met Linux.</span><span class="sxs-lookup"><span data-stu-id="60fca-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="60fca-133">meest recente versies van HPC Pack Hallo ondersteuning voor verschillende Linux-distributies toorun op rekenknooppunten in Azure Virtual machines, beheerd door een Windows Server-hoofdknooppunt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="60fca-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="60fca-134">HPC Pack kunt met RDMA-compatibele Linux-rekenknooppunten met Intel MPI, plannen en uitvoeren van Linux MPI-toepassingen die toegang tot het netwerk Hallo RDMA.</span><span class="sxs-lookup"><span data-stu-id="60fca-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="60fca-135">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60fca-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="60fca-136">Andere grootten</span><span class="sxs-lookup"><span data-stu-id="60fca-136">Other sizes</span></span>
- [<span data-ttu-id="60fca-137">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="60fca-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="60fca-138">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="60fca-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="60fca-139">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="60fca-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="60fca-140">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="60fca-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="60fca-141">GPU</span><span class="sxs-lookup"><span data-stu-id="60fca-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="60fca-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60fca-142">Next steps</span></span>

- <span data-ttu-id="60fca-143">tooget gestart distributie en het gebruik van rekenintensieve grootten met RDMA op Linux, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60fca-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="60fca-144">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="60fca-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




