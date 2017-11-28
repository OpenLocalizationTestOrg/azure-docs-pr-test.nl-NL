---
title: aaaManage hello groepen uw groep behoort tooin Azure Active Directory | Microsoft Docs
description: Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier ziet u hoe toomanage deze lidmaatschappen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="4d58b-104">Toowhich groepen die deel uitmaakt van een groep in uw Azure Active Directory-tenant beheren</span><span class="sxs-lookup"><span data-stu-id="4d58b-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="4d58b-105">Groepen kunnen andere Azure Active Directory-groepen bevatten.</span><span class="sxs-lookup"><span data-stu-id="4d58b-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="4d58b-106">Hier ziet u hoe toomanage deze lidmaatschappen.</span><span class="sxs-lookup"><span data-stu-id="4d58b-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="4d58b-107">Hoe kan ik mijn groep deel uit van maakt Hallo-groepen vinden?</span><span class="sxs-lookup"><span data-stu-id="4d58b-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="4d58b-108">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="4d58b-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="4d58b-109">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4d58b-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="4d58b-111">Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="4d58b-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Openen Hallo groepen blade](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="4d58b-113">Op Hallo **gebruikers en groepen - alle groepen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="4d58b-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="4d58b-114">Op Hallo **groep - *groupname***  blade Selecteer **groepslidmaatschappen**.</span><span class="sxs-lookup"><span data-stu-id="4d58b-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Blade met lidmaatschappen Hallo openen](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="4d58b-116">tooadd uw groep als lid van een andere groep, op Hallo **Group - groepslidmaatschappen** blade, selecteer Hallo **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="4d58b-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="4d58b-117">Selecteer een groep in Hallo **groep selecteren** blade en selecteer vervolgens Hallo **Selecteer** knop Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="4d58b-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="4d58b-118">U kunt uw tooonly één groep tegelijk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d58b-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="4d58b-119">Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat.</span><span class="sxs-lookup"><span data-stu-id="4d58b-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="4d58b-120">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="4d58b-120">No wildcard characters are accepted in that box.</span></span>

   ![Geen groepslidmaatschap toevoegen](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="4d58b-122">tooremove uw groep als lid van een andere groep, op Hallo **Group - groepslidmaatschappen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="4d58b-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="4d58b-123">Op Hallo ***groupname*** blade, selecteer Hallo **verwijderen** opdracht in en Bevestig uw keuze op Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="4d58b-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![lidmaatschap opdracht verwijderen](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="4d58b-125">Wanneer u klaar bent met het wijzigen van groepslidmaatschappen voor uw groep, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4d58b-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="4d58b-126">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="4d58b-126">Additional information</span></span>
<span data-ttu-id="4d58b-127">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4d58b-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4d58b-128">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="4d58b-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4d58b-129">Een nieuwe groep maken en leden toe te voegen</span><span class="sxs-lookup"><span data-stu-id="4d58b-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="4d58b-130">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4d58b-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="4d58b-131">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4d58b-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="4d58b-132">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="4d58b-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
