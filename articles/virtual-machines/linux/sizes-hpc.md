---
title: Azure Linux VM-groottes - HPC | Microsoft Docs
description: Hier worden de verschillende grootten beschikbaar voor Linux high performance computing-virtuele machines in Azure.
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
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="e5e77-103">Hoge prestaties compute Linux VM-grootten</span><span class="sxs-lookup"><span data-stu-id="e5e77-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="e5e77-104">RDMA-compatibele exemplaren</span><span class="sxs-lookup"><span data-stu-id="e5e77-104">RDMA-capable instances</span></span>
<span data-ttu-id="e5e77-105">Een netwerkinterface voor remote direct memory access (RDMA) connectiviteit zijn uitgerust met een subset van de exemplaren rekenintensieve (H16mr H16r A8 en A9).</span><span class="sxs-lookup"><span data-stu-id="e5e77-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="e5e77-106">Deze interface is naast de standaard Azure netwerkinterface beschikbaar voor andere VM-groottes.</span><span class="sxs-lookup"><span data-stu-id="e5e77-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="e5e77-107">Deze interface kunt de RDMA-compatibele exemplaren om te communiceren via een InfiniBand-netwerk op FDR tarieven voor H16r en H16mr virtuele machines en QDR tarieven voor A8 en A9 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e5e77-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="e5e77-108">Deze RDMA-mogelijkheden kunnen verbeteren de schaalbaarheid en prestaties van Message Passing Interface (MPI)-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e5e77-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="e5e77-109">Hier volgen de vereisten voor RDMA-compatibele Linux VM's toegang tot het netwerk van Azure RDMA:</span><span class="sxs-lookup"><span data-stu-id="e5e77-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="e5e77-110">**Distributies** -u moet virtuele machines implementeren vanuit de RDMA-compatibele SUSE Linux Enterprise Server (SLES) of Rogue Wave-Software (voorheen OpenLogic) op basis van CentOS HPC-installatiekopieën in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e5e77-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="e5e77-111">De volgende Marketplace-installatiekopieën bieden ondersteuning voor RDMA-verbindingen:</span><span class="sxs-lookup"><span data-stu-id="e5e77-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="e5e77-112">SLES 12 SP1 voor HPC of SLES 12 SP1 voor HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="e5e77-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="e5e77-113">7.3 HPC op basis van centOS, 7.1 HPC op basis van CentOS, op basis van CentOS 6,8 HPC of 6.5 HPC op basis van CentOS</span><span class="sxs-lookup"><span data-stu-id="e5e77-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="e5e77-114">Voor virtuele machines H-serie, wordt aangeraden een SLES 12 SP1 voor HPC-installatiekopie of op basis van CentOS 7.1 of hoger HPC-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e5e77-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="e5e77-115">Op de installatiekopieën op basis van CentOS HPC kernel-updates zijn uitgeschakeld in de **yum** configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="e5e77-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="e5e77-116">Dit is omdat de Linux RDMA-stuurprogramma's zijn gedistribueerd als een RPM-pakket en updates voor stuurprogramma's niet werken mogelijk als de kernel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e5e77-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="e5e77-117">**MPI** -Intel MPI-bibliotheek 5.x</span><span class="sxs-lookup"><span data-stu-id="e5e77-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="e5e77-118">Afhankelijk van de Marketplace-installatiekopie u kiest, afzonderlijke licentieverlening, installatie, of de configuratie van Intel MPI kan nodig zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="e5e77-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="e5e77-119">**SLES 12 SP1 voor HPC-installatiekopie** -Intel MPI-pakketten worden gedistribueerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e5e77-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="e5e77-120">Installeer de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="e5e77-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="e5e77-121">**CentOS HPC-installatiekopieën** -Intel MPI 5.1 is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e5e77-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="e5e77-122">MPI-taken uitvoeren op geclusterde virtuele machines is aanvullende configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="e5e77-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="e5e77-123">Op een cluster van virtuele machines moet u bijvoorbeeld een vertrouwensrelatie tussen de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="e5e77-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="e5e77-124">Zie voor de gebruikelijke instellingen [instellen van een cluster Linux RDMA MPI-toepassingen uitvoeren](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e5e77-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="e5e77-125">Aandachtspunten voor topologie netwerk</span><span class="sxs-lookup"><span data-stu-id="e5e77-125">Network topology considerations</span></span>
* <span data-ttu-id="e5e77-126">Eth1 is op RDMA-functionaliteit Linux virtuele machines in Azure gereserveerd voor RDMA-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="e5e77-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="e5e77-127">Wijzig niet alle instellingen Eth1 of gegevens in het configuratiebestand verwijzen naar dit netwerk.</span><span class="sxs-lookup"><span data-stu-id="e5e77-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="e5e77-128">Eth0 is gereserveerd voor reguliere Azure-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="e5e77-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="e5e77-129">IP via InfiniBand (IB) wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e77-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="e5e77-130">Alleen RDMA over IB wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e5e77-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="e5e77-131">Met behulp van HPC Pack</span><span class="sxs-lookup"><span data-stu-id="e5e77-131">Using HPC Pack</span></span>
<span data-ttu-id="e5e77-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak beheeroplossing, is een optie voor u de exemplaren rekenintensieve gebruiken met Linux.</span><span class="sxs-lookup"><span data-stu-id="e5e77-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="e5e77-133">De nieuwste versies van HPC Pack ondersteuning van verschillende Linux-distributies worden uitgevoerd op rekenknooppunten in Azure Virtual machines, beheerd door een Windows Server-hoofdknooppunt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e5e77-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="e5e77-134">Met RDMA-compatibele Linux-rekenknooppunten Intel MPI uitgevoerd, kunt HPC Pack plannen en uitvoeren van Linux MPI-toepassingen die toegang het netwerk RDMA tot.</span><span class="sxs-lookup"><span data-stu-id="e5e77-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="e5e77-135">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5e77-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="e5e77-136">Andere grootten</span><span class="sxs-lookup"><span data-stu-id="e5e77-136">Other sizes</span></span>
- [<span data-ttu-id="e5e77-137">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="e5e77-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="e5e77-138">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="e5e77-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="e5e77-139">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="e5e77-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="e5e77-140">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="e5e77-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="e5e77-141">GPU</span><span class="sxs-lookup"><span data-stu-id="e5e77-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="e5e77-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e5e77-142">Next steps</span></span>

- <span data-ttu-id="e5e77-143">Als u wilt implementeren en gebruiken van rekenintensieve grootten met RDMA op Linux aan de slag, Zie [instellen van een cluster Linux RDMA MPI-toepassingen uitvoeren](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5e77-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="e5e77-144">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="e5e77-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




