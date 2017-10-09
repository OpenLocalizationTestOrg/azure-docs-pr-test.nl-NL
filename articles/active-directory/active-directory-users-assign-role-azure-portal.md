---
title: een gebruiker aaaAssign tooadministrator rollen in Azure Active Directory | Microsoft Docs
description: Legt uit hoe toochange beheerdersrechten gebruikersgegevens in Azure Active Directory
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
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a><span data-ttu-id="6e527-103">Een gebruiker toewijzen tooadministrator rollen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e527-103">Assign a user tooadministrator roles in Azure Active Directory</span></span>
<span data-ttu-id="6e527-104">Dit artikel wordt uitgelegd hoe tooassign een gebruiker met beheerdersrechten rol tooa in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e527-104">This article explains how tooassign an administrative role tooa user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6e527-105">Zie voor meer informatie over het toevoegen van nieuwe gebruikers in uw organisatie [toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6e527-105">For information about adding new users in your organization, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="6e527-106">Toegevoegde gebruikers hebben geen beheerdersrechten standaard, maar u kunt functies toothem toewijzen op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="6e527-106">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="6e527-107">Een rol tooa gebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="6e527-107">Assign a role tooa user</span></span>
1. <span data-ttu-id="6e527-108">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="6e527-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="6e527-109">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6e527-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Gebruikersbeheer openen](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="6e527-111">Op Hallo **gebruikers en groepen** blade Selecteer **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="6e527-111">On hello **Users and groups** blade, select **All users**.</span></span>

   ![Openen Hallo blade voor alle gebruikers](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="6e527-113">Op Hallo **gebruikers en groepen - alle gebruikers** blade, selecteert u een gebruiker in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e527-113">On hello **Users and groups - All users** blade, select a user from hello list.</span></span>
5. <span data-ttu-id="6e527-114">Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **functie Directory**, en wijs de gebruikersrol tooa Hallo van Hallo **functie Directory** lijst.</span><span class="sxs-lookup"><span data-stu-id="6e527-114">On hello blade for hello selected user, select **Directory role**, and then assign hello user tooa role from hello **Directory role** list.</span></span> <span data-ttu-id="6e527-115">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="6e527-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Een gebruikersrol tooa toewijzen](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="6e527-117">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e527-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e527-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e527-118">Next steps</span></span>
* [<span data-ttu-id="6e527-119">Een gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e527-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="6e527-120">Wachtwoord van een gebruiker in de nieuwe Azure portal Hallo opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6e527-120">Reset a user's password in hello new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="6e527-121">Informatie over de werkzaamheden van een gebruiker wijzigen</span><span class="sxs-lookup"><span data-stu-id="6e527-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="6e527-122">Gebruikersprofielen beheren</span><span class="sxs-lookup"><span data-stu-id="6e527-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="6e527-123">Verwijderen van een gebruiker in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e527-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
