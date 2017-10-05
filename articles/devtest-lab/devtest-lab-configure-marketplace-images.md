---
title: Configureren van instellingen voor Azure Marketplace-installatiekopie in Azure DevTest Labs | Microsoft Docs
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="91d49-103">Configureren van instellingen voor Azure Marketplace-installatiekopie in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="91d49-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="91d49-104">DevTest Labs ondersteunt maken VMs op basis van Azure Marketplace-installatiekopieën, afhankelijk van hoe u Azure Marketplace-installatiekopieën hebt geconfigureerd in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="91d49-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="91d49-105">Dit artikel laat zien hoe u kunt opgeven die, indien aanwezig, Azure Marketplace-installatiekopieën kunnen worden gebruikt bij het maken van virtuele machines in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="91d49-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="91d49-106">Dit zorgt ervoor dat uw team alleen toegang heeft tot de Marketplace-installatiekopieën die ze nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="91d49-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="91d49-107">Selecteer welke Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="91d49-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="91d49-108">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="91d49-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="91d49-109">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="91d49-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="91d49-110">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="91d49-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="91d49-111">Selecteer op de labblade **configuratie en het beleid**.</span><span class="sxs-lookup"><span data-stu-id="91d49-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="91d49-112">Op het lab **configuratie en het beleid** blade onder **basissen voor virtuele Machine**, selecteer **Marketplace-installatiekopieën**.</span><span class="sxs-lookup"><span data-stu-id="91d49-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="91d49-113">Geef op of alle gekwalificeerde Azure Marketplace-installatiekopieën beschikbaar voor gebruik als een basis van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="91d49-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="91d49-114">Als u selecteert **Ja**, en vervolgens alle Azure Marketplace-installatiekopieën die voldoen aan de volgende criteria zijn toegestaan in de testomgeving:</span><span class="sxs-lookup"><span data-stu-id="91d49-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="91d49-115">De installatiekopie wordt gemaakt van één VM **en**</span><span class="sxs-lookup"><span data-stu-id="91d49-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="91d49-116">De installatiekopie van het Azure Resource Manager gebruikt om in te richten virtuele machines, **en**</span><span class="sxs-lookup"><span data-stu-id="91d49-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="91d49-117">De installatiekopie van het vereist aanschaffen van extra licentieabonnement geen</span><span class="sxs-lookup"><span data-stu-id="91d49-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="91d49-118">Als u wilt geen afbeeldingen worden toegestaan, of u opgeven wilt welke afbeeldingen kunnen worden gebruikt, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="91d49-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Optie voor het toestaan van alle Marketplace-installatiekopieën worden gebruikt als basis van installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="91d49-120">Als u selecteert **Nee** naar de vorige stap, de **toegestane installatiekopieën/Selecteer alle** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="91d49-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="91d49-121">Gebruik deze optie samen met het zoekvak om snel te selecteren of selectie opheffen van alle items in de lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="91d49-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="91d49-122">Selecteer de Azure Marketplace-installatiekopieën die u toestaan voor het maken van de virtuele machine afzonderlijk wilt door het bijbehorende selectievakje van elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="91d49-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="91d49-123">Selecteer niets uit de lijst als u niet wilt dat alle Azure Marketplace-installatiekopieën worden gebruikt in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="91d49-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![U kunt opgeven welke Azure Marketplace-installatiekopieën kunnen worden gebruikt als basis van installatiekopieën voor virtuele machines](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="91d49-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="91d49-125">Next steps</span></span>
<span data-ttu-id="91d49-126">Wanneer u de manier waarop Azure Marketplace-installatiekopieën zijn toegestaan bij het maken van een virtuele machine hebt geconfigureerd, wordt de volgende stap is het [een virtuele machine toevoegen aan uw testomgeving](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="91d49-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

