---
title: aaaCreate uw eerste virtuele machine in een testomgeving in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over hoe toocreate uw eerste virtuele machine in een testomgeving in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="b8daa-103">Uw eerste virtuele machine maken in een testomgeving in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b8daa-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="b8daa-104">Wanneer u in eerste instantie DevTest Labs toegang en toocreate uw eerste virtuele machine, wordt waarschijnlijk hiervoor met behulp van een vooraf geladen [base marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="b8daa-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="b8daa-105">Later ook, moet u kunnen toochoose van een [aangepaste installatiekopie en een formule](devtest-lab-add-vm.md) bij het maken van meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="b8daa-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="b8daa-106">Deze zelfstudie leert u met behulp van Azure portal tooadd Hallo uw eerste VM tooa lab in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="b8daa-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="b8daa-107">Stappen tooadd uw eerste VM tooa lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b8daa-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="b8daa-108">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b8daa-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="b8daa-109">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="b8daa-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="b8daa-110">Selecteer in lijst Hallo van labs Hallo lab waarin wordt gezocht toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="b8daa-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="b8daa-111">Op de Hallo lab **overzicht** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b8daa-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="b8daa-113">Op Hallo **kiezen een base** blade, selecteer een marketplace-installatiekopie voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="b8daa-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="b8daa-114">Op Hallo **virtuele machine** blade, voer een naam voor de nieuwe virtuele machine Hallo in Hallo **virtuele-machinenaam** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="b8daa-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="b8daa-116">Voer een **gebruikersnaam** die administrator-bevoegdheden op Hallo virtuele machine wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="b8daa-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="b8daa-117">Voer een wachtwoord in Hallo tekstveld met het label **typt u een waarde**.</span><span class="sxs-lookup"><span data-stu-id="b8daa-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="b8daa-118">Hallo **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor Hallo virtuele machines in Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="b8daa-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="b8daa-119">Selecteer **grootte van virtuele machine** en selecteer een van de Hallo vooraf gedefinieerde items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven.</span><span class="sxs-lookup"><span data-stu-id="b8daa-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="b8daa-120">Selecteer **artefacten** - in de lijst Hallo van artefacten - en selecteer Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="b8daa-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="b8daa-121">**Opmerking:** als u nieuwe tooDevTest Labs of configureren van artefacten, Raadpleeg toohello [toevoegen van een bestaande artefact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="b8daa-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="b8daa-122">Selecteer **maken** tooadd Hallo VM toohello lab opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b8daa-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="b8daa-123">Hallo-status van Hallo van de virtuele machine maken: Hallo labblade eerst weergegeven als **maken**, klikt u vervolgens als **met** na Hallo VM is gestart.</span><span class="sxs-lookup"><span data-stu-id="b8daa-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8daa-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8daa-124">Next steps</span></span>
* <span data-ttu-id="b8daa-125">Eenmaal Hallo VM is gemaakt, kunt u toohello VM door te selecteren **Connect** op Hallo van de virtuele machine-blade.</span><span class="sxs-lookup"><span data-stu-id="b8daa-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="b8daa-126">Bekijk [toevoegen van een VM tooa lab](devtest-lab-add-vm.md) voor gedetailleerde informatie over het toevoegen van de volgende virtuele machines in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8daa-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="b8daa-127">Hallo verkennen [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="b8daa-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
