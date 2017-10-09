---
title: aaaAbout rekenintensieve virtuele machines met Linux | Microsoft Docs
description: Achtergrondinformatie en overwegingen voor het gebruik van Hallo H-serie en A8, A9, A10 en A11 rekenintensieve grootten voor virtuele Linux-machines ophalen
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="c4889-103">Over H-serie en rekenintensieve A-serie VM's voor Linux</span><span class="sxs-lookup"><span data-stu-id="c4889-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="c4889-104">Hier is achtergrondinformatie en enkele overwegingen voor het gebruik van Hallo nieuwere Azure H-serie en eerdere A8, A9, A10 en A11 grootten, ook wel bekend als Hallo *rekenintensieve* exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c4889-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="c4889-105">Dit artikel is gericht op het gebruik van deze grootten voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="c4889-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="c4889-106">U kunt ook gebruiken voor [VM's van Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c4889-107">Zie voor basic specificaties, opslagcapaciteit en details van de schijf, [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="c4889-108">Toegang tot toohello RDMA netwerk</span><span class="sxs-lookup"><span data-stu-id="c4889-108">Access toohello RDMA network</span></span>
<span data-ttu-id="c4889-109">U kunt clusters van RDMA-compatibele virtuele Linux-machines die worden uitgevoerd op een van de Hallo ondersteunde distributies van Linux HPC en een ondersteunde MPI-implementatie tootake voordeel van hello Azure RDMA-netwerk maken.</span><span class="sxs-lookup"><span data-stu-id="c4889-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="c4889-110">Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) voor implementatie-opties en voorbeeld-configuratiestappen.</span><span class="sxs-lookup"><span data-stu-id="c4889-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="c4889-111">**Distributies** - moet u virtuele machines van RDMA-compatibele SUSE Linux Enterprise Server (SLES) implementeren of Rogue Wave-Software (voorheen OpenLogic) op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c4889-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="c4889-112">Hallo volgende Marketplace-installatiekopieën bieden ondersteuning voor RDMA-verbindingen:</span><span class="sxs-lookup"><span data-stu-id="c4889-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="c4889-113">SLES 12 SP1 voor SLES 12 HPC SP1 voor HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="c4889-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="c4889-114">7.1 HPC op basis van centOS, op basis van CentOS 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="c4889-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="c4889-115">Voor virtuele machines H-serie, wordt aangeraden een SLES 12 SP1 voor HPC-installatiekopie ofwel 7.1 HPC-installatiekopie op basis van CentOS.</span><span class="sxs-lookup"><span data-stu-id="c4889-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="c4889-116">Op Hallo op basis van CentOS HPC-installatiekopieën, kernel-updates zijn uitgeschakeld in Hallo **yum** configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c4889-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="c4889-117">Dit is omdat hello zijn stuurprogramma's Linux RDMA gedistribueerd als een RPM-pakket en updates voor stuurprogramma's niet werken mogelijk als Hallo kernel wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c4889-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="c4889-118">**MPI** -Intel MPI-bibliotheek 5.x</span><span class="sxs-lookup"><span data-stu-id="c4889-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="c4889-119">Afhankelijk van de Marketplace-installatiekopie Hallo u kiest, afzonderlijke licentieverlening, installatie, of de configuratie van Intel MPI kan nodig zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="c4889-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="c4889-120">**SLES 12 SP1 voor HPC-installatiekopie** -Intel MPI-pakketten worden gedistribueerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c4889-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="c4889-121">Door het uitvoeren van de volgende opdracht Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="c4889-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="c4889-122">**CentOS HPC-installatiekopieën** -Intel MPI 5.1 is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c4889-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="c4889-123">Aanvullende configuratie is nodig toorun MPI-taken op geclusterde virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="c4889-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="c4889-124">Op een cluster van virtuele machines, moet u bijvoorbeeld tooestablish vertrouwensrelatie tussen Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="c4889-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="c4889-125">Zie voor de gebruikelijke instellingen [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="c4889-126">Overwegingen voor HPC Pack- en Linux</span><span class="sxs-lookup"><span data-stu-id="c4889-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="c4889-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak management-oplossing, biedt een optie voor u toouse Hallo rekenintensieve exemplaren met Linux.</span><span class="sxs-lookup"><span data-stu-id="c4889-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="c4889-128">meest recente versies van HPC Pack Hallo ondersteuning voor verschillende Linux-distributies toorun op rekenknooppunten in Azure Virtual machines, beheerd door een Windows Server-hoofdknooppunt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c4889-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="c4889-129">HPC Pack kunt met RDMA-compatibele Linux-rekenknooppunten met Intel MPI, plannen en uitvoeren van Linux MPI-toepassingen die toegang tot het netwerk Hallo RDMA.</span><span class="sxs-lookup"><span data-stu-id="c4889-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="c4889-130">tooget gestart, Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="c4889-131">Aandachtspunten voor topologie netwerk</span><span class="sxs-lookup"><span data-stu-id="c4889-131">Network topology considerations</span></span>
* <span data-ttu-id="c4889-132">Eth1 is op RDMA-functionaliteit Linux virtuele machines in Azure gereserveerd voor RDMA-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="c4889-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="c4889-133">Wijzig de instellingen Eth1 of gegevens in het configuratiebestand Hallo toothis netwerk verwijst niet.</span><span class="sxs-lookup"><span data-stu-id="c4889-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="c4889-134">Eth0 is gereserveerd voor reguliere Azure-netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="c4889-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="c4889-135">IP via InfiniBand (IB) wordt niet ondersteund in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4889-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="c4889-136">Alleen RDMA over IB wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c4889-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c4889-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4889-137">Next steps</span></span>
* <span data-ttu-id="c4889-138">Zie voor meer informatie over de beschikbaarheid en prijzen van Hallo rekenintensieve grootten [virtuele Machines prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="c4889-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="c4889-139">Zie voor opslagcapaciteit en details van de schijf [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="c4889-140">tooget gestart distributie en het gebruik van rekenintensieve grootten met RDMA op Linux, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4889-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

