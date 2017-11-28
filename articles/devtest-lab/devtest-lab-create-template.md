---
title: de aangepaste installatiekopie van een Azure DevTest Labs vanaf een VHD-bestand aaaCreate | Microsoft Docs
description: Meer informatie over hoe een aangepaste installatiekopie in Azure DevTest Labs vanaf een VHD-bestand met toocreate hello Azure-portal
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="086ff-103">Een aangepaste installatiekopie van een VHD-bestand maken</span><span class="sxs-lookup"><span data-stu-id="086ff-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="086ff-104">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="086ff-104">Step-by-step instructions</span></span>

<span data-ttu-id="086ff-105">Hallo volgende stappen maakt u een aangepaste installatiekopie maken van een VHD-bestand met behulp van hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="086ff-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="086ff-106">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="086ff-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="086ff-107">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="086ff-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="086ff-108">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="086ff-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="086ff-109">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="086ff-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="086ff-110">Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="086ff-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="086ff-111">Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="086ff-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Aangepaste installatiekopie toe te voegen](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="086ff-113">Hallo-naam van de aangepaste installatiekopie Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="086ff-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="086ff-114">Deze naam wordt weergegeven in de lijst Hallo met basisinstallatiekopieën bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="086ff-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="086ff-115">Hallo-omschrijving van de aangepaste installatiekopie Hallo invoeren.</span><span class="sxs-lookup"><span data-stu-id="086ff-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="086ff-116">Deze beschrijving wordt weergegeven in de lijst van basisinstallatiekopieën Hallo bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="086ff-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="086ff-117">Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="086ff-117">Select **VHD**.</span></span>

1. <span data-ttu-id="086ff-118">Van Hallo **VHD** blade, selecteer Hallo gewenst VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="086ff-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="086ff-119">Selecteer **OK** tooclose hello **VHD** blade.</span><span class="sxs-lookup"><span data-stu-id="086ff-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="086ff-120">Selecteer **configuratie van het besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="086ff-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="086ff-121">Op Hallo **configuratie van het besturingssysteem** tabblad, selecteert u **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="086ff-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="086ff-122">Als **Windows** is geselecteerd, geeft u via Hallo selectievakje of *Sysprep* op Hallo machine is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="086ff-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="086ff-123">Selecteer **OK** tooclose hello **configuratie van het besturingssysteem** blade.</span><span class="sxs-lookup"><span data-stu-id="086ff-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="086ff-124">Selecteer **OK** toocreate Hallo aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="086ff-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="086ff-125">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="086ff-125">Related blog posts</span></span>

- [<span data-ttu-id="086ff-126">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="086ff-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="086ff-127">Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="086ff-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="086ff-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="086ff-128">Next steps</span></span>

- [<span data-ttu-id="086ff-129">Een VM tooyour lab toevoegen</span><span class="sxs-lookup"><span data-stu-id="086ff-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
