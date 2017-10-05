---
title: Het oplossen van Azure Active Directory B2B-samenwerking | Microsoft Docs
description: Oplossingen voor bekende problemen met Azure Active Directory B2B-samenwerking
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="b1d56-103">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="b1d56-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="b1d56-104">Hier volgen een aantal oplossingen voor bekende problemen met Azure Active Directory (Azure AD) B2B-samenwerking.</span><span class="sxs-lookup"><span data-stu-id="b1d56-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="b1d56-105">Ik een externe gebruiker hebt toegevoegd, maar ze niet zien in mijn algemene adresboek of in de personen selecteren</span><span class="sxs-lookup"><span data-stu-id="b1d56-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="b1d56-106">In gevallen waarbij externe gebruikers niet worden ingevuld in de lijst, kan het object enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="b1d56-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="b1d56-107">Een gastgebruiker B2B, wordt niet weergegeven in SharePoint Online/OneDrive personen selecteren</span><span class="sxs-lookup"><span data-stu-id="b1d56-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="b1d56-108">De mogelijkheid om te zoeken naar bestaande gastgebruikers in de kiezer voor SharePoint Online (gesimuleerde Productieorder) mensen is uitgeschakeld standaard overeenkomen met de verouderde gedrag.</span><span class="sxs-lookup"><span data-stu-id="b1d56-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="b1d56-109">U kunt deze functie inschakelen met behulp van de instelling 'ShowPeoplePickerSuggestionsForGuestUsers' op het niveau van de verzameling tenant en de site.</span><span class="sxs-lookup"><span data-stu-id="b1d56-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="b1d56-110">U kunt de functie met de Set SPOTenant en Set-SPOSite-cmdlets waarmee leden toe aan alle bestaande gastgebruikers zoeken in de map instellen.</span><span class="sxs-lookup"><span data-stu-id="b1d56-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="b1d56-111">Wijzigingen in het tenantbereik is niet van invloed op al ingerichte gesimuleerde Productieorder sites.</span><span class="sxs-lookup"><span data-stu-id="b1d56-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="b1d56-112">Uitnodigingen zijn uitgeschakeld voor de directory</span><span class="sxs-lookup"><span data-stu-id="b1d56-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="b1d56-113">Als er een bericht dat u bent niet gemachtigd om uit te nodigen gebruikers, moet u controleren of uw gebruikersaccount is geautoriseerd om uit te nodigen externe gebruikers onder gebruikersinstellingen:</span><span class="sxs-lookup"><span data-stu-id="b1d56-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="b1d56-114">Als u deze instellingen onlangs hebt gewijzigd of de uitnodiging antwoorden Gast-rol wordt toegewezen aan een gebruiker, kan er een vertraging 15 tot 60 minuten voordat de wijzigingen van kracht.</span><span class="sxs-lookup"><span data-stu-id="b1d56-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="b1d56-115">De gebruiker die ik uitgenodigd ontvangt een fout opgetreden tijdens de inwisselcode</span><span class="sxs-lookup"><span data-stu-id="b1d56-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="b1d56-116">Veelvoorkomende fouten zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="b1d56-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="b1d56-117">Genodigden Admin is EmailVerified gebruikers worden gemaakt in de tenant toegestaan</span><span class="sxs-lookup"><span data-stu-id="b1d56-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="b1d56-118">Wanneer gebruikers uitnodigen waarvan organisatie gebruikmaakt van Azure Active Directory, maar waarin de specifieke gebruikersaccount bestaat niet (bijvoorbeeld: de gebruiker bestaat niet in Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="b1d56-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="b1d56-119">De beheerder van contoso.com kan beschikken over een beleid te voorkomen dat gebruikers worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b1d56-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="b1d56-120">De gebruiker moet contact op met de beheerder om te bepalen of de externe gebruikers zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="b1d56-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="b1d56-121">De beheerder van de externe gebruiker wilt toestaan dat gebruikers e-mailadres gecontroleerd in het domein (dit [artikel](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) op e-mailadres gecontroleerd gebruikers in staat).</span><span class="sxs-lookup"><span data-stu-id="b1d56-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="b1d56-122">Externe gebruiker bestaat niet al in een federatieve domein</span><span class="sxs-lookup"><span data-stu-id="b1d56-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="b1d56-123">Als u van federatieve authenticatie gebruikmaakt en de gebruiker al niet in Azure Active Directory bestaat, kan de gebruiker kan niet worden uitgenodigd.</span><span class="sxs-lookup"><span data-stu-id="b1d56-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="b1d56-124">U lost dit probleem, moet de beheerder van de externe gebruiker het gebruikersaccount met Azure Active Directory synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="b1d56-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="b1d56-125">Hoe biedt\#', die niet is normaal gesproken een ongeldig teken, synchroniseren met Azure AD?</span><span class="sxs-lookup"><span data-stu-id="b1d56-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="b1d56-126">"\#' is een gereserveerd teken in de UPN's voor Azure AD B2B-samenwerking of externe gebruikers, omdat de uitgenodigde account user@contoso.com user_contoso.com# wordtEXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b1d56-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="b1d56-127">Daarom \# in afkomstig van on-premises UPN's zijn niet toegestaan aan te melden bij de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b1d56-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="b1d56-128">Een foutbericht wanneer externe gebruikers toevoegen aan een gesynchroniseerde groep</span><span class="sxs-lookup"><span data-stu-id="b1d56-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="b1d56-129">Externe gebruikers kunnen worden toegevoegd, uitsluitend voor 'toegewezen' of '-' beveiligingsgroepen en niet voor groepen die Gemastered on-premises.</span><span class="sxs-lookup"><span data-stu-id="b1d56-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="b1d56-130">Mijn externe gebruiker heeft geen ontvangen een e-mailbericht te gebruiken</span><span class="sxs-lookup"><span data-stu-id="b1d56-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="b1d56-131">De genodigden moet controleren met hun ISP of spam filter om ervoor te zorgen dat het volgende adres is toegestaan:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="b1d56-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="b1d56-132">Ik zoals u ziet dat het aangepaste bericht geen deel uit van de Uitnodigingsberichten op tijdstippen krijgt</span><span class="sxs-lookup"><span data-stu-id="b1d56-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="b1d56-133">Om te voldoen aan de privacywetten onze API's bevatten geen aangepaste berichten in de uitnodiging e-mailbericht wanneer:</span><span class="sxs-lookup"><span data-stu-id="b1d56-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="b1d56-134">De uitnodiging antwoorden geen een e-mailadres in de uitnodiging tenant</span><span class="sxs-lookup"><span data-stu-id="b1d56-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="b1d56-135">Wanneer een App service-principal verzendt de uitnodiging</span><span class="sxs-lookup"><span data-stu-id="b1d56-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="b1d56-136">Als dit scenario voor u belangrijk is, kunt u onze API uitnodigingsmail onderdrukken en versturen via het mechanisme voor e-mailadres van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="b1d56-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="b1d56-137">Raadpleeg uw juridische afdeling om te controleren of een e-mailbericht verzenden van dat deze manier ook privacywetten naleeft.</span><span class="sxs-lookup"><span data-stu-id="b1d56-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1d56-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b1d56-138">Next steps</span></span>

<span data-ttu-id="b1d56-139">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="b1d56-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b1d56-140">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="b1d56-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b1d56-141">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="b1d56-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="b1d56-142">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="b1d56-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="b1d56-143">De elementen van de uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="b1d56-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="b1d56-144">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="b1d56-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="b1d56-145">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="b1d56-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="b1d56-146">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="b1d56-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="b1d56-147">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="b1d56-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="b1d56-148">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="b1d56-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="b1d56-149">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="b1d56-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="b1d56-150">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="b1d56-150">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
