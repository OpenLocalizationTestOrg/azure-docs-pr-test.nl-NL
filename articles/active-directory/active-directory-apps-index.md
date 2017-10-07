---
title: aaaArticle Index for Application Management in Azure Active Directory | Microsoft Azure
description: Meer informatie over hoe toocustomize Hallo vervaldatum voor uw federatiecertificaten en hoe toorenew certificaten die binnenkort verlopen.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Article Index for Application Management in Azure Active Directory (Engelstalig)
Deze pagina bevat een uitgebreide lijst met elk document dat is geschreven over Hallo verschillende toepassing-gerelateerde functies in Azure Active Directory (Azure AD).

Er is een korte inleiding tooeach belangrijke functiegebied, evenals richtlijnen op welke tooread artikelen, afhankelijk van welke informatie u zoekt.

## <a name="overview-articles"></a>Overzicht van artikelen
Hallo-artikelen die hieronder zijn goede beginpunt voor gebruikers die alleen een korte uitleg van functies voor Azure AD-toepassing wilt.

| Artikel handleiding |  |
|:---:| --- |
| Een inleiding toohello management toepassingsproblemen die Azure AD is opgelost |[Toepassingen beheren met Azure Active Directory (AD)](active-directory-enable-sso-scenario.md) |
| Een overzicht van Hallo verschillende functies in Azure AD hebben tooenabling eenmalige aanmelding, definiëren wie heeft toegang tot tooapps en hoe gebruikers apps openen |[Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md) |
| Bekijkt hello verschillende stappen die betrokken zijn bij het integreren van apps in uw Azure AD |[Integratie van Azure Active Directory met toepassingen](active-directory-integrating-applications-getting-started.md)<br /><br />[Single Sign-On tooSaaS Apps inschakelen](active-directory-sso-integrate-saas-apps.md)<br /><br />[Het beheren van toegang tooApps](active-directory-managing-access-to-apps.md) |
| Een technische uitleg van hoe apps worden weergegeven in Azure AD |[Hoe en waarom toepassingen tooAzure AD worden toegevoegd](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Het oplossen van artikelen
In dit gedeelte biedt voor probleemoplossing handleidingen toorelevant snelle toegang. Meer informatie over elke functiegebied vindt u op Hallo rest van deze pagina.

| Functiegebied |  |
|:---:| --- |
| Federatieve eenmalige aanmelding |[Het oplossen van problemen op basis van SAML eenmalige aanmelding](active-directory-saml-debugging.md) |
| Op basis van wachtwoorden eenmalige aanmelding |[Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Toepassingsproxy |[Toepassingsproxy-handleiding voor probleemoplossing](active-directory-application-proxy-troubleshoot.md) |
| Eenmalige aanmelding tussen on-premises AD en Azure AD |[Wachtwoordsynchronisatie oplossen](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Wachtwoord terugschrijven probleemoplossing](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Lidmaatschap van dynamische groepen |[Het lidmaatschap van dynamische groepen oplossen](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Eenmalige aanmelding (SSO)
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Federatieve eenmalige aanmelding: Meld u aan bij veel apps met behulp van één identiteit
Eenmalige aanmelding kunt gebruikers tooaccess tal van apps en services met behulp van slechts één set referenties. Federatie is een methode waarmee u eenmalige aanmelding kunt inschakelen. Wanneer gebruikers toosign in federatieve apps proberen, krijgen ze van de organisatie van de omgeleide tootheir officiële aanmeldingspagina weergegeven door Azure Active Directory, en worden vervolgens omgeleid back toohello app bij verificatie is geslaagd.

| Artikel handleiding |  |
|:---:| --- |
| Een inleiding toofederation en andere typen van eenmalige aanmelding |[Eenmalige aanmelding met Azure AD](active-directory-appssoaccess-whatis.md) |
| SaaS-apps die vooraf geïntegreerd met Azure AD met zijn duizenden vereenvoudigd configuratiestappen voor eenmalige aanmelding |[Aan de slag met Azure AD-toepassingsgalerie Hallo](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Volledige lijst met vooraf geïntegreerde Apps die ondersteuning bieden voor Federatie](http://aka.ms/aadfederatedapps)<br /><br />[Hoe tooAdd Your App toohello App-galerie van Azure AD](active-directory-app-gallery-listing.md) |
| Meer dan 150 app-zelfstudies voor tooconfigure hoe eenmalige aanmelding voor apps zoals [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [Google Apps](active-directory-saas-google-apps-tutorial.md), [Workday](active-directory-saas-workday-tutorial.md), en nog veel meer |[Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Hoe toomanually instellen en aanpassen van uw configuratie voor eenmalige aanmelding |[Hoe tooConfigure tooApps federatieve eenmalige aanmelding die niet zijn opgenomen in hello Azure Active Directory-Toepassingsgalerie](active-directory-saas-custom-apps.md)<br /><br />[Hoe tooCustomize Claims uitgegeven hello SAML-Token voor Pre-Integrated Apps](active-directory-saml-claims-customization.md) |
| Problemen oplossen met federatieve apps die gebruikmaken van Hallo SAML-protocol |[Het oplossen van problemen op basis van SAML eenmalige aanmelding](active-directory-saml-debugging.md) |
| Hoe tooconfigure vervaldatum van het certificaat van uw app, en hoe toorenew uw certificaten |[Het beheer van certificaten voor federatieve eenmalige aanmelding bij Azure Active Directory](active-directory-sso-certs.md) |

Federatieve eenmalige aanmelding is beschikbaar voor alle edities van Azure AD voor up tooten apps per gebruiker. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) onbeperkte toepassingen worden ondersteund. Als uw organisatie heeft [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) of [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), kunt u [Gebruik groepen tooassign toegang toofederated toepassingen](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Op basis van wachtwoorden eenmalige aanmelding: Account delen en eenmalige aanmelding voor apps niet-gefedereerde
tooenable eenmalige aanmelding tooapplications die Federatie, Azure AD biedt wachtwoord management functies die kunnen worden veilig opgeslagen wachtwoorden tooSaaS apps en automatisch gebruikers aanmelden bij deze apps niet ondersteunen. U kunt eenvoudig referenties voor de zojuist gemaakte accounts distribueren en team accounts delen met meerdere personen. Gebruikers hoeven niet per se tooknow Hallo referenties toohello accounts die ze toegang tot krijgt.

| Artikel handleiding |  |
|:---:| --- |
| Een inleiding toohow op basis van wachtwoorden SSO werkt en een korte technisch overzicht |[Op basis van wachtwoorden eenmalige aanmelding met Azure AD](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Een overzicht van scenario's Hallo verwante tooaccount delen en hoe deze problemen kunnen worden opgelost door Azure AD |[Accounts delen met Azure AD](active-directory-sharing-accounts.md) |
| Hallo-wachtwoord voor bepaalde apps automatisch op een vast interval wijzigen |[Geautomatiseerde Rollover van wachtwoord (preview)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Implementatie en probleemoplossing van de handleidingen voor Internet Explorer versie Hallo Hallo Azure AD-wachtwoord-beheeruitbreiding |[Hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid](active-directory-saas-ie-group-policy.md)<br /><br />[Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Op basis van wachtwoorden eenmalige aanmelding is beschikbaar voor alle edities van Azure AD voor up tooten apps per gebruiker. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) onbeperkte toepassingen worden ondersteund. Als uw organisatie heeft [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) of [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), kunt u [Gebruik groepen tooassign toegang tooapplications](#managing-access-to-applications). Er wordt een geautomatiseerde wachtwoord rollover een [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) functie.

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>App-Proxy: Eenmalige aanmelding en externe toegang tooon-premises toepassingen
Als u toepassingen in uw particuliere netwerk die toegankelijk is voor gebruikers en apparaten buiten Hallo netwerk toobe nodig hebt, kunt u Azure AD-toepassingsproxy tooenable veilige externe toegang toothose apps kunt gebruiken.

| Artikel handleiding |  |
|:---:| --- |
| Overzicht van Azure AD-toepassingsproxy en hoe het werkt |[Een beveiligde externe toegang tooon-premises toepassingen](active-directory-application-proxy-get-started.md) |
| Zelfstudies voor het tooconfigure Application Proxy en hoe toopublish uw eerste app |[Hoe tooSet Up toepassingsproxy van Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Hoe tooSilently installeren Hallo App Proxy Connector](active-directory-application-proxy-silent-installation.md)<br /><br />[Hoe tooPublish van toepassingen via App-Proxy](active-directory-application-proxy-publish.md)<br /><br />[Hoe tooUse uw eigen domeinnaam](active-directory-application-proxy-custom-domains.md) |
| Hoe tooenable eenmalige aanmelding en voorwaardelijke toegang voor apps die zijn gepubliceerd met toepassingsproxy |[Single-sign-on met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Voorwaardelijke toegang en toepassingsproxy](active-directory-application-proxy-conditional-access.md) |
| Instructies voor het toouse toepassingsproxy voor Hallo volgen scenario's |[Hoe tooSupport Native Client-toepassingen](active-directory-application-proxy-native-client.md)<br /><br />[Hoe tooSupport claimbewuste toepassingen](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Hoe toepassingen tooSupport gepubliceerd op afzonderlijke netwerken en locaties](active-directory-application-proxy-connectors.md) |
| Gids voor probleemoplossing voor toepassingsproxy |[Toepassingsproxy-handleiding voor probleemoplossing](active-directory-application-proxy-troubleshoot.md) |

Toepassingsproxy is beschikbaar voor alle edities van Azure AD voor up tooten apps per gebruiker. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) onbeperkte toepassingen worden ondersteund. Als uw organisatie heeft [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) of [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), kunt u [Gebruik groepen tooassign toegang tooapplications](#managing-access-to-applications).

Hebt u mogelijk ook geïnteresseerd in [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md), waarmee u uw lokale toepassingen tooAzure terwijl u nog steeds voldoen aan Hallo identiteit van deze toepassingen moet toomigrate.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Inschakelen van eenmalige aanmelding tussen Azure AD en on-premises AD
Als uw organisatie een Windows Server Active Directory on-premises samen met uw Azure Active Directory in de cloud hello onderhoudt, zult u waarschijnlijk willen tooenable eenmalige aanmelding tussen deze twee systemen. Azure AD Connect (Hallo-hulpprogramma dat deze twee systemen samen integreert) biedt meerdere opties voor het instellen van eenmalige aanmelding: Federatie met AD FS of een andere federatieprovider maken of wachtwoordsynchronisatie inschakelen.

| Artikel handleiding |  |
|:---:| --- |
| Een overzicht op Hallo eenmalige aanmelding-opties in Azure AD Connect, evenals informatie over het beheren van hybride omgevingen |[Aanmelding van de gebruiker op opties in Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Algemene richtlijnen voor het beheren van omgevingen met zowel on-premises Active Directory en Azure Active Directory |[Ontwerpoverwegingen voor Azure AD-hybride identiteit](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Uw On-Premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md) |
| Richtlijnen over het gebruik van Wachtwoordsynchronisatie tooenable eenmalige aanmelding |[Wachtwoordsynchronisatie implementeren met Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Probleem met Wachtwoordsynchronisatie oplossen](https://support.microsoft.com/en-us/kb/2855271) |
| Richtlijnen over het gebruik van wachtwoord terugschrijven tooenable eenmalige aanmelding |[Aan de slag met wachtwoordbeheer in Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Problemen met Wachtwoord terugschrijven oplossen](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Richtlijnen over het gebruik van derden identiteit providers tooenable eenmalige aanmelding |[Lijst met compatibele van derden id-Providers dat kan worden gebruikt tooEnable eenmalige aanmelding](https://aka.ms/ssoproviders) |
| Hoe Windows 10-gebruikers kunnen profiteren van Hallo voordelen van eenmalige aanmelding via de Azure AD Join |[Cloudfuncties tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-overview.md) |

Azure AD Connect is beschikbaar voor [alle edities van Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). Azure AD selfservice voor wachtwoordherstel is beschikbaar voor [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) en [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Wachtwoord terugschrijven tooon-premises AD is een [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) functie.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Voorwaardelijke toegang: Afdwingen aanvullende beveiligingseisen voor apps met een hoog risico
Zodra u eenmalige aanmelding tooyour apps en resources hebt ingesteld, kunt u vervolgens meer gevoelige toepassingen beveiligen door af te dwingen specifieke beveiligingsvereisten op elke toothat-in-app. Bijvoorbeeld, kunt u Azure AD-toodemand dat alle toegang tooa bepaalde app altijd multi-factor authentication-server, ongeacht of die app innately ondersteunt deze functionaliteit vereist. Een andere algemene voorbeeld van voorwaardelijke toegang is toorequire dat gebruikers van de organisatie van de verbonden toohello worden vertrouwd netwerk in volgorde tooaccess bijzonder gevoelige toepassingen.

| Artikel handleiding |  |
|:---:| --- |
| Een inleiding toohello voorwaardelijke toegangsmogelijkheden geboden door Azure AD, Office365 en Intune |[Risico beheren met voorwaardelijke toegang](active-directory-conditional-access.md) |
| Hoe tooenable voorwaardelijke toegang voor de volgende typen resources Hallo |[Voorwaardelijke toegang voor SaaS-Apps](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Voorwaardelijke toegang voor Office 365-services](active-directory-conditional-access-device-policies.md)<br /><br />[Voorwaardelijke toegang voor On-Premises toepassingen](active-directory-conditional-access.md)<br /><br />[Voorwaardelijke toegang voor On-Premises toepassingen die zijn gepubliceerd via toepassingsproxy van Azure AD](active-directory-application-proxy-conditional-access.md) |

| Hoe apparaten met Azure Active Directory in tooregister bestellen tooenable beleidsregels voor voorwaardelijke toegang op basis van apparaten | [Overzicht van Azure Active Directory-apparaatregistratie](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Hoe tooEnable automatische apparaatregistratie voor Windows-apparaten met die lid zijn van een domein](active-directory-conditional-access-automatic-device-registration.md)<br />— [Stappen voor Windows 8.1-apparaten](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Stappen voor Windows 7-apparaten](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Hoe toouse Microsoft Authenticator-app voor verificatie in twee stappen Hallo | [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

Voorwaardelijke toegang is een [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) functie.

## <a name="apps--azure-ad"></a>Apps en Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Cloud App Discovery: Zoeken welke SaaS-apps in uw organisatie worden gebruikt
Cloud App Discovery helpt IT-afdelingen meer informatie over welke SaaS-apps in de gehele organisatie hello worden gebruikt. Het gebruik van de app kunt meten en populariteit zodat deze kan bepalen welke apps profiteert Hallo meest niet kan worden gebracht onder dat IT controle en waarin wordt geïntegreerd met Azure AD.

| Artikel handleiding |  |
|:---:| --- |
| Een algemeen overzicht van hoe het werkt |[Zoeken naar niet-toegestane cloud-toepassingen met Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Zie voor meer informatie in de manier waarop dit proces werkt, met tooquestions antwoorden op privacy |[Beveiliging en Privacy-overwegingen](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Veelgestelde vragen |[Veelgestelde vragen voor Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Zelfstudies voor het implementeren van Cloud App Discovery |[Group Policy Deployment Guide](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Implementatiehandleiding van System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Installeren op proxyservers met aangepaste poorten](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Hallo wijzigingenlogboek voor updates toohello Cloud App Discovery agent |[Wijzigingslogboek](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Cloud App Discovery is een [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) functie.

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Automatisch in te richten en inrichting ervan ongedaan gebruikersaccounts in de SaaS-apps
Hallo maken, onderhouden en verwijderen van de gebruikers-id's in de SaaS-toepassingen zoals Dropbox, Salesforce en ServiceNow automatiseren. Overeenkomen met en bestaande identiteiten tussen Azure AD synchroniseren en uw SaaS-apps en toegang beheren accounts automatisch uit te schakelen wanneer gebruikers Hallo organisatie verlaten.

| Artikel handleiding |  |
|:---:| --- |
| Meer informatie over hoe het werkt en antwoorden toocommon vragen |[Gebruikers inrichten & Deprovisioning tooSaaS Apps automatiseren](active-directory-saas-app-provisioning.md) |
| Configureren hoe de gegevens tussen Azure AD is toegewezen en uw SaaS-Apps |[Kenmerktoewijzingen aanpassen](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Expressies voor kenmerktoewijzingen schrijven](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Hoe tooenable geautomatiseerde inrichting tooany-app die Hallo SCIM protocol ondersteunt |[Geautomatiseerde Gebruikersinrichting tooany SCIM-Enabled App instellen](active-directory-scim-provisioning.md) |
| Hoe tooreport op en het oplossen van gebruikers inrichten |[Rapportage over automatisch gebruikers inrichten](active-directory-saas-provisioning-reporting.md)<br><br>[Inrichting van meldingen](active-directory-saas-account-provisioning-notifications.md)<br><br>[Het oplossen van gebruikers inrichten](active-directory-application-provisioning-content-map.md) |
| Wie ingerichte tooan-toepassing op basis van de kenmerkwaarden |[Bereikfilters](active-directory-saas-scoping-filters.md) |

Geautomatiseerde gebruikersinrichting is beschikbaar voor alle edities van Azure AD voor up tooten apps per gebruiker. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) onbeperkte toepassingen worden ondersteund. Als uw organisatie heeft [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) of [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), kunt u [Gebruik groepen toomanage welke gebruikers ophalen ingericht](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Toepassingen maken die kunnen worden geïntegreerd met Azure AD
Als uw organisatie ontwikkelt of onderhouden van line-of-business (LoB)-toepassingen, of als u een appontwikkelaars met klanten die gebruikmaken van Azure Active Directory, Hallo zelfstudies volgen helpt u uw toepassingen integreren met Azure AD.

| Artikel handleiding |  |
|:---:| --- |
| Richtlijnen voor IT-professionals en ontwikkelaars van toepassingen over de apps integratie met Azure AD |[Hallo IT-professionals van handleiding voor het ontwikkelen van toepassingen voor Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Hallo Ontwikkelaarshandleiding voor Azure Active Directory](active-directory-developers-guide.md) |
| Hoe tooapplication leveranciers hun apps toohello App-galerie van Azure AD kunnen toevoegen |[Uw toepassing in Azure Active Directory-Toepassingsgalerie Hallo aanbieding](active-directory-app-gallery-listing.md) |
| Hoe toomanage toegang krijgen tot toodeveloped toepassingen met Azure Active Directory |[Hoe tooEnable Gebruikerstoewijzing voor toepassingen die zijn ontwikkeld](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Toewijzen van gebruikers tooyour App](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[De groep toewijzen tooyour App](active-directory-applications-guiding-developers-assigning-groups.md) |

Als u consumententoepassingen ontwikkelt, hebt u mogelijk geïnteresseerd in met behulp van [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) zodat er geen toodevelop uw eigen identiteit system toomanage uw gebruikers. [Meer informatie](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Het beheren van toegang tooApplications
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Met behulp van groepen en selfservice toomanage wie toegang tot toowhich apps heeft
toohelp u beheert die toegang tot toowhich bronnen nodig hebben, Azure Active Directory kunt u tooset toewijzingen en de machtigingen op grote schaal met behulp van groepen. IT kan kiezen tooenable selfservicefuncties zodat gebruikers eenvoudig machtiging aanvragen kunnen als dat nodig.

| Artikel handleiding |  |
|:---:| --- |
| Een overzicht van Azure AD access management-functies |[Inleiding tooManaging toegang tooApps](active-directory-managing-access-to-apps.md)<br /><br />[De werking van toegangsbeheer in Azure AD](active-directory-manage-groups.md)<br /><br />[Hoe tooUse groepen tooManage toegang tooSaaS toepassingen](active-directory-accessmanagement-group-saasapps.md) |
| Beheer van apps en groepen selfservice inschakelen |[Selfservice Toepassingsbeheer](active-directory-self-service-application-access.md)<br /><br />[Self-Service groepsbeheer](active-directory-accessmanagement-self-service-group-management.md) |
| Instructies voor het instellen van de groepen in Azure AD |[Hoe tooCreate beveiligingsgroepen](active-directory-accessmanagement-manage-groups.md)<br /><br />[Hoe tooDesignate eigenaars voor een groep](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Hoe tooUse Hallo 'alle gebruikers' groeperen](active-directory-accessmanagement-dedicated-groups.md) |
| Gebruik dynamische groepen tooautomatically vullen van groepslidmaatschappen met lidmaatschapsregels op basis van kenmerken |[Lidmaatschap van dynamische groep: Geavanceerde regels](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Het lidmaatschap van dynamische groepen oplossen](active-directory-accessmanagement-troubleshooting.md) |

Beheer van toegang van toepassing op basis van een groep is beschikbaar voor [Azure AD Basic](https://azure.microsoft.com/pricing/details/active-directory/) en [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Self-service groepsbeheer, selfservice Toepassingsbeheer en dynamische groepen zijn [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) functies.

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>B2B-samenwerking: Partner toegang tooapplications inschakelen
Als uw bedrijf met andere bedrijven samen werkt, is het waarschijnlijk dat u nodig hebt toomanage partner toegang tooyour zakelijke toepassingen. Azure Active Directory B2B-samenwerking biedt een gemakkelijk en veilig tooshare uw apps met partners.

| Artikel handleiding |  |
|:---:| --- |
| Een overzicht van andere Azure AD functies dat kunt u helpt externe gebruikers zoals partners, klanten, enzovoort. |[Vergelijking van mogelijkheden voor het beheren van externe identiteiten in Azure AD](active-directory-b2b-compare-external-identities.md) |
| Een inleiding tooB2B samenwerking en hoe tooget gestart |[Veilige, eenvoudige Cloud Partner-integratie met Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Azure Active Directory B2B-samenwerking](active-directory-b2b-collaboration-overview.md) |
| Zie voor meer informatie naar Azure AD B2B-samenwerking en hoe toouse deze |[B2B-samenwerking: Hoe het werkt](active-directory-b2b-how-it-works.md)<br /><br />[Huidige beperkingen van Azure AD B2B-samenwerking](active-directory-b2b-current-limitations.md)<br /><br />[Gedetailleerd overzicht van het gebruik van Azure AD B2B-samenwerking](active-directory-b2b-detailed-walkthrough.md) |
| Verwijzing naar artikelen met technische gegevens over de werking van Azure AD B2B-samenwerking |[CSV-indeling voor het toevoegen van gebruikers van partners](active-directory-b2b-references-csv-file-format.md)<br /><br />[De kenmerken van de gebruiker is van invloed op een Azure AD B2B-samenwerking](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Token indeling van de gebruiker voor de Partner-gebruikers](active-directory-b2b-references-external-user-token-format.md) |

B2B-samenwerking is momenteel beschikbaar voor [alle edities van Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Toegangspaneel: Een portal voor toegang tot apps en selfservice-functies
Hello Azure AD-Toegangsvenster is waar eindgebruikers kunnen hun apps en toegang Hallo selfservice-functies waarmee ze toomanage starten hun apps en groepslidmaatschappen. Toohello paneel voor Apptoegang, andere opties voor toegang tot apps SSO-functionaliteit zijn ook opgenomen in Hallo onderstaande lijst.

| Artikel handleiding |  |
|:---:| --- |
| Een vergelijking van verschillende opties die beschikbaar zijn voor het implementeren van apps voor eenmalige aanmelding toousers Hallo |[Azure AD-geïntegreerde toepassingen tooUsers implementeren](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Een overzicht van Hallo Toegangspaneel en de mobiele gelijkwaardige MyApps |[Inleiding tooAccess deelvenster en MyApps](active-directory-saas-access-panel-introduction.md)<br />— [iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Hoe tooaccess Azure AD-apps van Office 365-website Hallo |[Met behulp van Hallo Office 365-App starten](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Hoe tooaccess Azure AD-apps uit de mobiele app Intune Managed Browser Hallo |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Hoe tooaccess Azure AD-apps met behulp van dieptekoppelingen tooinitiate eenmalige aanmelding |[Directe aanmelding koppelingen tooYour Apps ophalen](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Toegangspaneel is beschikbaar voor [alle edities van Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Rapporten: Eenvoudig wijzigingen aan de app toegang controleren en aanmeldingen tooapps bewaken
Azure Active Directory bevat verschillende rapporten en toohelp waarschuwt u van uw organisatie toegang tooapplications bewaken. U kunt waarschuwingen voor afwijkende aanmeldingen tooyour apps ontvangen en u kunt volgen wanneer en waarom een gebruiker toegang tooan toepassing is gewijzigd.

| Artikel handleiding |  |
|:---:| --- |
| Een overzicht van Hallo rapportagefuncties in Azure Active Directory |[Aan de slag met Azure AD-rapportage](active-directory-reporting-getting-started.md) |
| Hoe toomonitor Hallo aanmeldingen en app-gebruik van uw gebruikers |[Toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md) |
| Bijhouden van wijzigingen toowho toegang tot een bepaalde toepassing |[Azure Active Directory-Controlerapportgebeurtenissen](active-directory-reporting-audit-events.md) |
| Hallo gegevens exporteren van deze rapporten tooyour voorkeur hulpprogramma's met behulp van Hallo rapportage-API |[Aan de slag met Azure AD rapportage-API Hallo](active-directory-reporting-api-getting-started.md) |

welke rapporten opgenomen in verschillende versies van Azure Active Directory zijn, toosee [Klik hier](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Zie ook
[Wat is Azure Active Directory?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/)

[Azure multi-factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/)
