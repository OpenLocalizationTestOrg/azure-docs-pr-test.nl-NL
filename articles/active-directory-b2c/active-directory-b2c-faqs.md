---
title: Veelgestelde vragen (FAQ) - Azure AD B2C | Microsoft Docs
description: Veelgestelde vragen over Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C: Veelgestelde vragen (FAQ) 
Deze pagina antwoorden op veelgestelde vragen over Azure Active Directory (Azure AD) B2C Hallo. Houd regelmatig op updates controleren.

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>Kan ik Azure AD B2C-functies gebruiken in mijn bestaande, op basis van een werknemer Azure AD-tenant?
Azure AD en Azure AD B2C afzonderlijke producten zijn en kunnen niet worden gecombineerd in Hallo dezelfde tenant.  Een Azure AD-tenant vertegenwoordigt een organisatie.  Een Azure AD B2C-tenant vertegenwoordigt een verzameling van identiteiten toobe gebruikt met relying party-toepassingen.  Azure AD B2C kunt tooAzure AD zodat verificatie van werknemers in een organisatie federeren met aangepast beleid (in de openbare preview).

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>Kan ik Azure AD B2C tooprovide aanmelden bij sociale media (Facebook en Google +) in Office 365 gebruiken?
Azure AD B2C niet gebruikte tooauthenticate gebruikers voor Microsoft Office 365.  Azure AD is de oplossing van Microsoft voor het beheren van werknemers toegang tooSaaS apps en functies die zijn ontworpen voor dit doel zoals licentieverlening en voorwaardelijke toegang heeft.  Azure AD B2C biedt een platform voor identiteits- en toegangsbeheer voor het bouwen van webtoepassingen en mobiele toepassingen.  Wanneer Azure AD B2C geconfigureerde toofederate tooan Azure AD-tenant, beheert hello Azure AD-tenant werknemers toegang tooapplications die afhankelijk van Azure AD B2C zijn.

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Wat zijn lokale accounts in Azure AD B2C? Hoe zijn ze verschilt van het werk-of schoolaccounts in Azure AD?
In een Azure AD-tenant gebruikers die deel uitmaken van de tenant toohello aanmelden met een e-mailadres van Hallo formulier `<xyz>@<tenant domain>`.  Hallo `<tenant domain>` is een van de Hallo geverifieerd domeinen in Hallo tenant of Hallo initiële `<...>.onmicrosoft.com` domein. Dit type account is een werk- of schoolaccount-account.

In een Azure AD B2C-tenant de meeste apps wilt Hallo gebruiker toosign in met een willekeurige e-mailadres (bijvoorbeeld joe@comcast.net, bob@gmail.com, sarah@contoso.com, of jim@live.com). Dit type account is een lokale account.  We bieden ook ondersteuning voor willekeurige gebruikersnamen als lokale accounts (bijvoorbeeld Jan, bob, sarah of jim). U kunt een van deze twee lokale accounttypen door Azure AD B2C configureren in hello Azure-portal.

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>Welke sociale identiteitsproviders ondersteund nu? Welke u wilt dat u van plan bent toosupport in toekomstige Hallo?
Wordt ondersteund Facebook, Google + LinkedIn, Amazon, Twitter (preview), WeChat (preview), Weibo (preview) en q (Preview). Er wordt ondersteuning toevoegen voor andere populaire social identiteitsproviders op basis van vraag van klanten.

Azure AD B2C is ook ondersteuning toegevoegd voor [aangepast beleid](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom).  Deze [aangepast beleid](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom) een ontwikkelaar toocreate toestaan hun eigen beleid dat met een id-provider die ondersteuning biedt voor [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) of SAML. 

Aan de slag met aangepast beleid door het uitchecken van onze [aangepast beleid starter pack](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack).

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>Kan ik configureren scopes toogather meer informatie over de consumenten van verschillende sociale id-providers?
Nee, maar deze functie is op onze roadmap. Hallo standaard bereiken die worden gebruikt voor onze ondersteunde set sociale identiteitsproviders zijn:

