---
title: aaaAdd nieuwe gebruikers tooAzure Active Directory | Microsoft Docs
description: Legt uit hoe nieuwe gebruikers tooadd gebruikersgegevens in Azure Active Directory of wijzigen.
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
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="916a6-103">Nieuwe gebruikers toevoegen of met Microsoft-accounts tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="916a6-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="916a6-104">Toevoegen van gebruikers toopopulate uw directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="916a6-105">Dit artikel wordt uitgelegd hoe tooadd nieuwe gebruikers in uw organisatie en hoe tooadd gebruikers die Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="916a6-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="916a6-106">Zie [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md) (Engelstalig) voor meer informatie over het toevoegen van gebruikers van andere directory's in Azure Active Directory of over het toevoegen van gebruikers van partnerbedrijven.</span><span class="sxs-lookup"><span data-stu-id="916a6-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="916a6-107">Toegevoegde gebruikers hebben geen beheerdersrechten standaard, maar u kunt functies toothem toewijzen op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="916a6-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="916a6-108">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="916a6-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="916a6-109">Voor hoe tooadd een gebruiker in hello Azure AD-beheercentrum, Zie [toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="916a6-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="916a6-110">Een gebruiker toevoegen</span><span class="sxs-lookup"><span data-stu-id="916a6-110">Add a user</span></span>
1. <span data-ttu-id="916a6-111">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="916a6-112">Selecteer **Active Directory**, en selecteer vervolgens Hallo-naam van de organisatiedirectory.</span><span class="sxs-lookup"><span data-stu-id="916a6-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="916a6-113">Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens in de opdrachtbalk Hallo **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="916a6-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="916a6-114">Op Hallo **Vertel ons meer over deze gebruiker** pagina onder **Type gebruiker**, selecteer:</span><span class="sxs-lookup"><span data-stu-id="916a6-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="916a6-115">**Nieuwe gebruiker in uw organisatie**: hiermee voegt u een nieuw gebruikersaccount toe aan uw directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="916a6-116">**Gebruiker met een bestaand Microsoft-account** – voegt u een bestaande Microsoft consumer account tooyour map (bijvoorbeeld een Outlook-account)</span><span class="sxs-lookup"><span data-stu-id="916a6-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="916a6-117">Afhankelijk van de waarde van **Type gebruiker** voert u een gebruikersnaam in (voor de nieuwe gebruiker) of een e-mailadres (voor een gebruiker met een Microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="916a6-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="916a6-118">Op gebruiker Hallo **profiel** pagina, Geef een naam en achternaam, een gebruiksvriendelijke naam en een gebruikersrol uit Hallo **rollen** lijst.</span><span class="sxs-lookup"><span data-stu-id="916a6-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="916a6-119">Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.</span><span class="sxs-lookup"><span data-stu-id="916a6-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="916a6-120">Opgeven of te**multi-factor Authentication inschakelen** voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="916a6-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="916a6-121">Op Hallo **tijdelijk wachtwoord** pagina **maken**.</span><span class="sxs-lookup"><span data-stu-id="916a6-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="916a6-122">Als uw organisatie meer dan één domein gebruikt, moet u weten over Hallo problemen te volgen wanneer u een gebruikersaccount toevoegen:</span><span class="sxs-lookup"><span data-stu-id="916a6-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="916a6-123">tooadd gebruikersaccounts met dezelfde UPN (User Principal Name) in meerdere domeinen, Hallo **eerste** toevoegen, bijvoorbeeld geoffgrisso@contoso.onmicrosoft.com, **gevolgd door** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="916a6-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="916a6-124">Voeg geoffgrisso@contoso.com **niet** vóór geoffgrisso@contoso.onmicrosoft.com toe. Deze volgorde is belangrijk en omslachtige tooundo kan zijn.</span><span class="sxs-lookup"><span data-stu-id="916a6-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="916a6-125">Gebruikersgegevens wijzigen</span><span class="sxs-lookup"><span data-stu-id="916a6-125">Change user information</span></span>
<span data-ttu-id="916a6-126">U kunt elk gebruikerskenmerk, met uitzondering van Hallo object-ID.</span><span class="sxs-lookup"><span data-stu-id="916a6-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="916a6-127">Open uw directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-127">Open your directory.</span></span>
2. <span data-ttu-id="916a6-128">Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens Hallo weergavenaam van de gebruiker die u wilt dat toochange Hallo.</span><span class="sxs-lookup"><span data-stu-id="916a6-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="916a6-129">Voer de wijzigingen uit en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="916a6-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="916a6-130">Als het Hallo-gebruiker die u wilt wijzigen, is gesynchroniseerd met uw on-premises Active Directory-service, kunt u gebruikersgegevens Hallo met deze procedure niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="916a6-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="916a6-131">toochange hello gebruiker, uw lokale Active Directory-beheerhulpprogramma's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="916a6-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="916a6-132">Beheer van gastgebruikers en beperkingen</span><span class="sxs-lookup"><span data-stu-id="916a6-132">Guest user management and limitations</span></span>
<span data-ttu-id="916a6-133">Gastaccounts zijn accounts van gebruikers uit andere directory's die uitgenodigde tooyour directory tooaccess SharePoint-documenten, toepassingen of andere Azure-resources zijn.</span><span class="sxs-lookup"><span data-stu-id="916a6-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="916a6-134">Een gastaccount in uw directory heeft de onderliggende UserType-kenmerk ingesteld te 'gast'.</span><span class="sxs-lookup"><span data-stu-id="916a6-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="916a6-135">Gewone gebruikers (met name de leden van uw directory) hebben Hallo UserType-kenmerk "Lid."</span><span class="sxs-lookup"><span data-stu-id="916a6-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="916a6-136">Gasten hebben een beperkte set rechten in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="916a6-137">Deze rechten beperken Hallo mogelijkheid voor gasten toodiscover informatie over andere gebruikers in de directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="916a6-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="916a6-138">Gastgebruikers kunnen echter wel communiceren met het Hallo-gebruikers en groepen die zijn gekoppeld aan Hallo resources waarmee die ze werken op.</span><span class="sxs-lookup"><span data-stu-id="916a6-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="916a6-139">Gastgebruikers hebben de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="916a6-139">Guest users can:</span></span>

* <span data-ttu-id="916a6-140">Zie andere gebruikers en groepen die zijn gekoppeld aan een Azure-abonnement toowhich waaraan ze zijn toegewezen</span><span class="sxs-lookup"><span data-stu-id="916a6-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="916a6-141">Zie Hallo leden van groepen toowhich die ze horen</span><span class="sxs-lookup"><span data-stu-id="916a6-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="916a6-142">Opzoeken van andere gebruikers in de directory hello, als ze Hallo volledige e-mailadres van Hallo gebruiker kennen</span><span class="sxs-lookup"><span data-stu-id="916a6-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="916a6-143">Zie een beperkt aantal kenmerken van Hallo gebruikers die ze--de naam van de beperkte toodisplay, e-mailadres, UPN (user Principal name) en een foto van miniatuurformaat opzoeken</span><span class="sxs-lookup"><span data-stu-id="916a6-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="916a6-144">Een lijst met geverifieerde domeinen in de map Hallo ophalen</span><span class="sxs-lookup"><span data-stu-id="916a6-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="916a6-145">Toestemming tooapplications, zodat ze Hallo dezelfde toegang hebben als leden in uw directory hebben</span><span class="sxs-lookup"><span data-stu-id="916a6-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="916a6-146">Toegangsbeleid instellen voor gasten</span><span class="sxs-lookup"><span data-stu-id="916a6-146">Set guest user access policies</span></span>
<span data-ttu-id="916a6-147">Hallo **configureren** tabblad van een directory bevat opties toocontrol toegang van gastgebruikers.</span><span class="sxs-lookup"><span data-stu-id="916a6-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="916a6-148">Deze opties kunnen alleen worden gewijzigd in de klassieke Azure-portal door een hoofdbeheerder van de directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="916a6-149">Op dit moment is er geen PowerShell- of API-methode beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="916a6-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="916a6-150">Hallo tooopen **configureren** tabblad hello Azure classic portal, selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="916a6-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Het tabblad Configureren in Azure Active Directory][1]

<span data-ttu-id="916a6-152">U kunt vervolgens Hallo opties toocontrol toegang van gastgebruikers bewerken.</span><span class="sxs-lookup"><span data-stu-id="916a6-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![Opties voor het beheren van toegang voor gastgebruikers][2]

## <a name="whats-next"></a><span data-ttu-id="916a6-154">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="916a6-154">What's next</span></span>
* [<span data-ttu-id="916a6-155">Gebruikers vanuit andere mappen of partnerbedrijven toevoegen in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="916a6-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* <span data-ttu-id="916a6-156">[Administering Azure AD](active-directory-administer.md) (Azure AD beheren)</span><span class="sxs-lookup"><span data-stu-id="916a6-156">[Administering Azure AD](active-directory-administer.md)</span></span>
* [<span data-ttu-id="916a6-157">Wachtwoorden beheren in Azure AD</span><span class="sxs-lookup"><span data-stu-id="916a6-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="916a6-158">Groepen beheren in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="916a6-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
