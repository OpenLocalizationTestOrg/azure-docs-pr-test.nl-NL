---
title: aaaAzure Active Directory B2B-samenwerking Veelgestelde vragen | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over Azure Active Directory B2B-samenwerking ophalen.
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Azure Active Directory B2B-samenwerking Veelgestelde vragen

Deze Veelgestelde vragen (FAQ's) over Azure Active Directory (Azure AD) business-to-business (B2B) samenwerking zijn geregeld bijgewerkte tooinclude nieuwe onderwerpen.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Is Azure AD B2B-samenwerking beschikbaar in de klassieke Azure-portal Hallo?
Nee. Azure AD B2B-samenwerkingsfuncties zijn alleen beschikbaar in Hallo [Azure-portal](https://portal.azure.com) en in Hallo [Toegangspaneel](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Kunnen we onze aanmeldingspagina aanpassen zodat u meer intuïtieve van onze gastgebruikers B2B-samenwerking?
Absoluut! Zie onze [blogbericht over deze functie](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Voor meer informatie over hoe toocustomize uw organisatie de aanmelden pagina, Zie [huisstijl toosign in en Toegangsvenster toevoegen](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>B2B-samenwerking gebruikers toegang tot SharePoint Online en OneDrive?
Ja. Hallo mogelijkheid toosearch van bestaande gastgebruikers in SharePoint Online via Hallo personen selecteren is echter **uit** standaard. tooturn op Hallo optie toosearch voor gastgebruikers van ingesteld **ShowPeoplePickerSuggestionsForGuestUsers** te**op**. U kunt deze instelling inschakelen op Hallo tenant niveau of op het niveau van de siteverzameling Hallo. U kunt deze instelling wijzigen met behulp van Hallo Set SPOTenant en Set-SPOSite cmdlets. Met deze cmdlets kunnen leden alle bestaande gastgebruikers op Hallo directory zoeken. Wijzigingen in Hallo tenantscope hebben geen invloed op SharePoint Online-sites die al zijn ingericht.

### <a name="is-hello-csv-upload-feature-still-supported"></a>Hallo CSV-functie wordt nog steeds ondersteund uploaden is?
Ja. Zie voor meer informatie over het gebruik Hallo CSV-bestand uploaden functie [deze PowerShell-voorbeeld](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Hoe kan ik mijn e-mailberichten voor de uitnodiging aanpassen?
U kunt bijna alles over Hallo uitnodiging antwoorden proces aanpassen met behulp van Hallo [B2B uitnodiging API's](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Kan een uitgenodigde externe gebruiker Hallo-organisatie na worden uitgenodigd verlaten?
Hallo nodigen organisatie beheerder gastgebruiker B2B-samenwerking kunt verwijderen uit de directory, maar gastgebruiker Hallo Hallo organisatiedirectory uitnodigen zelf niet verlaten. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Gastgebruikers kunnen opnieuw hun methode multi-factor authentication-server instellen?
Ja. Gastgebruikers kunnen opnieuw instellen van hun multi-factor authentication-methode Hallo die dezelfde manier die reguliere gebruikers doen.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Welke organisatie is verantwoordelijk voor meervoudige verificatie licenties?
Hallo nodigen organisatie wordt multi-factor authentication uitgevoerd. Hallo organisatie uitnodigen moet ervoor zorgen dat Hallo organisatie voldoende licenties voor hun B2B-gebruikers met multi-factor authentication-server heeft.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Wat gebeurt er als heeft al een partnerorganisatie meervoudige verificatie instellen? Kunnen we vertrouwt hun multi-factor authentication-server, en geen gebruik van ons eigen multi-factor authentication?
Deze functie is gepland voor een toekomstige release, zodat u vervolgens een die specifieke partners tooexclude van (Hallo uitnodigen van uw organisatie) Multi-factor authentication kunt selecteren.

### <a name="how-can-i-use-delayed-invitations"></a>Hoe kan ik vertraagde uitnodigingen gebruiken?
Een organisatie mogelijk tooadd B2B-samenwerking gebruikers wilt richten tooapplications zo nodig en vervolgens de uitnodiging. U kunt Hallo B2B-samenwerking uitnodiging API toocustomize Hallo onboarding werkstroom gebruiken.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Kan ik maken een gastgebruiker beperkt beheerder?
Absoluut. Zie voor meer informatie [toevoegen Gast gebruikers tooa rol](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Kan Azure AD B2B-samenwerking B2B gebruikers tooaccess hello Azure-portal
Tenzij een gebruiker kan Hallo-rol van beperkt beheerder of de globale beheerdersrol is toegewezen, won't B2B-samenwerking gebruikers toegang toohello Azure-portal vereist. B2B-samenwerking gebruikers die de rol Hallo van beperkt beheerder of de globale beheerdersrol is toegewezen kunnen echter toegang tot Hallo-portal. Ook als een gastgebruiker die een van deze rollen niet is toegewezen naar Hallo-portal, Hallo gebruiker mogelijk kunnen tooaccess bepaalde delen van Hallo ervaring. Hallo Gast gebruikersrol heeft bepaalde machtigingen in Hallo-directory.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Kan ik toegang toohello Azure-portal voor gastgebruikers blokkeren?
Ja. Als u dit beleid configureert, worden zorgvuldige tooavoid per ongeluk blokkerende toegang toomembers en beheerders.
tooblock gastgebruiker van toegang tot toohello [Azure-portal](https://portal.azure.com), beleid voor voorwaardelijke toegang in Windows Azure classic deployment model API hello gebruiken:
1. Hallo wijzigen **alle gebruikers** groeperen, zodat deze alleen leden bevat.
  ![Schermafbeelding van de groep Hallo wijzigen](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Maak een dynamische groep waarin gastgebruikers.
  ![Schermafbeelding van de groep maken](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Stelt u een gastgebruikers voorwaardelijk beleid tooblock van toegang tot portal Hallo, zoals wordt weergegeven in de volgende Hallo video:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Ondersteunt Azure AD B2B-samenwerking multi-factor authentication en e-mailaccounts consument?
Ja. Meervoudige verificatie- en e-mailaccounts worden beide ondersteund voor Azure AD B2B-samenwerking.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Bent u van plan toosupport voor wachtwoordherstel voor gebruikers van Azure AD B2B-samenwerking?
Ja. Hier vindt u belangrijke informatie voor selfservice voor wachtwoordherstel (SSPR) voor een B2B-gebruiker die wordt verzocht van een partnerorganisatie Hallo:
 
* SSPR treedt alleen op Hallo identiteit tenant van Hallo B2B-gebruiker.
* Als Hallo identiteit tenant een Microsoft-account is, wordt Hallo SSPR-mechanisme voor Microsoft-account gebruikt.
* Als Hallo identiteit tenant een just-in-time (Just in time is) of 'een' tenant, wordt een wachtwoord opnieuw instellen van e-mailadres verzonden.
* Hallo standaardproces SSPR wordt voor andere tenants gevolgd voor B2B-gebruikers. Zoals member SSPR voor B2B-gebruikers in de context van Hallo resource, Hallo is tenancymodus geblokkeerd. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>Wachtwoord opnieuw ingesteld beschikbaar voor gastgebruikers in een just-in-time (Just in time) of 'een' tenant die geaccepteerd uitnodigingen met een werk of school e-mailadres, maar die geen bestaande Azure AD-account?
Ja. Een wachtwoord opnieuw instellen van e-mailbericht kan worden verzonden waarmee een gebruiker tooreset hun wachtwoord in Hallo JIT-tenancymodus.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Biedt Microsoft Dynamics CRM online ondersteuning voor Azure AD B2B-samenwerking?
Op dit moment biedt Microsoft Dynamics CRM geen ondersteuning voor online voor Azure AD B2B-samenwerking. Maar zullen we toosupport dit in toekomstige Hallo.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Wat is Hallo levensduur van een eerste wachtwoord voor een nieuwe gebruiker voor B2B-samenwerking?
Azure AD heeft een vaste set van teken, Wachtwoordsterkte en account lockout vereisten die gelden voor zowel tooall Azure AD cloud-gebruikersaccounts. Cloud-gebruikersaccounts zijn accounts die zijn niet federatief met een andere id-provider, zoals 
* Microsoft-account
* Facebook
* Active Directory Federatieservices
* Een andere cloudtenant (voor B2B-samenwerking)

Wachtwoordbeleid afhankelijk Hallo-beleid dat is toegepast in Hallo on-premises-tenancymodus en Hallo gebruiker van Microsoft-accountinstellingen voor federatieve accounts.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Een organisatie eventueel toohave verschillende ervaringen in hun toepassingen voor gebruikers van de tenant en gastgebruikers. Is er standaard richtlijnen voor dit? Hallo aanwezigheid van Hallo identiteit provider claim Hallo juist model toouse is?
 Gastgebruiker kan elke provider identiteit tooauthenticate kunt gebruiken. Zie voor meer informatie [eigenschappen van een gebruiker B2B-samenwerking](active-directory-b2b-user-properties.md). Gebruik Hallo **UserType** eigenschap toodetermine gebruikerservaring. Hallo **UserType** claim momenteel niet is opgenomen in het Hallo-token. Toepassingen voor Hallo gebruiker en tooget Hallo UserType Hallo Graph API tooquery Hallo directory gebruiken.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Waar vind ik een B2B-samenwerking community tooshare oplossingen en ideeën toosubmit?
Er luistert voortdurend tooyour feedback, tooimprove B2B-samenwerking. We nodigen u tooshare uw gebruiker scenario's, aanbevolen procedures en wat u leuk vindt aan Azure AD B2B-samenwerking. Hallo Hallo discussie join [Microsoft Tech-Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
We nodigen ook toosubmit u uw ideeën en stem voor toekomstige functies op [B2B-samenwerking ideeën](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>We een uitnodiging die automatisch wordt ingewisseld, zodat die gebruiker Hallo is 'toogo gereed' NET kunt verzenden? Of Hallo gebruiker altijd heeft tooclick via toohello inwisseling URL?
Uitnodigingen die zijn verzonden door de gebruiker in de organisatie die ook lid zijn van de partnerorganisatie Hallo uitnodigen Hallo vereisen geen inwisseling door Hallo B2B-gebruiker.

Het is raadzaam dat u één gebruiker uit Hallo partner organisatie toojoin Hallo uitnodigen organisatie uitnodigen. [Toevoegen van deze gebruikersrol toohello Gast uitnodiging antwoorden in de bronorganisatie Hallo](active-directory-b2b-add-guest-to-role.md). Deze gebruiker andere gebruikers in de organisatie van de accountpartner Hallo kunt uitnodigen Hallo aanmelden via PowerShell-scripts,-gebruikersinterface of API's. Vervolgens B2B-samenwerking gebruikers van die organisatie zijn niet vereist tooredeem hun uitnodigingen.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Hoe werkt B2B-samenwerking als Hallo uitgenodigd partner federation tooadd hun eigen lokale verificatie?
Als Hallo partner heeft een Azure AD-tenant is gefedereerd toohello on-premises infrastructuur voor verificatie, lokale eenmalige aanmelding (SSO) automatisch is bereikt. Als partner Hallo niet beschikt over een Azure AD-tenant, wordt een Azure AD-account gemaakt voor nieuwe gebruikers. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Ik Azure AD B2B niet geaccepteerd door de gmail.com en outlook.com e-mailadressen en dat B2C is gebruikt voor deze typen accounts beschouwd?
Hallo verschillen tussen B2B- en business naar bedrijf (B2C) samenwerking in termen van welke identiteiten worden ondersteund worden verwijderd. Hallo-id die wordt gebruikt, is niet een goede reden toochoose B2B gebruiken of B2C. Zie voor meer informatie over het kiezen van de optie voor samenwerking [vergelijken B2B-samenwerking en B2C in Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Welke toepassingen en services ondersteuning voor Azure B2B gastgebruikers?
Alle Azure AD-geïntegreerde toepassingen ondersteuning bieden voor Azure B2B gastgebruikers. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Kunnen we multi-factor authentication voor gastgebruikers B2B forceren als onze partners geen multi-factor authentication-server hebt?
Ja. Zie voor meer informatie [voorwaardelijke toegang voor gebruikers voor B2B-samenwerking](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>In SharePoint, kunt u een lijst met voor 'toestaan' of 'weigeren' voor externe gebruikers definiëren. We dit kunt doen in Azure?
Ja. Azure AD B2B-samenwerking ondersteunt lijsten toestaan en weigeren van lijsten. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Wat licenties doen we toouse Azure AD B2B nodig?
Zie voor meer informatie over wat uw organisatie licenties toouse Azure AD B2B moet, [Azure Active Directory B2B-samenwerking richtlijnen licentieverlening](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Volgende stappen

Lees ook onze andere artikelen over Azure AD B2B-samenwerking:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Hoe voeg beheerders van Azure AD B2B-samenwerking gebruikers?](active-directory-b2b-admin-add-users.md)
* [Hoe kunnen IT-medewerkers B2B-samenwerking gebruikers toevoegen](active-directory-b2b-iw-add-users.md)
* [Hallo-elementen van Hallo uitnodigingsmail voor B2B-samenwerking](active-directory-b2b-invitation-email.md)
* [B2B-samenwerking uitnodiging inwisseling](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B-samenwerking licentieverlening](active-directory-b2b-licensing.md)
* [Het oplossen van Azure AD B2B-samenwerking](active-directory-b2b-troubleshooting.md)
* [Azure AD B2B-samenwerking API en de aanpassing](active-directory-b2b-api.md)
* [Multi-Factor Authentication voor gebruikers van B2B-samenwerking](active-directory-b2b-mfa-instructions.md)
* [B2B-samenwerking gebruikers zonder een uitnodiging toevoegen](active-directory-b2b-add-user-without-invite.md)
* [Artikel index voor application management in Azure AD](active-directory-apps-index.md)
