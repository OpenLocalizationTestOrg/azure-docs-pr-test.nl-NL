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
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Het oplossen van Azure Active Directory B2B-samenwerking

Hier volgen een aantal oplossingen voor bekende problemen met Azure Active Directory (Azure AD) B2B-samenwerking.


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Ik een externe gebruiker hebt toegevoegd, maar ze niet zien in mijn algemene adresboek of Hallo personen selecteren

In gevallen waarbij externe gebruikers niet worden ingevuld in de lijst Hallo kan Hallo object tooreplicate met een paar minuten duren.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Een gastgebruiker B2B, wordt niet weergegeven in SharePoint Online/OneDrive personen selecteren 
 
Hallo mogelijkheid toosearch van bestaande gastgebruikers in Hallo SharePoint Online (gesimuleerde Productieorder) personen selecteren is uitgeschakeld door verouderde standaardgedrag toomatch.

U kunt deze functie inschakelen met behulp van Hallo instellen 'ShowPeoplePickerSuggestionsForGuestUsers' Hallo-tenant en site-verzameling. U kunt instellen Hallo-functie met Hallo Set SPOTenant en Set-SPOSite-cmdlets, waarmee de leden toosearch alle bestaande gastgebruikers in Hallo-directory. Wijzigingen in Hallo tenantscope hebben geen invloed op al ingerichte gesimuleerde Productieorder sites.

## <a name="invitations-have-been-disabled-for-directory"></a>Uitnodigingen zijn uitgeschakeld voor de directory

Als er een bericht dat u geen machtigingen tooinvite gebruikers hebt, controleert u of uw gebruikersaccount geautoriseerde tooinvite externe gebruikers onder gebruikersinstellingen:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Als u deze instellingen onlangs hebt gewijzigd of Hallo Gast uitnodiging antwoorden rol tooa gebruiker is toegewezen, is er mogelijk een vertraging 15 tot 60 minuten voordat Hallo wijzigingen van kracht.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>Hallo-gebruiker die ik uitgenodigd ontvangt een fout opgetreden tijdens de inwisselcode

Veelvoorkomende fouten zijn onder andere:

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Genodigden Admin is EmailVerified gebruikers worden gemaakt in de tenant toegestaan

Wanneer gebruikers zich waarvan organisatie gebruikmaakt van Azure Active Directory, maar waarbij Hallo specifiek gebruikersaccount bestaat niet (bijvoorbeeld Hallo gebruiker bestaat niet in Azure AD contoso.com). Hallo beheerder contoso.com kan beschikken over een beleid te voorkomen dat gebruikers worden gemaakt. Hallo-gebruiker moet controleren met hun toodetermine admin als externe gebruikers zijn toegestaan. Hallo beheerder van de externe gebruiker wellicht tooallow e geverifieerd gebruikers in het domein (dit [artikel](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) op e-mailadres gecontroleerd gebruikers in staat).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Externe gebruiker bestaat niet al in een federatieve domein

Als u van federatieve authenticatie gebruikmaakt en Hallo gebruiker niet in Azure Active Directory bestaat nog, kan niet Hallo-gebruiker worden uitgenodigd.

Dit probleem hello tooresolve externe Gebruikerbeheerder moet synchroniseren van de gebruiker Hallo account tooAzure Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Hoe biedt\#', die niet is normaal gesproken een ongeldig teken, synchroniseren met Azure AD?

"\#' is een gereserveerd teken in de UPN's voor Azure AD B2B-samenwerking of externe gebruikers omdat Hallo uitgenodigd account user@contoso.com user_contoso.com# wordtEXT@fabrikam.onmicrosoft.com. Daarom \# in afkomstig van on-premises UPN's toosign zijn niet toegestaan in toohello Azure-portal. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Een foutbericht wanneer groep toe te voegen tooa externe gebruikers worden gesynchroniseerd

Externe gebruikers kunnen worden toegevoegd alleen te 'toegewezen' of 'Beveiliging' groepen en niet toogroups die als lokale master.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Mijn externe gebruiker heeft een tooredeem e-mail niet ontvangen

Hallo genodigde moet controleren met de ISP of spam filter tooensure die het volgende adres Hallo is toegestaan:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Ik zoals u ziet dat aangepaste Hallo-bericht krijgt geen deel uit van de Uitnodigingsberichten op tijdstippen

toocomply met privacywetten onze API's bevatten geen aangepaste berichten in Hallo e uitnodiging wanneer:

- Hallo uitnodiging antwoorden geen een e-mailadres in Hallo uitnodigen tenant
- Wanneer een App service-principal Hallo uitnodiging verzendt

Als dit scenario belangrijk tooyou is, kunt u onze API uitnodigingsmail onderdrukken en verzenden via e-mail-mechanisme Hallo van uw keuze. Raadpleeg toomake voor juridische afdeling van uw organisatie of een e-mailbericht verzenden van deze manier ook privacywetten naleeft.

## <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure Active Directory B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking](active-directory-b2b-invitation-email.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B-samenwerking licentieverlening](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B-samenwerking Veelgestelde vragen (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B-samenwerking API en de aanpassing](active-directory-b2b-api.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
