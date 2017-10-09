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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Over H-serie en rekenintensieve A-serie VM's voor Linux
Hier is achtergrondinformatie en enkele overwegingen voor het gebruik van Hallo nieuwere Azure H-serie en eerdere A8, A9, A10 en A11 grootten, ook wel bekend als Hallo *rekenintensieve* exemplaren. Dit artikel is gericht op het gebruik van deze grootten voor virtuele Linux-machines. U kunt ook gebruiken voor [VM's van Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Zie voor basic specificaties, opslagcapaciteit en details van de schijf, [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Toegang tot toohello RDMA netwerk
U kunt clusters van RDMA-compatibele virtuele Linux-machines die worden uitgevoerd op een van de Hallo ondersteunde distributies van Linux HPC en een ondersteunde MPI-implementatie tootake voordeel van hello Azure RDMA-netwerk maken. Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) voor implementatie-opties en voorbeeld-configuratiestappen.

* **Distributies** - moet u virtuele machines van RDMA-compatibele SUSE Linux Enterprise Server (SLES) implementeren of Rogue Wave-Software (voorheen OpenLogic) op basis van CentOS HPC-afbeeldingen in hello Azure Marketplace. Hallo volgende Marketplace-installatiekopieën bieden ondersteuning voor RDMA-verbindingen:
  
    * SLES 12 SP1 voor SLES 12 HPC SP1 voor HPC (Premium)
    
    * 7.1 HPC op basis van centOS, op basis van CentOS 6.5 HPC  
 
        > [!NOTE]
        > Voor virtuele machines H-serie, wordt aangeraden een SLES 12 SP1 voor HPC-installatiekopie ofwel 7.1 HPC-installatiekopie op basis van CentOS.
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
    
    Aanvullende configuratie is nodig toorun MPI-taken op geclusterde virtuele machines. Op een cluster van virtuele machines, moet u bijvoorbeeld tooestablish vertrouwensrelatie tussen Hallo rekenknooppunten. Zie voor de gebruikelijke instellingen [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Overwegingen voor HPC Pack- en Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), van Microsoft gratis HPC-cluster en taak management-oplossing, biedt een optie voor u toouse Hallo rekenintensieve exemplaren met Linux. meest recente versies van HPC Pack Hallo ondersteuning voor verschillende Linux-distributies toorun op rekenknooppunten in Azure Virtual machines, beheerd door een Windows Server-hoofdknooppunt geïmplementeerd. HPC Pack kunt met RDMA-compatibele Linux-rekenknooppunten met Intel MPI, plannen en uitvoeren van Linux MPI-toepassingen die toegang tot het netwerk Hallo RDMA. tooget gestart, Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Aandachtspunten voor topologie netwerk
* Eth1 is op RDMA-functionaliteit Linux virtuele machines in Azure gereserveerd voor RDMA-netwerkverkeer. Wijzig de instellingen Eth1 of gegevens in het configuratiebestand Hallo toothis netwerk verwijst niet. Eth0 is gereserveerd voor reguliere Azure-netwerkverkeer.
* IP via InfiniBand (IB) wordt niet ondersteund in Azure. Alleen RDMA over IB wordt ondersteund.



## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over de beschikbaarheid en prijzen van Hallo rekenintensieve grootten [virtuele Machines prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Zie voor opslagcapaciteit en details van de schijf [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget gestart distributie en het gebruik van rekenintensieve grootten met RDMA op Linux, Zie [instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

