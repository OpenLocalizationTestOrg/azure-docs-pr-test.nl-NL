---
title: aaaAzure-grootten voor virtuele machine van Windows - HPC | Microsoft Docs
description: Geeft een lijst Hallo verschillende grootten beschikbaar voor Windows high performance computing-virtuele machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="6d341-103">Hoge prestaties compute-VM-grootten</span><span class="sxs-lookup"><span data-stu-id="6d341-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="6d341-104">RDMA-compatibele exemplaren</span><span class="sxs-lookup"><span data-stu-id="6d341-104">RDMA-capable instances</span></span>
<span data-ttu-id="6d341-105">Een netwerkinterface voor remote direct memory access (RDMA) connectiviteit zijn uitgerust met een subset van Hallo rekenintensieve exemplaren (H16mr H16r A8 en A9).</span><span class="sxs-lookup"><span data-stu-id="6d341-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="6d341-106">Deze interface is bovendien toohello standaard Azure-netwerk interface beschikbaar tooother VM-grootten.</span><span class="sxs-lookup"><span data-stu-id="6d341-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="6d341-107">Deze interface kunt Hallo RDMA-compatibele exemplaren toocommunicate via een InfiniBand-netwerk op FDR tarieven voor H16r en H16mr virtuele machines en QDR tarieven voor A8 en A9 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6d341-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="6d341-108">Deze RDMA-mogelijkheden kunnen verhogen Hallo schaalbaarheid en prestaties van Message Passing Interface (MPI)-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="6d341-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="6d341-109">Zijn de vereisten voor tooaccess RDMA-compatibele VM's van Windows hello Azure RDMA netwerk:</span><span class="sxs-lookup"><span data-stu-id="6d341-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="6d341-110">**Besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="6d341-110">**Operating system**</span></span>
  
  <span data-ttu-id="6d341-111">Windows Server 2012 R2, WindowsServer 2012</span><span class="sxs-lookup"><span data-stu-id="6d341-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6d341-112">Windows Server 2016 biedt momenteel geen ondersteuning voor RDMA-connectiviteit in Azure.</span><span class="sxs-lookup"><span data-stu-id="6d341-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="6d341-113">**Beschikbaarheidsset of cloudservice** – implementeren Hallo RDMA-compatibele virtuele machines in dezelfde beschikbaarheidsset (bij gebruik van hello Azure Resource Manager-implementatiemodel) Hallo of dezelfde cloudservice Hallo (wanneer u het klassieke implementatiemodel hello gebruiken).</span><span class="sxs-lookup"><span data-stu-id="6d341-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="6d341-114">Als u Azure Batch gebruikt, Hallo RDMA-compatibele virtuele machines moet zich in Hallo dezelfde groep.</span><span class="sxs-lookup"><span data-stu-id="6d341-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="6d341-115">**MPI** -Microsoft MPI (MS-MPI) 2012 R2 of hoger, Intel MPI-bibliotheek 5.x</span><span class="sxs-lookup"><span data-stu-id="6d341-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="6d341-116">Ondersteunde MPI-implementaties gebruikt Hallo Microsoft Network Direct interface toocommunicate tussen exemplaren.</span><span class="sxs-lookup"><span data-stu-id="6d341-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="6d341-117">**RDMA netwerkadresruimte** -Hallo adresruimte 172.16.0.0/16 Hallo RDMA netwerk in Azure zijn gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="6d341-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="6d341-118">toorun MPI-toepassingen op instanties zijn geïmplementeerd in een Azure-netwerk, zorg ervoor dat adresruimte voor Hallo virtuele netwerk niet Hallo RDMA netwerk overlapt.</span><span class="sxs-lookup"><span data-stu-id="6d341-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="6d341-119">**HpcVmDrivers VM-extensie** -op RDMA-compatibele virtuele machines, moet u Hallo HpcVmDrivers extensie tooinstall Windows netwerk apparaatstuurprogramma's voor connectiviteit RDMA toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6d341-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="6d341-120">(In bepaalde implementaties van A8 en A9 exemplaren Hallo HpcVmDrivers uitbreiding wordt automatisch toegevoegd.) tooadd hello VM-extensie tooa VM, kunt u [Azure PowerShell](/powershell/azure/overview) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="6d341-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="6d341-121">Hallo van de volgende opdracht installeert de meest recente versie 1.1 HpcVMDrivers-extensie op een bestaande RDMA-compatibele virtuele machine met de naam Hallo *myVM* geïmplementeerd in Hallo resourcegroep met de naam *myResourceGroup* in Hallo  *VS-West* regio:</span><span class="sxs-lookup"><span data-stu-id="6d341-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="6d341-122">Zie voor meer informatie [uitbreidingen van de virtuele machine en functies](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d341-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6d341-123">U kunt ook werken met uitbreidingen voor virtuele machines die zijn geïmplementeerd in Hallo [klassieke implementatiemodel](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="6d341-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="6d341-124">Met behulp van HPC Pack</span><span class="sxs-lookup"><span data-stu-id="6d341-124">Using HPC Pack</span></span>

<span data-ttu-id="6d341-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak beheeroplossing, is een optie voor toocreate een compute cluster in Azure toorun MPI op basis van Windows-toepassingen en andere HPC-workloads.</span><span class="sxs-lookup"><span data-stu-id="6d341-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="6d341-126">HPC Pack 2012 R2 en hoger, bevatten een runtime-omgeving voor MS-MPI die gebruikmaakt van hello Azure RDMA netwerk wanneer geïmplementeerd op RDMA-compatibele virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="6d341-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="6d341-127">Andere grootten</span><span class="sxs-lookup"><span data-stu-id="6d341-127">Other sizes</span></span>
- [<span data-ttu-id="6d341-128">Algemeen doel</span><span class="sxs-lookup"><span data-stu-id="6d341-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="6d341-129">Geoptimaliseerde rekenkracht</span><span class="sxs-lookup"><span data-stu-id="6d341-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="6d341-130">Geoptimaliseerd geheugen</span><span class="sxs-lookup"><span data-stu-id="6d341-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="6d341-131">Geoptimaliseerde opslag</span><span class="sxs-lookup"><span data-stu-id="6d341-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="6d341-132">Geoptimaliseerde GPU</span><span class="sxs-lookup"><span data-stu-id="6d341-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="6d341-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d341-133">Next steps</span></span>

- <span data-ttu-id="6d341-134">Zie voor controlelijsten toouse Hallo rekenintensieve exemplaren met HPC Pack op Windows Server [instellen van een cluster met Windows RDMA met HPC Pack toorun MPI-toepassingen](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d341-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="6d341-135">Zie toouse rekenintensieve exemplaren bij het uitvoeren van MPI-toepassingen met Azure Batch [gebruik meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="6d341-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="6d341-136">Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.</span><span class="sxs-lookup"><span data-stu-id="6d341-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




