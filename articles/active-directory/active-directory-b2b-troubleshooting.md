---
title: Azure Active Directory B2B-samenwerking aaaTroubleshooting | Microsoft Docs
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="c6d88-103">Het oplossen van Azure Active Directory B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="c6d88-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="c6d88-104">Hier volgen een aantal oplossingen voor bekende problemen met Azure Active Directory (Azure AD) B2B-samenwerking.</span><span class="sxs-lookup"><span data-stu-id="c6d88-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="c6d88-105">Ik een externe gebruiker hebt toegevoegd, maar ze niet zien in mijn algemene adresboek of Hallo personen selecteren</span><span class="sxs-lookup"><span data-stu-id="c6d88-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="c6d88-106">In gevallen waarbij externe gebruikers niet worden ingevuld in de lijst Hallo kan Hallo object tooreplicate met een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="c6d88-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="c6d88-107">Een gastgebruiker B2B, wordt niet weergegeven in SharePoint Online/OneDrive personen selecteren</span><span class="sxs-lookup"><span data-stu-id="c6d88-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="c6d88-108">Hallo mogelijkheid toosearch van bestaande gastgebruikers in Hallo SharePoint Online (gesimuleerde Productieorder) personen selecteren is uitgeschakeld door verouderde standaardgedrag toomatch.</span><span class="sxs-lookup"><span data-stu-id="c6d88-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="c6d88-109">U kunt deze functie inschakelen met behulp van Hallo instellen 'ShowPeoplePickerSuggestionsForGuestUsers' Hallo-tenant en site-verzameling.</span><span class="sxs-lookup"><span data-stu-id="c6d88-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="c6d88-110">U kunt instellen Hallo-functie met Hallo Set SPOTenant en Set-SPOSite-cmdlets, waarmee de leden toosearch alle bestaande gastgebruikers in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="c6d88-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="c6d88-111">Wijzigingen in Hallo tenantscope hebben geen invloed op al ingerichte gesimuleerde Productieorder sites.</span><span class="sxs-lookup"><span data-stu-id="c6d88-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="c6d88-112">Uitnodigingen zijn uitgeschakeld voor de directory</span><span class="sxs-lookup"><span data-stu-id="c6d88-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="c6d88-113">Als er een bericht dat u geen machtigingen tooinvite gebruikers hebt, controleert u of uw gebruikersaccount geautoriseerde tooinvite externe gebruikers onder gebruikersinstellingen:</span><span class="sxs-lookup"><span data-stu-id="c6d88-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="c6d88-114">Als u deze instellingen onlangs hebt gewijzigd of Hallo Gast uitnodiging antwoorden rol tooa gebruiker is toegewezen, is er mogelijk een vertraging 15 tot 60 minuten voordat Hallo wijzigingen van kracht.</span><span class="sxs-lookup"><span data-stu-id="c6d88-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="c6d88-115">Hallo-gebruiker die ik uitgenodigd ontvangt een fout opgetreden tijdens de inwisselcode</span><span class="sxs-lookup"><span data-stu-id="c6d88-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="c6d88-116">Veelvoorkomende fouten zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="c6d88-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="c6d88-117">Genodigden Admin is EmailVerified gebruikers worden gemaakt in de tenant toegestaan</span><span class="sxs-lookup"><span data-stu-id="c6d88-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="c6d88-118">Wanneer gebruikers zich waarvan organisatie gebruikmaakt van Azure Active Directory, maar waarbij Hallo specifiek gebruikersaccount bestaat niet (bijvoorbeeld Hallo gebruiker bestaat niet in Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="c6d88-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="c6d88-119">Hallo beheerder contoso.com kan beschikken over een beleid te voorkomen dat gebruikers worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c6d88-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="c6d88-120">Hallo-gebruiker moet controleren met hun toodetermine admin als externe gebruikers zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="c6d88-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="c6d88-121">Hallo beheerder van de externe gebruiker wellicht tooallow e geverifieerd gebruikers in het domein (dit [artikel](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) op e-mailadres gecontroleerd gebruikers in staat).</span><span class="sxs-lookup"><span data-stu-id="c6d88-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="c6d88-122">Externe gebruiker bestaat niet al in een federatieve domein</span><span class="sxs-lookup"><span data-stu-id="c6d88-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="c6d88-123">Als u van federatieve authenticatie gebruikmaakt en Hallo gebruiker niet in Azure Active Directory bestaat nog, kan niet Hallo-gebruiker worden uitgenodigd.</span><span class="sxs-lookup"><span data-stu-id="c6d88-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="c6d88-124">Dit probleem hello tooresolve externe Gebruikerbeheerder moet synchroniseren van de gebruiker Hallo account tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6d88-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="c6d88-125">Hoe biedt\#', die niet is normaal gesproken een ongeldig teken, synchroniseren met Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c6d88-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="c6d88-126">"\#' is een gereserveerd teken in de UPN's voor Azure AD B2B-samenwerking of externe gebruikers omdat Hallo uitgenodigd account user@contoso.com user_contoso.com# wordtEXT@fabrikam.onmicrosoft.com. Daarom \# in afkomstig van on-premises UPN's toosign zijn niet toegestaan in toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c6d88-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="c6d88-127">Een foutbericht wanneer groep toe te voegen tooa externe gebruikers worden gesynchroniseerd</span><span class="sxs-lookup"><span data-stu-id="c6d88-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="c6d88-128">Externe gebruikers kunnen worden toegevoegd alleen te 'toegewezen' of 'Beveiliging' groepen en niet toogroups die als lokale master.</span><span class="sxs-lookup"><span data-stu-id="c6d88-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="c6d88-129">Mijn externe gebruiker heeft een tooredeem e-mail niet ontvangen</span><span class="sxs-lookup"><span data-stu-id="c6d88-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="c6d88-130">Hallo genodigde moet controleren met de ISP of spam filter tooensure die het volgende adres Hallo is toegestaan:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="c6d88-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="c6d88-131">Ik zoals u ziet dat aangepaste Hallo-bericht krijgt geen deel uit van de Uitnodigingsberichten op tijdstippen</span><span class="sxs-lookup"><span data-stu-id="c6d88-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="c6d88-132">toocomply met privacywetten onze API's bevatten geen aangepaste berichten in Hallo e uitnodiging wanneer:</span><span class="sxs-lookup"><span data-stu-id="c6d88-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="c6d88-133">Hallo uitnodiging antwoorden geen een e-mailadres in Hallo uitnodigen tenant</span><span class="sxs-lookup"><span data-stu-id="c6d88-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="c6d88-134">Wanneer een App service-principal Hallo uitnodiging verzendt</span><span class="sxs-lookup"><span data-stu-id="c6d88-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="c6d88-135">Als dit scenario belangrijk tooyou is, kunt u onze API uitnodigingsmail onderdrukken en verzenden via e-mail-mechanisme Hallo van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="c6d88-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="c6d88-136">Raadpleeg toomake voor juridische afdeling van uw organisatie of een e-mailbericht verzenden van deze manier ook privacywetten naleeft.</span><span class="sxs-lookup"><span data-stu-id="c6d88-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6d88-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6d88-137">Next steps</span></span>

