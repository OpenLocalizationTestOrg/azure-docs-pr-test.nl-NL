---
title: Hallo-Toegangsvenster aaaWhat is in Azure Active Directory? | Microsoft Docs
description: Meer informatie over hoe toouse variaties van Hallo toegang krijgen tot Configuratiescherm (webbrowser, Android-app, app iPhone en iPad) tooaccess SaaS-apps.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Wat is het toegangsvenster Hallo?

Hallo toegangspaneel is een webportal. Dit kan een gebruiker met een werk of schoolaccount in Azure Active Directory tooview en start cloud-gebaseerde toepassingen een Azure AD-beheerder heeft verleend ze toegang hebben tot. U kunt ook groepsbeheer met Self-service en beheermogelijkheden van de app via het toegangsvenster hello gebruiken.

Hallo toegangspaneel is gescheiden van hello Azure-portal en doet u dit niet toohave een Azure-abonnement.

![Toegangsvenster][1]

Hallo-Toegangsvenster kunt u enkele van uw profielinstellingen, inclusief de mogelijkheid om te Hallo tooedit:

- Hallo-wachtwoord wijzigen die zijn gekoppeld aan een account voor werk of school

- Bewerken van instellingen voor wachtwoord opnieuw instellen

- Neem contact op met en voorkeur instellingen gerelateerde toomulti-factor authentication bewerken (voor accounts die vereist toouse zijn deze door een beheerder)

- Account details, zoals gebruikers-ID, alternatieve e-mailadres en mobile en office telefoonnummers en apparaten bekijken

- Weergeven en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot. Zie voor meer informatie over Hallo Toegangsvenster vanuit Hallo gebruikers perspectief met behulp van het toegangsvenster Hallo. 

