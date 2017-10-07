---
title: aaaAdd eigenaars en gebruikers in Azure DevTest Labs | Microsoft Docs
description: Eigenaars- en gebruikers toevoegen in Azure DevTest Labs met hello Azure-portal of PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: 2a98f5fe1efbd7c23e0d97f58f47c37462aed3b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="5bd54-103">Eigenaars- en gebruikers toevoegen in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="5bd54-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="5bd54-104">Toegang in Azure DevTest Labs wordt beheerd door [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="5bd54-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="5bd54-105">Met RBAC kunt kunt u taken scheiden binnen uw team in *rollen* waarin u alleen Hallo hoeveelheid toegang nodig toousers tooperform hun taken toekennen.</span><span class="sxs-lookup"><span data-stu-id="5bd54-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only hello amount of access necessary toousers tooperform their jobs.</span></span> <span data-ttu-id="5bd54-106">Drie van deze RBAC-rollen zijn *eigenaar*, *DevTest Labs gebruiker*, en *Inzender*.</span><span class="sxs-lookup"><span data-stu-id="5bd54-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="5bd54-107">In dit artikel leert u welke acties worden uitgevoerd in elk Hallo drie belangrijkste RBAC rollen.</span><span class="sxs-lookup"><span data-stu-id="5bd54-107">In this article, you learn what actions can be performed in each of hello three main RBAC roles.</span></span> <span data-ttu-id="5bd54-108">Van daaruit leert u hoe tooadd gebruikers tooa lab - die beide via Hallo portal en via een PowerShell-script en hoe gebruikers tooadd op abonnementsniveau Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bd54-108">From there, you learn how tooadd users tooa lab - both via hello portal and via a PowerShell script, and how tooadd users at hello subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="5bd54-109">Acties die kunnen worden uitgevoerd in elke rol</span><span class="sxs-lookup"><span data-stu-id="5bd54-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="5bd54-110">Er zijn drie belangrijkste rollen kunt u een gebruiker toewijzen:</span><span class="sxs-lookup"><span data-stu-id="5bd54-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="5bd54-111">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="5bd54-111">Owner</span></span>
* <span data-ttu-id="5bd54-112">DevTest Labs gebruiker</span><span class="sxs-lookup"><span data-stu-id="5bd54-112">DevTest Labs User</span></span>
* <span data-ttu-id="5bd54-113">Inzender</span><span class="sxs-lookup"><span data-stu-id="5bd54-113">Contributor</span></span>

