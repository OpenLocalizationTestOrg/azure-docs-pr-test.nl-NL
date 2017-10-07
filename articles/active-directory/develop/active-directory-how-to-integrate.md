---
title: aaaHow tooIntegrate met Azure Active Directory | Microsoft Docs
description: Een handleiding toobenefits van en resources voor de integratie met Azure Active Directory.
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: d13bba54-96bd-4b81-bee9-c8025ffa1648
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 4542965ae4a7756eda9f57e9e895f8044892f20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-azure-active-directory"></a>Integreren met Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory biedt organisaties met bedrijfsniveau Identiteitsbeheer voor cloud-toepassingen.  Azure AD-integratie geeft uw gebruikers een gestroomlijnde ervaring aanmelden en helpt u uw toepassing tooIT beleid voldoen.

## <a name="how-toointegrate"></a>Hoe tooIntegrate
Er zijn verschillende manieren om uw toepassing toointegrate met Azure AD.  Profiteren van veel of enkele van deze scenario's zoals geschikt is voor uw toepassing.

### <a name="support-azure-ad-as-a-way-toosign-in-tooyour-application"></a>Ondersteuning voor Azure AD als een manier tooSign In tooYour toepassing
**Aanmelden wrijving verminderen en de ondersteuningskosten reduceren.** Met behulp van Azure AD-toosign in tooyour toepassing, uw gebruikers hebben geen één meer naam en het wachtwoord tooremember.  Als ontwikkelaar, u hebt een minder wachtwoord toostore en beveiligen.  Omdat u niet hoeft toohandle vergeten wachtwoorden, kan een aanzienlijke besparing alleen zijn.  Azure AD drijft aanmelden voor een aantal Hallo wereld van meest populaire cloudtoepassingen, met inbegrip van Office 365 en Microsoft Azure.  Met honderden miljoenen gebruikers van miljoenen organisaties kans op zijn tooAzure AD al uw gebruiker is aangemeld.  Meer informatie over [ondersteuning voor Azure AD aanmelding toe te voegen](active-directory-authentication-scenarios.md).

