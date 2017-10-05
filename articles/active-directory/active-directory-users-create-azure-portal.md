---
title: Nieuwe gebruikers toevoegen aan Azure Active Directory | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u nieuwe gebruikers kunt toevoegen of gebruikersinformatie kunt wijzigen in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a><span data-ttu-id="37034-103">Nieuwe gebruikers toevoegen aan Azure Active Directory (Engelstalig artikel)</span><span class="sxs-lookup"><span data-stu-id="37034-103">Add new users to Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37034-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="37034-104">Azure portal</span></span>](active-directory-users-create-azure-portal.md)
> * [<span data-ttu-id="37034-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="37034-105">Azure classic portal</span></span>](active-directory-create-users.md)
>
>

<span data-ttu-id="37034-106">In dit artikel wordt uitgelegd hoe u nieuwe gebruikers toevoegen in uw organisatie in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37034-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD).</span></span> 

1. <span data-ttu-id="37034-107">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="37034-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="37034-108">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="37034-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Openen gebruikers en groepen](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="37034-110">Op de **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="37034-110">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![De opdracht Add selecteren](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="37034-112">Voer details voor de gebruiker, zoals **naam** en **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="37034-112">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="37034-113">Het domeingedeelte van de naam van de gebruikersnaam moet de eerste standaarddomeinnaam domain name 'foo.onmicrosoft.com' of een geverifieerde, niet-gefedereerde domeinnaam zoals 'contoso.com'.</span><span class="sxs-lookup"><span data-stu-id="37034-113">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="37034-114">Kopieer of het wachtwoord van de gebruiker gegenereerde anders opmerking zodat u deze informatie aan de gebruiker verstrekt kunt nadat dit proces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="37034-114">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="37034-115">U kunt desgewenst openen en vul de informatie in de **profiel** blade de **groepen** blade of de **functie Directory** blade voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="37034-115">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="37034-116">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="37034-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="37034-117">Op de **gebruiker** blade Selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="37034-117">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="37034-118">Het gegenereerde wachtwoord naar de nieuwe gebruiker veilig distribueren zodat de gebruiker zich kan aanmelden.</span><span class="sxs-lookup"><span data-stu-id="37034-118">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="37034-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37034-119">Next steps</span></span>
* [<span data-ttu-id="37034-120">Een externe gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="37034-120">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="37034-121">Opnieuw instellen van het wachtwoord van een gebruiker in de nieuwe Azure portal</span><span class="sxs-lookup"><span data-stu-id="37034-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="37034-122">Informatie over de werkzaamheden van een gebruiker wijzigen</span><span class="sxs-lookup"><span data-stu-id="37034-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="37034-123">Gebruikersprofielen beheren</span><span class="sxs-lookup"><span data-stu-id="37034-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="37034-124">Verwijderen van een gebruiker in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="37034-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="37034-125">Een gebruiker toewijzen aan een rol in uw Azure AD</span><span class="sxs-lookup"><span data-stu-id="37034-125">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