<span data-ttu-id="5bd54-114">Hallo volgende tabel ziet u Hallo-acties die kunnen worden uitgevoerd door gebruikers in elk van deze rollen:</span><span class="sxs-lookup"><span data-stu-id="5bd54-114">hello following table illustrates hello actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="5bd54-115">**Gebruikers met deze rol acties kunnen uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="5bd54-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="5bd54-116">**DevTest Labs gebruiker**</span><span class="sxs-lookup"><span data-stu-id="5bd54-116">**DevTest Labs User**</span></span> | <span data-ttu-id="5bd54-117">**Eigenaar**</span><span class="sxs-lookup"><span data-stu-id="5bd54-117">**Owner**</span></span> | <span data-ttu-id="5bd54-118">**Inzender**</span><span class="sxs-lookup"><span data-stu-id="5bd54-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5bd54-119">**Taken voor het testlab**</span><span class="sxs-lookup"><span data-stu-id="5bd54-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="5bd54-120">Gebruikers tooa lab toevoegen</span><span class="sxs-lookup"><span data-stu-id="5bd54-120">Add users tooa lab</span></span> |<span data-ttu-id="5bd54-121">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-121">No</span></span> |<span data-ttu-id="5bd54-122">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-122">Yes</span></span> |<span data-ttu-id="5bd54-123">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-123">No</span></span> |
| <span data-ttu-id="5bd54-124">Update-instellingen</span><span class="sxs-lookup"><span data-stu-id="5bd54-124">Update cost settings</span></span> |<span data-ttu-id="5bd54-125">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-125">No</span></span> |<span data-ttu-id="5bd54-126">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-126">Yes</span></span> |<span data-ttu-id="5bd54-127">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-127">Yes</span></span> |
| <span data-ttu-id="5bd54-128">**Basis VM-taken**</span><span class="sxs-lookup"><span data-stu-id="5bd54-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="5bd54-129">Toevoegen en verwijderen van aangepaste installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="5bd54-129">Add and remove custom images</span></span> |<span data-ttu-id="5bd54-130">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-130">No</span></span> |<span data-ttu-id="5bd54-131">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-131">Yes</span></span> |<span data-ttu-id="5bd54-132">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-132">Yes</span></span> |
| <span data-ttu-id="5bd54-133">Toevoegen, bijwerken en verwijderen van formules</span><span class="sxs-lookup"><span data-stu-id="5bd54-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="5bd54-134">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-134">Yes</span></span> |<span data-ttu-id="5bd54-135">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-135">Yes</span></span> |<span data-ttu-id="5bd54-136">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-136">Yes</span></span> |
| <span data-ttu-id="5bd54-137">Geaccepteerde Azure Marketplace-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="5bd54-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="5bd54-138">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-138">No</span></span> |<span data-ttu-id="5bd54-139">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-139">Yes</span></span> |<span data-ttu-id="5bd54-140">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-140">Yes</span></span> |
| <span data-ttu-id="5bd54-141">**VM-taken**</span><span class="sxs-lookup"><span data-stu-id="5bd54-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="5bd54-142">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="5bd54-142">Create VMs</span></span> |<span data-ttu-id="5bd54-143">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-143">Yes</span></span> |<span data-ttu-id="5bd54-144">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-144">Yes</span></span> |<span data-ttu-id="5bd54-145">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-145">Yes</span></span> |
| <span data-ttu-id="5bd54-146">Starten, stoppen en verwijderen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="5bd54-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="5bd54-147">Alleen virtuele machines die zijn gemaakt door gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="5bd54-147">Only VMs created by hello user</span></span> |<span data-ttu-id="5bd54-148">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-148">Yes</span></span> |<span data-ttu-id="5bd54-149">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-149">Yes</span></span> |
| <span data-ttu-id="5bd54-150">Beleidsregels voor virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="5bd54-150">Update VM policies</span></span> |<span data-ttu-id="5bd54-151">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-151">No</span></span> |<span data-ttu-id="5bd54-152">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-152">Yes</span></span> |<span data-ttu-id="5bd54-153">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-153">Yes</span></span> |
| <span data-ttu-id="5bd54-154">Gegevensschijven van VM's toevoegen of verwijderen</span><span class="sxs-lookup"><span data-stu-id="5bd54-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="5bd54-155">Alleen virtuele machines die zijn gemaakt door gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="5bd54-155">Only VMs created by hello user</span></span> |<span data-ttu-id="5bd54-156">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-156">Yes</span></span> |<span data-ttu-id="5bd54-157">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-157">Yes</span></span> |
| <span data-ttu-id="5bd54-158">**Taken van artefacten**</span><span class="sxs-lookup"><span data-stu-id="5bd54-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="5bd54-159">Toevoegen en verwijderen van artefacten opslagplaatsen</span><span class="sxs-lookup"><span data-stu-id="5bd54-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="5bd54-160">Nee</span><span class="sxs-lookup"><span data-stu-id="5bd54-160">No</span></span> |<span data-ttu-id="5bd54-161">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-161">Yes</span></span> |<span data-ttu-id="5bd54-162">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-162">Yes</span></span> |
| <span data-ttu-id="5bd54-163">Toepassen van artefacten</span><span class="sxs-lookup"><span data-stu-id="5bd54-163">Apply artifacts</span></span> |<span data-ttu-id="5bd54-164">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-164">Yes</span></span> |<span data-ttu-id="5bd54-165">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-165">Yes</span></span> |<span data-ttu-id="5bd54-166">Ja</span><span class="sxs-lookup"><span data-stu-id="5bd54-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="5bd54-167">Wanneer een gebruiker een virtuele machine maakt, wordt deze gebruiker toohello automatisch toegewezen **eigenaar** rol Hallo VM gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5bd54-167">When a user creates a VM, that user is automatically assigned toohello **Owner** role of hello created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-hello-lab-level"></a><span data-ttu-id="5bd54-168">Toevoegen van een eigenaar of gebruiker op Hallo lab niveau</span><span class="sxs-lookup"><span data-stu-id="5bd54-168">Add an owner or user at hello lab level</span></span>
<span data-ttu-id="5bd54-169">Eigenaars- en gebruikers kunnen worden toegevoegd op Hallo lab niveau via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5bd54-169">Owners and users can be added at hello lab level via hello Azure portal.</span></span> <span data-ttu-id="5bd54-170">Dit omvat externe gebruikers met een geldig [Microsoft-account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="5bd54-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="5bd54-171">Hallo stappen volgen helpt u bij Hallo van het toevoegen van een eigenaar of gebruiker tooa lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="5bd54-171">hello following steps guide you through hello process of adding an owner or user tooa lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="5bd54-172">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5bd54-172">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="5bd54-173">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="5bd54-173">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="5bd54-174">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="5bd54-174">From hello list of labs, select hello desired lab.</span></span>
4. <span data-ttu-id="5bd54-175">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-175">On hello lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="5bd54-176">Op Hallo **configuratie** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-176">On hello **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="5bd54-177">Op Hallo **gebruikers** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-177">On hello **Users** blade, select **+Add**.</span></span>
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="5bd54-179">Op Hallo **Selecteer een rol** blade, selecteer Hallo gewenste functie.</span><span class="sxs-lookup"><span data-stu-id="5bd54-179">On hello **Select a role** blade, select hello desired role.</span></span> <span data-ttu-id="5bd54-180">sectie Hallo [acties die kunnen worden uitgevoerd in elke rol](#actions-that-can-be-performed-in-each-role) lijsten Hallo verschillende acties die kunnen worden uitgevoerd door gebruikers in Hallo eigenaar, DevTest gebruiker en Inzender rollen.</span><span class="sxs-lookup"><span data-stu-id="5bd54-180">hello section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists hello various actions that can be performed by users in hello Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="5bd54-181">Op Hallo **gebruikers toevoegen** blade Voer Hallo e-mailadres of de naam van Hallo gebruiker gewenste tooadd in Hallo-rol die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5bd54-181">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd in hello role you specified.</span></span> <span data-ttu-id="5bd54-182">Als Hallo-gebruiker kan niet worden gevonden, wordt een foutbericht uitgelegd Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="5bd54-182">If hello user can't be found, an error message explains hello issue.</span></span> <span data-ttu-id="5bd54-183">Als de gebruiker hello wordt gevonden, wordt die gebruiker weergegeven en geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="5bd54-183">If hello user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="5bd54-184">Selecteer **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-184">Select **Select**.</span></span>
10. <span data-ttu-id="5bd54-185">Selecteer **OK** tooclose hello **toegang toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="5bd54-185">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="5bd54-186">Als u terugkeert toohello **gebruikers** blade Hallo gebruiker is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5bd54-186">When you return toohello **Users** blade, hello user has been added.</span></span>  

## <a name="add-an-external-user-tooa-lab-using-powershell"></a><span data-ttu-id="5bd54-187">Toevoegen van een externe gebruiker tooa lab met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bd54-187">Add an external user tooa lab using PowerShell</span></span>
<span data-ttu-id="5bd54-188">Bovendien tooadding gebruikers in hello Azure-portal, kunt u toevoegen een externe gebruiker tooyour testomgeving met een PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="5bd54-188">In addition tooadding users in hello Azure portal, you can add an external user tooyour lab using a PowerShell script.</span></span> <span data-ttu-id="5bd54-189">Hallo bijvoorbeeld na gewoon Wijzig in Hallo parameterwaarden onder Hallo **waarden toochange** opmerking.</span><span class="sxs-lookup"><span data-stu-id="5bd54-189">In hello following example, simply modify hello parameter values under hello **Values toochange** comment.</span></span>
<span data-ttu-id="5bd54-190">U kunt ophalen Hallo `subscriptionId`, `labResourceGroup`, en `labName` waarden uit de labblade Hallo in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5bd54-190">You can retrieve hello `subscriptionId`, `labResourceGroup`, and `labName` values from hello lab blade in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5bd54-191">Hallo-voorbeeldscript wordt ervan uitgegaan dat Hallo opgegeven gebruiker is toegevoegd als een gast toohello Active Directory en als dat niet Hallo geval mislukken.</span><span class="sxs-lookup"><span data-stu-id="5bd54-191">hello sample script assumes that hello specified user has been added as a guest toohello Active Directory, and will fail if that is not hello case.</span></span> <span data-ttu-id="5bd54-192">tooadd een gebruiker niet in Active Directory tooa lab, Hallo hello Azure portal tooassign Hallo-gebruikersrol tooa gebruiken zoals wordt geïllustreerd in de sectie Hallo [toevoegen van een eigenaar of gebruiker op Hallo lab niveau](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="5bd54-192">tooadd a user not in hello Active Directory tooa lab, use hello Azure portal tooassign hello user tooa role as illustrated in hello section, [Add an owner or user at hello lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role tooa lab
    # Ensure that guest users can be added toohello Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve hello user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create hello role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-hello-subscription-level"></a><span data-ttu-id="5bd54-193">Toevoegen van een eigenaar of gebruiker op het abonnementsniveau Hallo</span><span class="sxs-lookup"><span data-stu-id="5bd54-193">Add an owner or user at hello subscription level</span></span>
<span data-ttu-id="5bd54-194">Azure machtigingen worden overgenomen van bovenliggende bereik toochild bereik in Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd54-194">Azure permissions are propagated from parent scope toochild scope in Azure.</span></span> <span data-ttu-id="5bd54-195">Eigenaren van een Azure-abonnement met labs worden dus automatisch eigenaren van deze labs.</span><span class="sxs-lookup"><span data-stu-id="5bd54-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="5bd54-196">Ze ook eigenaar Hallo VM's en andere resources die zijn gemaakt door Hallo lab van gebruikers en hello Azure DevTest Labs service.</span><span class="sxs-lookup"><span data-stu-id="5bd54-196">They also own hello VMs and other resources created by hello lab's users, and hello Azure DevTest Labs service.</span></span> 

<span data-ttu-id="5bd54-197">U kunt aanvullende eigenaars tooa lab via Hallo labblade toevoegen in Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5bd54-197">You can add additional owners tooa lab via hello lab's blade in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="5bd54-198">Hallo toegevoegd echter van eigenaar in het bereik van beheer beperken dan Hallo abonnement eigenaar scope zijn.</span><span class="sxs-lookup"><span data-stu-id="5bd54-198">However, hello added owner's scope of administration is more narrow than hello subscription owner's scope.</span></span> <span data-ttu-id="5bd54-199">Hallo toegevoegd bijvoorbeeld eigenaars hebben geen volledige toegang toosome Hallo-resources die zijn gemaakt in Hallo abonnement door Hallo DevTest Labs service.</span><span class="sxs-lookup"><span data-stu-id="5bd54-199">For example, hello added owners do not have full access toosome of hello resources that are created in hello subscription by hello DevTest Labs service.</span></span> 

<span data-ttu-id="5bd54-200">tooadd een eigenaar tooan Azure-abonnement, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5bd54-200">tooadd an owner tooan Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="5bd54-201">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5bd54-201">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="5bd54-202">Selecteer **meer Services**, en selecteer vervolgens **abonnementen** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="5bd54-202">Select **More Services**, and then select **Subscriptions** from hello list.</span></span>
3. <span data-ttu-id="5bd54-203">Hallo gewenste abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="5bd54-203">Select hello desired subscription.</span></span>
4. <span data-ttu-id="5bd54-204">Selecteer **toegang** pictogram.</span><span class="sxs-lookup"><span data-stu-id="5bd54-204">Select **Access** icon.</span></span> 
   
    ![-Gebruikers](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="5bd54-206">Op Hallo **gebruikers** blade Selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-206">On hello **Users** blade, select **Add**.</span></span>
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="5bd54-208">Op Hallo **Selecteer een rol** blade Selecteer **eigenaar**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-208">On hello **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="5bd54-209">Op Hallo **gebruikers toevoegen** blade Hallo e-mailadres of de naam invoeren van Hallo gebruiker gewenste tooadd als eigenaar.</span><span class="sxs-lookup"><span data-stu-id="5bd54-209">On hello **Add users** blade, enter hello email address or name of hello user you want tooadd as an owner.</span></span> <span data-ttu-id="5bd54-210">Als het Hallo-gebruiker kan niet worden gevonden, krijgt u een foutbericht weergegeven waarin wordt uitgelegd Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="5bd54-210">If hello user can't be found, you get an error message explaining hello issue.</span></span> <span data-ttu-id="5bd54-211">Als de gebruiker hello wordt gevonden, die gebruiker wordt vermeld onder Hallo **gebruiker** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="5bd54-211">If hello user is found, that user is listed under hello **User** text box.</span></span>
8. <span data-ttu-id="5bd54-212">Selecteer Hallo bevindt gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="5bd54-212">Select hello located user name.</span></span>
9. <span data-ttu-id="5bd54-213">Selecteer **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="5bd54-213">Select **Select**.</span></span>
10. <span data-ttu-id="5bd54-214">Selecteer **OK** tooclose hello **toegang toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="5bd54-214">Select **OK** tooclose hello **Add access** blade.</span></span>
11. <span data-ttu-id="5bd54-215">Als u terugkeert toohello **gebruikers** blade Hallo gebruiker is toegevoegd als een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="5bd54-215">When you return toohello **Users** blade, hello user has been added as an owner.</span></span> <span data-ttu-id="5bd54-216">Deze gebruiker is nu eigenaar van een labs gemaakt onder dit abonnement, en dus kunnen tooperform eigenaar taken.</span><span class="sxs-lookup"><span data-stu-id="5bd54-216">This user is now an owner of any labs created under this subscription, and thus be able tooperform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

