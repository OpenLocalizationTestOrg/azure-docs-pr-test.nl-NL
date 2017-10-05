---
title: Eenmalige aanmelding beheer voor zakelijke apps in Azure Active Directory | Microsoft Docs
description: Meer informatie over het beheren van eenmalige aanmelding op voor zakelijke apps met de Azure Active Directory
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: c975428550690254ba989935fe5110c5903e7102
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Eenmalige aanmelding voor zakelijke apps beheren
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klassieke Azure Portal](active-directory-sso-integrate-saas-apps.md)
> 

In dit artikel wordt beschreven hoe u de [Azure-portal](https://portal.azure.com) voor het beheren van instellingen voor eenmalige aanmelding voor bedrijfstoepassingen. Zakelijke apps zijn apps die zijn geïmplementeerd en worden gebruikt binnen uw organisatie. In dit artikel geldt met name voor apps die zijn toegevoegd vanuit de [Azure Active Directory-toepassingsgalerie](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-the-portal"></a>Uw apps te zoeken in de portal
Alle zakelijke apps die zijn ingesteld voor eenmalige aanmelding kunnen worden weergegeven en beheerd in de Azure portal. De toepassingen vindt u in de **meer Services** &gt; **bedrijfstoepassingen** sectie van de portal. 

![Blade bedrijfstoepassingen][1]

Selecteer **alle toepassingen** om weer te geven een lijst met alle apps die zijn geconfigureerd. Als u een app laadt de resourceblade voor die app, waarbij de rapporten kunnen worden weergegeven voor die app en een aantal instellingen kan worden beheerd.

Selecteer voor het beheren van instellingen voor eenmalige aanmelding **eenmalige aanmelding**.

![De resource-blade toepassing][2]

## <a name="single-sign-on-modes"></a>Modi voor eenmalige aanmelding
De **eenmalige aanmelding** blade begint met een **modus** menu, waardoor de modus voor één aanmelding moet worden geconfigureerd. De beschikbare opties zijn onder andere:

* **Op basis van SAML aanmelding** -deze optie is beschikbaar als de toepassing ondersteunt volledige federatieve eenmalige aanmelding met Azure Active Directory met het SAML 2.0-protocol.
* **Meld u op wachtwoord gebaseerde** -deze optie is beschikbaar als Azure AD ondersteunt wachtwoord formulier invullen voor deze toepassing.
* **Aanmelding gekoppeld op** -voorheen bekend als 'Bestaande single sign-on', deze optie kan beheerders een koppeling naar deze toepassing in hun gebruiker Azure AD-Toegangsvenster of Office 365 startprogramma voor toepassingen plaatsen.

Zie voor meer informatie over deze modi [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Op basis van SAML eenmalige aanmelding
De **op basis van SAML aanmelding** optie wordt weergegeven, een blade die is onderverdeeld in vier secties:

### <a name="domains-and-urls"></a>Domeinen en URL 's
Dit is waar alle informatie over het domein en de URL's van de toepassing worden toegevoegd aan uw Azure AD-directory. Alle invoer nodig zijn om één aanmelding werk app rechtstreeks op het scherm worden weergegeven terwijl alle optionele invoer kunnen worden bekeken door het selecteren van de **weergeven geavanceerde instellingen voor URL** selectievakje. De volledige lijst van ondersteunde invoerwaarden omvat:

* **Meld u op URL** – waar de gebruiker naar aanmelden bij deze toepassing gaat. Als de toepassing is geconfigureerd voor het uitvoeren van service provider geïnitieerde eenmalige aanmelding op vervolgens wanneer een gebruiker naar deze URL navigeert, komt de serviceprovider de benodigde omleiding naar Azure AD om te verifiëren en meld u aan de gebruiker. Als dit veld is ingevuld, klikt u vervolgens Azure AD gebruikt deze URL om de toepassing van Office 365 en de Azure AD-Toegangsvenster te starten. Als dit veld wordt weggelaten, wordt in plaats daarvan identiteitsprovider Azure AD voert-geïnitieerd aanmelding wanneer de app wordt gestart vanuit Office 365, het Azure AD-Toegangsvenster of vanuit de Azure AD eenmalige aanmeldings-URL.
* **Id** -deze URI moet een unieke identificatie van de toepassing voor welke één aanmelding wordt geconfigureerd. Dit is de waarde die Azure AD teruggestuurd naar de toepassing als de parameter van de doelgroep van het SAML-token wordt en wordt verwacht dat de toepassing te valideren. Deze waarde wordt ook weergegeven als de entiteit-ID in een SAML-metagegevens geleverd door de toepassing.
* **Antwoord-URL** -de antwoord-URL is waar de toepassing voor het ontvangen van het SAML-token verwacht. Dit is ook de URL van de verklaring Consumer Service (ACS) genoemd. Nadat deze zijn ingevoerd, klikt u op volgende om door te gaan naar het volgende scherm. Dit scherm bevat informatie over wat er worden geconfigureerd aan de kant van de toepassing moet te kunnen worden geaccepteerd van een SAML-token van Azure AD.
* **Status van de relay** -de status van de relay is een optionele parameter waarmee de toepassing instrueren waar de gebruiker wordt omgeleid als verificatie is voltooid. De waarde is meestal een geldige URL op de toepassing, maar sommige toepassingen anders dit veld gebruiken (Zie de app voor eenmalige op documentatie voor meer informatie). De mogelijkheid om de status van de relay is een nieuwe functie die uniek is voor de nieuwe Azure portal.

### <a name="user-attributes"></a>Gebruikerskenmerken
Dit is waar beheerders kunnen weergeven en bewerken van de kenmerken die worden verzonden in het SAML-token dat Azure AD tot de toepassing van elke geeft keer dat gebruikers zich aanmelden.

Het alleen worden bewerkt kenmerk ondersteund is de **gebruikers-id** kenmerk. De waarde van dit kenmerk is het veld in Azure AD dat is uniek voor elke gebruiker in de toepassing. Bijvoorbeeld als de app is geïmplementeerd met behulp van de 'e-mailadres' als de gebruikersnaam en een unieke id, klikt u vervolgens de waarde zou worden ingesteld op het veld 'user.mail' in Azure AD.

### <a name="saml-signing-certificate"></a>Certificaat voor ondertekening van SAML
Deze sectie worden de details van het certificaat dat Azure AD wordt gebruikt voor het ondertekenen van de SAML-tokens die zijn verleend aan de toepassing telkens wanneer de gebruiker wordt geverifieerd. Hierdoor kan de eigenschappen van het huidige certificaat moet worden gecontroleerd, met inbegrip van de vervaldatum.

### <a name="application-configuration"></a>De configuratie van toepassing
De laatste sectie vindt u de documentatie en/of de besturingselementen die zijn vereist voor het configureren van de toepassing zelf op Azure Active Directory gebruiken als een id-provider.

De **toepassing configureren** vervolgmenu biedt nieuwe beknopte, ingesloten instructies voor het configureren van de toepassing. Dit is een andere nieuwe functie die uniek is voor de nieuwe Azure portal.

> [!NOTE]
> Zie voor een compleet voorbeeld van embedded-documentatie, de toepassing Salesforce.com. Documentatie voor Aanvullende apps wordt voortdurend toegevoegd.
> 
> 

![Ingesloten docs][3]

## <a name="password-based-sign-on"></a>Meld u op wachtwoord gebaseerde
Als voor de toepassing wordt ondersteund, de eenmalige aanmelding op basis van wachtwoorden modus selecteren en te selecteren **opslaan** onmiddellijk configureert u eenmalige aanmelding op basis van wachtwoorden. Zie voor meer informatie over het implementeren van eenmalige aanmelding op basis van wachtwoorden [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Meld u op wachtwoord gebaseerde][4]

## <a name="linked-sign-on"></a>Gekoppelde aanmelding
Als voor de toepassing wordt ondersteund, kunt de gekoppelde SSO-modus u de URL die u wilt de Azure AD-Toegangsvenster of Office 365 waarnaar wordt doorverwezen wanneer gebruikers op deze app klikt, invoeren. Zie voor meer informatie over gekoppelde eenmalige aanmelding (voorheen bekend als 'bestaande SSO'), [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Gekoppelde aanmelding][5]

##<a name="feedback"></a>Feedback

We hopen dat u u zoals het gebruik van het verbeterde ervaring voor Azure AD. Zorg ervoor dat uw feedback! Plaats uw feedback en ideeën voor verbetering van de **beheerportal** sectie van onze [Feedbackforum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  We enthousiast bent over het bouwen van cool nieuw per dag uit, en gebruik de richtlijnen voor vorm en definiëren wat we hierna bouwen.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
