---
title: aaaUsing beheerd schijven met Azure Virtual Machine-Schaalsets | Microsoft Docs
description: Meer informatie over waarom en hoe toouse beheerd schijven met virtuele-machineschaalsets
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="defc4-103">Virtuele-machineschaalsets in Azure en beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="defc4-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="defc4-104">[Virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) in Azure ondersteunen virtuele machines met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="defc4-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="defc4-105">Het gebruik van beheerde schijven met schaalsets heeft een aantal voordelen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="defc4-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="defc4-106">U hoeft niet meer toopre-maken en beheren van accounts toostore Hallo OS opslagschijven voor Hallo virtuele machines schaalset.</span><span class="sxs-lookup"><span data-stu-id="defc4-106">You no longer need toopre-create and manage storage accounts toostore hello OS disks for hello scale set VMs.</span></span>

* <span data-ttu-id="defc4-107">U kunt beheerde gegevens schijven toohello scale set toevoegen.</span><span class="sxs-lookup"><span data-stu-id="defc4-107">You can attach managed data disks toohello scale set.</span></span>

* <span data-ttu-id="defc4-108">Met een beheerde schijf kan een schaalset een capaciteit van wel 1000 virtuele machines hebben als deze is gebaseerd op een platforminstallatiekopie, of 100 virtuele machines als deze is gebaseerd op een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="defc4-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="defc4-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="defc4-109">Get started</span></span>

<span data-ttu-id="defc4-110">Een eenvoudige manier tooget gestart met beheerde schijf-schaalsets is toodeploy van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="defc4-110">A simple way tooget started with managed disk scale sets is toodeploy one from hello Azure portal.</span></span> <span data-ttu-id="defc4-111">Raadpleeg [dit artikel](./virtual-machine-scale-sets-portal-create.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="defc4-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="defc4-112">Een andere eenvoudige manier tooget gestart is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy een schaalset.</span><span class="sxs-lookup"><span data-stu-id="defc4-112">Another simple way tooget started is toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy a scale set.</span></span> <span data-ttu-id="defc4-113">Hallo volgende voorbeeld ziet u hoe scale 10 virtuele machines, elk met een gegevensschijf van 50- en 100 GB in te stellen op basis van een Ubuntu toocreate:</span><span class="sxs-lookup"><span data-stu-id="defc4-113">hello following example shows how toocreate an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="defc4-114">U kunt ook zoeken in Hallo [Azure Quick Start-sjablonen GitHub-repo-](https://github.com/Azure/azure-quickstart-templates) voor mappen met `vmss` toosee vooraf gemaakte voorbeelden van sjablonen die schaalsets implementeren.</span><span class="sxs-lookup"><span data-stu-id="defc4-114">Alternatively, you could look in hello [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` toosee pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="defc4-115">tootell welke sjablonen al beheerde schijven gebruikt, kunt u verwijzen te[deze lijst](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span><span class="sxs-lookup"><span data-stu-id="defc4-115">tootell which templates are already using managed disks, you can refer too[this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="defc4-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="defc4-116">Next steps</span></span>

<span data-ttu-id="defc4-117">In [dit artikel](../virtual-machines/windows/managed-disks-overview.md) vindt u meer informatie over beheerde schijven in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="defc4-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="defc4-118">toosee de wijze waarop een schaal van Resource Manager sjabloon tooprovision ingesteld met tooconvert beheerd schijven, Zie [in dit artikel](./virtual-machine-scale-sets-convert-template-to-md.md).</span><span class="sxs-lookup"><span data-stu-id="defc4-118">toosee how tooconvert a Resource Manager template tooprovision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="defc4-119">Hallo toepassen dezelfde wijzigingen toohello Resource Manager-sjablonen ook toohello REST API van Azure.</span><span class="sxs-lookup"><span data-stu-id="defc4-119">hello same modifications toohello Resource Manager templates apply toohello Azure REST API as well.</span></span>

<span data-ttu-id="defc4-120">toolearn meer informatie over het gebruik van beheerde gegevensschijven met schaalsets, Zie [in dit artikel](./virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="defc4-120">toolearn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="defc4-121">werken met grote schaalsets, toobegin te verwijzen[in dit artikel](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="defc4-121">toobegin working with large scale sets, refer too[this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


