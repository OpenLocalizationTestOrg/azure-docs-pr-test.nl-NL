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
# <a name="high-performance-compute-vm-sizes"></a>Hoge prestaties compute-VM-grootten

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>RDMA-compatibele exemplaren
Een netwerkinterface voor remote direct memory access (RDMA) connectiviteit zijn uitgerust met een subset van Hallo rekenintensieve exemplaren (H16mr H16r A8 en A9). Deze interface is bovendien toohello standaard Azure-netwerk interface beschikbaar tooother VM-grootten. 
  
Deze interface kunt Hallo RDMA-compatibele exemplaren toocommunicate via een InfiniBand-netwerk op FDR tarieven voor H16r en H16mr virtuele machines en QDR tarieven voor A8 en A9 virtuele machines. Deze RDMA-mogelijkheden kunnen verhogen Hallo schaalbaarheid en prestaties van Message Passing Interface (MPI)-toepassingen.

Zijn de vereisten voor tooaccess RDMA-compatibele VM's van Windows hello Azure RDMA netwerk: 

* **Besturingssysteem**
  
  Windows Server 2012 R2, WindowsServer 2012
  
  > [!NOTE]
  > Windows Server 2016 biedt momenteel geen ondersteuning voor RDMA-connectiviteit in Azure.
  >

* **Beschikbaarheidsset of cloudservice** – implementeren Hallo RDMA-compatibele virtuele machines in dezelfde beschikbaarheidsset (bij gebruik van hello Azure Resource Manager-implementatiemodel) Hallo of dezelfde cloudservice Hallo (wanneer u het klassieke implementatiemodel hello gebruiken). Als u Azure Batch gebruikt, Hallo RDMA-compatibele virtuele machines moet zich in Hallo dezelfde groep.

* **MPI** -Microsoft MPI (MS-MPI) 2012 R2 of hoger, Intel MPI-bibliotheek 5.x

  Ondersteunde MPI-implementaties gebruikt Hallo Microsoft Network Direct interface toocommunicate tussen exemplaren. 

* **RDMA netwerkadresruimte** -Hallo adresruimte 172.16.0.0/16 Hallo RDMA netwerk in Azure zijn gereserveerd. toorun MPI-toepassingen op instanties zijn geïmplementeerd in een Azure-netwerk, zorg ervoor dat adresruimte voor Hallo virtuele netwerk niet Hallo RDMA netwerk overlapt.

* **HpcVmDrivers VM-extensie** -op RDMA-compatibele virtuele machines, moet u Hallo HpcVmDrivers extensie tooinstall Windows netwerk apparaatstuurprogramma's voor connectiviteit RDMA toevoegen. (In bepaalde implementaties van A8 en A9 exemplaren Hallo HpcVmDrivers uitbreiding wordt automatisch toegevoegd.) tooadd hello VM-extensie tooa VM, kunt u [Azure PowerShell](/powershell/azure/overview) cmdlets. 

  
  Hallo van de volgende opdracht installeert de meest recente versie 1.1 HpcVMDrivers-extensie op een bestaande RDMA-compatibele virtuele machine met de naam Hallo *myVM* geïmplementeerd in Hallo resourcegroep met de naam *myResourceGroup* in Hallo  *VS-West* regio:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Zie voor meer informatie [uitbreidingen van de virtuele machine en functies](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). U kunt ook werken met uitbreidingen voor virtuele machines die zijn geïmplementeerd in Hallo [klassieke implementatiemodel](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Met behulp van HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak beheeroplossing, is een optie voor toocreate een compute cluster in Azure toorun MPI op basis van Windows-toepassingen en andere HPC-workloads. HPC Pack 2012 R2 en hoger, bevatten een runtime-omgeving voor MS-MPI die gebruikmaakt van hello Azure RDMA netwerk wanneer geïmplementeerd op RDMA-compatibele virtuele machines.




## <a name="other-sizes"></a>Andere grootten
- [Algemeen doel](sizes-general.md)
- [Geoptimaliseerde rekenkracht](sizes-compute.md)
- [Geoptimaliseerd geheugen](../virtual-machines-windows-sizes-memory.md)
- [Geoptimaliseerde opslag](../virtual-machines-windows-sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)

## <a name="next-steps"></a>Volgende stappen

- Zie voor controlelijsten toouse Hallo rekenintensieve exemplaren met HPC Pack op Windows Server [instellen van een cluster met Windows RDMA met HPC Pack toorun MPI-toepassingen](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- Zie toouse rekenintensieve exemplaren bij het uitvoeren van MPI-toepassingen met Azure Batch [gebruik meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).

- Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.




