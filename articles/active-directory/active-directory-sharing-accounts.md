---
title: aaaSharing accounts met behulp van Azure AD | Microsoft Docs
description: Hierin wordt beschreven hoe Azure Active Directory kunnen organisaties toosecurely share accounts voor consumer-cloudservices en lokale apps.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Accounts delen met Azure AD
## <a name="overview"></a>Overzicht
Soms moeten organisaties toouse een één gebruikersnaam en wachtwoord voor meerdere mensen. Dit gebeurt gewoonlijk in twee gevallen:

* Bij het openen van toepassingen waarvoor een unieke gebruikersnaam en wachtwoord voor elke gebruiker of lokale apps of de consument cloudservices (bijvoorbeeld zakelijke sociale media-accounts).
* Bij het maken van omgeving met meerdere gebruikers. U hebt een lokale account met bevoegdheden verhoogde en gebruikte toodo core-installatie, beheer en herstel activiteiten (bijvoorbeeld Hallo 'globale beheerder' lokale account voor Office 365 of Hallo root-account in Salesforce) kan worden.

Normaal, zou deze accounts worden gedeeld door distribueren Hallo referenties (gebruikersnaam en wachtwoord) toohello juiste personen of ze opslaan in een gedeelde locatie waar meerdere vertrouwde agents er toegang toe.

Hallo traditionele delen model heeft enkele nadelen:

* Toegang toonew toepassingen inschakelen, moet u toodistribute referenties tooeveryone die toegang nodig heeft.
* Elke gedeelde toepassing moet mogelijk een eigen unieke set van gedeelde referenties, meerdere sets met referenties van gebruikers tooremember vereisen. Wanneer gebruikers tooremember veel referenties hebben, verhoogt Hallo risico dat ze is het versiebeheer van toorisky procedures. (bijvoorbeeld schrijven wachtwoorden).
* U kunt niet controleren wie heeft toegang tot tooan toepassing.
* U kunt niet controleren wie heeft *toegankelijk* een toepassing.
* Wanneer u tooremove toegang tooan toepassing, u tooupdate Hallo referenties hebben en deze opnieuw distribueren tooeveryone die toegang moet hebben tot toothat toepassing.

## <a name="azure-active-directory-account-sharing"></a>Azure Active Directory-account delen
Azure AD levert een nieuwe benadering toousing gedeeld accounts waarmee deze nadelen.

Hello Azure AD-beheerder configureert welke toepassingen die een gebruiker toegang heeft met Hallo Toegangspaneel en type van eenmalige aanmelding het meest geschikt voor die toepassing hello kiezen. Een van deze typen *op basis van wachtwoorden eenmalige aanmelding*, kunt u Azure AD fungeren als een soort 'broker' tijdens het Hallo eenmalige aanmelding voor die app.

Gebruikers melden zich in één keer aan hun organisatieaccount is gekoppeld. Dit is Hallo hetzelfde account dat ze tooaccess regelmatig hun bureaublad of e-mailbericht gebruiken. Ze kunnen detecteren en toegang tot alleen de toepassingen die ze worden toegewezen aan. Deze lijst van toepassingen kan een onbeperkt aantal gedeelde referenties bevatten met gedeelde accounts. Hallo eindgebruiker niet tooremember moet of schrijf Hallo diverse accounts dat kunnen worden gebruikt.

Gedeelde accounts niet alleen toezicht verhogen en de bruikbaarheid verbeteren, ze ook de beveiliging verbeteren. Gebruikers met machtigingen toouse Hallo referenties Hallo gedeelde wachtwoord niet ziet, maar in plaats daarvan krijgt machtigingen toouse Hallo wachtwoord als onderdeel van een verificatiestroom geregiseerde. Met sommige toepassingen van de SSO-wachtwoord hebt u bovendien Hallo optie toohave Azure AD periodiek rollover (update) Hallo-wachtwoord met behulp van grote, complexe wachtwoorden, Hallo accountbeveiliging verhogen. Hallo beheerder kan eenvoudig verlenen of intrekken van toegang tooan toepassing en ook weten wie heeft toegang tot toohello account en wie het heeft geopend in de afgelopen Hallo.

Azure AD biedt ondersteuning voor gedeelde accounts voor een Enterprise Mobility Suite (EMS) Premium of Basic gelicentieerde gebruikers alle typen van één wachtwoord aanmelden op toepassingen. U kunt accounts voor een van de duizenden vooraf geïntegreerde toepassingen in Hallo-toepassingsgalerie delen en uw eigen toepassing wachtwoord verifiëren met toevoegen [aangepaste SSO apps](active-directory-sso-integrate-saas-apps.md).

Azure AD-functies die delen van het account inschakelen:

* [Eenmalige aanmelding wachtwoord](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Één wachtwoord aanmelding agent
* [Toewijzing van updategroep](active-directory-accessmanagement-self-service-group-management.md)
* Aangepast wachtwoord apps
* [App-dashboard/gebruiksrapporten](active-directory-passwords-get-insights.md)
* De gebruiker toegang portals
* [App-proxy](active-directory-application-proxy-get-started.md)
* [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Delen van een account
Azure AD toouse tooshare een account moet u naar:

* Een toepassing toevoegen [app-galerie](https://azure.microsoft.com/marketplace/active-directory/) of [aangepaste toepassing](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Hallo-toepassing voor eenmalige aanmelding (SSO) wachtwoord configureren
* Gebruik [toewijzing op basis van een groep](active-directory-accessmanagement-group-saasapps.md) en selecteer optie tooenter Hallo een gedeelde referentie
* Optioneel: in sommige toepassingen, zoals Facebook, Twitter en LinkedIn, kunt u Hallo optie inschakelen voor [Azure AD geautomatiseerde wachtwoord roll-over](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

U kunt ook uw gedeelde account beter beveiligen met multi-factor Authentication (MFA) (meer informatie over [beveiliging van toepassingen met Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) en kunt u Hallo mogelijkheid toomanage die gebruikt voor toegang tot toohello toepassing is delegeren [Azure AD-Self-service](active-directory-accessmanagement-self-service-group-management.md) groepsbeheer.

## <a name="related-articles"></a>Verwante artikelen:
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Apps met voorwaardelijke toegang beveiligen](active-directory-conditional-access.md)
* [Groepsbeheer met Self-Service management/SSAA](active-directory-accessmanagement-self-service-group-management.md)

