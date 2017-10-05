---
title: Nieuwe gebruikers toevoegen aan Azure Active Directory | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u nieuwe gebruikers kunt toevoegen of gebruikersinformatie kunt wijzigen in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="fff9f-103">Nieuwe gebruikers of gebruikers met een Microsoft-account toevoegen aan Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fff9f-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="fff9f-104">Gebruikers toevoegen om uw directory te vullen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-104">Add users to populate your directory.</span></span> <span data-ttu-id="fff9f-105">In dit artikel wordt uitgelegd hoe u nieuwe gebruikers kunt toevoegen in uw organisatie en hoe u gebruikers met een Microsoft-account kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="fff9f-106">Zie [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md) (Engelstalig) voor meer informatie over het toevoegen van gebruikers van andere directory's in Azure Active Directory of over het toevoegen van gebruikers van partnerbedrijven.</span><span class="sxs-lookup"><span data-stu-id="fff9f-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="fff9f-107">Toegevoegde gebruikers hebben standaard geen gebruikersrechten, maar u kunt op elk gewenst moment rollen aan ze toewijzen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fff9f-108">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="fff9f-109">Voor informatie over het toevoegen van een gebruiker in de Azure AD-beheercentrum, Zie [nieuwe gebruikers toevoegen aan Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fff9f-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="fff9f-110">Een gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="fff9f-110">Add a user</span></span>
1. <span data-ttu-id="fff9f-111">Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com) met een account met globale beheerdersrechten voor de directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="fff9f-112">Selecteer **Active Directory** en selecteer vervolgens de naam van de organisatiedirectory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="fff9f-113">Selecteer de tab **Gebruikers** en selecteer vervolgens in de opdrachtbalk **Gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fff9f-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="fff9f-114">Selecteer op de pagina **Vertel ons meer over deze gebruiker** onder **Type gebruiker** een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="fff9f-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="fff9f-115">**Nieuwe gebruiker in uw organisatie**: hiermee voegt u een nieuw gebruikersaccount toe aan uw directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="fff9f-116">**Gebruiker met een bestaand Microsoft-account**: hiermee voegt u een bestaand Microsoft-consumentenaccount toe aan uw directory (bijvoorbeeld een Outlook-account)</span><span class="sxs-lookup"><span data-stu-id="fff9f-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="fff9f-117">Afhankelijk van de waarde van **Type gebruiker** voert u een gebruikersnaam in (voor de nieuwe gebruiker) of een e-mailadres (voor een gebruiker met een Microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="fff9f-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="fff9f-118">Geef op de **profielpagina** van de gebruiker een voor- en achternaam op, een gebruiksvriendelijke naam en een gebruikersrol uit de lijst **Rollen**.</span><span class="sxs-lookup"><span data-stu-id="fff9f-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="fff9f-119">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="fff9f-120">Activeer desgewenst de optie **Meervoudige verificatie inschakelen** voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fff9f-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="fff9f-121">Selecteer op de pagina **Tijdelijk wachtwoord instellen** de optie **Maken**.</span><span class="sxs-lookup"><span data-stu-id="fff9f-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fff9f-122">Als uw organisatie meer dan één domein gebruikt, is het nuttig op de hoogte te zijn van de volgende problemen die zich kunnen voordoen bij het toevoegen van een gebruikersaccount:</span><span class="sxs-lookup"><span data-stu-id="fff9f-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="fff9f-123">Als u gebruikersaccounts met dezelfde UPN (user principal name) wilt toevoegen in meerdere domeinen, voegt u bijvoorbeeld **eerst** geoffgrisso@contoso.onmicrosoft.com toe, **gevolgd door** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fff9f-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="fff9f-124">Voeg geoffgrisso@contoso.com **niet** vóór geoffgrisso@contoso.onmicrosoft.com toe.</span><span class="sxs-lookup"><span data-stu-id="fff9f-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="fff9f-125">De volgorde is belangrijk en het kan lastig zijn verkeerd ingevoerde adressen ongedaan te maken.</span><span class="sxs-lookup"><span data-stu-id="fff9f-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="fff9f-126">Gebruikersgegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="fff9f-126">Change user information</span></span>
<span data-ttu-id="fff9f-127">U kunt elk gebruikerskenmerk wijzigen, behalve de object-ID.</span><span class="sxs-lookup"><span data-stu-id="fff9f-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="fff9f-128">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-128">Open your directory.</span></span>
2. <span data-ttu-id="fff9f-129">Selecteer de tab **Gebruikers** en selecteer vervolgens de weergavenaam van de gebruiker die u wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="fff9f-130">Voer de wijzigingen uit en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fff9f-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="fff9f-131">Als de gebruiker die u wijzigt, is gesynchroniseerd met uw on-premises Active Directory-service, kunt u de gebruikersinformatie niet wijzigen met deze procedure.</span><span class="sxs-lookup"><span data-stu-id="fff9f-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="fff9f-132">Gebruik uw beheerhulpprogramma's voor on-premises Active Directory om de gebruiker te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fff9f-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="fff9f-133">Beheer van gastgebruikers en beperkingen</span><span class="sxs-lookup"><span data-stu-id="fff9f-133">Guest user management and limitations</span></span>
<span data-ttu-id="fff9f-134">Gastaccounts zijn accounts van gebruikers uit andere directory's. Ze zijn uitgenodigd voor uw directory zodat ze toegang hebben tot SharePoint-documenten, toepassingen of andere Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="fff9f-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="fff9f-135">Bij een gastaccount in een directory is het onderliggende UserType-kenmerk ingesteld op "Gast."</span><span class="sxs-lookup"><span data-stu-id="fff9f-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="fff9f-136">Gewone gebruikers (met name de leden van uw directory) hebben het UserType-kenmerk "Lid."</span><span class="sxs-lookup"><span data-stu-id="fff9f-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="fff9f-137">Gasten hebben een beperkte set rechten in de directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="fff9f-138">Deze rechten beperken de mogelijkheden van gasten om informatie over andere gebruikers in de directory te bekijken.</span><span class="sxs-lookup"><span data-stu-id="fff9f-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="fff9f-139">Gastgebruikers kunnen echter wel communiceren met de gebruikers en groepen van de resources waarmee ze werken.</span><span class="sxs-lookup"><span data-stu-id="fff9f-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="fff9f-140">Gastgebruikers hebben de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="fff9f-140">Guest users can:</span></span>

* <span data-ttu-id="fff9f-141">Andere gebruikers en groepen zien die gekoppeld zijn aan een Azure-abonnement waaraan ze zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="fff9f-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="fff9f-142">De leden zien van groepen waar ze bij horen</span><span class="sxs-lookup"><span data-stu-id="fff9f-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="fff9f-143">Andere gebruikers opzoeken in de directory, als ze het volledige e-mailadres van de gebruiker kennen</span><span class="sxs-lookup"><span data-stu-id="fff9f-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="fff9f-144">Een beperkte set kenmerken bekijken van de gebruikers die ze opzoeken. Het gaat om de weergavenaam, het e-mailadres, de UPN (user principal name) en een foto van miniatuurformaat</span><span class="sxs-lookup"><span data-stu-id="fff9f-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="fff9f-145">Een lijst samenstellen met geverifieerde domeinen in de directory</span><span class="sxs-lookup"><span data-stu-id="fff9f-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="fff9f-146">Instemmen met toepassingen zodat ze dezelfde toegang hebben als leden in uw directory</span><span class="sxs-lookup"><span data-stu-id="fff9f-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="fff9f-147">Toegangsbeleid instellen voor gasten</span><span class="sxs-lookup"><span data-stu-id="fff9f-147">Set guest user access policies</span></span>
<span data-ttu-id="fff9f-148">De tab **Configureren** van een directory bevat opties voor het beheren van toegang van gastgebruikers.</span><span class="sxs-lookup"><span data-stu-id="fff9f-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="fff9f-149">Deze opties kunnen alleen worden gewijzigd in de klassieke Azure-portal door een hoofdbeheerder van de directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="fff9f-150">Op dit moment is er geen PowerShell- of API-methode beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="fff9f-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="fff9f-151">Als u het tabblad **Configureren** wilt openen in de klassieke Azure-portal, selecteert u **Active Directory** en vervolgens de naam van de directory.</span><span class="sxs-lookup"><span data-stu-id="fff9f-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Het tabblad Configureren in Azure Active Directory][1]

<span data-ttu-id="fff9f-153">Vervolgens kunt u de opties voor het beheren van toegang van gastgebruikers bewerken.</span><span class="sxs-lookup"><span data-stu-id="fff9f-153">Then you can edit the options to control access for guest users.</span></span>

![Opties voor het beheren van toegang voor gastgebruikers][2]

## <a name="whats-next"></a><span data-ttu-id="fff9f-155">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="fff9f-155">What's next</span></span>
* [<span data-ttu-id="fff9f-156">Gebruikers vanuit andere mappen of partnerbedrijven toevoegen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fff9f-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* <span data-ttu-id="fff9f-157">[Administering Azure AD](active-directory-administer.md) (Azure AD beheren)</span><span class="sxs-lookup"><span data-stu-id="fff9f-157">[Administering Azure AD](active-directory-administer.md)</span></span>
* [<span data-ttu-id="fff9f-158">Wachtwoorden beheren in Azure AD</span><span class="sxs-lookup"><span data-stu-id="fff9f-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="fff9f-159">Groepen beheren in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fff9f-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
