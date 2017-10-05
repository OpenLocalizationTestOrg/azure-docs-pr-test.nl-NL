---
title: Toevoegen of verwijderen van een gebruikersrol | Microsoft Docs
description: Informatie over het toevoegen van functies aan bevoegde identiteiten met de Azure Active Directory Privileged Identity Management-toepassing.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: 3ac07bb7b070f44595c099a454b3d0dbc66126c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-privileged-identity-management-how-to-add-or-remove-a-user-role"></a><span data-ttu-id="66ac6-103">Azure AD Privileged Identity Management: Hoe kan ik een gebruiker toevoegen of verwijderen?</span><span class="sxs-lookup"><span data-stu-id="66ac6-103">Azure AD Privileged Identity Management: How to add or remove a user role</span></span>
<span data-ttu-id="66ac6-104">Met Azure Active Directory (AD), een algemeen beheerder (of bedrijfsbeheerder) kunt bijwerken die gebruikers **permanent** toegewezen aan rollen in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66ac6-104">With Azure Active Directory (AD), a global administrator (or company administrator) can update which users are **permanently** assigned to roles in Azure AD.</span></span> <span data-ttu-id="66ac6-105">Dit wordt gedaan met PowerShell-cmdlets, zoals `Add-MsolRoleMember` en `Remove-MsolRoleMember`.</span><span class="sxs-lookup"><span data-stu-id="66ac6-105">This is done with PowerShell cmdlets like `Add-MsolRoleMember` and `Remove-MsolRoleMember`.</span></span> <span data-ttu-id="66ac6-106">Of ze kunnen de klassieke Azure portal gebruiken, zoals beschreven in [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="66ac6-106">Or they can use the Azure classic portal as described in [assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="66ac6-107">De Azure AD Privileged Identity Management-toepassing kan bevoorrechte rol beheerders ook permanente roltoewijzingen maken.</span><span class="sxs-lookup"><span data-stu-id="66ac6-107">The Azure AD Privileged Identity Management application allows privileged role administrators to make permanent role assignments, as well.</span></span> <span data-ttu-id="66ac6-108">Bovendien bevoorrechte rol administrators gebruikers kunnen aanbrengen **in aanmerking komende** voor beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="66ac6-108">Additionally, privileged role administrators can make users **eligible** for admin roles.</span></span> <span data-ttu-id="66ac6-109">Een in aanmerking komende beheerder kan de rol activeren wanneer nodig en vervolgens hun machtigingen verlopen zodra ze klaar bent.</span><span class="sxs-lookup"><span data-stu-id="66ac6-109">An eligible admin can activate the role when they need it, and then their permissions expire once they're done.</span></span>

