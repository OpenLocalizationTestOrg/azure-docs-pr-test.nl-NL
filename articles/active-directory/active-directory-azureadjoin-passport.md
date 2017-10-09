---
title: aaaAuthenticating identiteiten zonder wachtwoorden via Windows Hello voor bedrijven en Azure AD | Microsoft Docs
description: Biedt een overzicht van Windows Hello voor bedrijven en aanvullende informatie over het implementeren van Windows Hello voor bedrijven.
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Identiteiten zonder wachtwoorden via Windows Hello voor bedrijven verifiëren
Hallo huidige methoden voor verificatie met wachtwoorden die alleen zijn niet voldoende tookeep gebruikers veilig. Gebruikers gebruiken en vergeten wachtwoorden. Wachtwoorden worden breachable, phishable, foutgevoelige toocracks en te raden. Krijgen ze ook moeilijk tooremember en foutgevoelige tooattacks, zoals '[pass-Hallo hash](https://technet.microsoft.com/dn785092.aspx)'.

## <a name="about-windows-hello-for-business"></a>Over Windows Hello voor bedrijven
Windows Hello voor bedrijven is een persoonlijke/openbare sleutel of benadering voor verificatie op basis van certificaten voor organisaties en consumenten die zich verder uitstrekt dan wachtwoorden. Deze vorm van verificatie, afhankelijk van sleutelpaar referenties die wachtwoorden en toobreaches zijn tegen diefstal en phishing kunnen vervangen.

 Windows Hello voor bedrijven een gebruiker kan verifiëren tooa Microsoft-account, een Windows Server Active Directory-account, een Microsoft Azure Active Directory (Azure AD)-account of een niet-Microsoft-service die snel identiteit Online (FIDO) authenticatie ondersteunt. Na een initiële in twee stappen verificatie tijdens Windows Hello voor bedrijven-inschrijving, Windows Hello voor bedrijven is ingesteld op Hallo gebruikersapparaat en Hallo gebruiker stelt een gebaar, kan dit Windows Hello of een PINCODE. Hallo gebruiker biedt Hallo gebaar tooverify hun identiteit. Windows maakt gebruik van Windows Hello voor bedrijven tooauthenticate Hallo gebruiker vervolgens en sneller tooaccess beveiligde resources en services.

Hallo persoonlijke sleutel wordt beschikbaar gesteld uitsluitend via een 'Gebaar van de gebruiker' zoals een PINCODE, biometrie of een extern apparaat zoals een smartcard die gebruiker Hallo toosign toohello apparaat gebruikt. Deze informatie is gekoppelde tooa certificaat of een asymmetrisch sleutelpaar. Hallo persoonlijke sleutel is hardware Attestation als Hallo apparaat een chip Trusted Platform Module (TPM heeft). de persoonlijke sleutel Hallo nooit Hallo apparaat zal verlaten.

Hallo openbare sleutel is geregistreerd bij Azure Active Directory en Windows Server Active Directory (voor on-premises). ID-Providers (IDPs) Hallo gebruiker valideren door toewijzing Hallo openbare sleutel van Hallo gebruiker toohello persoonlijke sleutel en informatie aanmelden via één keer wachtwoord (OTP), PhoneFactor of een andere meldingsmechanisme bieden.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Waarom ondernemingen dient vast te stellen Windows Hello voor bedrijven
Als u Windows Hello voor bedrijven, kunnen ondernemingen maken hun resources nog beter beveiligen door:

* Instellen van Windows Hello voor bedrijven met een hardware-voorkeurs-optie. Dit betekent dat sleutels op TPM 1.2 of TPM 2.0 zodra deze beschikbaar wordt gegenereerd. Wanneer er geen TPM beschikbaar is, wordt de software Hallo sleutel gegenereerd.
* Definiërende Hallo complexiteit en de lengte van Hallo VASTMAKEN aan en of gebruik Hallo is ingeschakeld in uw organisatie.
* Configuratie van Windows Hello voor bedrijven toosupport smartcard-achtige scenario's door gebruik te maken op basis van het certificaat vertrouwen.

## <a name="how-windows-hello-for-business-works"></a>Hoe Windows Hello voor bedrijven werkt
1. Sleutels worden gegenereerd op Hallo-hardware door TPM of software. Veel apparaten hebben een ingebouwde TPM-chip die Hallo hardware beveiligt door te integreren cryptografische sleutels in apparaten. TPM 1.2 of TPM 2.0 genereert sleutels of certificaten die zijn gemaakt op basis van sleutels Hallo gegenereerd.
2. Hallo TPM verklaart deze sleutels hardware is gebonden.
3. Een gebaar van één ontgrendelen ontgrendelt Hallo-apparaat. Dit gebaar kunt toegang tot toomultiple bronnen als Hallo-apparaat lid van een domein of Azure is die lid zijn van AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>De werking van Hallo Windows Hello voor bedrijven-levenscyclus
![Windows Hello voor bedrijven levenscyclus](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Hallo illustreert voorgaande diagram Hallo persoonlijke/openbare sleutelpaar en Hallo validatie door de identiteitsprovider Hallo. Elk van deze stappen wordt uitgelegd in detail hier:

1. Hallo gebruiker uw bewijs van hun identiteit via meerdere ingebouwde taalprogramma methoden (gebaren, fysieke smartcards, multi-factor authentication-Server) en verzendt deze gegevens tooan identiteit Provider (IDP) zoals Azure Active Directory of on-premises Active Directory.
2. Hallo apparaat vervolgens Hallo sleutel gemaakt, verklaart Hallo sleutel Hallo openbare deel van deze sleutel wordt, worden deze gekoppeld met station instructies, zich aanmeldt en verzendt het toohello IDP tooregister Hallo sleutel.
3. Zodra de Hallo IDP registreert Hallo openbare deel van de sleutel hello, Hallo Hallo IDP uitdagingen apparaat toosign met Hallo persoonlijke gedeelte van Hallo-sleutel.
4. Hallo IDP vervolgens valideert en problemen Hallo verificatietoken waarmee Hallo gebruiker en Hallo apparaat toegang tot Hallo beveiligde bronnen. IDPs kunt schrijven platformoverschrijdende apps of gebruik toocreate voor browser-ondersteuning (via JavaScript/Webcrypto API's) en gebruiken Windows Hello voor bedrijven-referenties voor de gebruikers.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>Hallo-implementatievereisten voor Windows Hello voor bedrijven
### <a name="at-hello-enterprise-level"></a>Op ondernemingsniveau Hallo
* Hallo enterprise heeft een Azure-abonnement.

### <a name="at-hello-user-level"></a>Op gebruikersniveau Hallo
* computer van de gebruiker Hello wordt uitgevoerd voor Windows 10 Professional of Enterprise.

Zie voor gedetailleerde implementatie-instructies [inschakelen Windows Hello voor bedrijven in Hallo organisatie](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)