* Facebook: e-mailadres
* Google +: e-mailadres
* Microsoft-account: openid e-mailprofiel
* Amazon: profiel
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>Beschikt over mijn toepassing toobe uitvoeren in Azure voor het werken met Azure AD B2C?
Nee, kunt u uw toepassing overal (in Hallo cloud of on-premises) hosten. Alle benodigde toointeract met Azure AD B2C Hallo mogelijkheid toosend en ontvangen van HTTP-aanvragen op eindpunten openbaar toegankelijk is.

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>Ik heb meerdere tenants van Azure AD B2C. Hoe kan ik ze beheren op Hallo Azure-portal?
Voordat u het 'Azure AD B2C' Hallo linkerkant menu van hello Azure-portal opent, moet u overschakelen naar de map Hallo gewenste toomanage.  Overschakelen van mappen door te klikken op uw identiteit in de rechterbovenhoek Hallo van hello Azure-portal en kies vervolgens een map in Hallo vervolgkeuzelijst die wordt weergegeven.  Zie voor stapsgewijze met afbeeldingen, [tooAzure AD B2C-instellingen te navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>Hoe aanpassen bevestigingsmails (Hallo inhoud en Hallo ' uit: ' veld) die door Azure AD B2C verzonden?
U kunt Hallo [functie huisstijl van uw bedrijf](../active-directory/active-directory-add-company-branding.md) toocustomize Hallo inhoud van bevestigingsmails. In het bijzonder kunnen deze twee elementen van Hallo e-mail worden aangepast:

* **Logo banner**: die wordt weergegeven op Hallo rechtsonder.
* **De achtergrondkleur**: Hallo boven weergegeven.

    ![Schermopname van een aangepaste bevestigingsmail](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

Hallo e handtekening bevat de naam van de Hallo B2C tenant die u hebt opgegeven tijdens het maken van Hallo B2C-tenant. U kunt deze instructies Hallo-naam wijzigen:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) zoals Hallo Abonnementsbeheerder.
1. Navigeer tooyour B2C-tenant.
1. Klik op Hallo **configureren** tabblad.
1. Wijziging Hallo **naam** veld onder Hallo **mapeigenschappen** sectie.
1. Klik op **opslaan** Hallo Hallo pagina onderaan in.

Er is momenteel geen manier toochange Hallo ' uit: ' op Hallo e-mail. Stemmen over [feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails) u geïnteresseerd bent in het Hallo-hoofdtekst van Hallo bevestigingsmail aanpassen.

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>Hoe kan ik mijn bestaande gebruikersnamen en wachtwoorden, profielen van mijn database tooAzure AD B2C migreren?
U kunt het hulpprogramma voor migratie van hello Azure AD Graph API toowrite. Zie Hallo [Graph API-voorbeeld](active-directory-b2c-devquickstarts-graph-dotnet.md) voor meer informatie.

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Welke beleidsregels voor wachtwoorden voor lokale accounts in Azure AD B2C wordt gebruikt?
Hello Azure AD B2C-wachtwoordbeleid voor lokale accounts is gebaseerd op Hallo beleid voor Azure AD. Azure AD B2C wordt de registratie, registreren of aanmelden en het wachtwoord opnieuw instellen van beleidsregels gebruikt Hallo 'sterk' Wachtwoordsterkte en wachtwoorden niet verloopt. Lees Hallo [Azure AD-wachtwoordbeleid](https://msdn.microsoft.com/library/azure/jj943764.aspx) voor meer informatie.

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>Kan ik Azure AD Connect toomigrate consumentidentiteiten die zijn opgeslagen op mijn lokale Active Directory tooAzure AD B2C gebruiken?
Nee, Azure AD Connect is niet ontworpen toowork met Azure AD B2C. Overweeg het gebruik van Hallo [Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md) voor gebruikersmigratie.

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>Kan mijn app openen om Azure AD B2C-pagina's binnen een iFrame?
Nee, uit veiligheidsoverwegingen Azure AD B2C-pagina's niet openen binnen een iFrame.  Onze service communiceert met de Hallo browser tooprohibit iFrames.  in het algemeen security-community Hallo en Hallo OAUTH2-specificatie, met iFrames voor identiteitservaringen vanwege toohello risico steunpunten klik is voor u wordt aangeraden.

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Werkt Azure AD B2C met zoals Microsoft Dynamics CRM-systemen?
Integratie met Microsoft Dynamics 365 Portal is beschikbaar.  Zie [Dynamics 365-Portal configureren toouse Azure AD B2C voor verificatie](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c).

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C komt met SharePoint on-premises 2016 werk- of eerdere?
Azure AD B2C is niet bedoeld voor Hallo SharePoint externe partner delen scenario; Zie [Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx) in plaats daarvan.

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>Moet ik Azure AD B2C of B2B toomanage externe identiteiten gebruiken?
Lees dit artikel over [externe identiteiten](../active-directory/active-directory-b2b-compare-external-identities.md) toolearn meer over het toepassen van Hallo geschikte functies tooyour externe identiteit scenario's.

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Welke rapportage- en controle van functies Azure AD B2C biedt? Zijn dat ze dezelfde als in Azure AD Premium Hallo?
Nee, Azure AD B2C ondersteunt geen Hallo dezelfde met rapporten als Azure AD Premium set. Er zijn echter veel commonalities:

* Hallo-aanmelden-rapporten geven een record van elke aanmelden met verminderde details.
* Controlerapporten zijn beschikbaar in hello Azure-portal onder Azure Active Directory > activiteit controlelogboeken > Kies B2C en filters naar wens toepassen. Zowel admin-activiteit als activiteit van de toepassing worden behandeld. 
* Een gebruiksrapport die betrekking hebben op het aantal gebruikers, aantal aanmeldingen en volume van MFA is beschikbaar op [gebruik rapportage-API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>Kan ik Hallo UI van pagina's die worden bediend door Azure AD B2C localize? Welke talen worden ondersteund?
Ja.  Meer informatie over [taal aanpassing](active-directory-b2c-reference-language-customization.md), deze bevindt zich in de openbare preview.  We bieden vertalingen voor 36 talen en u kunt elke tekenreeks toosuit te overschrijven uw behoeften.

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>Kan ik mijn eigen URL's op mijn zich kunnen registreren en aanmelden pagina's die worden behandeld door Azure AD B2C gebruiken? Bijvoorbeeld, kan ik Hallo-URL van login.microsoftonline.com toologin.contoso.com wijzigen?
Momenteel niet. Deze functie is op onze roadmap. Verifiëren van uw domein in Hallo **domeinen** tabblad op Hallo klassieke Azure-portal biedt geen dit doel te bereiken.

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>Hoe verwijder ik mijn Azure AD B2C-tenant?
Volg deze stappen toodelete uw Azure AD B2C-tenant:

1. Volg deze stappen te[tooAzure AD B2C-instellingen te navigeren](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) op Hallo Azure-portal.
1. Navigeer toohello **toepassingen**, **identiteitsproviders**, en **alle beleidsregels** en verwijder alle Hallo vermeldingen in elk van deze servers.
1. Nu aanmelden toohello [klassieke Azure-portal](https://manage.windowsazure.com/) zoals Hallo Abonnementsbeheerder. (Gebruik Hallo dezelfde werken of schoolaccount of hetzelfde Microsoft-account dat u toosign voor Azure gebruikt Hallo.)
1. Active Directory-extensie aan de linkerkant Hallo toohello navigeren en klik op uw B2C-tenant.
1. Klik op Hallo **gebruikers** tabblad.
1. Selecteer elke gebruiker daarmee (uitsluiten Hallo Abonnementsbeheerder gebruiker u momenteel bent aangemeld als). Klik op **verwijderen** onderaan Hallo Hallo pagina en klik op **Ja** wanneer u wordt gevraagd.
1. Klik op Hallo **toepassingen** tabblad.
1. Selecteer **toepassingen mijn bedrijf eigenaar is van** in Hallo **weergeven** vervolgkeuzelijst en klik op Hallo selectievakje is ingeschakeld.
1. Een toepassing aangeroepen **b2c-uitbreidingen-app**. Klik op **verwijderen** onderaan Hallo Hallo pagina en klik op **Ja** wanneer u wordt gevraagd.
1. Navigeer toohello Active Directory-extensie opnieuw en selecteer uw B2C-tenant.
1. Klik op **verwijderen** Hallo Hallo pagina onderaan in. toocomplete hello proces Hallo Volg de instructies op het welkomstscherm.

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>Kan ik Azure AD B2C als onderdeel van Enterprise Mobility Suite krijgen?
Nee, Azure AD B2C wordt een betalen naar gebruik Azure-service en is geen onderdeel van Enterprise Mobility Suite.

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>Hoe meld ik problemen met Azure AD B2C
Zie [bestand ondersteuningsaanvragen voor Azure Active Directory B2C](active-directory-b2c-support.md).