## <a name="manage-roles-with-pim-in-the-azure-portal"></a><span data-ttu-id="66ac6-110">Rollen met PIM in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="66ac6-110">Manage roles with PIM in the Azure portal</span></span>
<span data-ttu-id="66ac6-111">In uw organisatie, kunt u gebruikers toewijzen aan andere beheerdersrollen in Azure AD, Office 365 en andere Microsoft-services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="66ac6-111">In your organization, you can assign users to different administrative roles in Azure AD, Office 365, and other Microsoft services and applications.</span></span>  <span data-ttu-id="66ac6-112">Meer informatie over de beschikbare rollen kunnen worden gevonden op [rollen in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span><span class="sxs-lookup"><span data-stu-id="66ac6-112">More details on the available roles can be found at [Roles in Azure AD PIM](active-directory-privileged-identity-management-roles.md).</span></span>

<span data-ttu-id="66ac6-113">Als u wilt toevoegen of verwijderen van een gebruiker een rol met Privileged Identity Management, online zetten van de PIM-dashboard.</span><span class="sxs-lookup"><span data-stu-id="66ac6-113">To add or remove a user in a role using Privileged Identity Management, bring up the PIM dashboard.</span></span> <span data-ttu-id="66ac6-114">Klik vervolgens op de **gebruikers in beheerdersrollen** knop of Selecteer een specifieke rol (zoals hoofdbeheerder) uit de tabel functies.</span><span class="sxs-lookup"><span data-stu-id="66ac6-114">Then either click the **Users in Admin Roles** button, or select a specific role (such as Global Administrator) from the roles table.</span></span>

> [!NOTE]
> <span data-ttu-id="66ac6-115">Als u nog PIM in de Azure portal dat nog niet hebt ingeschakeld, gaat u naar [aan de slag met Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="66ac6-115">If you haven't enabled PIM in the Azure portal yet, go to [Get started with Azure AD PIM](active-directory-privileged-identity-management-getting-started.md) for details.</span></span>

<span data-ttu-id="66ac6-116">Als u een andere gebruikerstoegang geven tot PIM zelf wilt, de functies die PIM moet de gebruiker hebben worden beschreven verder in [hoe toegang geven tot PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="66ac6-116">If you want to give another user access to PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="66ac6-117">Een gebruiker toevoegen aan een rol</span><span class="sxs-lookup"><span data-stu-id="66ac6-117">Add a user to a role</span></span>
1. <span data-ttu-id="66ac6-118">In de [Azure-portal](https://portal.azure.com/), selecteer de **Azure AD Privileged Identity Management** tegel op het dashboard.</span><span class="sxs-lookup"><span data-stu-id="66ac6-118">In the [Azure portal](https://portal.azure.com/), select the **Azure AD Privileged Identity Management** tile on the dashboard.</span></span>
2. <span data-ttu-id="66ac6-119">Selecteer **bevoorrechte rollen beheren**.</span><span class="sxs-lookup"><span data-stu-id="66ac6-119">Select **Manage privileged roles**.</span></span>
3. <span data-ttu-id="66ac6-120">In de **Overzicht rollen** tabel, selecteer de rol die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="66ac6-120">In the **Role summary** table, select the role you want to manage.</span></span>
4. <span data-ttu-id="66ac6-121">Selecteer in de rolblade **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="66ac6-121">In the role blade, select **Add**.</span></span>
5. <span data-ttu-id="66ac6-122">Klik op **Selecteer gebruikers** en zoek naar de gebruiker op de **Selecteer gebruikers** blade.</span><span class="sxs-lookup"><span data-stu-id="66ac6-122">Click **Select users** and search for the user on the **Select users** blade.</span></span>  
6. <span data-ttu-id="66ac6-123">Selecteer de gebruiker in de lijst met zoekresultaten en klik op **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="66ac6-123">Select the user from the search results list, and click **Done**.</span></span>
7. <span data-ttu-id="66ac6-124">Klik op **OK** opslaan van uw selectie.</span><span class="sxs-lookup"><span data-stu-id="66ac6-124">Click **OK** to save your selection.</span></span> <span data-ttu-id="66ac6-125">De gebruiker die u hebt geselecteerd, wordt weergegeven in de lijst als in aanmerking komen voor de rol.</span><span class="sxs-lookup"><span data-stu-id="66ac6-125">The user you have selected will appear in the list as eligible for the role.</span></span>

> [!NOTE]
> <span data-ttu-id="66ac6-126">Er zijn alleen nieuwe gebruikers met een rol in aanmerking komen voor de functie standaard.</span><span class="sxs-lookup"><span data-stu-id="66ac6-126">New users in a role are only eligible for the role by default.</span></span> <span data-ttu-id="66ac6-127">Als u de rol permanent te maken wilt, klikt u op de gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="66ac6-127">If you want to make the role permanent, click the user in the list.</span></span> <span data-ttu-id="66ac6-128">Gegevens van de gebruiker wordt weergegeven in een nieuwe blade.</span><span class="sxs-lookup"><span data-stu-id="66ac6-128">The user's information will appear in a new blade.</span></span> <span data-ttu-id="66ac6-129">Selecteer **zorg toeg** in het menu van de gebruiker informatie.</span><span class="sxs-lookup"><span data-stu-id="66ac6-129">Select **Make perm** in the user information menu.</span></span>  
> <span data-ttu-id="66ac6-130">Als een gebruiker niet voor Azure multi-factor Authentication (MFA registreren kan) of met behulp van een Microsoft-account (meestal @outlook.com), moet u deze permanent in alle hun rollen te maken.</span><span class="sxs-lookup"><span data-stu-id="66ac6-130">If a user cannot register for Azure Multi-Factor Authentication (MFA), or is using a Microsoft account (usually @outlook.com), you need to make them permanent in all their roles.</span></span> <span data-ttu-id="66ac6-131">In aanmerking komende admins wordt gevraagd om u te registreren voor MFA tijdens de activering.</span><span class="sxs-lookup"><span data-stu-id="66ac6-131">Eligible admins are asked to register for MFA during activation.</span></span>

<span data-ttu-id="66ac6-132">Nu dat de gebruiker in aanmerking voor een rol komt, laten weten dat ze dit kunnen activeren volgens de instructies in [hoe een rol activeren of deactiveren](active-directory-privileged-identity-management-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="66ac6-132">Now that the user is eligible for a role, let them know that they can activate it according to the instructions in [How to activate or deactivate a role](active-directory-privileged-identity-management-how-to-activate-role.md).</span></span>

## <a name="remove-a-user-from-a-role"></a><span data-ttu-id="66ac6-133">Een gebruiker vanuit een functie verwijderen</span><span class="sxs-lookup"><span data-stu-id="66ac6-133">Remove a user from a role</span></span>
<span data-ttu-id="66ac6-134">U kunt gebruikers van in aanmerking komende roltoewijzingen verwijderen, maar zorg ervoor dat er altijd ten minste één gebruiker aan wie een permanente globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="66ac6-134">You can remove users from eligible role assignments, but make sure there is always at least one user who is a permanent global administrator.</span></span>

<span data-ttu-id="66ac6-135">Volg deze stappen voor een specifieke gebruiker verwijderen uit een rol:</span><span class="sxs-lookup"><span data-stu-id="66ac6-135">Follow these steps to remove a specific user from a role:</span></span>

1. <span data-ttu-id="66ac6-136">Navigeer naar de rol in de lijst van de functie door het selecteren van een rol in het dashboard van Azure AD PIM of door te klikken op de **gebruikers in beheerdersrollen** knop.</span><span class="sxs-lookup"><span data-stu-id="66ac6-136">Navigate to the role in the role list either by selecting a role in the Azure AD PIM dashboard or by clicking on the **Users in Admin Roles** button.</span></span>
2. <span data-ttu-id="66ac6-137">Klik op de gebruiker in de lijst met gebruikers.</span><span class="sxs-lookup"><span data-stu-id="66ac6-137">Click on the user in the user list.</span></span>
3. <span data-ttu-id="66ac6-138">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="66ac6-138">Click **Remove**.</span></span> <span data-ttu-id="66ac6-139">Een bericht wordt u gevraagd te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="66ac6-139">A message will ask you to confirm.</span></span>
4. <span data-ttu-id="66ac6-140">Klik op **Ja** de functie te verwijderen van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="66ac6-140">Click **Yes** to remove the role from the user.</span></span>

<span data-ttu-id="66ac6-141">Als u niet zeker weet welke gebruikers moeten nog steeds hun roltoewijzingen, dan u kunt [een revisie toegang voor de rol starten](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="66ac6-141">If you're not sure which users still need their role assignments, then you can [start an access review for the role](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66ac6-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66ac6-142">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

