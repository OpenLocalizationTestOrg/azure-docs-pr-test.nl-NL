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
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="2640c-103">Opties met HPC Pack toocreate en beheren van een HPC-cluster in Azure voor Linux-werkbelastingen</span><span class="sxs-lookup"><span data-stu-id="2640c-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="2640c-104">Dit artikel is gericht op Opties toouse HPC Pack toorun Linux werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="2640c-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="2640c-105">Er zijn ook opties voor het werken met [Windows HPC-workloads met HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2640c-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="2640c-106">Een HPC Pack-cluster worden uitgevoerd in Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="2640c-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="2640c-107">Azure-sjablonen</span><span class="sxs-lookup"><span data-stu-id="2640c-107">Azure templates</span></span>
* <span data-ttu-id="2640c-108">(GitHub) [HPC Pack 2016 cluster sjablonen](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="2640c-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="2640c-109">(Marketplace) [HPC Pack cluster voor Linux-werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="2640c-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="2640c-110">(Quick Start) [Een HPC-cluster maken met Linux-rekenknooppunten](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="2640c-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="2640c-111">PowerShell-script voor implementatie</span><span class="sxs-lookup"><span data-stu-id="2640c-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="2640c-112">Maken van een Linux-HPC-cluster met Hallo HPC Pack IaaS-implementatiescript</span><span class="sxs-lookup"><span data-stu-id="2640c-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="2640c-113">Zelfstudies</span><span class="sxs-lookup"><span data-stu-id="2640c-113">Tutorials</span></span>
* [<span data-ttu-id="2640c-114">Zelfstudie: Aan de slag met Linux-rekenknooppunten in een cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="2640c-115">Zelfstudie: NAMD met Microsoft HPC Pack wordt uitgevoerd op Linux rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="2640c-116">Zelfstudie: Voer OpenFOAM met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="2640c-117">Zelfstudie: Uitvoeren STER-CCM + met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="2640c-118">Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="2640c-118">Cluster management</span></span>
* [<span data-ttu-id="2640c-119">Verzenden van taken tooan HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2640c-120">Beheer van de taak in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2640c-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="2640c-121">RDMA-clusters voor MPI-belastingen maken</span><span class="sxs-lookup"><span data-stu-id="2640c-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="2640c-122">Zelfstudie: Voer OpenFOAM met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="2640c-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="2640c-123">Instellen van een Linux RDMA cluster toorun MPI-toepassingen</span><span class="sxs-lookup"><span data-stu-id="2640c-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

