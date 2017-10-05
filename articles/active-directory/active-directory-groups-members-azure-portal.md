---
title: De leden voor een groep in Azure Active Directory beheren | Microsoft Docs
description: Toevoegen of verwijderen van gebruikers en apparaten uit een groep in Azure Active Directory
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
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="88337-103">Groepslidmaatschap voor gebruikers in uw Azure Active Directory-tenant beheren</span><span class="sxs-lookup"><span data-stu-id="88337-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="88337-104">In dit artikel wordt uitgelegd hoe u voor het beheren van de leden voor een groep in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88337-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="88337-105">Hoe ik de leden vinden en ze beheren?</span><span class="sxs-lookup"><span data-stu-id="88337-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="88337-106">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="88337-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="88337-107">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="88337-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="88337-109">Op de **gebruikers en groepen** blade Selecteer **alle groepen**.</span><span class="sxs-lookup"><span data-stu-id="88337-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![De blade groepen openen](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="88337-111">Op de **gebruikers en groepen - alle groepen** blade, selecteert u een groep.</span><span class="sxs-lookup"><span data-stu-id="88337-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="88337-112">Op de **groep - *groupname***  blade Selecteer **leden**.</span><span class="sxs-lookup"><span data-stu-id="88337-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![De blade leden openen](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="88337-114">Leden toevoegen aan de groep op de **groep - leden** blade Selecteer **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="88337-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![De opdracht leden toevoegen](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="88337-116">Op de **leden** blade, selecteer een of meer gebruikers of apparaten aan de groep wilt toevoegen en selecteer de **Selecteer** knop aan de onderkant van de blade aan toe te voegen aan de groep.</span><span class="sxs-lookup"><span data-stu-id="88337-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="88337-117">De **gebruiker** vak gefilterd op basis van overeenkomst van uw invoer voor een deel van de naam van een gebruiker of het apparaat weergegeven.</span><span class="sxs-lookup"><span data-stu-id="88337-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="88337-118">Er is geen jokertekens worden in dit vak geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="88337-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="88337-119">Leden verwijderen uit de groep op de **groep - leden** blade, selecteert u een lid.</span><span class="sxs-lookup"><span data-stu-id="88337-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="88337-120">Op de ***membername*** blade, selecteer de **verwijderen** opdracht in en Bevestig uw keuze bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="88337-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Verwijder leden opdracht](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="88337-122">Wanneer u klaar bent met het wijzigen van de leden van de groep, selecteert u **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="88337-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="88337-123">Aanvullende informatie</span><span class="sxs-lookup"><span data-stu-id="88337-123">Additional information</span></span>
<span data-ttu-id="88337-124">Deze artikelen bevatten aanvullende informatie over Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="88337-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="88337-125">Zie de bestaande groepen</span><span class="sxs-lookup"><span data-stu-id="88337-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="88337-126">Een nieuwe groep maken en leden toe te voegen</span><span class="sxs-lookup"><span data-stu-id="88337-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="88337-127">Instellingen van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="88337-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="88337-128">Lidmaatschap van een groep beheren</span><span class="sxs-lookup"><span data-stu-id="88337-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="88337-129">Dynamische regels voor gebruikers in een groep beheren</span><span class="sxs-lookup"><span data-stu-id="88337-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
