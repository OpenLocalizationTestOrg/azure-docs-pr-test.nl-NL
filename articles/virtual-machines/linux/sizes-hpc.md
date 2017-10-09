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
# <a name="high-performance-compute-linux-vm-sizes"></a>Hoge prestaties compute Linux VM-grootten

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>RDMA-compatibele exemplaren
Een netwerkinterface voor remote direct memory access (RDMA) connectiviteit zijn uitgerust met een subset van Hallo rekenintensieve exemplaren (H16mr H16r A8 en A9). Deze interface is bovendien toohello standaard Azure-netwerk interface beschikbaar tooother VM-grootten. 
  
Deze interface kunt Hallo RDMA-compatibele exemplaren toocommunicate via een InfiniBand-netwerk op FDR tarieven voor H16r en H16mr virtuele machines en QDR tarieven voor A8 en A9 virtuele machines. Deze RDMA-mogelijkheden kunnen verhogen Hallo schaalbaarheid en prestaties van Message Passing Interface (MPI)-toepassingen.

Zijn de vereisten voor RDMA-compatibele virtuele Linux-machines tooaccess hello Azure RDMA netwerk:
 
* **Distributies** - moet u virtuele machines van RDMA-compatibele SUSE Linux Enterprise Server (SLES) implementeren of Rogue Wave-Software (voorheen OpenLogic) op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace. Hallo volgende Marketplace-installatiekopieën bieden ondersteuning voor RDMA-verbindingen:
  
    * SLES 12 SP1 voor HPC of SLES 12 SP1 voor HPC (Premium)
    
    * 7.3 HPC op basis van centOS, 7.1 HPC op basis van CentOS, op basis van CentOS 6,8 HPC of 6.5 HPC op basis van CentOS  
 
        > [!NOTE]
        > Voor virtuele machines H-serie, wordt aangeraden een SLES 12 SP1 voor HPC-installatiekopie of op basis van CentOS 7.1 of hoger HPC-installatiekopie.
        >
        > Op Hallo op basis van CentOS HPC-installatiekopieën, kernel-updates zijn uitgeschakeld in Hallo **yum** configuratiebestand. Dit is omdat hello zijn stuurprogramma's Linux RDMA gedistribueerd als een RPM-pakket en updates voor stuurprogramma's niet werken mogelijk als Hallo kernel wordt bijgewerkt.
        > 
        > 
* **MPI** -Intel MPI-bibliotheek 5.x
  
    Afhankelijk van de Marketplace-installatiekopie Hallo u kiest, afzonderlijke licentieverlening, installatie, of de configuratie van Intel MPI kan nodig zijn als volgt: 
  
  * **SLES 12 SP1 voor HPC-installatiekopie** -Intel MPI-pakketten worden gedistribueerd op Hallo VM. Door het uitvoeren van de volgende opdracht Hallo installeren:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS HPC-installatiekopieën** -Intel MPI 5.1 is al geïnstalleerd.  
    
    Aanvullende configuratie is nodig toorun MPI-taken op geclusterde virtuele machines. Op een cluster van virtuele machines, moet u bijvoorbeeld tooestablish vertrouwensrelatie tussen Hallo rekenknooppunten. Zie voor de gebruikelijke instellingen [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Aandachtspunten voor topologie netwerk
* Eth1 is op RDMA-functionaliteit Linux virtuele machines in Azure gereserveerd voor RDMA-netwerkverkeer. Wijzig de instellingen Eth1 of gegevens in het configuratiebestand Hallo toothis netwerk verwijst niet. Eth0 is gereserveerd voor reguliere Azure-netwerkverkeer.

* IP via InfiniBand (IB) wordt niet ondersteund in Azure. Alleen RDMA over IB wordt ondersteund.

## <a name="using-hpc-pack"></a>Met behulp van HPC Pack
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak beheeroplossing, is een optie voor u toouse Hallo rekenintensieve exemplaren met Linux. meest recente versies van HPC Pack Hallo ondersteuning voor verschillende Linux-distributies toorun op rekenknooppunten in Azure Virtual machines, beheerd door een Windows Server-hoofdknooppunt geïmplementeerd. HPC Pack kunt met RDMA-compatibele Linux-rekenknooppunten met Intel MPI, plannen en uitvoeren van Linux MPI-toepassingen die toegang tot het netwerk Hallo RDMA. Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Andere grootten
- [Algemeen doel](sizes-general.md)
- [Geoptimaliseerde rekenkracht](sizes-compute.md)
- [Geoptimaliseerd geheugen](sizes-memory.md)
- [Geoptimaliseerde opslag](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Volgende stappen

- tooget gestart distributie en het gebruik van rekenintensieve grootten met RDMA op Linux, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Meer informatie over het [Azure compute-eenheden (ACU)](acu.md) kunt u de prestaties van Azure-SKU's met elkaar vergelijken.




