---
title: Beheerde schijven gebruiken met Azure Virtual Machine Scale Sets | Microsoft Docs
description: Meer informatie over waarom en hoe u beheerde schijven gebruikt met virtuele-machineschaalsets
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
ms.openlocfilehash: 3ab1d432a2f90db57b99f0e7d419d85e2958c308
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a><span data-ttu-id="c19ae-103">Virtuele-machineschaalsets in Azure en beheerde schijven</span><span class="sxs-lookup"><span data-stu-id="c19ae-103">Azure VM scale sets and managed disks</span></span>

<span data-ttu-id="c19ae-104">[Virtuele-machineschaalsets](/azure/virtual-machine-scale-sets/) in Azure ondersteunen virtuele machines met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="c19ae-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) supports virtual machines with managed disks.</span></span> <span data-ttu-id="c19ae-105">Het gebruik van beheerde schijven met schaalsets heeft een aantal voordelen, waaronder:</span><span class="sxs-lookup"><span data-stu-id="c19ae-105">Using managed disks with scale sets has several benefits, including:</span></span>

* <span data-ttu-id="c19ae-106">Het is niet meer nodig om op voorhand opslagaccounts te maken en deze te beheren om de besturingssysteemschijven voor virtuele machines met schaalsets op te slaan.</span><span class="sxs-lookup"><span data-stu-id="c19ae-106">You no longer need to pre-create and manage storage accounts to store the OS disks for the scale set VMs.</span></span>

* <span data-ttu-id="c19ae-107">U kunt beheerde gegevensschijven aan de schaalset koppelen.</span><span class="sxs-lookup"><span data-stu-id="c19ae-107">You can attach managed data disks to the scale set.</span></span>

* <span data-ttu-id="c19ae-108">Met een beheerde schijf kan een schaalset een capaciteit van wel 1000 virtuele machines hebben als deze is gebaseerd op een platforminstallatiekopie, of 100 virtuele machines als deze is gebaseerd op een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="c19ae-108">With managed disk, a scale set can have capacity as high as 1,000 VMs if based on a platform image or 100 VMs if based on a custom image.</span></span>

## <a name="get-started"></a><span data-ttu-id="c19ae-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c19ae-109">Get started</span></span>

<span data-ttu-id="c19ae-110">Een eenvoudige manier om aan de slag te gaan met schaalsets met beheerde schijven, is door er een te implementeren vanuit Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c19ae-110">A simple way to get started with managed disk scale sets is to deploy one from the Azure portal.</span></span> <span data-ttu-id="c19ae-111">Raadpleeg [dit artikel](./virtual-machine-scale-sets-portal-create.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c19ae-111">For more information, see [this article](./virtual-machine-scale-sets-portal-create.md).</span></span> <span data-ttu-id="c19ae-112">Een andere eenvoudige manier om aan de slag te gaan, is door [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) te gebruiken om een schaalset te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c19ae-112">Another simple way to get started is to use [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) to deploy a scale set.</span></span> <span data-ttu-id="c19ae-113">In het volgende voorbeeld ziet u hoe een op Ubuntu gebaseerde schaalset met 10 virtuele machines wordt gemaakt, elk met een gegevensschijf van 50 GB en 100 GB:</span><span class="sxs-lookup"><span data-stu-id="c19ae-113">The following example shows how to create an Ubuntu based scale set with 10 VMs, each with a 50-GB and 100-GB data disk:</span></span>

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

<span data-ttu-id="c19ae-114">U kunt ook eens in de [GitHub-opslagplaats met snelstartsjablonen voor Azure](https://github.com/Azure/azure-quickstart-templates) naar mappen zoeken die `vmss` bevatten, om kant-en-klare voorbeelden te bekijken van sjablonen waarmee schaalsets worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c19ae-114">Alternatively, you could look in the [Azure Quickstart Templates GitHub repo](https://github.com/Azure/azure-quickstart-templates) for folders that contain `vmss` to see pre-built examples of templates that deploy scale sets.</span></span> <span data-ttu-id="c19ae-115">Raadpleeg [deze lijst](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md) als u wilt weten welke sjablonen al gebruikmaken van beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="c19ae-115">To tell which templates are already using managed disks, you can refer to [this list](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c19ae-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c19ae-116">Next steps</span></span>

<span data-ttu-id="c19ae-117">In [dit artikel](../virtual-machines/windows/managed-disks-overview.md) vindt u meer informatie over beheerde schijven in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="c19ae-117">For more information on managed disks in general, see [this article](../virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="c19ae-118">Raadpleeg [dit artikel](./virtual-machine-scale-sets-convert-template-to-md.md) als u wilt weten hoe u een Resource Manager-sjabloon omzet voor het inrichten van schaalsets met beheerde schijven.</span><span class="sxs-lookup"><span data-stu-id="c19ae-118">To see how to convert a Resource Manager template to provision scale sets with managed disks, see [this article](./virtual-machine-scale-sets-convert-template-to-md.md).</span></span> <span data-ttu-id="c19ae-119">De wijzigingen in de Resource Manager-sjablonen zijn ook van toepassing op de Azure REST API.</span><span class="sxs-lookup"><span data-stu-id="c19ae-119">The same modifications to the Resource Manager templates apply to the Azure REST API as well.</span></span>

<span data-ttu-id="c19ae-120">Raadpleeg [dit artikel](./virtual-machine-scale-sets-attached-disks.md) voor meer informatie over het gebruik van beheerde gegevensschijven met schaalsets.</span><span class="sxs-lookup"><span data-stu-id="c19ae-120">To learn more about using managed data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="c19ae-121">Raadpleeg [dit artikel](./virtual-machine-scale-sets-placement-groups.md) als u met grote schaalsets wilt gaan werken.</span><span class="sxs-lookup"><span data-stu-id="c19ae-121">To begin working with large scale sets, refer to [this article](./virtual-machine-scale-sets-placement-groups.md).</span></span>


