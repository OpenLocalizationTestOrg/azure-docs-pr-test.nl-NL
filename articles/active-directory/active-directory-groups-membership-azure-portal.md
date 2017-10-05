---
title: De groepen die uw groep bij Azure Active Directory behoort beheren | Microsoft Docs
description: Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier volgt deze lidmaatschappen beheren.
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="b0865-104">Beheren welke groepen door een groep behoort in uw Azure Active Directory-tenant</span><span class="sxs-lookup"><span data-stu-id="b0865-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="b0865-105">Groepen kunnen andere Azure Active Directory-groepen bevatten.</span><span class="sxs-lookup"><span data-stu-id="b0865-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="b0865-106">Hier volgt deze lidmaatschappen beheren.</span><span class="sxs-lookup"><span data-stu-id="b0865-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="b0865-107">Hoe kan ik mijn groep deel uit van maakt groepen vinden?</span><span class="sxs-lookup"><span data-stu-id="b0865-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="b0865-108">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="b0865-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="b0865-109">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b0865-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="b0865-111">Op de **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="b0865-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![De blade groepen openen](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="b0865-113">Op de **gebruikers en groepen - alle groepen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="b0865-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="b0865-114">Op de **groep - *groupname***  blade Selecteer **groepslidmaatschappen**.</span><span class="sxs-lookup"><span data-stu-id="b0865-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Openen van de groep lidmaatschappen-blade](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="b0865-116">Uw groep toevoegen als lid van een andere groep, op de **Group - groepslidmaatschappen** blade, selecteer de **toevoegen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="b0865-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="b0865-117">Selecteer een groep in de **groep selecteren** blade en selecteer vervolgens de **Selecteer** knop aan de onderkant van de blade.</span><span class="sxs-lookup"><span data-stu-id="b0865-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="b0865-118">U kunt uw groep toevoegen aan slechts één groep tegelijk.</span><span class="sxs-lookup"><span data-stu-id="b0865-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="b0865-119">De **gebruiker** vak gefilterd op basis van overeenkomst van uw invoer voor een deel van de naam van een gebruiker of het apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b0865-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="b0865-120">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="b0865-120">No wildcard characters are accepted in that box.</span></span>

   ![Geen groepslidmaatschap toevoegen](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="b0865-122">Verwijderen van uw groep als lid van een andere groep voor de **Group - groepslidmaatschappen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="b0865-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="b0865-123">Op de ***groupname*** blade, selecteer de **verwijderen** opdracht in en Bevestig uw keuze bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="b0865-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![lidmaatschap opdracht verwijderen](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="b0865-125">Wanneer u klaar bent met het wijzigen van groepslidmaatschappen voor uw groep, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b0865-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="b0865-126">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="b0865-126">Additional information</span></span>
<span data-ttu-id="b0865-127">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0865-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="b0865-128">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="b0865-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b0865-129">Een nieuwe groep maken en leden toe te voegen</span><span class="sxs-lookup"><span data-stu-id="b0865-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="b0865-130">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="b0865-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="b0865-131">Leden van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="b0865-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="b0865-132">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="b0865-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
