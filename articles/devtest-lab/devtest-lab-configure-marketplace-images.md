---
title: instellingen voor de aaaConfigure Azure Marketplace-installatiekopie in Azure DevTest Labs | Microsoft Docs
description: "Configureren welke Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van een virtuele machine in Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="bc88a-103">Configureren van instellingen voor Azure Marketplace-installatiekopie in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bc88a-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="bc88a-104">DevTest Labs ondersteunt maken virtuele machines op basis van Azure Marketplace-installatiekopieën, afhankelijk van hoe u Azure Marketplace-installatiekopieën toobe gebruikt in uw lab hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bc88a-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="bc88a-105">Dit artikel ziet u hoe toospecify die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="bc88a-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="bc88a-106">Dit zorgt ervoor dat uw team alleen toegang toohello Marketplace-installatiekopieën die ze nodig heeft.</span><span class="sxs-lookup"><span data-stu-id="bc88a-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="bc88a-107">Selecteer welke Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="bc88a-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="bc88a-108">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bc88a-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="bc88a-109">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="bc88a-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="bc88a-110">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="bc88a-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="bc88a-111">Selecteer op Hallo van labblade, **configuratie en het beleid**.</span><span class="sxs-lookup"><span data-stu-id="bc88a-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="bc88a-112">Op het lab **configuratie en het beleid** blade onder **basissen voor virtuele Machine**, selecteer **Marketplace-installatiekopieën**.</span><span class="sxs-lookup"><span data-stu-id="bc88a-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="bc88a-113">Geef op of u wilt dat alle Hallo gekwalificeerde Azure Marketplace-installatiekopieën toobe beschikbaar voor gebruik als basis van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bc88a-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="bc88a-114">Als u selecteert **Ja**, klikt u vervolgens alle hello Azure Marketplace-installatiekopieën die voldoen aan alle volgende criteria Hallo zijn toegestaan in Hallo lab:</span><span class="sxs-lookup"><span data-stu-id="bc88a-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="bc88a-115">Hallo-installatiekopie wordt gemaakt van één VM **en**</span><span class="sxs-lookup"><span data-stu-id="bc88a-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="bc88a-116">Hallo installatiekopie maakt gebruik van Azure Resource Manager tooprovision virtuele machines, **en**</span><span class="sxs-lookup"><span data-stu-id="bc88a-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="bc88a-117">Hallo installatiekopie vereist geen extra licentieabonnement aanschaffen</span><span class="sxs-lookup"><span data-stu-id="bc88a-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="bc88a-118">Als u geen afbeeldingen toobe toegestaan wilt, of u wilt dat toospecify welke afbeeldingen kunnen worden gebruikt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="bc88a-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Optie tooallow alle Marketplace-installatiekopieën toobe gebruikt als basis installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="bc88a-120">Als u selecteert **Nee** toohello vorige stap, hello **toegestane installatiekopieën/Selecteer alle** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="bc88a-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="bc88a-121">U kunt gebruik deze optie samen met de Hallo zoeken vak tooquickly selecteren of selectie van alle Hallo items weergegeven in de lijst Hallo opheffen.</span><span class="sxs-lookup"><span data-stu-id="bc88a-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="bc88a-122">Selecteer hello Azure Marketplace-installatiekopieën gewenste tooallow voor het maken van de virtuele machine afzonderlijk door het bijbehorende selectievakje van elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="bc88a-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="bc88a-123">Selecteer niets uit de lijst Hallo als u niet tooallow alle Azure Marketplace-installatiekopieën toobe gebruikt in Hallo lab wilt.</span><span class="sxs-lookup"><span data-stu-id="bc88a-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![U kunt opgeven welke Azure Marketplace-installatiekopieën kunnen worden gebruikt als basis van installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bc88a-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc88a-125">Next steps</span></span>
<span data-ttu-id="bc88a-126">Wanneer u de manier waarop Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine hebt geconfigureerd, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="bc88a-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

