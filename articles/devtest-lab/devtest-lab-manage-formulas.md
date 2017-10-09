---
title: aaaManage formules in Azure DevTest Labs toocreate VMs | Microsoft Docs
description: Meer informatie over hoe Azure DevTest Labs formules voor tooupdate en verwijderen
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="67673-103">Azure DevTest Labs formules beheren</span><span class="sxs-lookup"><span data-stu-id="67673-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="67673-104">Dit artikel wordt beschreven hoe toocreate een formule van een base (aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule) of een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67673-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="67673-105">In dit artikel helpt u ook bij het beheren van bestaande formules.</span><span class="sxs-lookup"><span data-stu-id="67673-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="67673-106">Maak een formule</span><span class="sxs-lookup"><span data-stu-id="67673-106">Create a formula</span></span>
<span data-ttu-id="67673-107">Iedereen met DevTest Labs *gebruikers* machtigingen kunnen toocreate virtuele machines met een formule als basis is.</span><span class="sxs-lookup"><span data-stu-id="67673-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="67673-108">Er zijn twee manieren toocreate formules:</span><span class="sxs-lookup"><span data-stu-id="67673-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="67673-109">Gebruik van een basis - als u alle Hallo kenmerken van Hallo formule toodefine wilt.</span><span class="sxs-lookup"><span data-stu-id="67673-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="67673-110">Van een bestaande lab VM - gebruiken als u wilt dat toocreate een formule op basis van Hallo-instellingen van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67673-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="67673-111">Zie voor meer informatie over het toevoegen van gebruikers en machtigingen [eigenaars en gebruikers toevoegen in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="67673-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="67673-112">Maak een formule van een basis</span><span class="sxs-lookup"><span data-stu-id="67673-112">Create a formula from a base</span></span>
<span data-ttu-id="67673-113">Hallo stappen volgen helpt u bij het Hallo-proces voor het maken van een formule van een aangepaste installatiekopie, Marketplace-installatiekopie of een andere formule.</span><span class="sxs-lookup"><span data-stu-id="67673-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="67673-114">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67673-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="67673-115">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="67673-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="67673-116">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="67673-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="67673-117">Selecteer op Hallo van labblade, **formules (herbruikbare bases)**.</span><span class="sxs-lookup"><span data-stu-id="67673-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu formule](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="67673-119">Op Hallo **formules** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="67673-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Een formule toevoegen](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="67673-121">Op Hallo **kiezen een base** blade Selecteer Hallo base (aangepaste installatiekopie, Marketplace-installatiekopie of formule) waaruit de toocreate Hallo formule.</span><span class="sxs-lookup"><span data-stu-id="67673-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Base lijst](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="67673-123">Op Hallo **formule maken** blade Hallo volgende waarden opgeven:</span><span class="sxs-lookup"><span data-stu-id="67673-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="67673-124">**Formulenaam** -Voer een naam voor de formule.</span><span class="sxs-lookup"><span data-stu-id="67673-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="67673-125">Deze waarde wordt weergegeven in de lijst Hallo met basisinstallatiekopieën bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67673-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="67673-126">Hallo-naam wordt al gevalideerd als u deze typen, en als dat niet geldig, er wordt gemeld Hallo-vereisten voor een geldige naam.</span><span class="sxs-lookup"><span data-stu-id="67673-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="67673-127">**Beschrijving** -Voer een duidelijke beschrijving voor de formule.</span><span class="sxs-lookup"><span data-stu-id="67673-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="67673-128">Deze waarde is beschikbaar in het contextmenu van de formule Hallo bij het maken van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67673-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="67673-129">**Gebruikersnaam** -Voer een gebruikersnaam die wordt verleend administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="67673-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="67673-130">**Wachtwoord** : Geef - of Selecteer in de vervolgkeuzelijst Hallo - u op een waarde die is gekoppeld aan het Hallo-geheim (wachtwoord) wilt u toouse voor Hallo opgegeven gebruiker.</span><span class="sxs-lookup"><span data-stu-id="67673-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="67673-131">Zie voor meer informatie over Hallo geheimen [Azure DevTest Labs: persoonlijke archief van de geheime](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="67673-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="67673-132">**Virtuele machine schijftype** – Geef de harde schijf (harde schijf) of SSD (solid-state drive) tooindicate welke opslagschijf type is toegestaan voor Hallo virtuele machines zijn ingericht met behulp van deze basisinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="67673-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="67673-133">** Virtuele machine grootte ** - Selecteer een van de vooraf gedefinieerde Hallo-items die Hallo processorcores, RAM-geheugen en grootte van de vaste schijf Hallo van Hallo VM toocreate opgeven.</span><span class="sxs-lookup"><span data-stu-id="67673-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="67673-134">**Artefacten** -Selecteer tooopen hello **artefacten toevoegen** blade die u selecteert en Hallo artefacten die u tooadd toohello basisinstallatiekopie wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="67673-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="67673-135">Zie voor meer informatie over artefacten [beheren VM artefacten in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="67673-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="67673-136">**Geavanceerde instellingen** -Selecteer tooopen hello **Geavanceerd** blade waar u Hallo volgende instellingen configureren:</span><span class="sxs-lookup"><span data-stu-id="67673-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="67673-137">**Virtueel netwerk** -Hallo gewenst virtueel netwerk opgeven.</span><span class="sxs-lookup"><span data-stu-id="67673-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="67673-138">**Subnet** -Hallo gewenst subnet opgeven.</span><span class="sxs-lookup"><span data-stu-id="67673-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="67673-139">**IP-adresconfiguratie** -opgeven of u wilt dat Hallo Public, Private of gedeelde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="67673-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="67673-140">Zie voor meer informatie over gedeelde IP-adressen [Understand gedeelde IP-adressen in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="67673-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="67673-141">**Zorg dat deze machine claimable** -maken van een machine 'claimable' betekent dat deze wordt niet worden toegewezen eigendom op Hallo moment gemaakt.</span><span class="sxs-lookup"><span data-stu-id="67673-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="67673-142">In plaats daarvan lab kunnen gebruikers zich kunnen tootake eigendom ("claim") Hallo machine in Hallo labblade.</span><span class="sxs-lookup"><span data-stu-id="67673-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="67673-143">**Afbeelding** -dit veld bevat de naam van Hallo basisinstallatiekopie u hebt geselecteerd op de vorige blade Hallo.</span><span class="sxs-lookup"><span data-stu-id="67673-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Formule maken](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="67673-145">Selecteer **maken** toocreate Hallo formule.</span><span class="sxs-lookup"><span data-stu-id="67673-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="67673-146">Wanneer het Hallo-formule is gemaakt, wordt weergegeven in de lijst Hallo op Hallo **formules** blade.</span><span class="sxs-lookup"><span data-stu-id="67673-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="67673-147">Maak een formule van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="67673-147">Create a formula from a VM</span></span>
<span data-ttu-id="67673-148">Hallo volgende stappen begeleiden u bij Hallo-proces voor het maken van een formule op basis van een bestaande virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="67673-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="67673-149">toocreate een formule van een virtuele machine, Hallo VM moet zijn gemaakt na 30 maart 2016.</span><span class="sxs-lookup"><span data-stu-id="67673-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="67673-150">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67673-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67673-151">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="67673-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="67673-152">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="67673-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="67673-153">Op de Hallo lab **overzicht** blade Selecteer Hallo VM van waaruit u wilt dat toocreate Hallo formule.</span><span class="sxs-lookup"><span data-stu-id="67673-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Virtuele machines Labs](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="67673-155">Selecteer op de blade Hallo van de virtuele machine **formule (op basis van herbruikbare) maken**.</span><span class="sxs-lookup"><span data-stu-id="67673-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Formule maken](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="67673-157">Op Hallo **formule maken** blade, voer een **naam** en **beschrijving** voor uw nieuwe formule.</span><span class="sxs-lookup"><span data-stu-id="67673-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Formule blade maken](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="67673-159">Selecteer **OK** toocreate Hallo formule.</span><span class="sxs-lookup"><span data-stu-id="67673-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="67673-160">Een formule wijzigen</span><span class="sxs-lookup"><span data-stu-id="67673-160">Modify a formula</span></span>
<span data-ttu-id="67673-161">een formule toomodify als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="67673-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="67673-162">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67673-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67673-163">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="67673-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="67673-164">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="67673-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="67673-165">Selecteer op Hallo van labblade, **formules (herbruikbare bases)**.</span><span class="sxs-lookup"><span data-stu-id="67673-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="67673-167">Op Hallo **Lab formules** blade, selecteer Hallo-formule die u wenst dat toomodify.</span><span class="sxs-lookup"><span data-stu-id="67673-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="67673-168">Op Hallo **formule bijwerken** blade Hallo gewenst bewerkingen en selecteer **Update**.</span><span class="sxs-lookup"><span data-stu-id="67673-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="67673-169">Verwijderen van een formule</span><span class="sxs-lookup"><span data-stu-id="67673-169">Delete a formula</span></span>
<span data-ttu-id="67673-170">een formule toodelete als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="67673-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="67673-171">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="67673-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="67673-172">Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="67673-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="67673-173">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="67673-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="67673-174">Op Hallo lab **instellingen** blade Selecteer **formules**.</span><span class="sxs-lookup"><span data-stu-id="67673-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="67673-176">Op Hallo **Lab formules** blade, selecteer Hallo weglatingsteken toohello rechts van de formule Hallo gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="67673-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Menu formule](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="67673-178">Selecteer in het contextmenu van de formule hello, **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="67673-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Formule contextmenu](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="67673-180">Selecteer **Ja** toohello verwijdering bevestigen.</span><span class="sxs-lookup"><span data-stu-id="67673-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="67673-181">Verwante blogberichten</span><span class="sxs-lookup"><span data-stu-id="67673-181">Related blog posts</span></span>
* [<span data-ttu-id="67673-182">Aangepaste installatiekopieën of formules?</span><span class="sxs-lookup"><span data-stu-id="67673-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="67673-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67673-183">Next steps</span></span>
<span data-ttu-id="67673-184">Nadat u een formule voor gebruik gemaakt hebt bij het maken van een virtuele machine, Hallo volgende stap is te[toevoegen van een VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="67673-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

