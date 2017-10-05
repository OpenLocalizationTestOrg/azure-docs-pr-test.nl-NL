---
title: Uw eerste virtuele machine maken in een testomgeving in Azure DevTest Labs | Microsoft Docs
description: Informatie over het maken van uw eerste virtuele machine in een testomgeving in Azure DevTest Labs
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
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="15ba9-103">Uw eerste virtuele machine maken in een testomgeving in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15ba9-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="15ba9-104">Wanneer u in eerste instantie DevTest Labs openen en u wilt maken van uw eerste virtuele machine, wordt waarschijnlijk hiervoor met behulp van een vooraf geladen [base marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="15ba9-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="15ba9-105">Later in het moet ook mogelijk om te kiezen uit een [aangepaste installatiekopie en een formule](devtest-lab-add-vm.md) bij het maken van meer virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="15ba9-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="15ba9-106">Deze zelfstudie leert u met de Azure portal uw eerste virtuele machine toevoegen aan een lab in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="15ba9-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="15ba9-107">Stappen voor het toevoegen van uw eerste virtuele machine aan een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="15ba9-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="15ba9-108">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="15ba9-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="15ba9-109">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="15ba9-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="15ba9-110">Selecteer in de lijst van labs in het lab waarin u wilt maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="15ba9-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="15ba9-111">Op de testomgeving **overzicht** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="15ba9-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="15ba9-113">Op de **kiezen een base** blade, selecteer een marketplace-installatiekopie voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="15ba9-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="15ba9-114">Op de **virtuele machine** blade een naam voor de nieuwe virtuele machine in de **virtuele-machinenaam** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="15ba9-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="15ba9-116">Voer een **gebruikersnaam** die administrator-bevoegdheden op de virtuele machine wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="15ba9-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="15ba9-117">Voer een wachtwoord in het veld met het label **typt u een waarde**.</span><span class="sxs-lookup"><span data-stu-id="15ba9-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="15ba9-118">De **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor de virtuele machines in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="15ba9-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="15ba9-119">Selecteer **grootte van virtuele machine** en selecteer een van de vooraf gedefinieerde items die de processor-cores, RAM-geheugen en de grootte van de vaste schijf van de virtuele machine maken opgeven.</span><span class="sxs-lookup"><span data-stu-id="15ba9-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="15ba9-120">Selecteer **artefacten** - uit de lijst met artefacten - en selecteer de artefacten die u wilt toevoegen aan de basisinstallatiekopie configureren.</span><span class="sxs-lookup"><span data-stu-id="15ba9-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="15ba9-121">**Opmerking:** als u niet vertrouwd met DevTest Labs bent of configureren van artefacten, naar verwijzen de [een bestaande artefact toevoegen aan een virtuele machine](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="15ba9-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="15ba9-122">Selecteer **maken** opgegeven virtuele machine toevoegen aan het lab.</span><span class="sxs-lookup"><span data-stu-id="15ba9-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="15ba9-123">De blade testlab toont de status van het maken van de VM - eerst als **maken**, klikt u vervolgens als **met** nadat de virtuele machine is gestart.</span><span class="sxs-lookup"><span data-stu-id="15ba9-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ba9-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15ba9-124">Next steps</span></span>
* <span data-ttu-id="15ba9-125">Wanneer de virtuele machine is gemaakt, kunt u verbinden met de virtuele machine door te selecteren **Connect** op de blade van de VM.</span><span class="sxs-lookup"><span data-stu-id="15ba9-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="15ba9-126">Bekijk [een virtuele machine toevoegen aan een lab](devtest-lab-add-vm.md) voor gedetailleerde informatie over het toevoegen van de volgende virtuele machines in uw testomgeving.</span><span class="sxs-lookup"><span data-stu-id="15ba9-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="15ba9-127">Verken de [DevTest Labs Azure Resource Manager QuickStart sjablonengalerie](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="15ba9-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