<span data-ttu-id="c6d88-138">Lees ook onze andere artikelen over Azure AD B2B-samenwerking:</span><span class="sxs-lookup"><span data-stu-id="c6d88-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c6d88-139">Wat is Azure AD B2B-samenwerking?</span><span class="sxs-lookup"><span data-stu-id="c6d88-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c6d88-140">Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?</span><span class="sxs-lookup"><span data-stu-id="c6d88-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="c6d88-141">Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6d88-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="c6d88-142">Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="c6d88-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="c6d88-143">B2B-samenwerking uitnodiging inwisseling</span><span class="sxs-lookup"><span data-stu-id="c6d88-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="c6d88-144">Azure AD B2B-samenwerking licentieverlening</span><span class="sxs-lookup"><span data-stu-id="c6d88-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="c6d88-145">Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)</span><span class="sxs-lookup"><span data-stu-id="c6d88-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="c6d88-146">Azure Active Directory B2B-samenwerking API en de aanpassing</span><span class="sxs-lookup"><span data-stu-id="c6d88-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="c6d88-147">Multi-Factor Authentication voor gebruikers van B2B-samenwerking</span><span class="sxs-lookup"><span data-stu-id="c6d88-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="c6d88-148">B2B-samenwerking gebruikers zonder een uitnodiging toevoegen</span><span class="sxs-lookup"><span data-stu-id="c6d88-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* <span data-ttu-id="c6d88-149">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="c6d88-149">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
