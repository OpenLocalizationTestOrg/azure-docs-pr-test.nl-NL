---
title: Een virtuele machine maken in de Azure portal | Microsoft Docs
description: Maak een virtuele Windows-machine in de Azure portal.
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
ms.openlocfilehash: 0981872ff819fdf49a9cc97afce3c212013ce76b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-running-windows-in-the-azure-portal"></a><span data-ttu-id="5d3b1-103">Maak een virtuele machine waarop Windows wordt uitgevoerd in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="5d3b1-103">Create a virtual machine running Windows in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d3b1-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5d3b1-104">Azure portal</span></span>](tutorial.md)
> * [<span data-ttu-id="5d3b1-105">PowerShell: Klassieke implementatie</span><span class="sxs-lookup"><span data-stu-id="5d3b1-105">PowerShell: Classic deployment</span></span>](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="5d3b1-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5d3b1-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5d3b1-107">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5d3b1-108">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5d3b1-109">Meer informatie over hoe [u deze stappen uitvoert met het implementatiemodel van Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) met behulp van de **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-109">Learn how to [perform these steps using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) using the **Azure portal**.</span></span>

<span data-ttu-id="5d3b1-110">Deze zelfstudie laat zien hoe u een Azure virtuele machine (VM) waarop Windows wordt uitgevoerd in de Azure portal maken.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-110">This tutorial shows you how to create an Azure virtual machine (VM) running Windows in the Azure portal.</span></span> <span data-ttu-id="5d3b1-111">We een installatiekopie van Windows Server gebruiken als voorbeeld, maar dat is slechts een van de vele installatiekopieën die Azure biedt.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-111">We'll use a Windows Server image as an example, but that's just one of the many images Azure offers.</span></span> <span data-ttu-id="5d3b1-112">Houd er rekening mee dat uw opties in de installatiekopie, afhankelijk van uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-112">Note that your image choices depend on your subscription.</span></span> <span data-ttu-id="5d3b1-113">Windows-bureaublad installatiekopieën kunnen bijvoorbeeld zijn beschikbaar voor MSDN-abonnees.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-113">For example, Windows desktop images may be available to MSDN subscribers.</span></span>

<span data-ttu-id="5d3b1-114">In deze sectie leest u hoe u de **Dashboard** in de Azure portal om te selecteren en vervolgens de virtuele machine te maken.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-114">This section shows you how to use the **Dashboard** in the Azure portal to select and then create the virtual machine.</span></span>

<span data-ttu-id="5d3b1-115">U kunt ook maken met virtuele machines met [uw eigen installatiekopieën](createupload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="5d3b1-115">You can also create VMs using [your own images](createupload-vhd.md).</span></span> <span data-ttu-id="5d3b1-116">Zie voor meer informatie over deze en andere methoden, [verschillende manieren voor het maken van een virtuele Windows-machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d3b1-116">To learn about this and other methods, see [Different ways to create a Windows virtual machine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<!-- 02/27/2017 Video removed as it was based on the classic portal. -->

## <span data-ttu-id="5d3b1-117"><a id="createvirtualmachine"></a>Maak de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5d3b1-117"><a id="createvirtualmachine"> </a>Create the virtual machine</span></span>
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a><span data-ttu-id="5d3b1-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d3b1-118">Next steps</span></span>
* <span data-ttu-id="5d3b1-119">Meer informatie over hoe [een virtuele machine maken met het implementatiemodel van Resource Manager](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-119">Learn how to [create a VM using the Resource Manager deployment model](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in the Azure portal.</span></span>
* <span data-ttu-id="5d3b1-120">Meld u bij de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-120">Log on to the virtual machine.</span></span> <span data-ttu-id="5d3b1-121">Zie voor instructies [Meld u aan bij een virtuele machine met Windows Server](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5d3b1-121">For instructions, see [Log on to a virtual machine running Windows Server](connect-logon.md).</span></span>
* <span data-ttu-id="5d3b1-122">Koppel een schijf voor het opslaan van gegevens.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-122">Attach a disk to store data.</span></span> <span data-ttu-id="5d3b1-123">U kunt zowel leeg schijven en schijven met gegevens koppelen.</span><span class="sxs-lookup"><span data-stu-id="5d3b1-123">You can attach both empty disks and disks that contain data.</span></span> <span data-ttu-id="5d3b1-124">Voor instructies raadpleegt u de [een gegevensschijf koppelen aan een virtuele Windows-machine gemaakt met het klassieke implementatiemodel](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5d3b1-124">For instructions, see the [Attach a data disk to a Windows virtual machine created with the classic deployment model](attach-disk.md).</span></span>
