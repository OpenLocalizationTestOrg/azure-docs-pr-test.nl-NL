---
title: een virtuele machine in Azure-portal Hallo aaaCreate | Microsoft Docs
description: Een virtuele Windows-machine maken in hello Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a><span data-ttu-id="fc9de-103">Maak een virtuele machine met Windows in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="fc9de-103">Create a virtual machine running Windows in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc9de-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="fc9de-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="fc9de-105">PowerShell: Klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="fc9de-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="fc9de-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fc9de-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fc9de-107">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fc9de-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fc9de-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc9de-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fc9de-109">Meer informatie over hoe te[u deze stappen uitvoert met behulp van Resource Manager-implementatiemodel Hallo](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) met Hallo **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="fc9de-109">Learn how too[perform these steps using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using hello **Azure portal**.</span></span>

<span data-ttu-id="fc9de-110">Deze zelfstudie leert u hoe toocreate een Azure virtuele machine (VM) met Windows in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc9de-110">This tutorial shows you how toocreate an Azure virtual machine (VM) running Windows in hello Azure portal.</span></span> <span data-ttu-id="fc9de-111">We een installatiekopie van Windows Server gebruiken als voorbeeld, maar dat is slechts een Hallo veel installatiekopieën van Azure biedt.</span><span class="sxs-lookup"><span data-stu-id="fc9de-111">We'll use a Windows Server image as an example, but that's just one of hello many images Azure offers.</span></span> <span data-ttu-id="fc9de-112">Houd er rekening mee dat uw opties in de installatiekopie, afhankelijk van uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="fc9de-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="fc9de-113">Windows-bureaublad installatiekopieën is bijvoorbeeld mogelijk beschikbaar tooMSDN abonnees.</span><span class="sxs-lookup"><span data-stu-id="fc9de-113">For example, Windows desktop images may be available tooMSDN subscribers.</span></span>

<span data-ttu-id="fc9de-114">Deze sectie leest u hoe toouse hello **Dashboard** in Azure portal tooselect Hallo en maak vervolgens Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fc9de-114">This section shows you how toouse hello **Dashboard** in hello Azure portal tooselect and then create hello virtual machine.</span></span>

<span data-ttu-id="fc9de-115">U kunt ook maken met virtuele machines met [uw eigen installatiekopieën](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="fc9de-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="fc9de-116">toolearn over deze en andere methoden, Zie [toocreate verschillende manieren een virtuele Windows-machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc9de-116">toolearn about this and other methods, see [Different ways toocreate a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <span data-ttu-id="fc9de-117"><a id="createvirtualmachine"></a>Hello virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="fc9de-117"><a id="createvirtualmachine"> </a>Create hello virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="fc9de-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fc9de-118">Next steps</span></span>
* <span data-ttu-id="fc9de-119">Meer informatie over hoe te[een virtuele machine maken met Resource Manager-implementatiemodel Hallo](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc9de-119">Learn how too[create a VM using hello Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in hello Azure portal.</span></span>
* <span data-ttu-id="fc9de-120">Meld u aan toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fc9de-120">Log on toohello virtual machine.</span></span> <span data-ttu-id="fc9de-121">Zie voor instructies [tooa virtuele machine met Windows Server aanmelden](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="fc9de-121">For instructions, see [Log on tooa virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="fc9de-122">Voeg een schijf toostore gegevens.</span><span class="sxs-lookup"><span data-stu-id="fc9de-122">Attach a disk toostore data.</span></span> <span data-ttu-id="fc9de-123">U kunt zowel leeg schijven en schijven met gegevens koppelen.</span><span class="sxs-lookup"><span data-stu-id="fc9de-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="fc9de-124">Zie voor instructies Hallo [koppelen van een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fc9de-124">For instructions, see hello [Attach a data disk tooa Windows virtual machine created with hello classic deployment model](attach-disk.md).</span></span>
