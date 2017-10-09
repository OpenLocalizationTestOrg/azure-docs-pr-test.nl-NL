---
title: aaaLinux HPC Pack cluster opties in de cloud Hallo | Microsoft Docs
description: Meer informatie over opties met Microsoft HPC Pack toocreate en beheren van een Linux-krachtige computing (HPC)-cluster in hello Azure-cloud
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>Opties met HPC Pack toocreate en beheren van een HPC-cluster in Azure voor Linux-werkbelastingen
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Dit artikel is gericht op Opties toouse HPC Pack toorun Linux werkbelastingen. Er zijn ook opties voor het werken met [Windows HPC-workloads met HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Een HPC Pack-cluster worden uitgevoerd in Azure Virtual machines
### <a name="azure-templates"></a>Azure-sjablonen
* (GitHub) [HPC Pack 2016 cluster sjablonen](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Quick Start) [Een HPC-cluster maken met Linux-rekenknooppunten](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>PowerShell-script voor implementatie
* [Maken van een Linux-HPC-cluster met Hallo HPC Pack IaaS-implementatiescript](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Zelfstudies
* [Zelfstudie: Aan de slag met Linux-rekenknooppunten in een cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Zelfstudie: NAMD met Microsoft HPC Pack wordt uitgevoerd op Linux rekenknooppunten in Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Zelfstudie: Voer OpenFOAM met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Zelfstudie: Uitvoeren STER-CCM + met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Clusterbeheer
* [Verzenden van taken tooan HPC Pack cluster in Azure](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Beheer van de taak in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>RDMA-clusters voor MPI-belastingen maken
* [Zelfstudie: Voer OpenFOAM met Microsoft HPC Pack op een Linux RDMA-cluster in Azure](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Instellen van een Linux RDMA cluster toorun MPI-toepassingen](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

