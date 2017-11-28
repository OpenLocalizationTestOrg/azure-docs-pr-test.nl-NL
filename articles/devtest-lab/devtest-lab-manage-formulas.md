---
title: Beheer formules in Azure DevTest Labs virtuele machines maken | Microsoft Docs
description: Meer informatie over het bijwerken en verwijderen van Azure DevTest Labs formules
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="161ea-103">Azure DevTest Labs formules beheren</span><span class="sxs-lookup"><span data-stu-id="161ea-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="161ea-104">In dit artikel laat zien hoe een formule te maken van een base (aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule) of een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="161ea-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="161ea-105">In dit artikel helpt u ook bij het beheren van bestaande formules.</span><span class="sxs-lookup"><span data-stu-id="161ea-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="161ea-106">Maak een formule</span><span class="sxs-lookup"><span data-stu-id="161ea-106">Create a formula</span></span>
<span data-ttu-id="161ea-107">Iedereen met DevTest Labs *gebruikers* machtigingen kunnen maken van virtuele machines met een formule als basis is.</span><span class="sxs-lookup"><span data-stu-id="161ea-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="161ea-108">Er zijn twee manieren om formules te maken:</span><span class="sxs-lookup"><span data-stu-id="161ea-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="161ea-109">Gebruik van een basis - als u wilt de eigenschappen van de formule definiëren.</span><span class="sxs-lookup"><span data-stu-id="161ea-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="161ea-110">Van een bestaande lab VM - Gebruik deze optie wanneer u wilt maken van een formule op basis van de instellingen van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="161ea-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="161ea-111">Zie voor meer informatie over het toevoegen van gebruikers en machtigingen [eigenaars en gebruikers toevoegen in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="161ea-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="161ea-112">Maak een formule van een basis</span><span class="sxs-lookup"><span data-stu-id="161ea-112">Create a formula from a base</span></span>
<span data-ttu-id="161ea-113">De volgende stappen begeleiden u bij het proces van het maken van een formule van een aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="161ea-114">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="161ea-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="161ea-115">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="161ea-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="161ea-116">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="161ea-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="161ea-117">Selecteer op de labblade **formules (herbruikbare bases)**.</span><span class="sxs-lookup"><span data-stu-id="161ea-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="161ea-119">Op de **formules** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="161ea-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Een formule toevoegen](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="161ea-121">Op de **kiezen een base** blade, selecteer de base (aangepaste installatiekopie, Marketplace-installatiekopie of formule) van waaruit u wilt maken van de formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Base lijst](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="161ea-123">Op de **formule maken** blade, geef de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="161ea-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="161ea-124">**Formulenaam** -Voer een naam voor de formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="161ea-125">Deze waarde wordt weergegeven in de lijst met basisinstallatiekopieën wanneer u een virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="161ea-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="161ea-126">De naam wordt al gevalideerd als u deze typen, en als dat niet geldig, een bericht geeft aan de vereisten voor een geldige naam.</span><span class="sxs-lookup"><span data-stu-id="161ea-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="161ea-127">**Beschrijving** -Voer een duidelijke beschrijving voor de formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="161ea-128">Deze waarde is beschikbaar in het contextmenu van de formule bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="161ea-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="161ea-129">**Gebruikersnaam** -Voer een gebruikersnaam die wordt verleend administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="161ea-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="161ea-130">**Wachtwoord** : Geef - op of Selecteer in de vervolgkeuzelijst - een waarde die is gekoppeld aan het geheim (wachtwoord) dat u wilt gebruiken voor de opgegeven gebruiker.</span><span class="sxs-lookup"><span data-stu-id="161ea-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="161ea-131">Zie voor meer informatie over de geheimen [Azure DevTest Labs: persoonlijke archief van de geheime](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="161ea-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="161ea-132">**Virtuele machine schijftype** – Geef de harde schijf (harde schijf) of SSD (solid-state drive) om aan te geven welk type opslagschijf is toegestaan voor de virtuele machines ingericht met behulp van deze basisinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="161ea-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="161ea-133">** Virtuele machine grootte ** - Selecteer een van de vooraf gedefinieerde items die de processor-cores, RAM-geheugen en de grootte van de vaste schijf van de virtuele machine maken opgeven.</span><span class="sxs-lookup"><span data-stu-id="161ea-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="161ea-134">**Artefacten** - wilt openen de **artefacten toevoegen** blade, waarin u gegevens kunt selecteren en configureren van de artefacten die u wilt toevoegen aan de basisinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="161ea-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="161ea-135">Zie voor meer informatie over artefacten [beheren VM artefacten in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="161ea-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="161ea-136">**Geavanceerde instellingen** - wilt openen de **Geavanceerd** blade waar u de volgende instellingen configureren:</span><span class="sxs-lookup"><span data-stu-id="161ea-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="161ea-137">**Virtueel netwerk** -Geef de gewenste virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="161ea-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="161ea-138">**Subnet** -Geef de gewenste subnet.</span><span class="sxs-lookup"><span data-stu-id="161ea-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="161ea-139">**IP-adresconfiguratie** -opgeven of u wilt dat de Public, Private of gedeelde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="161ea-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="161ea-140">Zie voor meer informatie over gedeelde IP-adressen [Understand gedeelde IP-adressen in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="161ea-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="161ea-141">**Zorg dat deze machine claimable** -maken van een machine 'claimable' betekent dat deze wordt niet worden toegewezen eigendom op het moment van maken.</span><span class="sxs-lookup"><span data-stu-id="161ea-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="161ea-142">In plaats daarvan zich lab gebruikers eigenaar ("claim") de machine zich in het lab-blade.</span><span class="sxs-lookup"><span data-stu-id="161ea-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="161ea-143">**Afbeelding** -dit veld bevat de naam van de basisinstallatiekopie die u hebt geselecteerd op de vorige blade.</span><span class="sxs-lookup"><span data-stu-id="161ea-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Formule maken](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="161ea-145">Selecteer **maken** om de formule te maken.</span><span class="sxs-lookup"><span data-stu-id="161ea-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="161ea-146">Wanneer de formule is gemaakt, wordt weergegeven in de lijst op de **formules** blade.</span><span class="sxs-lookup"><span data-stu-id="161ea-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="161ea-147">Maak een formule van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="161ea-147">Create a formula from a VM</span></span>
<span data-ttu-id="161ea-148">De volgende stappen begeleiden u bij het proces van het maken van een formule op basis van een bestaande VM.</span><span class="sxs-lookup"><span data-stu-id="161ea-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="161ea-149">Als u wilt een formule van een virtuele machine maakt, moet de virtuele machine zijn gemaakt na 30 maart 2016.</span><span class="sxs-lookup"><span data-stu-id="161ea-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="161ea-150">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="161ea-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="161ea-151">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="161ea-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="161ea-152">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="161ea-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="161ea-153">Op de testomgeving **overzicht** blade, selecteert u de virtuele machine van waaruit u wilt maken van de formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Virtuele machines Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="161ea-155">Selecteer op de VM-blade **formule (op basis van herbruikbare) maken**.</span><span class="sxs-lookup"><span data-stu-id="161ea-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Formule maken](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="161ea-157">Op de **formule maken** blade, voer een **naam** en **beschrijving** voor uw nieuwe formule.</span><span class="sxs-lookup"><span data-stu-id="161ea-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Formule blade maken](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="161ea-159">Selecteer **OK** om de formule te maken.</span><span class="sxs-lookup"><span data-stu-id="161ea-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="161ea-160">Een formule wijzigen</span><span class="sxs-lookup"><span data-stu-id="161ea-160">Modify a formula</span></span>
<span data-ttu-id="161ea-161">Volg deze stappen voor het wijzigen van een formule:</span><span class="sxs-lookup"><span data-stu-id="161ea-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="161ea-162">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="161ea-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="161ea-163">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="161ea-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="161ea-164">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="161ea-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="161ea-165">Selecteer op de labblade **formules (herbruikbare bases)**.</span><span class="sxs-lookup"><span data-stu-id="161ea-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="161ea-167">Op de **Lab formules** blade, selecteer de formule die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="161ea-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="161ea-168">Op de **formule bijwerken** blade Breng de gewenste wijzigingen en selecteer **Update**.</span><span class="sxs-lookup"><span data-stu-id="161ea-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="161ea-169">Verwijderen van een formule</span><span class="sxs-lookup"><span data-stu-id="161ea-169">Delete a formula</span></span>
<span data-ttu-id="161ea-170">Volg deze stappen voor het verwijderen van een formule:</span><span class="sxs-lookup"><span data-stu-id="161ea-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="161ea-171">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="161ea-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="161ea-172">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="161ea-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="161ea-173">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="161ea-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="161ea-174">Op de testomgeving **instellingen** blade Selecteer **formules**.</span><span class="sxs-lookup"><span data-stu-id="161ea-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="161ea-176">Op de **Lab formules** blade, selecteer het weglatingsteken rechts van de formule die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="161ea-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="161ea-178">Selecteer in het contextmenu van de formule, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="161ea-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Formule contextmenu](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="161ea-180">Selecteer **Ja** naar het bevestigingsvenster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="161ea-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="161ea-181">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="161ea-181">Related blog posts</span></span>
* [<span data-ttu-id="161ea-182">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="161ea-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="161ea-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="161ea-183">Next steps</span></span>
<span data-ttu-id="161ea-184">Nadat u een formule voor gebruik gemaakt hebt bij het maken van een virtuele machine, de volgende stap is het [een virtuele machine toevoegen aan uw testomgeving](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="161ea-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

