---
title: Een Azure DevTest Labs aangepaste installatiekopie maken van een virtuele machine | Microsoft Docs
description: Meer informatie over het maken van een aangepaste installatiekopie in Azure DevTest Labs van een ingerichte virtuele machine met de Azure portal
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="15f41-103">Een aangepaste installatiekopie van een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="15f41-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="15f41-104">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="15f41-104">Step-by-step instructions</span></span>

<span data-ttu-id="15f41-105">U kunt een aangepaste installatiekopie maken van een ingerichte virtuele machine en gebruik daarna die aangepaste installatiekopie identieke virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="15f41-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="15f41-106">De volgende stappen uit te laten zien hoe u een aangepaste installatiekopie maken van een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="15f41-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="15f41-107">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="15f41-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="15f41-108">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="15f41-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="15f41-109">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="15f41-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="15f41-110">Selecteer op de labblade **mijn virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="15f41-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="15f41-111">Op de **mijn virtuele machines** blade, selecteert u de virtuele machine van waaruit u wilt maken van de aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="15f41-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="15f41-112">Selecteer op de VM-blade **maken aangepaste installatiekopie (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="15f41-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Afbeelding van aangepaste menu-item maken](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="15f41-114">Op de **afbeelding maken** blade een naam en beschrijving voor de aangepaste installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="15f41-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="15f41-115">Deze informatie wordt weergegeven in de lijst met databases wanneer u een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="15f41-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Blade voor aangepaste installatiekopie maken](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="15f41-117">Geef op of sysprep is uitgevoerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="15f41-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="15f41-118">Als de sysprep is niet uitgevoerd op de virtuele machine, moet u opgeven of u wilt dat sysprep uitgevoerd wanneer een virtuele machine wordt gemaakt van deze aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="15f41-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="15f41-119">Selecteer **OK** wanneer u klaar bent met het maken van de aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="15f41-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="15f41-120">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="15f41-120">Related blog posts</span></span>

- [<span data-ttu-id="15f41-121">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="15f41-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="15f41-122">Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15f41-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="15f41-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15f41-123">Next steps</span></span>

- [<span data-ttu-id="15f41-124">Een virtuele machine toevoegen aan uw testomgeving</span><span class="sxs-lookup"><span data-stu-id="15f41-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
