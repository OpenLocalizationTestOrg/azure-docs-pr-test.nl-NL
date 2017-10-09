---
title: aaaWhat is toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory? | Microsoft Docs
description: Gebruik Azure Active Directory tooenable eenmalige aanmelding tooall Hallo website en SaaS toepassingen die u nodig hebt voor bedrijven.
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?
Eenmalige aanmelding betekent kunnen tooaccess wordt alle Hallo toepassingen en bronnen dat u nodig hebt toodo bedrijven, met slechts één keer met behulp van één gebruikersaccount aanmelden. Wanneer u bent aangemeld, kunt u alle Hallo toepassingen zonder de vereiste tooauthenticate wordt openen (bv. Typ een wachtwoord) een tweede keer.

Veel organisaties zijn afhankelijk van de software als een dienst (SaaS)-toepassingen zoals Office 365, het selectievakje en Salesforce voor de productiviteit van eindgebruikers. In het verleden hebben IT-personeel moet tooindividually maken en bijwerken van gebruikersaccounts in elke SaaS-toepassing en gebruikers hebben tooremember een wachtwoord op voor elke SaaS-toepassing.

Azure Active Directory door op de lokale Active Directory in de cloud hello, schakelen gebruikers toouse hun primaire organisatieaccount toonot alleen aanmelden tootheir domein apparaten en resources van het bedrijf, maar ook alle Hallo web en SaaS-toepassingen nodig voor hun taak.

Dus niet alleen gebruikers hebben geen toomanage meerdere sets met gebruikersnamen en wachtwoorden, hun toepassingen toegang kan automatisch worden ingericht of buiten gebruik gesteld op basis van hun organisatie groepsleden en hun status als een werknemers. Azure Active Directory maakt u kennis met beveiliging en beheeracties toegangsbeheer waarmee u toocentrally toegang van gebruikers in de SaaS-toepassingen beheren.

Azure AD kunt eenvoudige integratie toomany van de hedendaagse populaire SaaS-toepassingen. voorziet in identiteits- en toegangsbeheer, beheer, en kunnen gebruikers toosingle aanmelding tooapplications rechtstreeks of detecteren en ze te starten vanuit een portal zoals Office 365 of hello Azure AD-Toegangsvenster.

Hallo-architectuur van Hallo-integratie bestaat uit vier belangrijkste bouwstenen na Hallo:

* Eenmalige aanmelding kunt gebruikers tooaccess hun SaaS-toepassingen op basis van hun organisatieaccount in Azure AD. Eenmalige aanmelding is wat gebruikers tooauthenticate tooan toepassing met hun enkele organisatie-account maakt.
* Gebruikers inrichten, kunt u gebruikers inrichten en de inrichting op doel die SaaS op basis van wijzigingen in Windows Server Active Directory en/of Azure AD. Er is een ingerichte account wat een gebruiker is gemachtigd toobe toouse een toepassing maakt nadat ze zijn geverifieerd via eenmalige aanmelding.
* Gecentraliseerde Toepassingsbeheer toegang in hello Azure-beheerportal kunt u toegang tot één punt van SaaS-toepassingen en beheer met Hallo mogelijkheid toodelegate toepassing toegang beslissing nemen en goedkeuringen tooanyone in Hallo organisatie
* Geïntegreerde rapportage en controle van gebruikersactiviteit in Azure AD

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>How does single sign-on with Azure Active Directory work? (Hoe werkt eenmalige aanmelding met Azure Active Directory?)
Wanneer een gebruiker-toepassing 'zich heeft aangemeld' tooan doorlopen ze een verificatieproces waar ze zijn vereist tooprove die ze die zij beweren te zijn. Zonder eenmalige aanmelding, dit gebeurt meestal door te voeren van een wachtwoord dat is opgeslagen in de toepassing hello en Hallo gebruiker is vereist tooknow dit wachtwoord.

Azure AD ondersteunt drie verschillende manieren toosign in tooapplications:

