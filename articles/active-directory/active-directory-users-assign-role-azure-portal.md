---
title: Een gebruiker toewijzen aan beheerdersrollen in Azure Active Directory | Microsoft Docs
description: Wordt uitgelegd hoe u beheerdersrechten gebruikersgegevens in Azure Active Directory wijzigen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="f8227-103">Een gebruiker toewijzen aan beheerdersrollen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8227-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="f8227-104">In dit artikel wordt uitgelegd hoe een beheerderrol toewijzen aan een gebruiker in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8227-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f8227-105">Zie voor meer informatie over het toevoegen van nieuwe gebruikers in uw organisatie [nieuwe gebruikers toevoegen aan Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f8227-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="f8227-106">Toegevoegde gebruikers hebben standaard geen gebruikersrechten, maar u kunt op elk gewenst moment rollen aan ze toewijzen.</span><span class="sxs-lookup"><span data-stu-id="f8227-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="f8227-107">Een rol toewijzen aan een gebruiker</span><span class="sxs-lookup"><span data-stu-id="f8227-107">Assign a role to a user</span></span>
1. <span data-ttu-id="f8227-108">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="f8227-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="f8227-109">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f8227-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="f8227-111">Op de **gebruikers en groepen** blade Selecteer **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="f8227-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Openen van de blade met alle gebruikers](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="f8227-113">Op de **gebruikers en groepen - alle gebruikers** blade, selecteert u een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="f8227-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="f8227-114">Selecteer op de blade voor de geselecteerde gebruiker **functie Directory**, en vervolgens de gebruiker toewijzen aan een functie uit de **functie Directory** lijst.</span><span class="sxs-lookup"><span data-stu-id="f8227-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="f8227-115">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="f8227-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Een gebruiker toewijzen aan een rol](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="f8227-117">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f8227-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8227-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8227-118">Next steps</span></span>
* [<span data-ttu-id="f8227-119">Een gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="f8227-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="f8227-120">Opnieuw instellen van het wachtwoord van een gebruiker in de nieuwe Azure portal</span><span class="sxs-lookup"><span data-stu-id="f8227-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="f8227-121">Informatie over de werkzaamheden van een gebruiker wijzigen</span><span class="sxs-lookup"><span data-stu-id="f8227-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="f8227-122">Gebruikersprofielen beheren</span><span class="sxs-lookup"><span data-stu-id="f8227-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="f8227-123">Verwijderen van een gebruiker in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8227-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
