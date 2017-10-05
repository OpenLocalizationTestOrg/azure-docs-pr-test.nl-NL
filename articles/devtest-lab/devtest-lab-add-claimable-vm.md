---
title: Een claimable virtuele machine toevoegen aan een lab in Azure DevTest Labs | Microsoft Docs
description: Meer informatie over het toevoegen van een claimable virtuele machine aan een lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="20528-103">Een claimable virtuele machine toevoegen aan een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="20528-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="20528-104">U een claimable virtuele machine toevoegen aan een lab op een vergelijkbare manier met de manier waarop u [toevoegen van een standaard virtuele machine](devtest-lab-add-vm.md) – Selecteer in een *base* dat ofwel een [aangepaste installatiekopie](devtest-lab-create-template.md), [formule](devtest-lab-manage-formulas.md), of [Marketplace-installatiekopie](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="20528-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="20528-105">Deze zelfstudie wordt u begeleid bij met de Azure portal een claimable virtuele machine toevoegen aan een lab in DevTest Labs en ziet u dat een gebruiker om de virtuele machine via het proces.</span><span class="sxs-lookup"><span data-stu-id="20528-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="20528-106">Als u virtuele machines lab via implementeert [Azure Resource Manager-sjablonen](devtest-lab-create-environment-from-arm.md), kunt u claimable virtuele machines maken door in te stellen de **allowClaim** eigenschap op true in de sectie met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="20528-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="20528-107">Stappen voor het toevoegen van een claimable VM aan een lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="20528-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="20528-108">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="20528-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="20528-109">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="20528-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="20528-110">Selecteer in de lijst van labs in het lab waarin u wilt maken van de claimable VM.</span><span class="sxs-lookup"><span data-stu-id="20528-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="20528-111">Op de testomgeving **overzicht** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="20528-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM-knop toevoegen](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="20528-113">Op de **kiezen een base** blade, selecteert u een basis voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="20528-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="20528-114">Op de **virtuele machine** blade een naam voor de nieuwe virtuele machine in de **virtuele-machinenaam** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="20528-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![VM-labblade](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="20528-116">Voer een **gebruikersnaam** die administrator-bevoegdheden op de virtuele machine wordt verleend.</span><span class="sxs-lookup"><span data-stu-id="20528-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="20528-117">Als u gebruiken van een wachtwoord opgeslagen wilt in uw [geheime store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), selecteer **een opgeslagen geheim**, en geef de waarde van een sleutel die overeenkomt met uw geheime (wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="20528-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="20528-118">Anders, voer een wachtwoord in het veld met het label **typt u een waarde**.</span><span class="sxs-lookup"><span data-stu-id="20528-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="20528-119">De **virtuele machine schijftype** wordt bepaald welk type opslagschijf is toegestaan voor de virtuele machines in de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="20528-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="20528-120">Selecteer **grootte van virtuele machine** en selecteer een van de vooraf gedefinieerde items die de processor-cores, RAM-geheugen en de grootte van de vaste schijf van de virtuele machine maken opgeven.</span><span class="sxs-lookup"><span data-stu-id="20528-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="20528-121">Selecteer **artefacten** uit de lijst van artefacten en selecteer de artefacten die u wilt toevoegen aan de basisinstallatiekopie configureren.</span><span class="sxs-lookup"><span data-stu-id="20528-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="20528-122">Als u niet vertrouwd met DevTest Labs bent of configureren van artefacten, naar verwijzen de [een bestaande artefact toevoegen aan een virtuele machine](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sectie en ga vervolgens terug hier na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="20528-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="20528-123">Selecteer **geavanceerde instellingen** om de netwerkopties en opties van de virtuele machine te configureren.</span><span class="sxs-lookup"><span data-stu-id="20528-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="20528-124">Onder **opties Claim**, kies **Ja** op de machine claimable maken.</span><span class="sxs-lookup"><span data-stu-id="20528-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Wilt u de VM claimable maken.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="20528-126">Als u wilt weergeven of kopiëren van de Azure Resource Manager-sjabloon, raadpleegt u de [opslaan Azure Resource Manager-sjabloon](devtest-lab-add-vm.md#save-azure-resource-manager-template) sectie en hier terug wanneer voltooid.</span><span class="sxs-lookup"><span data-stu-id="20528-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="20528-127">Selecteer **maken** opgegeven virtuele machine toevoegen aan het lab.</span><span class="sxs-lookup"><span data-stu-id="20528-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="20528-128">De blade testlab toont de status van het maken van de VM - eerst als **maken**, klikt u vervolgens als **met** nadat de virtuele machine is gestart.</span><span class="sxs-lookup"><span data-stu-id="20528-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="20528-129">Met behulp van een claimable VM</span><span class="sxs-lookup"><span data-stu-id="20528-129">Using a claimable VM</span></span>

<span data-ttu-id="20528-130">Een gebruiker kan een virtuele machine uit de lijst met 'Claimable virtuele machines' claim op een van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="20528-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="20528-131">In de lijst met 'Claimable virtuele machines' onderaan de blade overzicht van de testomgeving, met de rechtermuisknop op een van de virtuele machines in de lijst en kies **Claim machine**.</span><span class="sxs-lookup"><span data-stu-id="20528-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Aanvragen van een specifieke claimable virtuele machine.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="20528-133">Aan de bovenkant van de **overzicht** blade kiezen **een Claim**.</span><span class="sxs-lookup"><span data-stu-id="20528-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="20528-134">Een willekeurige virtuele machine wordt toegewezen uit de lijst met claimable virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="20528-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Aanvraag geen claimable VM.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="20528-136">Nadat een gebruiker claims van een virtuele machine, omhoog verplaatst naar hun lijst met 'Mijn virtuele machines' en is niet langer claimable door een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="20528-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20528-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20528-137">Next steps</span></span>
* <span data-ttu-id="20528-138">Wanneer de virtuele machine is gemaakt, kunt u verbinden met de virtuele machine door te selecteren **Connect** op de blade van de VM.</span><span class="sxs-lookup"><span data-stu-id="20528-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="20528-139">Verken de [sjablonengalerie DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="20528-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
