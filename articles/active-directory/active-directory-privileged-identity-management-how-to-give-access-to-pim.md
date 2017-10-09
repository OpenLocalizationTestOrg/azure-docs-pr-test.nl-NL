---
title: aaaHow toogive toegang tooPrivileged Identity Management - Azure | Microsoft Docs
description: Meer informatie over hoe tooadd rollen toousers met Azure Active Directory Privileged Identity Management-extensie Hallo zodat ze PIM kunnen beheren.
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
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="4a33e-103">Geeft toegang tot toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="4a33e-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="4a33e-104">Hallo-hoofdbeheerder die Azure AD Privileged Identity Management (PIM) voor een organisatie automatisch kunt roltoewijzingen ophalen en toegang tot tooPIM.</span><span class="sxs-lookup"><span data-stu-id="4a33e-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="4a33e-105">Niemand anders opgehaald schrijftoegang standaard, met inbegrip van andere globale beheerders.</span><span class="sxs-lookup"><span data-stu-id="4a33e-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="4a33e-106">Andere globale beheerders, Beveiligingsbeheerders en beveiliging lezers hebben alleen-lezentoegang tooAzure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="4a33e-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="4a33e-107">toogive toegang tooPIM, die de eerste gebruiker Hallo kunt toewijzen anderen toohello **beheerder met bevoorrechte rol** rol.</span><span class="sxs-lookup"><span data-stu-id="4a33e-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="4a33e-108">Deze toewijzing moet worden uitgevoerd in PIM zelf en kan niet worden gewijzigd via PowerShell of andere portals.</span><span class="sxs-lookup"><span data-stu-id="4a33e-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="4a33e-109">Het beheren van Azure AD PIM Azure MFA is vereist.</span><span class="sxs-lookup"><span data-stu-id="4a33e-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="4a33e-110">Omdat Microsoft-accounts niet voor Azure MFA registreren, kan niet een gebruiker die zich met een Microsoft-account aanmeldt toegang tot de Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="4a33e-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="4a33e-111">Zorg ervoor dat er altijd ten minste twee gebruikers in een beheerdersrol bevoorrechte rol als een gebruiker is vergrendeld of hun account is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4a33e-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="4a33e-112">Geef een andere gebruiker toegang toomanage PIM</span><span class="sxs-lookup"><span data-stu-id="4a33e-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="4a33e-113">Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo **Azure AD Privileged Identity Management** app op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="4a33e-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="4a33e-114">Selecteer **bevoorrechte rollen beheren** > **beheerder met bevoorrechte rol** > **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4a33e-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Toevoegen van bevoorrechte rol administrators - schermafbeelding][1]
3. <span data-ttu-id="4a33e-116">Stap 1 is al voltooid op Hallo toevoegen beheerde gebruikers blade.</span><span class="sxs-lookup"><span data-stu-id="4a33e-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="4a33e-117">Selecteer stap 2, **Selecteer gebruikers** en de zoekcriteria voor Hallo gebruiker gewenste tooadd.</span><span class="sxs-lookup"><span data-stu-id="4a33e-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Selecteer de gebruikers - schermafbeelding][2]
4. <span data-ttu-id="4a33e-119">Selecteer Hallo gebruiker in de zoekresultaten Hallo en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="4a33e-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="4a33e-120">Klik op **OK** toosave uw selectie.</span><span class="sxs-lookup"><span data-stu-id="4a33e-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="4a33e-121">Hallo-gebruiker die u hebt geselecteerd worden weergegeven in de lijst Hallo bevoorrechte rol beheerders.</span><span class="sxs-lookup"><span data-stu-id="4a33e-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="4a33e-122">Wanneer u een nieuwe rol toosomeone toewijst, worden ze automatisch ingesteld als in aanmerking komende tooactivate Hallo rol.</span><span class="sxs-lookup"><span data-stu-id="4a33e-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="4a33e-123">Als u wilt dat toomake ze permanent in de rol hello, klikt u op Hallo-gebruiker in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a33e-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="4a33e-124">Selecteer **zorg toeg** in het menu van Hallo gebruiker informatie.</span><span class="sxs-lookup"><span data-stu-id="4a33e-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="4a33e-125">Hallo-gebruiker te een koppeling sturen[aan de slag met Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a33e-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="4a33e-126">Verwijder de toegangsrechten van een andere gebruiker voor het beheren van PIM</span><span class="sxs-lookup"><span data-stu-id="4a33e-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="4a33e-127">Voordat u uit rol van Hallo bevoorrechte rol beheerder verwijderen, zorg er altijd er wordt nog steeds twee gebruikers tooit toegewezen.</span><span class="sxs-lookup"><span data-stu-id="4a33e-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="4a33e-128">Hallo PIM-dashboard, klik op Hallo rol **beheerder met bevoorrechte rol**.</span><span class="sxs-lookup"><span data-stu-id="4a33e-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="4a33e-129">Hallo-lijst met gebruikers in die rol momenteel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4a33e-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="4a33e-130">Klik op het Hallo-gebruiker in de gebruikerslijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a33e-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="4a33e-131">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="4a33e-131">Click on **Remove**.</span></span>  <span data-ttu-id="4a33e-132">Een bevestigingsbericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4a33e-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="4a33e-133">Klik op **Ja** tooremove Hallo gebruiker uit Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="4a33e-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="4a33e-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a33e-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
