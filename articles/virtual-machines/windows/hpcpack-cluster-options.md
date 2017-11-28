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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="7f1fa-103">Opties met HPC Pack toocreate en een Windows HPC-cluster in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="7f1fa-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="7f1fa-104">In dit artikel is gericht op Opties toocreate HPC Pack clusters toorun Windows werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="7f1fa-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="7f1fa-105">Er zijn ook opties voor maken HPC Pack clusters toorun [Linux HPC-workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f1fa-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="7f1fa-106">Een HPC Pack-cluster worden uitgevoerd in Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="7f1fa-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="7f1fa-107">Azure-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-107">Azure templates</span></span>
* <span data-ttu-id="7f1fa-108">(GitHub) [HPC Pack 2016 cluster sjablonen](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="7f1fa-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="7f1fa-109">(Marketplace) [Cluster HPC Pack voor Windows werkbelasting](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="7f1fa-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="7f1fa-110">(Marketplace) [HPC Pack cluster voor Excel werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="7f1fa-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="7f1fa-111">(Quick Start) [Een HPC-cluster maken](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="7f1fa-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="7f1fa-112">(Quick Start) [Een HPC-cluster maken met de installatiekopie van de aangepaste rekenservice-knooppunt](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="7f1fa-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="7f1fa-113">Installatiekopieën van Azure VM</span><span class="sxs-lookup"><span data-stu-id="7f1fa-113">Azure VM images</span></span>
* [<span data-ttu-id="7f1fa-114">HPC Pack 2016 hoofdknooppunt op Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f1fa-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="7f1fa-115">HPC Pack 2016-rekenknooppunt op Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f1fa-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="7f1fa-116">HPC Pack 2016 hoofdknooppunt in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f1fa-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="7f1fa-117">HPC Pack 2016-rekenknooppunt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f1fa-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="7f1fa-118">HPC Pack 2012 R2-hoofdknooppunt dat wordt gebruikt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f1fa-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="7f1fa-119">HPC Pack 2012 R2-rekenknooppunt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f1fa-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="7f1fa-120">HPC Pack rekenknooppunt in Excel op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7f1fa-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="7f1fa-121">PowerShell-script voor implementatie</span><span class="sxs-lookup"><span data-stu-id="7f1fa-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="7f1fa-122">Een HPC-cluster met Hallo HPC Pack IaaS-implementatiescript maken</span><span class="sxs-lookup"><span data-stu-id="7f1fa-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="7f1fa-123">Zelfstudies</span><span class="sxs-lookup"><span data-stu-id="7f1fa-123">Tutorials</span></span>
* [<span data-ttu-id="7f1fa-124">Zelfstudie: Een cluster HPC Pack 2016 in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="7f1fa-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7f1fa-125">Zelfstudie: Aan de slag met een cluster HPC Pack in Azure toorun Excel- en SOA-werkbelastingen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="7f1fa-126">Handmatige implementatie Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7f1fa-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="7f1fa-127">Hallo hoofdknooppunt van een cluster HPC Pack in een Azure VM instellen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="7f1fa-128">Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="7f1fa-128">Cluster management</span></span>
* [<span data-ttu-id="7f1fa-129">Rekenknooppunten in een cluster HPC Pack in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="7f1fa-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f1fa-130">Vergroten of verkleinen van Azure-rekenresources in een cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="7f1fa-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f1fa-131">Verzenden van taken tooan HPC Pack cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="7f1fa-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7f1fa-132">Beheer van de taak in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="7f1fa-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="7f1fa-133">Een HPC Pack cluster in Azure met Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="7f1fa-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="7f1fa-134">Worker-rol knooppunten tooan HPC Pack cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="7f1fa-135">Burst tooAzure werkrolinstanties HPC Pack</span><span class="sxs-lookup"><span data-stu-id="7f1fa-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="7f1fa-136">Zelfstudie: Een cluster hybride HPC Pack in Azure instellen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="7f1fa-137">Azure 'burst' knooppunten tooan HPC Pack hoofdknooppunt toevoegen in Azure</span><span class="sxs-lookup"><span data-stu-id="7f1fa-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="7f1fa-138">Integreren met Azure Batch</span><span class="sxs-lookup"><span data-stu-id="7f1fa-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="7f1fa-139">Burst tooAzure Batch met HPC Pack</span><span class="sxs-lookup"><span data-stu-id="7f1fa-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="7f1fa-140">RDMA-clusters voor MPI-belastingen maken</span><span class="sxs-lookup"><span data-stu-id="7f1fa-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="7f1fa-141">Instellen van een cluster met Windows RDMA met HPC Pack toorun MPI-toepassingen</span><span class="sxs-lookup"><span data-stu-id="7f1fa-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

