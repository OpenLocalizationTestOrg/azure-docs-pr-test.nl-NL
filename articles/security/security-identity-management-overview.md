---
title: aaaAzure beveiligingsfuncties die helpen met identity management | Microsoft Docs
description: " Dit artikel bevat een overzicht van hello Azure-beveiliging kernfuncties die u bij het identiteitsbeheer helpen. Microsoft identiteits- en toegangsbeheer management oplossingen zorgen ervoor dat IT beveiligen toegang tooapplications en bronnen in zakelijke datacenter hello en in de cloud hello, extra niveaus van validatie van de multi-factor Authentication-verificatie en voorwaardelijke inschakelen beleid voor toegang. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Overzicht van Azure identity management-beveiliging
Microsoft identiteits- en toegangsbeheer management oplossingen zorgen ervoor dat IT beveiligen toegang tooapplications en bronnen in zakelijke datacenter hello en in de cloud hello, extra niveaus van validatie van de multi-factor Authentication-verificatie en voorwaardelijke inschakelen beleid voor toegang. Bewaking verdachte activiteiten via geavanceerde beveiliging rapportage, controle en waarschuwingen helpt bij het verminderen mogelijke beveiligingsproblemen. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) biedt eenmalige aanmelding toothousands van cloudtoepassingen (SaaS)-apps en toegang tooweb apps u on-premises uitgevoerd.

Beveiligingsvoordelen van Azure Active Directory (AD) omvatten Hallo kunnen:

* Maken en beheren van één identiteit voor elke gebruiker in uw onderneming hybride, gebruikers, groepen en apparaten synchroon te houden
* Geef één aanmelding toegang tooyour toepassingen, waaronder duizenden vooraf geïntegreerde SaaS-apps
* Toepassingsbeveiliging toegang inschakelen door het afdwingen van multi-factor Authentication op basis van regels voor zowel on-premises en cloudtoepassingen
* Inrichten veilige externe toegang tooon-premises webtoepassingen via Azure AD-toepassingsproxy

Hallo doel van dit artikel is een overzicht van hello Azure-beveiliging kernfuncties die u bij het identiteitsbeheer helpen tooprovide. We bieden ook koppelingen tooarticles waarmee details van elk onderdeel, zodat u meer informatie.  

Hallo artikel is gericht op de volgende mogelijkheden voor identiteitsbeheer van Azure core Hallo:

* Eenmalige aanmelding
* Omgekeerde proxy
* Multi-Factor Authentication
* Beveiligingsbewaking, waarschuwingen en machine learning gebaseerde rapporten
* Identiteits- en toegangsbeheer van consumenten
* Apparaatregistratie
* Beschermde identiteitsbeheer
* Identiteitsbeveiliging
* Beheer van hybride identiteit

## <a name="single-sign-on"></a>Eenmalige aanmelding
Eenmalige aanmelding (SSO) betekent kunnen tooaccess wordt alle Hallo toepassingen en bronnen die u toodo bedrijven, nodig wanneer u zich aanmeldt bij het gebruik van slechts één keer één gebruikersaccount. Wanneer u bent aangemeld, kunt u alle Hallo toepassingen zonder de vereiste tooauthenticate wordt openen (bijvoorbeeld: Typ een wachtwoord) een tweede keer.

Veel organisaties zijn afhankelijk van de software als een dienst (SaaS)-toepassingen zoals Office 365, het selectievakje en Salesforce voor de productiviteit van eindgebruikers. In het verleden hebben IT-personeel nodig tooindividually maken en bijwerken van gebruikersaccounts in elke SaaS-toepassing en moesten gebruikers deze tooremember een wachtwoord op voor elke SaaS-toepassing.

Azure AD breidt on-premises Active Directory-omgevingen in de cloud hello, schakelen gebruikers toouse hun primaire organisatieaccount toonot alleen aanmelden tootheir domein apparaten en resources van het bedrijf, maar ook alle Hallo web- en SaaS-toepassingen nodig voor hun taak.

Niet alleen hebben gebruikers geen toomanage meerdere sets met gebruikersnamen en wachtwoorden, toegang tot de toepassing kan worden automatisch ingerichte of ongedaan ingerichte op basis van organisatie-groepen en hun status als een werknemer. Azure AD introduceert beveiliging en beheeracties toegangsbeheer waarmee u toocentrally toegang van gebruikers in de SaaS-toepassingen beheren.

Meer informatie:

