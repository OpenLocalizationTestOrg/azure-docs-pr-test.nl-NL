---
title: Eigenaars- en gebruikers toevoegen in Azure DevTest Labs | Microsoft Docs
description: Eigenaars- en gebruikers toevoegen in Azure DevTest Labs met de Azure-portal of PowerShell
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
ms.openlocfilehash: d67fa257574d6cb4ad4b18521900374fb51da290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="df24f-103">Eigenaars- en gebruikers toevoegen in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="df24f-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="df24f-104">Toegang in Azure DevTest Labs wordt beheerd door [gebaseerd toegangsbeheer (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="df24f-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="df24f-105">Met RBAC kunt kunt u taken scheiden binnen uw team in *rollen* waar u de hoeveelheid toegang nodig is voor gebruikers voor het uitvoeren van hun taken verlenen.</span><span class="sxs-lookup"><span data-stu-id="df24f-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="df24f-106">Drie van deze RBAC-rollen zijn *eigenaar*, *DevTest Labs gebruiker*, en *Inzender*.</span><span class="sxs-lookup"><span data-stu-id="df24f-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="df24f-107">In dit artikel leert u welke acties kunnen worden uitgevoerd in elk van de drie belangrijkste RBAC-rollen.</span><span class="sxs-lookup"><span data-stu-id="df24f-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="df24f-108">Van daaruit u meer informatie over hoe u gebruikers toevoegen aan een lab - zowel via de portal en via een PowerShell-script en gebruikers toevoegen op het abonnementsniveau.</span><span class="sxs-lookup"><span data-stu-id="df24f-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="df24f-109">Acties die kunnen worden uitgevoerd in elke rol</span><span class="sxs-lookup"><span data-stu-id="df24f-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="df24f-110">Er zijn drie belangrijkste rollen kunt u een gebruiker toewijzen:</span><span class="sxs-lookup"><span data-stu-id="df24f-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="df24f-111">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="df24f-111">Owner</span></span>
* <span data-ttu-id="df24f-112">DevTest Labs gebruiker</span><span class="sxs-lookup"><span data-stu-id="df24f-112">DevTest Labs User</span></span>
* <span data-ttu-id="df24f-113">Inzender</span><span class="sxs-lookup"><span data-stu-id="df24f-113">Contributor</span></span>

