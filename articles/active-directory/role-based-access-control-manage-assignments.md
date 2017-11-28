---
title: toewijzingen aaaView Azure-resource-access | Microsoft Docs
description: Weergeven en beheren van alle toewijzingen van Hallo toegangsbeheer op basis van rollen voor elke gebruiker of groep in hello Azure-portal
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="e3492-103">Toegang tot toewijzingen weergeven voor gebruikers en groepen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e3492-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3492-104">Toegang beheren per gebruiker of groep</span><span class="sxs-lookup"><span data-stu-id="e3492-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="e3492-105">Toegang beheren per resource</span><span class="sxs-lookup"><span data-stu-id="e3492-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="e3492-106">Met op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure Active Directory (Azure AD), kunt u access tooyour Azure beheren resources.</span><span class="sxs-lookup"><span data-stu-id="e3492-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="e3492-107">Toegang met RBAC toegewezen is fijnmazig omdat er zijn twee manieren kunt u Hallo machtigingen beperken:</span><span class="sxs-lookup"><span data-stu-id="e3492-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="e3492-108">**Bereik:** RBAC-roltoewijzingen zijn binnen het bereik tooa specifiek abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="e3492-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="e3492-109">Een gebruiker toegang tooa één resource krijgt geen toegang tot alle andere resources in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="e3492-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="e3492-110">**Rol:** binnen het bereik van de Hallo van Hallo toewijzing, de toegang wordt teruggebracht nog verder door een rol toewijst.</span><span class="sxs-lookup"><span data-stu-id="e3492-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="e3492-111">Rollen kunnen worden op hoog niveau, zoals eigenaar of specifieke, zoals de lezer van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e3492-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="e3492-112">Rollen kunnen alleen binnen het Hallo-abonnement, resourcegroep of resource die Hallo bereik voor de toewijzing van Hallo worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e3492-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="e3492-113">Maar u kunt alle Hallo toegangstoewijzingen voor een bepaalde gebruiker of groep bekijken op één plaats.</span><span class="sxs-lookup"><span data-stu-id="e3492-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="e3492-114">U kunt up too2000 roltoewijzingen in elk abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="e3492-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="e3492-115">Meer informatie over het te verkrijgen[rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e3492-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="e3492-116">De toewijzingen toegang weergeven</span><span class="sxs-lookup"><span data-stu-id="e3492-116">View access assignments</span></span>
<span data-ttu-id="e3492-117">toolook up Hallo toegangstoewijzingen voor een enkele gebruiker of groep te starten in Azure Active Directory in Hallo [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3492-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="e3492-118">Selecteer **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3492-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="e3492-119">Als deze optie niet zichtbaar in de navigatie-lijst is, selecteert u **meer Services** en schuif omlaag toofind **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3492-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="e3492-120">Selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers** of **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="e3492-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="e3492-121">In dit voorbeeld richten we op afzonderlijke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e3492-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="e3492-122">![Beheren van gebruikers en groepen in Azure Active Directory - schermafbeelding](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="e3492-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="e3492-123">Hallo gebruiker zoeken op naam of gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="e3492-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="e3492-124">Selecteer **Azure-resources** op Hallo gebruiker blade.</span><span class="sxs-lookup"><span data-stu-id="e3492-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="e3492-125">Alle Hallo toegangstoewijzingen voor die gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e3492-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="e3492-126">Leesmachtigingen tooview toewijzingen</span><span class="sxs-lookup"><span data-stu-id="e3492-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="e3492-127">Deze pagina bevat alleen Hallo toegangstoewijzingen u tooread machtiging hebt.</span><span class="sxs-lookup"><span data-stu-id="e3492-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="e3492-128">Bijvoorbeeld: u hebt leestoegang toosubscription A en ga toohello Azure-resources blade toocheck toewijzingen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e3492-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="e3492-129">U kunt zien haar toegangstoewijzingen voor een abonnement, maar niet zien dat zij ook toegangstoewijzingen op abonnement B. heeft</span><span class="sxs-lookup"><span data-stu-id="e3492-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="e3492-130">Toegangstoewijzingen verwijderen</span><span class="sxs-lookup"><span data-stu-id="e3492-130">Delete access assignments</span></span>
<span data-ttu-id="e3492-131">U kunt via deze blade toegangstoewijzingen die rechtstreeks zijn toegewezen tooa gebruiker of groep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3492-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="e3492-132">Als Hallo toegang toewijzing is overgenomen van een bovenliggende groep, kunt u toogo toohello resource of -abonnement nodig hebt en er Hallo-toewijzing te beheren.</span><span class="sxs-lookup"><span data-stu-id="e3492-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="e3492-133">Selecteer Hallo een gewenste toodelete in Hallo lijst van alle Hallo toegangstoewijzingen voor een gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="e3492-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="e3492-134">Selecteer **verwijderen** en vervolgens **Ja** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e3492-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="e3492-135">![Verwijder toegang toewijzing - schermafbeelding](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="e3492-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3492-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3492-136">Next steps</span></span>

* <span data-ttu-id="e3492-137">Aan de slag met toegangsbeheer op basis van rollen te[rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="e3492-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="e3492-138">Zie Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="e3492-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

