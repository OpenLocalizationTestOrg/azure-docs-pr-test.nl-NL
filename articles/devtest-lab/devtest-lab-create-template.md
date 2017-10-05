---
title: Een Azure DevTest Labs aangepaste installatiekopie maken van een VHD-bestand | Microsoft Docs
description: Meer informatie over het maken van een aangepaste installatiekopie in Azure DevTest Labs van een VHD-bestand met de Azure portal
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
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="ad844-103">Een aangepaste installatiekopie van een VHD-bestand maken</span><span class="sxs-lookup"><span data-stu-id="ad844-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="ad844-104">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="ad844-104">Step-by-step instructions</span></span>

<span data-ttu-id="ad844-105">De volgende stappen maakt u een aangepaste installatiekopie van een VHD-bestand met de Azure portal maken:</span><span class="sxs-lookup"><span data-stu-id="ad844-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="ad844-106">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ad844-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ad844-107">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="ad844-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="ad844-108">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="ad844-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="ad844-109">Selecteer op de labblade **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="ad844-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="ad844-110">Op de testomgeving **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="ad844-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="ad844-111">Op de **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ad844-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Aangepaste installatiekopie toe te voegen](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="ad844-113">Voer de naam van de aangepaste afbeelding.</span><span class="sxs-lookup"><span data-stu-id="ad844-113">Enter the name of the custom image.</span></span> <span data-ttu-id="ad844-114">Deze naam wordt weergegeven in de lijst met basisinstallatiekopieën bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad844-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="ad844-115">Geef de beschrijving van de aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="ad844-115">Enter the description of the custom image.</span></span> <span data-ttu-id="ad844-116">Deze beschrijving wordt weergegeven in de lijst met basisinstallatiekopieën bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ad844-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="ad844-117">Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="ad844-117">Select **VHD**.</span></span>

1. <span data-ttu-id="ad844-118">Van de **VHD** blade selecteert de gewenste VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="ad844-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="ad844-119">Selecteer **OK** sluiten de **VHD** blade.</span><span class="sxs-lookup"><span data-stu-id="ad844-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="ad844-120">Selecteer **configuratie van het besturingssysteem**.</span><span class="sxs-lookup"><span data-stu-id="ad844-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="ad844-121">Op de **configuratie van het besturingssysteem** tabblad, selecteert u **Windows** of **Linux**.</span><span class="sxs-lookup"><span data-stu-id="ad844-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="ad844-122">Als **Windows** is geselecteerd, geeft u via het selectievakje of *Sysprep* is uitgevoerd op de machine.</span><span class="sxs-lookup"><span data-stu-id="ad844-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="ad844-123">Selecteer **OK** sluiten de **configuratie van het besturingssysteem** blade.</span><span class="sxs-lookup"><span data-stu-id="ad844-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="ad844-124">Selecteer **OK** om de aangepaste installatiekopie te maken.</span><span class="sxs-lookup"><span data-stu-id="ad844-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="ad844-125">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="ad844-125">Related blog posts</span></span>

- [<span data-ttu-id="ad844-126">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="ad844-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="ad844-127">Kopiëren van aangepaste installatiekopieën tussen Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ad844-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="ad844-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad844-128">Next steps</span></span>

- [<span data-ttu-id="ad844-129">Een virtuele machine toevoegen aan uw testomgeving</span><span class="sxs-lookup"><span data-stu-id="ad844-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