* [Overzicht van eenmalige aanmelding](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Eenmalige aanmelding Azure Active Directory integreren met SaaS-apps](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Omgekeerde proxy
Azure AD-toepassingsproxy kunt u on-premises toepassingen, zoals publiceren [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) sites, [Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), en [IIS](http://www.iis.net/)-gebaseerde apps binnen uw particuliere netwerk en veilige toegang toousers buiten uw netwerk biedt. Een toepassing biedt externe toegang en eenmalige aanmelding (SSO) voor veel soorten on-premises webtoepassingen Hello duizendtallen van SaaS-toepassingen die ondersteuning biedt voor Azure AD. Werknemers kunnen zich aanmelden tooyour Apps uit home op hun eigen apparaten en via deze proxy cloud-gebaseerde te verifiëren.

Meer informatie:

* [Azure AD-toepassingsproxy inschakelen](../active-directory/active-directory-application-proxy-enable.md)
* [Toepassingen publiceren met Azure AD-toepassingsproxy](../active-directory/active-directory-application-proxy-publish.md)
* [Single-sign-on met toepassingsproxy](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Werken met voorwaardelijke toegang](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA) is een authenticatiemethode die vereist Hallo gebruik van meer dan één verificatiemethode en voegt een cruciale tweede beveiligingslaag van beveiliging toouser aanmeldingen en transacties. MFA helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Levert sterke verificatie via een aantal opties voor verificatie: telefoonoproep, tekstbericht of mobiele app melding of verificatie van code en van derden OAuth-tokens.

Meer informatie:

* [Multi-factor authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Wat is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)
* [De werking van Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Beveiligingsbewaking, waarschuwingen en machine learning gebaseerde rapporten
Beveiligingsbewaking en waarschuwingen en machine learning gebaseerde rapporten die inconsistente toegangspatronen aangeven kunt u uw bedrijf te beveiligen. U kunt toegang tot Azure Active Directory en gebruik rapporten toogain inzicht in Hallo integriteit en beveiliging van de directory van uw organisatie gebruiken. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.

Rapporten zijn in de klassieke Azure-portal hello onderverdeeld in Hallo volgende manieren:

* Rapporten voor afwijkingsdetectie – bevatten Meld u aan dat we toobe afwijkende gevonden gebeurtenissen. Ons doel is toomake u rekening houden met deze activiteit en kunt u toobe kunnen toomake om te bepalen of een gebeurtenis verdacht is.
* Geïntegreerde toepassing rapporten – bieden inzicht in hoe cloud-toepassingen in uw organisatie worden gebruikt. Azure Active Directory biedt integratie met duizenden cloud-toepassingen.
* Foutenrapporten – fouten die zich kunnen voordoen bij het inrichten van accounts tooexternal toepassingen aangeven.
* Apparaat/teken weergeven gebruikersspecifieke rapporten – in de activiteitsgegevens voor een specifieke gebruiker.
* Activiteitenlogboeken – bevatten een record van alle controlegebeurtenissen binnen Hallo afgelopen 24 uur en de laatste 7 dagen, of afgelopen 30 dagen en wijzigingen in groep activiteiten en activiteit voor wachtwoord opnieuw instellen en registratie.

Meer informatie:

* [Uw toegangs- en gebruiksrapporten weergeven](../active-directory/active-directory-view-access-usage-reports.md)
* [Aan de slag met Azure Active Directory-rapportage](../active-directory/active-directory-reporting-getting-started.md)
* [Handleiding voor rapportage van Azure Active Directory](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Identiteits- en toegangsbeheer van consumenten
Azure Active Directory B2C is een maximaal beschikbare, wereldwijde, identity management-service voor consumententoepassingen die schaalbaar toohundreds miljoenen identiteiten. De service kan worden geïntegreerd in zowel mobiele als webplatforms. Uw consumenten kunnen aanmelden tooall uw toepassingen via aanpasbare ervaringen met behulp van hun bestaande sociale accounts of maken van nieuwe referenties.

In de Hallo is afgelopen, zou toepassingsontwikkelaars die toosign up en meld u aan consumenten in hun toepassingen wilden hun eigen code hebt geschreven. En ze gebruikten lokale databases of systemen toostore gebruikersnamen en wachtwoorden. Azure Active Directory B2C biedt uw organisatie een betere manier toointegrate identiteitsbeheer van consumenten in toepassingen met help Hallo van een veilige, op standaarden gebaseerd platform en een grote set uitbreidbare beleidsregels.

Wanneer u Azure Active Directory B2C gebruikt, uw consumenten zich registreren voor uw toepassingen met behulp van hun bestaande sociale accounts (Facebook, Google, Amazon, LinkedIn) of door het maken van nieuwe referenties (e-mailadres en wachtwoord of gebruikersnaam en wachtwoord).

Meer informatie:

* [Wat is Azure Active Directory B2C?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C preview: aanmelden en aanmelden van gebruikers in uw toepassingen](../active-directory-b2c/active-directory-b2c-overview.md)
* [Azure Active Directory B2C Preview: Typen toepassingen](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Apparaatregistratie
Azure AD-apparaatregistratie vormt de basis Hallo voor op basis van apparaten [voorwaardelijke toegang](../active-directory/active-directory-conditional-access-device-registration-overview.md) scenario's. Wanneer een apparaat is geregistreerd, biedt Azure Active Directory-apparaatregistratie Hallo-apparaat met een identiteit die is gebruikt tooauthenticate Hallo apparaat wanneer Hallo gebruiker zich aanmeldt. vervolgens Hallo geverifieerde apparaat en Hallo kenmerken van Hallo-apparaat, kunnen de gebruikte tooenforce beleidsregels voor voorwaardelijke toegang voor toepassingen die worden gehost in Hallo cloud en on-premises worden.

In combinatie met een oplossing voor mobiele apparaten management (MDM) zoals Intune, worden Hallo apparaatkenmerken in Azure Active Directory bijgewerkt met aanvullende informatie over het Hallo-apparaat. Hiermee kunt u regels voor voorwaardelijke toegang toocreate die toegang van apparaten toomeet afdwingen uw standaarden voor beveiliging en naleving.

Meer informatie:

* [Aan de slag met Azure Active Directory-apparaatregistratie](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Automatische apparaatregistratie met Azure Active Directory voor Windows-domein-apparaten](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Instellen van automatische registratie van Windows-apparaten met Azure Active Directory-domein](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Beschermde identiteitsbeheer
Azure Active Directory (AD) Privileged Identity Management kunt u beheren, te beheren en bewaken van bevoegde identiteiten en toegang tooresources in Azure AD, evenals andere Microsoft online services zoals Office 365 of Microsoft Intune.

Gebruikers moeten soms toocarry bevoorrechte bewerkingen in de resources in Azure of Office 365 of andere SaaS-apps. Dit betekent vaak organisaties hebben toogive ze permanente bevoegde toegang in Azure AD. Dit is een groeiende beveiligingsrisico voor cloud-gebaseerde bronnen omdat organisaties voldoende kunnen niet controleren wat gebruikers doen met hun beheerdersbevoegdheden. Als een gebruikersaccount met uitgebreide toegang is aangetast, kan die een inbreuk bovendien invloed op de algehele beveiliging van de cloud. Azure AD Privileged Identity Management helpt tooresolve dit risico.

Azure AD Privileged Identity Management kunt u:

* Zien welke gebruikers zijn Azure AD-beheerders
* On-demand 'just in time' beheerderstoegang tooMicrosoft Online Services, zoals Office 365 en Intune inschakelen
* Rapporten over beheerder toegang tot geschiedenis en wijzigingen in beheerderstoewijzingen ophalen
* Ontvang waarschuwingen over toegang tooa bevoorrechte rol

Meer informatie:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Rollen in Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Hoe tooadd of een gebruikersrol verwijderen](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Identiteitsbeveiliging
Azure AD Identity Protection is een beveiligingsservice waarmee een geconsolideerde weergave risicogebeurtenissen en mogelijke beveiligingsproblemen die invloed hebben op de identiteiten van uw organisatie. Identity Protection maakt gebruik van bestaande Azure Active Directory van afwijkingsdetectie-detectiemogelijkheden (beschikbaar via Azure AD-rapporten voor afwijkende activiteiten) en introduceert nieuwe risico gebeurtenistypen die afwijkingen in realtime kunnen detecteren.

Meer informatie:

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [Channel 9: Azure AD en Identity weergeven: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Beheer van hybride identiteit
Microsoft benadering tooidentity reeksen on-premises en Hallo cloud, tooall netwerkbronnen, ongeacht de locatie van de identiteit van een enkele gebruiker voor verificatie en autorisatie maken.

Meer informatie:

* [Witboek van hybride identiteit](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Active Directory-teamblog](https://blogs.technet.microsoft.com/ad/)