<span data-ttu-id="df24f-114">De volgende tabel ziet u de acties die kunnen worden uitgevoerd door gebruikers in elk van deze rollen:</span><span class="sxs-lookup"><span data-stu-id="df24f-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="df24f-115">**Gebruikers met deze rol acties kunnen uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="df24f-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="df24f-116">**DevTest Labs gebruiker**</span><span class="sxs-lookup"><span data-stu-id="df24f-116">**DevTest Labs User**</span></span> | <span data-ttu-id="df24f-117">**Eigenaar**</span><span class="sxs-lookup"><span data-stu-id="df24f-117">**Owner**</span></span> | <span data-ttu-id="df24f-118">**Inzender**</span><span class="sxs-lookup"><span data-stu-id="df24f-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df24f-119">**Taken voor het testlab**</span><span class="sxs-lookup"><span data-stu-id="df24f-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="df24f-120">Gebruikers toevoegen aan een lab</span><span class="sxs-lookup"><span data-stu-id="df24f-120">Add users to a lab</span></span> |<span data-ttu-id="df24f-121">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-121">No</span></span> |<span data-ttu-id="df24f-122">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-122">Yes</span></span> |<span data-ttu-id="df24f-123">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-123">No</span></span> |
| <span data-ttu-id="df24f-124">Update-instellingen</span><span class="sxs-lookup"><span data-stu-id="df24f-124">Update cost settings</span></span> |<span data-ttu-id="df24f-125">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-125">No</span></span> |<span data-ttu-id="df24f-126">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-126">Yes</span></span> |<span data-ttu-id="df24f-127">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-127">Yes</span></span> |
| <span data-ttu-id="df24f-128">**Basis VM-taken**</span><span class="sxs-lookup"><span data-stu-id="df24f-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="df24f-129">Toevoegen en verwijderen van aangepaste installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="df24f-129">Add and remove custom images</span></span> |<span data-ttu-id="df24f-130">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-130">No</span></span> |<span data-ttu-id="df24f-131">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-131">Yes</span></span> |<span data-ttu-id="df24f-132">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-132">Yes</span></span> |
| <span data-ttu-id="df24f-133">Toevoegen, bijwerken en verwijderen van formules</span><span class="sxs-lookup"><span data-stu-id="df24f-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="df24f-134">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-134">Yes</span></span> |<span data-ttu-id="df24f-135">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-135">Yes</span></span> |<span data-ttu-id="df24f-136">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-136">Yes</span></span> |
| <span data-ttu-id="df24f-137">Geaccepteerde Azure Marketplace-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="df24f-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="df24f-138">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-138">No</span></span> |<span data-ttu-id="df24f-139">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-139">Yes</span></span> |<span data-ttu-id="df24f-140">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-140">Yes</span></span> |
| <span data-ttu-id="df24f-141">**VM-taken**</span><span class="sxs-lookup"><span data-stu-id="df24f-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="df24f-142">Virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="df24f-142">Create VMs</span></span> |<span data-ttu-id="df24f-143">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-143">Yes</span></span> |<span data-ttu-id="df24f-144">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-144">Yes</span></span> |<span data-ttu-id="df24f-145">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-145">Yes</span></span> |
| <span data-ttu-id="df24f-146">Starten, stoppen en verwijderen van virtuele machines</span><span class="sxs-lookup"><span data-stu-id="df24f-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="df24f-147">Alleen virtuele machines die zijn gemaakt door de gebruiker</span><span class="sxs-lookup"><span data-stu-id="df24f-147">Only VMs created by the user</span></span> |<span data-ttu-id="df24f-148">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-148">Yes</span></span> |<span data-ttu-id="df24f-149">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-149">Yes</span></span> |
| <span data-ttu-id="df24f-150">Beleidsregels voor virtuele machine bijwerken</span><span class="sxs-lookup"><span data-stu-id="df24f-150">Update VM policies</span></span> |<span data-ttu-id="df24f-151">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-151">No</span></span> |<span data-ttu-id="df24f-152">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-152">Yes</span></span> |<span data-ttu-id="df24f-153">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-153">Yes</span></span> |
| <span data-ttu-id="df24f-154">Gegevensschijven van VM's toevoegen of verwijderen</span><span class="sxs-lookup"><span data-stu-id="df24f-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="df24f-155">Alleen virtuele machines die zijn gemaakt door de gebruiker</span><span class="sxs-lookup"><span data-stu-id="df24f-155">Only VMs created by the user</span></span> |<span data-ttu-id="df24f-156">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-156">Yes</span></span> |<span data-ttu-id="df24f-157">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-157">Yes</span></span> |
| <span data-ttu-id="df24f-158">**Taken van artefacten**</span><span class="sxs-lookup"><span data-stu-id="df24f-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="df24f-159">Toevoegen en verwijderen van artefacten opslagplaatsen</span><span class="sxs-lookup"><span data-stu-id="df24f-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="df24f-160">Nee</span><span class="sxs-lookup"><span data-stu-id="df24f-160">No</span></span> |<span data-ttu-id="df24f-161">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-161">Yes</span></span> |<span data-ttu-id="df24f-162">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-162">Yes</span></span> |
| <span data-ttu-id="df24f-163">Toepassen van artefacten</span><span class="sxs-lookup"><span data-stu-id="df24f-163">Apply artifacts</span></span> |<span data-ttu-id="df24f-164">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-164">Yes</span></span> |<span data-ttu-id="df24f-165">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-165">Yes</span></span> |<span data-ttu-id="df24f-166">Ja</span><span class="sxs-lookup"><span data-stu-id="df24f-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="df24f-167">Wanneer een gebruiker een virtuele machine maakt, wordt die gebruiker automatisch toegewezen aan de **eigenaar** rol van de gemaakte virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="df24f-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="df24f-168">Toevoegen van een eigenaar of gebruiker op het niveau van het lab</span><span class="sxs-lookup"><span data-stu-id="df24f-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="df24f-169">Eigenaars- en gebruikers kunnen worden toegevoegd op het niveau van het lab via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="df24f-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="df24f-170">Dit omvat externe gebruikers met een geldig [Microsoft-account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="df24f-170">This includes external users with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="df24f-171">De volgende stappen begeleiden u bij het proces van een eigenaar of gebruiker toevoegen aan een lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="df24f-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="df24f-172">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="df24f-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="df24f-173">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="df24f-173">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="df24f-174">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="df24f-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="df24f-175">Selecteer op de labblade **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="df24f-175">On the lab's blade, select **Configuration**.</span></span> 
5. <span data-ttu-id="df24f-176">Op de **configuratie** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="df24f-176">On the **Configuration** blade, select **Users**.</span></span>
6. <span data-ttu-id="df24f-177">Op de **gebruikers** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df24f-177">On the **Users** blade, select **+Add**.</span></span>
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
7. <span data-ttu-id="df24f-179">Op de **Selecteer een rol** blade, selecteer de gewenste rol.</span><span class="sxs-lookup"><span data-stu-id="df24f-179">On the **Select a role** blade, select the desired role.</span></span> <span data-ttu-id="df24f-180">De sectie [acties die kunnen worden uitgevoerd in elke rol](#actions-that-can-be-performed-in-each-role) staan de verschillende acties die kunnen worden uitgevoerd door gebruikers met de eigenaar, DevTest gebruiker en Inzender rollen.</span><span class="sxs-lookup"><span data-stu-id="df24f-180">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
8. <span data-ttu-id="df24f-181">Op de **gebruikers toevoegen** blade, voer het e-mailadres of de naam van de gebruiker die u wilt toevoegen in de rol die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="df24f-181">On the **Add users** blade, enter the email address or name of the user you want to add in the role you specified.</span></span> <span data-ttu-id="df24f-182">Als de gebruiker kan niet worden gevonden, wordt het probleem uitgelegd in een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="df24f-182">If the user can't be found, an error message explains the issue.</span></span> <span data-ttu-id="df24f-183">Als de gebruiker wordt gevonden, wordt die gebruiker weergegeven en geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="df24f-183">If the user is found, that user is listed and selected.</span></span> 
9. <span data-ttu-id="df24f-184">Selecteer **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="df24f-184">Select **Select**.</span></span>
10. <span data-ttu-id="df24f-185">Selecteer **OK** sluiten de **toegang toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="df24f-185">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="df24f-186">Als u terugkeert naar de **gebruikers** blade de gebruiker is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="df24f-186">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="df24f-187">Een externe gebruiker toevoegen aan een testomgeving met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="df24f-187">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="df24f-188">Naast het toevoegen van gebruikers in de Azure portal, kunt u een externe gebruiker toevoegen aan uw testomgeving met een PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="df24f-188">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="df24f-189">In het volgende voorbeeld wijzigt u gewoon de parameterwaarden onder de **waarden wijzigen** opmerking.</span><span class="sxs-lookup"><span data-stu-id="df24f-189">In the following example, simply modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="df24f-190">U kunt ophalen de `subscriptionId`, `labResourceGroup`, en `labName` waarden uit de labblade in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="df24f-190">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="df24f-191">Het voorbeeldscript wordt ervan uitgegaan dat de opgegeven gebruiker is als Gast toegevoegd aan de Active Directory en mislukt als dit niet het geval is.</span><span class="sxs-lookup"><span data-stu-id="df24f-191">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="df24f-192">Als u wilt een gebruiker niet in de Active Directory toevoegt aan een lab, kunt u de Azure portal gebruiken voor de gebruiker toewijzen aan een rol, zoals geïllustreerd in de sectie [een eigenaar of gebruiker toevoegen op het niveau van het lab](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="df24f-192">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/en-us/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Login-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="df24f-193">Toevoegen van een eigenaar of gebruiker op het abonnementsniveau</span><span class="sxs-lookup"><span data-stu-id="df24f-193">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="df24f-194">Azure machtigingen zijn doorgegeven van bovenliggende bereik aan het onderliggende bereik in Azure.</span><span class="sxs-lookup"><span data-stu-id="df24f-194">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="df24f-195">Eigenaren van een Azure-abonnement met labs worden dus automatisch eigenaren van deze labs.</span><span class="sxs-lookup"><span data-stu-id="df24f-195">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="df24f-196">Ze ook eigenaar van de virtuele machines en andere resources die zijn gemaakt door gebruikers van de testomgeving en de service Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="df24f-196">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="df24f-197">U kunt aanvullende eigenaars toevoegen aan een lab via de labblade in de [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="df24f-197">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="df24f-198">De toegevoegde eigenaar bereik van beheer is echter beperken dan bereik van de eigenaar van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="df24f-198">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="df24f-199">Bijvoorbeeld, de eigenaren van de toegevoegde geen volledige toegang tot sommige van de resources die door de service DevTest Labs in het abonnement worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="df24f-199">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="df24f-200">Als u wilt een eigenaar toevoegen aan een Azure-abonnement, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="df24f-200">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="df24f-201">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="df24f-201">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="df24f-202">Selecteer **meer Services**, en selecteer vervolgens **abonnementen** uit de lijst.</span><span class="sxs-lookup"><span data-stu-id="df24f-202">Select **More Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="df24f-203">Selecteer het gewenste abonnement.</span><span class="sxs-lookup"><span data-stu-id="df24f-203">Select the desired subscription.</span></span>
4. <span data-ttu-id="df24f-204">Selecteer **toegang** pictogram.</span><span class="sxs-lookup"><span data-stu-id="df24f-204">Select **Access** icon.</span></span> 
   
    ![-Gebruikers](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="df24f-206">Op de **gebruikers** blade Selecteer **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df24f-206">On the **Users** blade, select **Add**.</span></span>
   
    ![Gebruiker toevoegen](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="df24f-208">Op de **Selecteer een rol** blade Selecteer **eigenaar**.</span><span class="sxs-lookup"><span data-stu-id="df24f-208">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="df24f-209">Op de **gebruikers toevoegen** blade, voer het e-mailadres of de naam van de gebruiker die u wilt toevoegen als een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="df24f-209">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="df24f-210">Als de gebruiker kan niet worden gevonden, krijgt u een foutbericht weergegeven waarin wordt uitgelegd van het probleem.</span><span class="sxs-lookup"><span data-stu-id="df24f-210">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="df24f-211">Als de gebruiker wordt gevonden, wordt die gebruiker vermeld in de **gebruiker** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="df24f-211">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="df24f-212">Selecteer de gebruikersnaam bevindt.</span><span class="sxs-lookup"><span data-stu-id="df24f-212">Select the located user name.</span></span>
9. <span data-ttu-id="df24f-213">Selecteer **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="df24f-213">Select **Select**.</span></span>
10. <span data-ttu-id="df24f-214">Selecteer **OK** sluiten de **toegang toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="df24f-214">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="df24f-215">Als u terugkeert naar de **gebruikers** blade de gebruiker is toegevoegd als een eigenaar.</span><span class="sxs-lookup"><span data-stu-id="df24f-215">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="df24f-216">Deze gebruiker is nu eigenaar van een labs gemaakt onder dit abonnement, en dus mogelijk eigenaar taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="df24f-216">This user is now an owner of any labs created under this subscription, and thus be able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

