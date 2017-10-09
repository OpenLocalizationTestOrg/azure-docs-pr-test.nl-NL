---
title: Toegangsbeheer op basis van aaaRole in hello Azure-portal | Microsoft Docs
description: In het beheer van toegang aan de slag met toegangsbeheer op basis van rollen in hello Azure-Portal. Rol toewijzingen tooassign machtigingen tooyour resources gebruiken.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a><span data-ttu-id="0b524-104">Toegangsbeheer op basis van rollen toomanage toegang tooyour Azure-abonnementresources gebruiken</span><span class="sxs-lookup"><span data-stu-id="0b524-104">Use Role-Based Access Control toomanage access tooyour Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b524-105">Toegang beheren per gebruiker of groep</span><span class="sxs-lookup"><span data-stu-id="0b524-105">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="0b524-106">Toegang beheren per resource</span><span class="sxs-lookup"><span data-stu-id="0b524-106">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="0b524-107">Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over geavanceerd toegangsbeheer voor Azure.</span><span class="sxs-lookup"><span data-stu-id="0b524-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="0b524-108">Met RBAC kunt verleent u alleen Hallo hoeveelheid toegang die gebruikers nodig tooperform hun werk hebben.</span><span class="sxs-lookup"><span data-stu-id="0b524-108">Using RBAC, you can grant only hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="0b524-109">In dit artikel helpt u bij leren werken met RBAC in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0b524-109">This article helps you get up and running with RBAC in hello Azure portal.</span></span> <span data-ttu-id="0b524-110">Zie [Wat is op rollen gebaseerd toegangsbeheer](role-based-access-control-what-is.md) als u meer informatie wilt over het beheren van toegang met RBAC.</span><span class="sxs-lookup"><span data-stu-id="0b524-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="0b524-111">U kunt binnen elk abonnement verlenen up too2000 roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="0b524-111">Within each subscription, you can grant up too2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="0b524-112">Toegang voor weergeven</span><span class="sxs-lookup"><span data-stu-id="0b524-112">View access</span></span>
<span data-ttu-id="0b524-113">U kunt zien wie heeft toegang tot tooa resource, resourcegroep of abonnement op de hoofdblade in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0b524-113">You can see who has access tooa resource, resource group, or subscription from its main blade in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0b524-114">We willen bijvoorbeeld toosee wie toegang tot tooone van onze resourcegroepen heeft:</span><span class="sxs-lookup"><span data-stu-id="0b524-114">For example, we want toosee who has access tooone of our resource groups:</span></span>

