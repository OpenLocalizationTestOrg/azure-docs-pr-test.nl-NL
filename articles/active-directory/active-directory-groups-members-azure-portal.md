---
title: aaaManage hello leden voor een groep in Azure Active Directory | Microsoft Docs
description: Hoe tooadd of gebruikers en apparaten verwijderen uit een groep in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="e0f7d-103">Groepslidmaatschap voor gebruikers in uw Azure Active Directory-tenant beheren</span><span class="sxs-lookup"><span data-stu-id="e0f7d-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="e0f7d-104">Dit artikel wordt uitgelegd hoe toomanage Hallo leden voor een groep in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e0f7d-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="e0f7d-105">Hoe ik Hallo leden zoeken en deze beheren?</span><span class="sxs-lookup"><span data-stu-id="e0f7d-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="e0f7d-106">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e0f7d-107">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="e0f7d-109">Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Openen Hallo groepen blade](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="e0f7d-111">Op Hallo **gebruikers en groepen - alle groepen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="e0f7d-112">Op Hallo **groep - *groupname***  blade Selecteer **leden**.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Openen Hallo leden blade](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="e0f7d-114">tooadd leden toohello groep op Hallo **groep - leden** blade Selecteer **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![De opdracht leden toevoegen](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="e0f7d-116">Op Hallo **leden** blade, selecteert u een of meer gebruikers of apparaten tooadd toohello groep en selecteer Hallo **Selecteer** knop Hallo Hallo blade tooadd onder aan deze groep toohello.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="e0f7d-117">Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="e0f7d-118">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="e0f7d-119">tooremove leden uit de groep hello, op Hallo **groep - leden** blade, selecteert u een lid.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="e0f7d-120">Op Hallo ***membername*** blade, selecteer Hallo **verwijderen** opdracht in en Bevestig uw keuze op Hallo-prompt.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Verwijder leden opdracht](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="e0f7d-122">Wanneer u klaar bent met het wijzigen van leden voor Hallo groep, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e0f7d-123">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="e0f7d-123">Additional information</span></span>
<span data-ttu-id="e0f7d-124">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e0f7d-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e0f7d-125">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="e0f7d-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e0f7d-126">Een nieuwe groep maken en leden toe te voegen</span><span class="sxs-lookup"><span data-stu-id="e0f7d-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="e0f7d-127">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="e0f7d-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e0f7d-128">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="e0f7d-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="e0f7d-129">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="e0f7d-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