* **Federatieve eenmalige aanmelding** kunnen toepassingen tooredirect tooAzure AD voor verificatie van de gebruiker in plaats van naar een eigen wachtwoord wordt gevraagd. Dit wordt ondersteund voor toepassingen die ondersteuning protocollen zoals SAML 2.0, WS-Federation of OpenID Connect, en de allerbeste modus Hallo van eenmalige aanmelding.
* **Op basis van wachtwoorden Single Sign-On** veilige opslag voor servertoepassingen wachtwoord en opnieuw afspelen met een browser webextensie of mobiele app. Dit maakt gebruik van Hallo bestaande aanmelden dat is opgegeven door de toepassing hello, maar kunt een beheerder toomanage Hallo wachtwoorden en geen Hallo gebruiker tooknow Hallo wachtwoord nodig.
* **Bestaande Single Sign-On** kunt u Azure AD tooleverage eventuele bestaande eenmalige aanmelding die is ingesteld voor de toepassing hello, maar kan deze toepassingen toobe gekoppeld toohello Office 365 of Azure AD access Configuratiescherm portals en kan ook aanvullende rapportage in Azure AD wanneer Hallo toepassingen er worden gestart.

Wanneer een gebruiker met een toepassing hebt geverifieerd, moeten de record voor een account ingericht op Hallo-toepassing waarin wordt gemeld de toepassing hello dat toohave waar er machtigingen en toegangsniveau die zich binnen het Hallo-toepassing. Hallo inrichten van een record voor dit account ofwel automatisch kan worden uitgevoerd of kan optreden handmatig door een beheerder voordat Hallo gebruiker één aanmelding toegang ontvangt.

 Meer informatie over deze modi voor eenmalige aanmelding en inrichting hieronder.

### <a name="federated-single-sign-on"></a>Federatieve eenmalige aanmelding
Federatieve eenmalige aanmelding kan eenmalige aanmelding kunnen Hallo gebruikers in uw organisatie toobe tooa van derden SaaS-toepassing automatisch aangemeld door Azure AD dat gebruikmaakt van Hallo gebruikersaccountgegevens vanuit Azure AD.

In dit scenario wanneer u al hebt geregistreerd in Azure AD en u wilt dat tooaccess resources die worden beheerd door een derde partij SaaS-toepassing overbodig federation Hallo voor een gebruiker toobe opnieuw worden geverifieerd.

Azure AD kan ondersteuning voor federatieve eenmalige aanmelding met toepassingen die ondersteuning bieden voor Hallo SAML 2.0, WS-Federation, of OpenID connect protocollen.

