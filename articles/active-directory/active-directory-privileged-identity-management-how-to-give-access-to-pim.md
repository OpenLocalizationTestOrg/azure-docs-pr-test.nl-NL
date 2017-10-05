---
title: Het toegang geven tot Privileged Identity Management - Azure | Microsoft Docs
description: Informatie over het toevoegen van functies voor gebruikers met de extensie Azure Active Directory Privileged Identity Management zodat ze PIM kunnen beheren.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="b167e-103">Geeft toegang tot het beheer van Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b167e-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b167e-104">De hoofdbeheerder die Azure AD Privileged Identity Management (PIM) voor een organisatie automatisch kunt roltoewijzingen en toegang tot PIM ophalen.</span><span class="sxs-lookup"><span data-stu-id="b167e-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="b167e-105">Niemand anders opgehaald schrijftoegang standaard, met inbegrip van andere globale beheerders.</span><span class="sxs-lookup"><span data-stu-id="b167e-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="b167e-106">Andere globale beheerders, Beveiligingsbeheerders en beveiliging lezers hebben alleen-lezen toegang tot Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="b167e-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="b167e-107">Als u wilt toegang geven tot PIM, de eerste gebruiker toewijzen anderen de **beheerder met bevoorrechte rol** rol.</span><span class="sxs-lookup"><span data-stu-id="b167e-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="b167e-108">Deze toewijzing moet worden uitgevoerd in PIM zelf en kan niet worden gewijzigd via PowerShell of andere portals.</span><span class="sxs-lookup"><span data-stu-id="b167e-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="b167e-109">Het beheren van Azure AD PIM Azure MFA is vereist.</span><span class="sxs-lookup"><span data-stu-id="b167e-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="b167e-110">Omdat Microsoft-accounts niet voor Azure MFA registreren, kan niet een gebruiker die zich met een Microsoft-account aanmeldt toegang tot de Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="b167e-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="b167e-111">Zorg ervoor dat er altijd ten minste twee gebruikers in een beheerdersrol bevoorrechte rol als een gebruiker is vergrendeld of hun account is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b167e-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="b167e-112">Geef een andere gebruikerstoegang tot het beheer van PIM</span><span class="sxs-lookup"><span data-stu-id="b167e-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="b167e-113">Aanmelden bij de [Azure-portal](https://portal.azure.com/) en selecteer de **Azure AD Privileged Identity Management** app op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b167e-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="b167e-114">Selecteer **bevoorrechte rollen beheren** > **beheerder met bevoorrechte rol** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b167e-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Toevoegen van bevoorrechte rol administrators - schermafbeelding][1]
3. <span data-ttu-id="b167e-116">Stap 1 is al voltooid op de blade van de beheerde gebruikers toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b167e-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="b167e-117">Selecteer stap 2, **Selecteer gebruikers** en zoek naar de gebruiker die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b167e-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Selecteer de gebruikers - schermafbeelding][2]
4. <span data-ttu-id="b167e-119">Selecteer de gebruiker in de zoekresultaten en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="b167e-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="b167e-120">Klik op **OK** opslaan van uw selectie.</span><span class="sxs-lookup"><span data-stu-id="b167e-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="b167e-121">De gebruiker die u hebt geselecteerd, wordt weergegeven in de lijst met bevoorrechte rol beheerders.</span><span class="sxs-lookup"><span data-stu-id="b167e-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="b167e-122">Wanneer u een nieuwe rol aan iemand toewijst, worden ze automatisch ingesteld als in aanmerking komende om de rol te activeren.</span><span class="sxs-lookup"><span data-stu-id="b167e-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="b167e-123">Als u wilt dat ze in de functie permanent te maken, klikt u op de gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="b167e-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="b167e-124">Selecteer **zorg toeg** in het menu van de gebruiker informatie.</span><span class="sxs-lookup"><span data-stu-id="b167e-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="b167e-125">Verzenden van de gebruiker een koppeling naar [aan de slag met Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b167e-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="b167e-126">Verwijder de toegangsrechten van een andere gebruiker voor het beheren van PIM</span><span class="sxs-lookup"><span data-stu-id="b167e-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="b167e-127">Voordat u uit de rol van bevoorrechte rol administrator verwijderen, zorg er altijd er wordt nog steeds twee gebruikers die zijn toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b167e-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="b167e-128">Klik in het dashboard PIM op de rol **beheerder met bevoorrechte rol**.</span><span class="sxs-lookup"><span data-stu-id="b167e-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="b167e-129">De lijst met gebruikers die momenteel in die rol wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b167e-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="b167e-130">Klik op de gebruiker in de lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b167e-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="b167e-131">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b167e-131">Click on **Remove**.</span></span>  <span data-ttu-id="b167e-132">Een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b167e-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="b167e-133">Klik op **Ja** om de gebruiker verwijderen uit de rol.</span><span class="sxs-lookup"><span data-stu-id="b167e-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b167e-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b167e-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