- Groepen zelf beheren. Meer specifiek, kunt Hallo beheerder maken en beheren van beveiligingsgroepen en aanvraag beveiligingsgroepen in Azure AD. Zie voor meer informatie [groepsbeheer met Self-service voor gebruikers in Azure AD](active-directory-accessmanagement-self-service-group-management.md) en [groepen beheren](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Toegang tot het toegangsvenster Hallo

U kunt Hallo Toegangsvenster openen via de volgende URL in een webbrowser Hallo:`http://myapps.microsoft.com`

Als u aangepaste huisstijl is geconfigureerd voor de aanmeldingspagina hebt, kunt u deze huisstijl door uw organisatie domein toohello einde van Hallo-URL toe te voegen kunt laden:`http://myapps.microsoft.com/<your domain>.com`

In dit geval kunt u een actieve of een geverifieerde domeinnaam die is geconfigureerd in uw Azure-portal.

![Wingtip Toys domeinnaam][2]  

U moet toodistribute Hallo URL tooall gebruikers die u ondertekent in tooapplications die zijn geïntegreerd met Azure AD.

## <a name="authentication"></a>Authentication

toegangspaneel voor tooreach hello, u moet worden geverifieerd via een account voor werk of school in Azure AD. U kunt geverifieerde op tooAzure AD rechtstreeks zijn. U kunt ook als een organisatie heeft federation geconfigureerd met behulp van Active Directory Federation Services (AD FS) of andere technologieën, kan u worden geverifieerd door Windows Server Active Directory.

Als u een abonnement voor Azure of Office 365 hebt en u hebt gebruikt hello Azure-portal of een Office 365-toepassing, ziet u Hallo lijst met toepassingen zonder aanmelden opnieuw. Als u niet bent geverifieerd u na vragen aan gebruiker toosign in met behulp van Hallo gebruikersnaam en wachtwoord voor uw account in Azure AD zijn. Als uw organisatie heeft federation geconfigureerd, is te typen Hallo gebruikersnaam voldoende.

Wanneer u bent geverifieerd, kunt u samenwerken met Hallo-toepassingen die door uw beheerder is geïntegreerd met Hallo-directory. hoe toepassingen met Azure AD toointegrate zien toolearn [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Vereisten voor webbrowsers

Ten minste Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld. Voor Hallo gebruiker toobe aangemeld tooapplications via op basis van wachtwoorden eenmalige aanmelding (SSO), moet de uitbreiding voor toegang tot Configuratiescherm Hallo in uw browser worden geïnstalleerd. Hallo-extensie wordt automatisch gedownload wanneer u een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden selecteert.

Hallo toegang Configuratiescherm-uitbreiding is momenteel beschikbaar voor Internet Explorer 8 en hoger, Microsoft Edge en Chrome Firefox browsers.

## <a name="mobile-app-support"></a>Ondersteuning voor mobiele Apps

Hello Azure Active Directory-team publiceert Hallo mijn mobiele app van apps. Wanneer u Hallo-app installeert, kunt u zich aanmeldt toopassword gebaseerde SSO-toepassingen voor iOS en Android-apparaten.

> [!NOTE]
> U kunt tooapplications die ondersteuning bieden voor federatie met Azure AD (inclusief Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365 en meer dan 70 anderen) aanmelden op vrijwel elke webbrowser op elk apparaat zonder een invoegtoepassing of mobiele app. Alle andere [toegang tot Configuratiescherm ervaringen](https://myapps.microsoft.com/) ook vereisen geen Hallo mijn mobiele app apps toobe op een mobiel apparaat gebruikt.
>
>

### <a name="my-apps-for-android"></a>Mijn apps voor Android

Mijn apps voor Android wordt ondersteund op een Android-apparaat met Android versie 4.1 en hoger.  
Is beschikbaar in de Hallo [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![Mijn apps voor Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>Mijn apps voor iPhone en iPad

Mijn apps voor iOS wordt ondersteund op een iPhone of iPad met versie voor iOS 7 en hoger.  
Is beschikbaar in de Hallo [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![Mijn apps voor iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Beheerde browser voor mijn apps

Mijn apps is ook geïntegreerd in Hallo Intune Managed Browser. Hallo Intune Managed Browser voor iOS en Android-apparaten speelt een belangrijke rol om ervoor te zorgen dat de gegevens op mobiele apparaten beveiligd blijven. Hiermee kunt u veilig kunt weergeven en webpagina's die mogelijk bedrijfsgegevens bevatten en biedt een veilige websurfervaring.  
U vinden snel toegang toomy apps op uw startpagina van Managed Browser en in uw bladwijzers, zodat u minder tooreach klikt op elke gewenste tooaccess toepassing.

Is beschikbaar in de Hallo [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) en [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Mananged browser voor mijn apps][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Tips voor het testen van het Hallo-gebruikerservaring

Als u een Azure-beheerder bent en u toohello Azure-portal bent aangemeld met een account in de map hello, bent u toohello Toegangsvenster automatisch aangemeld als uw huidige account gebruiken. In dit geval kunt u alle toepassingen die zijn toegewezen aan de tooyou zien.

**tootest als een *verschillende* gebruikersaccount:**

1. Klik op Hallo gebruikersmenu in Hallo rechterbovenhoek hello Azure-portal of Hallo Toegangsvenster en selecteer vervolgens **Afmelden**. 
2. Ga toohello [toegangspaneel](http://myapps.microsoft.com).
3. U wilt tootest op de aanmeldingspagina hello, type Hallo gebruikersnaam en wachtwoord voor account Hallo in uw directory.


## <a name="starting-applications"></a>Starten van toepassingen

Verschillende soorten toepassingen kunnen worden weergegeven op het toegangsvenster Hallo.

### <a name="office-365-applications"></a>Office 365-toepassingen

Als u een licentie voor uw organisatie gebruikmaakt van Office 365-toepassingen weergegeven Hallo Office 365-toepassingen op uw Toegangsvenster.

Wanneer u klikt op de tegel van een toepassing voor een Office 365-toepassing, bent u omgeleide toohello toepassing en automatisch aangemeld.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>Microsoft en derden toepassingen die zijn geconfigureerd op basis van een federatieve aanmelding bij

Uw beheerder kan toepassingen toevoegen in Active Directory-sectie van de Azure-portal Hallo HALLO hallo SSO-modus ingesteld te**Azure AD Single Sign-On**. U kunt deze toepassingen alleen zien als de beheerder heeft expliciet verleend voor het openen van toohello toepassingen.

Als u op een tegel voor een van deze toepassingen, kunt u bent omgeleid en toohello toepassing automatisch aangemeld.

### <a name="password-based-sso-without-identity-provisioning"></a>Eenmalige aanmelding op basis van wachtwoorden zonder identiteit inrichten

Uw beheerder kan toepassingen toevoegen in Active Directory-sectie van de Azure-portal Hallo HALLO hallo SSO-modus ingesteld te**op basis van wachtwoorden Single Sign-On**. Alle gebruikers in de directory Hallo ziet alle toepassingen die zijn geconfigureerd in deze modus.

Hallo eerst u klikt op een tegel voor een van deze toepassingen, vraag tooinstall Hallo wachtwoord SSO-invoegtoepassing voor Internet Explorer of Chrome. Hallo-installatie mogelijk toorestart u uw webbrowser. Als u het toegangsvenster toohello retourneren en Hallo toepassing tegel opnieuw op u wordt gevraagd om een gebruikersnaam en wachtwoord voor de toepassing hello. Wanneer u uw gebruikersnaam en wachtwoord hebt ingevoerd, worden deze referenties zijn veilig opgeslagen en tooyour-account gekoppeld in Azure AD.

Wanneer u op Hallo toepassing tegel u automatisch aangemeld toohello toepassing Hello.  
U geen tooenter opnieuw uw referenties hebt en of Hallo wachtwoord SSO-invoegtoepassing installeren.

Als uw referenties in de doeltoepassing derde Hallo hebt gewijzigd, moet u ook de referenties die zijn opgeslagen in Azure AD bijwerken. 

**tooupdate referenties:**

1. Selecteer Hallo-pictogram op Hallo toepassing tegel.
2. Selecteer **referenties bijwerken** tooreenter Hallo gebruikersnaam en wachtwoord voor de toepassing hello.


### <a name="password-based-sso-with-identity-provisioning"></a>Eenmalige aanmelding op basis van wachtwoorden met het leveren van identiteit

Uw beheerder kan toepassingen toevoegen in Hallo **Active Directory** sectie Hallo Azure-portal met de Hallo SSO-modus ingesteld te**op basis van wachtwoorden Single Sign-On**, samen met het inrichten van de identiteit.

Hallo eerst u klikt op de tegel van een toepassing voor een van deze toepassingen, kunt u na vragen aan gebruiker tooinstall hello **wachtwoord SSO-invoegtoepassing voor Internet Explorer of Chrome**. Hallo-installatie mogelijk toorestart u uw webbrowser.  
Als u toohello toegangspaneel retourneren en Hallo toepassing tegel opnieuw op in de toepassing toohello wordt u automatisch afgemeld.

Sommige toepassingen moet u toochange uw wachtwoord op Hallo eerste aanmeldingspagina. Als uw referenties in de doeltoepassing derde Hallo hebt gewijzigd, moet u ook Hallo-referenties die zijn opgeslagen in Azure AD bijwerken. 

**tooupdate referenties:**

1. Selecteer Hallo-pictogram op Hallo toepassing tegel.
2. Selecteer **referenties bijwerken** tooreenter Hallo gebruikersnaam en wachtwoord voor de toepassing hello.


### <a name="application-with-existing-sso-solutions"></a>Toepassing met bestaande oplossingen voor eenmalige aanmelding

tooconfigure eenmalige aanmelding voor een toepassing hello Azure-portal biedt een derde optie, genaamd **bestaande Single Sign-On**. Deze optie kunnen uw beheerder toocreate een koppeling tooan toepassing en plaats het op Hallo toegangspaneel voor geselecteerde gebruikers.

Bijvoorbeeld, als een toepassing geconfigureerde tooauthenticate gebruikers met behulp van AD FS 2.0, uw beheerder kan gebruiken Hallo **bestaande Single Sign-On** optie toocreate een koppeling tooit op Hallo Toegangsvenster. Wanneer u Hallo koppeling opent, kunt u bent geverifieerd via AD FS 2.0 of de bestaande SSO-oplossing Hallo toepassing biedt.


## <a name="next-steps"></a>Volgende stappen

- een lijst met alle onderwerpen die gerelateerd tooapplication management zijn, toosee Zie Hallo [artikel index voor Toepassingsbeheer in Azure Active Directory](active-directory-apps-index.md).
 
- toolearn hoe toointegrate een SaaS-app met Azure AD Hallo zien [lijst met zelfstudies over het SaaS-apps toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn meer informatie over het beheren van apps in Azure AD, Zie Hallo [inleiding toosingle aanmelding en het beheren van toegang tot de app met Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn meer informatie over gebruikers inrichten, Zie [gebruikers inrichten en opheffen van inrichting tooSaaS toepassingen automatiseren](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
