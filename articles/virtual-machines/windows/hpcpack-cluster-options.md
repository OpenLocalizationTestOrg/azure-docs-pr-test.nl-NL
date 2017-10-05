---
title: Opties voor het cluster van Windows HPC Pack in de cloud | Microsoft Docs
description: Meer informatie over opties met Microsoft HPC Pack maken en beheren van een Windows HPC-cluster (HPC) in de Azure-cloud
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
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="0d145-103">Opties voor HPC Pack maken en beheren van een Windows HPC-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="0d145-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="0d145-104">Dit artikel is gericht op de opties voor het aanmaken van HPC Pack clusters om uit te voeren Windows werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="0d145-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="0d145-105">Er zijn ook opties voor het maken van clusters HPC Pack om uit te voeren [Linux HPC-workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d145-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="0d145-106">Een HPC Pack-cluster worden uitgevoerd in Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="0d145-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="0d145-107">Azure-sjablonen</span><span class="sxs-lookup"><span data-stu-id="0d145-107">Azure templates</span></span>
* <span data-ttu-id="0d145-108">(GitHub) [HPC Pack 2016 cluster sjablonen](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="0d145-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="0d145-109">(Marketplace) [Cluster HPC Pack voor Windows werkbelasting](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="0d145-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="0d145-110">(Marketplace) [HPC Pack cluster voor Excel werkbelastingen](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="0d145-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="0d145-111">(Quick Start) [Een HPC-cluster maken](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="0d145-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="0d145-112">(Quick Start) [Een HPC-cluster maken met de installatiekopie van de aangepaste rekenservice-knooppunt](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="0d145-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="0d145-113">Installatiekopieën van Azure VM</span><span class="sxs-lookup"><span data-stu-id="0d145-113">Azure VM images</span></span>
* [<span data-ttu-id="0d145-114">HPC Pack 2016 hoofdknooppunt op Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0d145-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="0d145-115">HPC Pack 2016-rekenknooppunt op Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0d145-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="0d145-116">HPC Pack 2016 hoofdknooppunt in Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0d145-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="0d145-117">HPC Pack 2016-rekenknooppunt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0d145-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="0d145-118">HPC Pack 2012 R2-hoofdknooppunt dat wordt gebruikt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0d145-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="0d145-119">HPC Pack 2012 R2-rekenknooppunt op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0d145-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="0d145-120">HPC Pack rekenknooppunt in Excel op Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0d145-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="0d145-121">PowerShell-script voor implementatie</span><span class="sxs-lookup"><span data-stu-id="0d145-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="0d145-122">Een HPC-cluster maken met het implementatiescript HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="0d145-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="0d145-123">Zelfstudies</span><span class="sxs-lookup"><span data-stu-id="0d145-123">Tutorials</span></span>
* [<span data-ttu-id="0d145-124">Zelfstudie: Een cluster HPC Pack 2016 in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="0d145-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0d145-125">Zelfstudie: Aan de slag met een HPC Pack-cluster in Azure uitvoeren van Excel- en SOA-werkbelastingen</span><span class="sxs-lookup"><span data-stu-id="0d145-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="0d145-126">Handmatige implementatie met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0d145-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="0d145-127">Instellen van het hoofdknooppunt van een cluster HPC Pack in een Azure VM</span><span class="sxs-lookup"><span data-stu-id="0d145-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="0d145-128">Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="0d145-128">Cluster management</span></span>
* [<span data-ttu-id="0d145-129">Rekenknooppunten in een cluster HPC Pack in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="0d145-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="0d145-130">Vergroten of verkleinen van Azure-rekenresources in een cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0d145-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="0d145-131">Verzenden van taken naar een cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="0d145-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0d145-132">Beheer van de taak in HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0d145-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="0d145-133">Een HPC Pack cluster in Azure met Azure Active Directory beheren</span><span class="sxs-lookup"><span data-stu-id="0d145-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="0d145-134">Worker-rolknooppunten toevoegen aan een cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0d145-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="0d145-135">Burst naar Azure worker-exemplaren met HPC Pack</span><span class="sxs-lookup"><span data-stu-id="0d145-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="0d145-136">Zelfstudie: Een cluster hybride HPC Pack in Azure instellen</span><span class="sxs-lookup"><span data-stu-id="0d145-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="0d145-137">Azure 'burst' knooppunten toevoegen aan een HPC Pack hoofdknooppunt in Azure</span><span class="sxs-lookup"><span data-stu-id="0d145-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="0d145-138">Integreren met Azure Batch</span><span class="sxs-lookup"><span data-stu-id="0d145-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="0d145-139">Azure batch met HPC Pack burst</span><span class="sxs-lookup"><span data-stu-id="0d145-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="0d145-140">RDMA-clusters voor MPI-belastingen maken</span><span class="sxs-lookup"><span data-stu-id="0d145-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="0d145-141">Een Windows RDMA-cluster met HPC Pack instellen voor het uitvoeren van MPI-toepassingen</span><span class="sxs-lookup"><span data-stu-id="0d145-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

