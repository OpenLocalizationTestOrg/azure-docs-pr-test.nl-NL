---
title: de aangepaste installatiekopie van een virtuele machine van een Azure DevTest Labs aaaCreate | Microsoft Docs
description: Meer informatie over hoe een aangepaste installatiekopie in Azure DevTest Labs vanuit een ingericht met VM toocreate hello Azure-portal
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="4d0b3-103">Een aangepaste installatiekopie van een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="4d0b3-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4d0b3-104">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="4d0b3-104">Step-by-step instructions</span></span>

<span data-ttu-id="4d0b3-105">U kunt een aangepaste installatiekopie van een ingerichte virtuele machine maken en daarna gebruiken die aangepaste installatiekopie toocreate identieke virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="4d0b3-106">Hallo stappen laten zien hoe toocreate een aangepaste installatiekopie van een virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="4d0b3-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="4d0b3-107">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d0b3-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4d0b3-108">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="4d0b3-109">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="4d0b3-110">Selecteer op Hallo van labblade, **mijn virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="4d0b3-111">Op Hallo **mijn virtuele machines** blade Selecteer Hallo VM waaruit de toocreate Hallo aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="4d0b3-112">Selecteer op de blade Hallo van de virtuele machine **maken aangepaste installatiekopie (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Afbeelding van aangepaste menu-item maken](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="4d0b3-114">Op Hallo **afbeelding maken** blade een naam en beschrijving voor de aangepaste installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="4d0b3-115">Deze informatie wordt weergegeven in de lijst Hallo van basissen bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Blade voor aangepaste installatiekopie maken](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="4d0b3-117">Geef op of sysprep is uitgevoerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="4d0b3-118">Als Hallo sysprep is niet uitgevoerd op Hallo VM, kunt u opgeven of u wilt dat sysprep uitgevoerd wanneer een virtuele machine vanuit deze aangepaste installatiekopie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="4d0b3-119">Selecteer **OK** wanneer klaar toocreate Hallo aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4d0b3-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4d0b3-120">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="4d0b3-120">Related blog posts</span></span>

- [<span data-ttu-id="4d0b3-121">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="4d0b3-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4d0b3-122">Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4d0b3-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4d0b3-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d0b3-123">Next steps</span></span>

- [<span data-ttu-id="4d0b3-124">Een VM tooyour lab toevoegen</span><span class="sxs-lookup"><span data-stu-id="4d0b3-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