1. <span data-ttu-id="0b524-115">Selecteer **resourcegroepen** Hallo navigatiebalk aan de linkerkant Hallo aan.</span><span class="sxs-lookup"><span data-stu-id="0b524-115">Select **Resource groups** in hello navigation bar on hello left.</span></span>  
    <span data-ttu-id="0b524-116">![Resourcegroepen - pictogram](./media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="0b524-116">![Resource groups - icon](./media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="0b524-117">Selecteer Hallo-naam van de resourcegroep Hallo van Hallo **resourcegroepen** blade.</span><span class="sxs-lookup"><span data-stu-id="0b524-117">Select hello name of hello resource group from hello **Resource groups** blade.</span></span>
3. <span data-ttu-id="0b524-118">Selecteer **toegangsbeheer (IAM)** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b524-118">Select **Access control (IAM)** from hello left menu.</span></span>  
4. <span data-ttu-id="0b524-119">Hallo Access control-blade geeft een lijst van alle gebruikers, groepen en toepassingen die toegang toohello resourcegroep hebben gekregen.</span><span class="sxs-lookup"><span data-stu-id="0b524-119">hello Access control blade lists all users, groups, and applications that have been granted access toohello resource group.</span></span>  
   
    ![Schermafbeelding van de blade Gebruikers - overgenomen en toegewezen toegang](./media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="0b524-121">U ziet dat sommige rollen zijn binnen het bereik te**deze resource** terwijl andere **overgenomen** vanuit een ander bereik.</span><span class="sxs-lookup"><span data-stu-id="0b524-121">Notice that some roles are scoped too**This resource** while others are **Inherited** it from another scope.</span></span> <span data-ttu-id="0b524-122">Toegang is specifiek toohello resourcegroep toegewezen of overgenomen van een toewijzing toohello bovenliggende abonnement.</span><span class="sxs-lookup"><span data-stu-id="0b524-122">Access is either assigned specifically toohello resource group or inherited from an assignment toohello parent subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0b524-123">Klassieke abonnementsbeheerders en co-beheerders worden beschouwd als eigenaar van het Hallo-abonnement in Hallo nieuwe RBAC-model.</span><span class="sxs-lookup"><span data-stu-id="0b524-123">Classic subscription admins and co-admins are considered owners of hello subscription in hello new RBAC model.</span></span>

## <a name="add-access"></a><span data-ttu-id="0b524-124">Toegang voor toevoegen</span><span class="sxs-lookup"><span data-stu-id="0b524-124">Add Access</span></span>
<span data-ttu-id="0b524-125">U verleent toegang vanuit het Hallo-resource, resourcegroep of abonnement dat is Hallo omvang van de roltoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b524-125">You grant access from within hello resource, resource group, or subscription that is hello scope of hello role assignment.</span></span>

1. <span data-ttu-id="0b524-126">Selecteer **toevoegen** op Hallo Access control-blade.</span><span class="sxs-lookup"><span data-stu-id="0b524-126">Select **Add** on hello Access control blade.</span></span>  
2. <span data-ttu-id="0b524-127">Selecteer Hallo rol desgewenst tooassign van Hallo **Selecteer een rol** blade.</span><span class="sxs-lookup"><span data-stu-id="0b524-127">Select hello role that you wish tooassign from hello **Select a role** blade.</span></span>
3. <span data-ttu-id="0b524-128">Hallo-gebruiker, groep of toepassing selecteren in uw directory die u toegang tot toogrant wilt.</span><span class="sxs-lookup"><span data-stu-id="0b524-128">Select hello user, group, or application in your directory that you wish toogrant access to.</span></span> <span data-ttu-id="0b524-129">Hallo-directory met weergavenamen, e-mailadressen en object-id's, kunt u zoeken.</span><span class="sxs-lookup"><span data-stu-id="0b524-129">You can search hello directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Schermafbeelding van de blade Gebruikers toevoegen - zoeken](./media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="0b524-131">Selecteer **OK** toocreate Hallo toewijzing.</span><span class="sxs-lookup"><span data-stu-id="0b524-131">Select **OK** toocreate hello assignment.</span></span> <span data-ttu-id="0b524-132">Hallo **gebruiker toevoegen** pop Hallo voortgang bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="0b524-132">hello **Adding user** popup tracks hello progress.</span></span>  
    <span data-ttu-id="0b524-133">![Schermafbeelding van de voortgangsbalk Gebruiker toevoegen](./media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="0b524-133">![Adding user progress bar - screenshot](./media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="0b524-134">Nadat een roltoewijzing is toegevoegd, wordt deze weergegeven op Hallo **gebruikers** blade.</span><span class="sxs-lookup"><span data-stu-id="0b524-134">After successfully adding a role assignment, it will appear on hello **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="0b524-135">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="0b524-135">Remove Access</span></span>
1. <span data-ttu-id="0b524-136">Houd de cursor boven het Hallo-naam van de gewenste tooremove Hallo-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="0b524-136">Hover your cursor over hello name of hello assignment that you want tooremove.</span></span> <span data-ttu-id="0b524-137">Een selectievakje weergegeven naam van de volgende toohello.</span><span class="sxs-lookup"><span data-stu-id="0b524-137">A check box appears next toohello name.</span></span>
2. <span data-ttu-id="0b524-138">Hallo selectievakjes tooselect gebruiken een of meer roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="0b524-138">Use hello check boxes tooselect one or more role assignments.</span></span>
2. <span data-ttu-id="0b524-139">Selecteer **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="0b524-139">Select **Remove**.</span></span>  
3. <span data-ttu-id="0b524-140">Selecteer **Ja** tooconfirm Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0b524-140">Select **Yes** tooconfirm hello removal.</span></span>

<span data-ttu-id="0b524-141">Overgenomen toewijzingen kunnen niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0b524-141">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="0b524-142">Als u een overgenomen toewijzing tooremove nodig hebt, moet u toodo op het Hallo bereik waarin Hallo roltoewijzing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0b524-142">If you need tooremove an inherited assignment, you need toodo it at hello scope where hello role assignment was created.</span></span> <span data-ttu-id="0b524-143">In Hallo **bereik** kolom, het volgende te**overgenomen** er is een koppeling waarmee u toohello resources waaraan deze rol is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="0b524-143">In hello **Scope** column, next too**Inherited** there is a link that takes you toohello resources where this role was assigned.</span></span> <span data-ttu-id="0b524-144">Ga toohello resource vermeld tooremove Hallo roltoewijzing.</span><span class="sxs-lookup"><span data-stu-id="0b524-144">Go toohello resource listed there tooremove hello role assignment.</span></span>

![Schermafbeelding van de blade Gebruikers - bij overgenomen toegang is knop Verwijderen uitgeschakeld](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a><span data-ttu-id="0b524-146">Andere hulpprogramma's voor toomanage toegang</span><span class="sxs-lookup"><span data-stu-id="0b524-146">Other tools toomanage access</span></span>
<span data-ttu-id="0b524-147">U kunt rollen toewijzen en toegang beheren met Azure RBAC-opdrachten in hulpprogramma's dan hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0b524-147">You can assign roles and manage access with Azure RBAC commands in tools other than hello Azure portal.</span></span>  <span data-ttu-id="0b524-148">Volg Hallo koppelingen toolearn meer over Hallo vereisten en aan de slag met hello Azure RBAC-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0b524-148">Follow hello links toolearn more about hello prerequisites and get started with hello Azure RBAC commands.</span></span>

* [<span data-ttu-id="0b524-149">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b524-149">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="0b524-150">Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="0b524-150">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="0b524-151">REST API</span><span class="sxs-lookup"><span data-stu-id="0b524-151">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="0b524-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0b524-152">Next Steps</span></span>
* [<span data-ttu-id="0b524-153">Een geschiedenisrapport voor gewijzigde toegang maken</span><span class="sxs-lookup"><span data-stu-id="0b524-153">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="0b524-154">Zie Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0b524-154">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="0b524-155">Definieer uw eigen [Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="0b524-155">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>

