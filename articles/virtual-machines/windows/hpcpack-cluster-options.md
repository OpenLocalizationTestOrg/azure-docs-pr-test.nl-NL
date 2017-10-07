---
title: aaaWindows HPC Pack cluster opties in de cloud Hallo | Microsoft Docs
description: Meer informatie over opties met Microsoft HPC Pack toocreate en beheren van een Windows HPC-cluster (HPC) in hello Azure-cloud
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Opties met HPC Pack toocreate en een Windows HPC-cluster in Azure beheren
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

In dit artikel is gericht op Opties toocreate HPC Pack clusters toorun Windows werkbelasting. Er zijn ook opties voor maken HPC Pack clusters toorun [Linux HPC-workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Een HPC Pack-cluster worden uitgevoerd in Azure Virtual machines
### <a name="azure-templates"></a>Azure-sjablonen
* (GitHub) [HPC Pack 2016 cluster sjablonen](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Cluster HPC Pack voor Windows werkbelasting](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [HPC Pack cluster voor Excel werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Quick Start) [Een HPC-cluster maken](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Quick Start) [Een HPC-cluster maken met de installatiekopie van de aangepaste rekenservice-knooppunt](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Installatiekopieën van Azure VM
* [HPC Pack 2016 hoofdknooppunt op Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [HPC Pack 2016-rekenknooppunt op Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [HPC Pack 2016 hoofdknooppunt in Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [HPC Pack 2016-rekenknooppunt op Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [HPC Pack 2012 R2-hoofdknooppunt dat wordt gebruikt op Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [HPC Pack 2012 R2-rekenknooppunt op Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [HPC Pack rekenknooppunt in Excel op Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>PowerShell-script voor implementatie
* [Een HPC-cluster met Hallo HPC Pack IaaS-implementatiescript maken](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Zelfstudies
* [Zelfstudie: Een cluster HPC Pack 2016 in Azure implementeren](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Zelfstudie: Aan de slag met een cluster HPC Pack in Azure toorun Excel- en SOA-werkbelastingen](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Handmatige implementatie Hello Azure-portal
* [Hallo hoofdknooppunt van een cluster HPC Pack in een Azure VM instellen](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Clusterbeheer
* [Rekenknooppunten in een cluster HPC Pack in Azure beheren](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Vergroten of verkleinen van Azure-rekenresources in een cluster HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Verzenden van taken tooan HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Beheer van de taak in HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)
* [Een HPC Pack cluster in Azure met Azure Active Directory beheren](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Worker-rol knooppunten tooan HPC Pack cluster toevoegen
* [Burst tooAzure werkrolinstanties HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Zelfstudie: Een cluster hybride HPC Pack in Azure instellen](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Azure 'burst' knooppunten tooan HPC Pack hoofdknooppunt toevoegen in Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Integreren met Azure Batch
* [Burst tooAzure Batch met HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>RDMA-clusters voor MPI-belastingen maken
* [Instellen van een cluster met Windows RDMA met HPC Pack toorun MPI-toepassingen](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