**Aanmelding van vereenvoudigen voor uw toepassing.**  Tijdens de aanmelding voor uw toepassing, kan Azure AD essentiële informatie over een gebruiker verzenden zodat u kunt vooraf vul je aanmelding formulier of volledig elimineren.  Gebruikers kunnen zich registreren voor uw toepassing met behulp van hun Azure AD-account via een bekend toestemming ervaring vergelijkbare toothose gevonden in sociale media en mobiele toepassingen.  Elke gebruiker kan registreren en aanmelden tooan-toepassing die is geïntegreerd met Azure AD zonder tussenkomst van de IT.  Meer informatie over [ondertekening van uw toepassing voor Azure AD-Account aanmelding](../../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

### <a name="browse-for-users-manage-user-provisioning-and-control-access-tooyour-application"></a>Zoeken naar gebruikers, beheren van gebruikers inrichten en toegangsbeheer tooYour toepassing
**Blader naar gebruikers in Hallo-directory.**  Gebruik Hallo Graph API toohelp gebruikers zoeken en bladeren voor andere personen in hun organisatie wanneer andere gebruikers uitnodigen of verlenen van toegang, in plaats van vereisen dat ze tootype e-mailadressen.  Gebruikers kunnen bladeren met behulp van een bekende adres adresboek stijlinterface, inclusief Hallo details weergeven van de organisatie-hiërarchie Hallo.  Meer informatie over Hallo [Graph API](active-directory-graph-api.md).

**Active Directory-groepen en distributielijsten die al wordt beheerd door de klant opnieuw gebruiken.**  Azure AD bevat Hallo groepen die uw klant al wordt gebruikt voor e-maildistributie en toegang beheren.  Hallo Graph API gebruikt, opnieuw gebruiken van deze groepen in plaats van uw klant toocreate vereisen en beheren van een afzonderlijke set met groepen in uw toepassing.  Groepsgegevens kunnen ook worden verzonden tooyour toepassing in aanmelden tokens.  Meer informatie over Hallo [Graph API](active-directory-graph-api.md).

**Azure AD-toocontrol wie toegang tot tooyour toepassing heeft gebruiken.**  Beheerders en eigenaren van de toepassing in Azure AD kunnen u access tooapplications toospecific gebruikers en groepen toewijzen.  Hallo Graph API gebruikt, kunt u deze lijst lezen en gebruiken deze toocontrol inrichten en de inrichting van resources en toegang in uw toepassing.

**Gebruik Azure AD voor rollen gebaseerd toegangsbeheer.**  Beheerders en eigenaren van de toepassing kunnen toewijzen, gebruikers en groepen tooroles die u definieert wanneer u uw toepassing in Azure AD registreren.  Gegevens over de serverfunctie tooyour toepassing wordt verzonden in tokens aanmelden en kan ook worden gelezen met Hallo Graph API.  Meer informatie over [gebruikmaken van Azure AD voor autorisatie](http://blogs.technet.com/b/ad/archive/2014/12/18/azure-active-directory-now-with-group-claims-and-application-roles.aspx).

### <a name="get-access-toousers-profile-calendar-email-contacts-files-and-more"></a>Get toegang tooUser profiel, agenda, E-mail, contactpersonen, bestanden en meer
**Azure AD is Hallo autorisatie server voor Office 365 en andere zakelijke services van Microsoft.**  Als u Azure AD voor aanmelding tooyour toepassing of ondersteuning voor het koppelen van de huidige gebruiker accounts tooAzure AD gebruikersaccounts met behulp van OAuth 2.0 ondersteunt, kunt u lezen en schrijftoegang tooa gebruiker profiel, agenda, e-mail, contactpersonen, bestanden en andere informatie vragen.  U kunt naadloos van gebeurtenissen toouser kalender, schrijven en lezen of schrijven bestanden tootheir OneDrive.  Meer informatie over [toegang tot Office 365-API's Hallo](https://msdn.microsoft.com/office/office365/howto/platform-development-overview).

### <a name="promote-your-application-in-hello-azure-and-office-365-marketplaces"></a>Uw toepassing in hello Azure en Office 365 marktplaatsen promoveren
**Promoveren van uw toepassing toohello miljoenen van organisaties die al van Azure AD gebruikmaken.**  Gebruikers die zoeken en deze marktplaatsen al gebruikmaakt van een of meer cloud-services, zodat ze cloud-serviceklanten gekwalificeerd.  Meer informatie over het wijzigen van uw toepassing in [hello Azure Marketplace](https://azure.microsoft.com/marketplace/partner-program/).

**Wanneer gebruikers zich registreren voor uw toepassing, wordt deze weergegeven in hun Azure AD-Toegangsvenster en Office 365-app starten.**  Kunnen gebruikers zich kunnen tooquickly en later eenvoudig return tooyour toepassing gebruiker engagement verbeteren.  Meer informatie over Hallo [Azure AD-Toegangsvenster](../active-directory-saas-access-panel-introduction.md).

### <a name="secure-device-to-service-and-service-to-service-communication"></a>Veilige communicatie voor apparaat-naar-Service en Service-naar-Service
**Hallo code u toowrite nodig hebt en kan IT toomanage toegang worden ingeschakeld met behulp van Azure AD voor het identiteitsbeheer van services en apparaten worden beperkt.**  Services en apparaten tokens van Azure AD met behulp van OAuth ophalen en deze tokens tooaccess web API's gebruiken.  Met behulp van Azure AD kunt u voorkomen schrijven complexe verificatiecode op te geven.  Omdat Hallo identiteiten Hallo services en apparaten worden opgeslagen in Azure AD, IT-sleutels en intrekken op één plek in plaats van toodo dit afzonderlijk in uw toepassing kunt beheren.

## <a name="benefits-of-integration"></a>Voordelen van de integratie
Integratie met Azure AD wordt geleverd met voordelen, u geen aanvullende code toowrite hoeft.

### <a name="integration-with-enterprise-identity-management"></a>Integratie met Enterprise-identiteitsbeheer
**Uw toepassing voldoen aan de IT-beleid helpen.**  Organisaties hun onderneming systemen voor identiteitsbeheer integreren met Azure AD, dus als een persoon een organisatie verlaat, ze automatisch toegang tooyour toepassing zonder gewenst tootake IT extra stappen uitvoeren verbroken wordt.  IT kunt beheren die toegang tot uw toepassing en bepalen welke toegangsbeleid zijn vereist - voorbeeld multi-factor Authentication - uw toocomply nodig toowrite code met complexe bedrijfsbeleid verminderen.  Azure AD biedt beheerders een gedetailleerde controlelogboek van die aangemeld tooyour toepassing zodat IT bijhouden van gebruik.

**Azure AD breidt de Active Directory toohello cloud zodat uw toepassing kan worden geïntegreerd met AD.**  Veel organisaties Hallo wereld Active Directory gebruiken als hun principal aanmelden en identiteitsbeheersysteem en hun toepassingen toowork met AD vereisen.  Uw app integreren met Azure AD worden geïntegreerd met Active Directory.

### <a name="advanced-security-features"></a>Geavanceerde beveiligingsfuncties
**Multi-factor authentication-server.**  Azure AD levert systeemeigen multi-factor authentication-server.  IT-beheerders kunnen vereisen multi-factorauthenticatie tooaccess uw toepassing, zodat er geen toocode deze ondersteuning zelf.  Meer informatie over [multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/).

**Afwijkende aanmelden detectie.**  Azure AD processen meer dan een miljard aanmeldingen per dag, tijdens het gebruik van machine learning-algoritmen toodetect verdachte activiteit en IT-beheerders van mogelijke problemen melden.  Dankzij de ondersteuning van Azure AD-aanmeldingspagina, haalt uw toepassing hello voordeel van deze beveiligingsgroep. Meer informatie over [Azure Active Directory-rapport weer te geven](../active-directory-view-access-usage-reports.md).

**Voorwaardelijke toegang.**  Bovendien toomulti-factor authentication, kunnen beheerders opgeven dat bepaalde voorwaarden worden voldaan voordat gebruikers kunnen aanmelden tooyour toepassing.  Voorwaarden die kunnen worden ingesteld zijn Hallo IP-adresbereik van clientapparaten, lidmaatschap in de opgegeven groepen en Hallo-status van de Hallo-apparaat wordt gebruikt om toegang te krijgen.  Meer informatie over [voorwaardelijke toegang van Azure Active Directory](../active-directory-conditional-access.md).

### <a name="easy-development"></a>Eenvoudige manier kunt ontwikkelen
**Protocollen volgens de industrienorm.**  Microsoft is doorgevoerd toosupporting industrienormen.  Azure AD ondersteunt Hallo SAML 2.0, OpenID Connect 1.0, OAuth 2.0 en WS-Federation 1.2 verificatieprotocollen.  Hallo Graph API is OData 4.0-compatibel.  Als de toepassing al Hallo SAML 2.0 of OpenID Connect 1.0-protocollen voor federatieve aanmelding ondersteunt, ondersteuning voor Azure AD toe te voegen zijn eenvoudige.  Meer informatie over [Azure AD-verificatieprotocollen ondersteund](active-directory-authentication-protocols.md).

**Open-source bibliotheken.**  Microsoft biedt een volledig ondersteunde open-source bibliotheken voor populaire talen en platforms toospeed-ontwikkeling.  Hallo-broncode wordt in licentie gegeven onder Apache 2.0 en u gratis toofork en bijdragen back toohello projecten.  Meer informatie over [Azure AD-verificatiebibliotheken](active-directory-authentication-libraries.md).

### <a name="worldwide-presence-and-high-availability"></a>Wereldwijde aanwezigheid en hoge beschikbaarheid
**Azure AD wordt is geïmplementeerd in datacenters Hallo wereld en beheerd en bewaakt rond Hallo klok.**  Azure AD is Hallo identiteitsbeheersysteem voor Microsoft Azure en Office 365 en is geïmplementeerd in 28 datacenters Hallo wereld.  Directorygegevens wordt gerepliceerd toobe tooat minimaal drie datacenters gegarandeerd.  Globale netwerktaakverdelers Zorg ervoor dat gebruikers toegang krijgen tot de dichtstbijzijnde Hallo-exemplaar van Azure AD met hun gegevens en automatisch opnieuw routeren vraagt tooother datacenters als er een probleem wordt gedetecteerd.

## <a name="next-steps"></a>Volgende stappen
[Schrijven van code aan de slag](active-directory-developers-guide.md#get-started).

[Gebruikers aanmelden met behulp van Azure AD](active-directory-authentication-scenarios.md)