Zie ook: [beheren van certificaten voor federatieve eenmalige aanmelding](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Op basis van wachtwoorden eenmalige aanmelding
U configureert op basis van wachtwoorden eenmalige aanmelding kunnen Hallo gebruikers in uw organisatie toobe tooa van derden SaaS-toepassing automatisch aangemeld door Azure AD met behulp van de gegevens van gebruikersaccounts Hallo van derden SaaS-toepassing hello. Wanneer u deze functie inschakelt, wordt Azure AD verzamelt en Hallo gebruikersaccountgegevens en gerelateerde wachtwoord Hallo veilig worden opgeslagen.

Azure AD ondersteuning biedt voor eenmalige aanmelding op basis van een wachtwoord op voor elke cloud-app die een op basis van een HTML-aanmeldingspagina is. Met behulp van een aangepaste browser-invoegtoepassing AAD van Hallo gebruiker aanmelden proces via veilig bij het ophalen van referenties van de toepassing zoals Hallo gebruikersnaam en het Hallo-wachtwoord van Hallo directory automatiseert en voert deze referenties in van de toepassing hello aanmeldingspagina op naam van de gebruiker Hallo. Er zijn twee gebruiksvoorbeelden:

1. **Beheerder beheert referenties** – beheerders kunnen maken en beheren van referenties van de toepassing en deze referenties toousers of groepen die toegang moeten hebben tot toohello toepassing toewijzen. In dergelijke gevallen Hallo gebruiker heeft geen tooknow Hallo referenties nodig, maar nog steeds één aanmelding toegang toohello toepassing krijgt gewoon door erop te klikken in het deelvenster toegang of via een opgegeven koppeling. Hierdoor kunnen beide levenscyclusbeheer van referenties door Hallo beheerder als gebruiksgemak Hallo voor eindgebruikers waarbij zij niet tooremember moet of app-specifiek wachtwoorden beheren. Hallo-referenties zijn verscholen uit van de eindgebruiker Hallo tijdens de automatische aanmelding Hallo in proces; maar ze zijn technisch detecteerbaar zijn door Hallo-gebruiker met behulp van de foutopsporing voor web hulpprogramma's en gebruikers en beheerders moeten volgen hetzelfde beveiligingsbeleid alsof hello referenties Hallo rechtstreeks door de gebruiker Hallo gepresenteerd. Beheerder geleverde referenties zijn zeer nuttig wanneer ze toegang verlenen account die wordt gedeeld door veel gebruikers, zoals sociale media of toepassingen delen van documenten.
2. **Gebruiker beheert referenties** – beheerders kunnen toepassingen tooend gebruikers of groepen toewijzen en Hallo end gebruikers tooenter toestaan hun eigen referenties rechtstreeks bij de toegang tot Hallo-toepassing voor Hallo eerst in het deelvenster toegang. Hiermee maakt u gemakkelijker te maken voor eindgebruikers waarbij ze niet toocontinually hoeven Voer Hallo app-specifiek wachtwoorden telkens wanneer die ze toegang krijgen de toepassing hello tot. Deze gebruiksvoorbeeld kan ook worden gebruikt als een stap voor stap steen tooadministrative management Hallo referenties, waarbij Hallo beheerder nieuwe referenties voor de toepassing hello op een later tijdstip instellen kan zonder Hallo van apps toegang van de eindgebruiker Hallo.

In beide gevallen moeten referenties worden opgeslagen in een versleutelde status in de map Hallo en alleen via HTTPS worden doorgegeven tijdens het Hallo automatisch aanmelden. Voor meer informatie over het gebruik van eenmalige aanmelding op basis van wachtwoorden op biedt Azure AD een oplossing voor identiteitsbeheer voor gemakkelijke toegang voor apps die niet kunnen ondersteunen federation-protocollen.

Eenmalige aanmelding op basis van wachtwoorden is afhankelijk van een browser extensie toosecurely ophalen Hallo toepassings- en specifieke gegevens van Azure AD en deze toohello service toe te passen. Deze functie wordt ondersteund door de meeste van derden SaaS-toepassingen die worden ondersteund door Azure AD.

Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:

* Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger (Zie ook [IE extensie Deployment Guide](active-directory-saas-ie-group-policy.md))
* Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger
* Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger

**Opmerking:** Hallo op basis van wachtwoorden SSO-uitbreiding beschikbaar komen voor de rand in de Windows 10 wanneer browseruitbreidingen worden ondersteund voor de rand.

### <a name="existing-single-sign-on"></a>Bestaande eenmalige aanmelding
Bij het configureren van eenmalige aanmelding voor een toepassing, biedt hello Azure-beheerportal een derde optie van ' bestaande Single Sign-On '. Deze optie gewoon Hallo beheerder toocreate een koppeling tooan-toepassing kan en plaats het op Hallo toegangspaneel voor geselecteerde gebruikers.

Bijvoorbeeld als er een toepassing die is geconfigureerd met behulp van Active Directory Federation Services 2.0 tooauthenticate-gebruikers, kan een beheerder Hallo ' bestaande Single Sign-On ' optie toocreate een tooit koppeling gebruiken op Hallo Toegangsvenster. Wanneer gebruikers toegang krijgen Hallo-koppeling tot, zijn ze geverifieerd met behulp van Active Directory Federation Services 2.0 of welke bestaande eenmalige aanmelding oplossing wordt geleverd door de toepassing hello.

### <a name="user-provisioning"></a>Gebruikers inrichten
Voor bepaalde toepassingen kunt u Azure AD geautomatiseerde gebruikersinrichting en ongedaan inrichten van accounts in de derde partij SaaS-toepassingen uit binnen hello Azure-beheerportal, met behulp van de gegevens van uw Windows Server Active Directory of Azure AD-identiteit. Wanneer een gebruiker is gemachtigd in Azure AD voor een van deze toepassingen, kan een account automatisch worden gemaakt (ingericht) in Hallo doel SaaS-toepassing.

Wanneer een gebruiker wordt verwijderd of hun gegevens worden gewijzigd in Azure AD, worden deze wijzigingen ook weergegeven in Hallo SaaS-toepassing. Dit houdt in dat configureren van de levenscyclus van geautomatiseerde Identiteitsbeheer kunnen beheerders toocontrol en geautomatiseerde inrichting en de inrichting van SaaS-toepassingen te bieden. In Azure AD, wordt deze automatisering van de levenscyclus van identiteitsbeheer ingeschakeld door gebruikers inrichten.

toolearn meer, Zie [geautomatiseerde Gebruikersinrichting en Deprovisioning tooSaaS toepassingen](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Aan de slag met Azure AD-toepassingsgalerie Hallo
Gereed tooget gestart? toodeploy eenmalige aanmelding tussen Azure AD en SaaS-toepassingen die uw organisatie gebruikt, volgt u deze richtlijnen.

### <a name="using-hello-azure-ad-application-gallery"></a>Met behulp van hello Azure AD-toepassingsgalerie
Hallo [Azure Active Directory-Toepassingsgalerie](https://azure.microsoft.com/marketplace/active-directory/all/) biedt een overzicht van toepassingen die bekend zijn toosupport een vorm van eenmalige aanmelding bij Azure Active Directory.

![][1]

Hier volgen enkele tips voor het vinden van apps door welke mogelijkheden die ze ondersteunen:

* Azure AD biedt ondersteuning voor automatische inrichting en ongedaan inrichten voor alle 'Aanbevolen' apps in Hallo [Azure Active Directory-Toepassingsgalerie](https://azure.microsoft.com/marketplace/active-directory/all/).
* Een lijst met federatieve toepassingen die specifiek ondersteuning bieden voor federatieve eenmalige aanmelding via een protocol zoals SAML, WS-Federation, of OpenID Connect vindt [hier](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Als u uw toepassing hebt gevonden, u kunt aan de slag door Hallo Stapsgewijze instructies die zijn gepresenteerd in app-galerie hello en in hello Azure management portal tooenable eenmalige aanmelding.

### <a name="application-not-in-hello-gallery"></a>De toepassing niet in de galerie Hallo?
Als uw toepassing niet in de Azure AD-toepassingsgalerie hello gevonden is, hebt u deze opties:

* **Toevoegen van een niet-vermelde app u** -gebruik Hallo aangepaste categorie in de app-galerie Hallo binnen hello Azure management portal tooconnect een niet-vermelde toepassing die van uw organisatie gebruikmaakt. U kunt elke toepassing die SAML 2.0 als federatieve app ondersteunt of elke toepassing die is een op basis van een HTML-aanmeldingspagina als wachtwoord SSO app toevoegen. Zie voor meer informatie in dit artikel op [uw eigen toepassing toe te voegen](active-directory-saas-custom-apps.md).
* **Toevoegen van uw eigen app die u ontwikkelt** : als u hebt ontwikkeld Hallo toepassing zelf, voert u de Hallo richtlijnen in hello Azure AD-ontwikkelaar documentatie tooimplement federatieve eenmalige aanmelding of inrichten met hello Azure AD graph API. Zie de volgende bronnen voor meer informatie:
  
  * [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md) (Verificatiescenario's voor Azure AD)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Aanvragen van een app-integratie** -vraag ondersteuning voor Hallo-toepassing u met behulp van moet Hallo [forum met feedback van Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Met behulp van hello Azure-beheerportal
U kunt Active Directory-extensie Hallo in hello Azure Management Portal tooconfigure Hallo toepassing eenmalige aanmelding gebruiken. Als eerste stap moet u een map van Active Directory-sectie in de portal Hallo Hallo tooselect:

![][2]

toomanage uw SaaS-toepassingen van derden die u kunt overschakelen naar Hallo op het tabblad toepassingen van de geselecteerde map Hallo. Deze weergave biedt beheerders:

* Nieuwe toepassingen uit de galerie van Azure AD hello, evenals de apps die u ontwikkelt toevoegen
* Geïntegreerde toepassingen verwijderen
* Hallo-toepassingen die ze al hebt geïntegreerd beheren

Typische administratieve taken voor een SaaS-toepassing van derden zijn:

* Inschakelen van eenmalige aanmelding met Azure AD, met behulp van wachtwoord SSO of, indien beschikbaar voor Hallo doel SaaS federatieve SSO
* Desgewenst schakelen gebruikers inrichten voor gebruikers inrichten en de inrichting ongedaan (identity lifecycle management)
* Selecteren welke gebruikers toegang hebben voor toepassingen waarvoor gebruikers inrichten is ingeschakeld, toothat toepassing

Voor apps die ondersteuning bieden voor federatieve eenmalige aanmelding galerie moet configuratie doorgaans u tooprovide extra configuratie-instellingen zoals certificaten en metagegevens toocreate een federatieve vertrouwensrelatie tussen Hallo van derden app en Azure AD. Hallo-configuratiewizard leidt u door Hallo details en biedt u eenvoudige toegang toohello specifieke gegevens voor SaaS-toepassing en instructies.

Voor apps die ondersteuning bieden voor Automatische gebruikersaanvragen galerie moet hiervoor u toogive Azure AD machtigingen toomanage je accounts via Hallo SaaS-toepassing. Ten minste moet u Azure AD-referenties moeten worden gebruikt wanneer verificatie via de doeltoepassing toohello tooprovide. Of extra configuratie-instellingen moeten toobe opgegeven, is afhankelijk van Hallo vereisten van de toepassing hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Implementatie van Azure AD geïntegreerde toepassingen toousers
Azure AD levert aanpasbare op verschillende manieren toodeploy toepassingen tooend-gebruikers in uw organisatie:

* Azure AD-Toegangsvenster
* Startprogramma voor toepassingen van Office 365
* Directe aanmelding toofederated apps
* Dieptekoppelingen toofederated, op basis van wachtwoorden of bestaande apps

Welke methode(n) u toodeploy kiezen in uw organisatie, is uw keuze.

### <a name="azure-ad-access-panel"></a>Azure AD-Toegangsvenster
Hallo Toegangsvenster op https://myapps.microsoft.com is een webgebaseerde portal waarmee gebruikers met een organisatieaccount in Azure Active Directory-tooview en starten van cloudtoepassingen toowhich ze zijn geweest toegangsrechten door hello Azure AD beheerder. Als u een eindgebruiker met [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), kunt u ook gebruikmaken van mogelijkheden voor groepsbeheer met Self-service via Hallo Toegangsvenster.

![][3]

Hallo Toegangspaneel is gescheiden van hello Azure-beheerportal en vereist geen gebruikers toohave een Azure-abonnement of een Office 365-abonnement.

Zie voor meer informatie over hello Azure AD-Toegangsvenster Hallo [inleiding toohello toegangspaneel](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Startprogramma voor toepassingen van Office 365
Voor organisaties die Office 365 hebt geïmplementeerd, worden toepassingen die zijn toegewezen toousers via Azure AD wordt ook weergegeven in Hallo Office 365-portal op https://portal.office.com/myapps. Dit maakt het eenvoudig en voor gebruikers in een organisatie toolaunch hun apps zonder toouse een tweede portal en wordt aanbevolen Hallo app starten van de oplossing voor organisaties met Office 365.

![][4]

Zie voor meer informatie over startprogramma voor toepassingen van Office 365 Hallo [uw App worden weergegeven in Office 365 Hallo app linksboven](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Directe aanmelding toofederated apps
De meeste federatieve toepassingen die ondersteuning bieden voor SAML 2.0 en WS-Federation en het OpenID Verbind ook ondersteuning Hallo mogelijkheid voor gebruikers toostart op Hallo-toepassing en vervolgens ophalen aangemeld via Azure AD door automatische omleiding of door te klikken op een koppeling toosign in. Dit staat bekend als serviceprovider-geïnitieerd eenmalige aanmelding en de meeste federatieve toepassingen in hello Azure AD-toepassingsgalerie deze ondersteunen (Zie de documentatie van Hallo Hallo app configuratie voor één aanmelding wizard in hello Azure-beheerportal voor gekoppeld meer informatie).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Directe aanmelding koppelingen voor federatieve, op basis van wachtwoorden of bestaande apps
Daarnaast ondersteunt Azure AD directe eenmalige aanmelding koppelingen tooindividual toepassingen die ondersteuning bieden voor op basis van wachtwoorden eenmalige aanmelding, bestaande eenmalige aanmelding en een vorm van federatieve eenmalige aanmelding.

Deze koppelingen zijn opzettelijk URL's die verzenden van een gebruiker via hello Azure AD-proces voor een specifieke toepassing zonder Hallo gebruiker aanmelden start ze van hello Azure AD-Toegangsvenster of Office 365. Deze URL voor eenmalige aanmelding kunt u vinden onder Hallo-dashboardtabblad van alle vooraf geïntegreerde toepassingen in Hallo Active Directory-sectie van hello Azure-beheerportal, zoals wordt weergegeven in onderstaande schermafbeelding voor Hallo.

![][6]

Deze koppelingen kunnen worden gekopieerd en geplakt elke locatie die u wilt dat tooprovide een aanmeldingspagina koppeling toohello geselecteerde toepassing. Dit kan zijn in een e-mailbericht, of in een aangepaste web gebaseerde portal die u hebt ingesteld voor toegang tot de toepassingen van gebruiker. Hier volgt een voorbeeld van een Azure AD direct één aanmeldings-URL voor Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Vergelijkbare tooorganization-specifieke URL's voor het toegangsvenster hello, u kunt deze URL verder aanpassen door een van de actieve of geverifieerde domeinen Hallo voor uw directory Hallo myapps.microsoft.com domein toe te voegen. Dit zorgt ervoor dat eventuele huisstijl van de organisatie is geladen onmiddellijk op de aanmeldingspagina Hallo zonder Hallo gebruiker tooenter eerst hun gebruikers-ID die:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Wanneer een geautoriseerde gebruiker op een van deze koppelingen toepassingsspecifieke klikt, ze eerst Zie van hun organisatie-aanmeldingspagina (ervan uitgaande dat ze nog niet bent aangemeld) en zijn na het aanmelden omgeleid tootheir app op Hallo Toegangsvenster zonder eerst te stoppen. Als Hallo gebruiker ontbreekt vereisten tooaccess Hallo toepassing, zoals Browseruitbreiding Hallo eenmalige aanmelding op basis van wachtwoorden, wordt koppeling Hallo Hallo gebruiker tooinstall Hallo ontbrekende extensie gevraagd. URL van de koppeling Hallo ook constant is gebleven als Hallo eenmalige aanmelding voor de toepassing hello configuratiewijzigingen.

Deze koppelingen hello gebruiken dezelfde toegangsmechanismen als Hallo openen Configuratiescherm en Office 365, en alleen die gebruikers of groepen die zijn toegewezen aan de toepassing in Azure-beheerportal Hallo toohello kan worden toosuccessfully verifiëren. Elke gebruiker die niet geautoriseerd is ziet echter een bericht waarin staat dat ze geen toegang hebben gekregen en krijgt een koppeling tooload Hallo toegang Configuratiescherm tooview beschikbare toepassingen waarvoor ze toegang hebben.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Zoeken naar niet-toegestane cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Inleiding tooManaging toegang tooApps](active-directory-managing-access-to-apps.md)
* [Vergelijking van mogelijkheden voor het beheren van externe identiteiten in Azure AD](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
