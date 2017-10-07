---
title: aaaSingle aanmelding beheer voor zakelijke apps in Azure Active Directory Hallo | Microsoft Docs
description: Meer informatie over hoe toomanage enkelvoudige aanmelding voor zakelijke apps met Azure Active Directory Hallo
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
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>Eenmalige aanmelding voor zakelijke apps beheren
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-enterprise-apps-manage-sso.md)
> * [Klassieke Azure Portal](active-directory-sso-integrate-saas-apps.md)
> 

Dit artikel wordt beschreven hoe toouse hello [Azure-portal](https://portal.azure.com) toomanage eenmalige aanmelding-instellingen voor zakelijke toepassingen. Zakelijke apps zijn apps die zijn geïmplementeerd en worden gebruikt binnen uw organisatie. Dit artikel geldt met name tooapps die zijn toegevoegd vanuit Hallo [Azure Active Directory-toepassingsgalerie](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). 

## <a name="finding-your-apps-in-hello-portal"></a>Uw apps zoeken in Hallo portal
Alle zakelijke apps die zijn ingesteld voor eenmalige aanmelding kunnen worden weergegeven en beheerd in hello Azure-portal. Hallo toepassingen vindt u in Hallo **meer Services** &gt; **bedrijfstoepassingen** sectie van het Hallo-portal. 

![Blade bedrijfstoepassingen][1]

Selecteer **alle toepassingen** tooview een lijst met alle apps die zijn geconfigureerd. Als u een app wordt geladen Hallo resource-blade voor die app, waarbij de rapporten kunnen worden weergegeven voor die app en een aantal instellingen kan worden beheerd.

toomanage eenmalige aanmelding-instellingen, selecteer **eenmalige aanmelding**.

![De resource-blade toepassing][2]

## <a name="single-sign-on-modes"></a>Modi voor eenmalige aanmelding
Hallo **eenmalige aanmelding** blade begint met een **modus** menu waarmee Hallo modus voor één aanmelding toobe geconfigureerd. Hallo beschikbare opties zijn onder andere:

* **Op basis van SAML aanmelding** -deze optie is beschikbaar als de toepassing hello ondersteunt volledige federatieve eenmalige aanmelding met Azure Active Directory met Hallo SAML 2.0-protocol.
* **Meld u op wachtwoord gebaseerde** -deze optie is beschikbaar als Azure AD ondersteunt wachtwoord formulier invullen voor deze toepassing.
* **Aanmelding gekoppeld op** -deze optie voorheen bekend als 'Bestaande single sign-on', kan beheerders tooplace-toothis toepassingen in hun gebruiker Azure AD-Toegangsvenster of Office 365 startprogramma voor toepassingen van een koppeling.

Zie voor meer informatie over deze modi [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="saml-based-sign-on"></a>Op basis van SAML eenmalige aanmelding
Hallo **op basis van SAML aanmelding** optie wordt weergegeven, een blade die is onderverdeeld in vier secties:

### <a name="domains-and-urls"></a>Domeinen en URL 's
Dit is waar alle informatie over het domein en de URL's van de toepassing hello tooyour Azure AD-directory worden toegevoegd. Alle invoer vereist toomake werk voor één aanmelding app zijn rechtstreeks op Hallo scherm weergegeven, terwijl alle optionele invoer kunnen worden bekeken door het selecteren van Hallo **weergeven geavanceerde instellingen voor URL** selectievakje. volledige lijst van ondersteunde invoerwaarden Hallo omvat:

* **Meld u op URL** – indien Hallo gebruiker toosign in toothis toepassing gaat. Als de toepassing hello geconfigureerde tooperform service provider geïnitieerde één aanmelding, wanneer een gebruiker toothis URL navigeert, Hallo serviceprovider nodig Hallo Hallo omleiding tooAzure AD tooauthenticate en meld u gebruiker in. Als dit veld is ingevuld, wordt deze URL toolaunch Hallo toepassing vanuit Office 365 en Azure AD-Toegangsvenster Hallo gebruikt door Azure AD. Als dit veld wordt weggelaten, wordt in plaats daarvan identiteitsprovider Azure AD voert-geïnitieerd aanmelding wanneer Hallo app wordt gestart vanuit Office 365, Azure AD-Toegangsvenster Hallo of vanuit hello Azure AD eenmalige aanmelding URL.
* **Id** -deze URI moet een unieke identificatie van de toepassing hello voor welke één aanmelding wordt geconfigureerd. Dit is de waarde Hallo dat Azure AD back tooapplication verzendt als parameter van de doelgroep van Hallo SAML-token Hallo en toepassing hello verwachte toovalidate deze. Deze waarde wordt ook weergegeven als Hallo entiteit-ID in een SAML-metagegevens door Hallo toepassing geleverd.
* **Antwoord-URL** -Hallo antwoord-URL is waar de toepassing hello tooreceive Hallo SAML-token verwacht. Dit is ook bedoeld tooas Hallo Assertion Consumer Service (ACS)-URL. Nadat deze zijn ingevoerd, klikt u op volgende tooproceed toohello het volgende scherm. Dit scherm bevat informatie over welke toobe behoeften deze heeft geconfigureerd op Hallo toepassing side tooenable tooaccept een SAML-token van Azure AD.
* **Status van de relay** -Hallo relay status is een optionele parameter waarmee toepassing hello laat weten waar tooredirect gebruiker Hallo nadat de verificatie is voltooid. Hallo-waarde is meestal een geldige URL op Hallo van toepassing, maar sommige toepassingen anders dit veld gebruiken (Zie eenmalige Hallo-app op de documentatie voor meer informatie). Hallo mogelijkheid tooset Hallo relay status is een nieuwe functie die de unieke toohello nieuwe Azure portal.

### <a name="user-attributes"></a>Gebruikerskenmerken
Dit is waar beheerders kunt weergeven en bewerken Hallo kenmerken die worden verzonden in Hallo SAML-token dat Azure AD toohello toepassing elke keer dat gebruikers geeft zich aanmelden.

alleen bewerkbaar kenmerk ondersteund Hallo is Hallo **gebruikers-id** kenmerk. Hallo-waarde van dit kenmerk is Hallo veld in Azure AD dat elke gebruiker in de toepassing hello wordt aangeduid. Bijvoorbeeld, als Hallo app is geïmplementeerd met Hallo 'e-mailadres' hello gebruikersnaam en de unieke id, wordt klikt u vervolgens Hallo-waarde ingesteld toohello 'user.mail' veld in Azure AD.

### <a name="saml-signing-certificate"></a>Certificaat voor ondertekening van SAML
Deze sectie Hallo worden details weergegeven van Hallo-certificaat dat gebruikmaakt van Azure AD toosign Hallo SAML-tokens die zijn uitgegeven toohello toepassing die elke keer Hallo gebruiker wordt geverifieerd. Kan eigenschappen van Hallo huidige certificaat toobe gecontroleerd, met inbegrip van de vervaldatum Hallo Hallo.

### <a name="application-configuration"></a>De configuratie van toepassing
het laatste gedeelte Hallo biedt Hallo documentatie en/of besturingselementen vereist tooconfigure Hallo toepassing zelf toouse Azure Active Directory als een id-provider.

Hallo **toepassing configureren** vervolgmenu bevat nieuwe beknopte, ingesloten instructies voor het configureren van de toepassing hello. Dit is een andere nieuwe functie unieke toohello nieuwe Azure portal.

> [!NOTE]
> Zie voor een compleet voorbeeld van ingesloten documentatie Hallo Salesforce.com-toepassing. Documentatie voor Aanvullende apps wordt voortdurend toegevoegd.
> 
> 

![Ingesloten docs][3]

## <a name="password-based-sign-on"></a>Meld u op wachtwoord gebaseerde
Als voor de toepassing hello wordt ondersteund, Hallo selecteren op basis van wachtwoorden SSO-modus en selecteren **opslaan** configureert onmiddellijk toodo eenmalige aanmelding op basis van wachtwoorden. Zie voor meer informatie over het implementeren van eenmalige aanmelding op basis van wachtwoorden [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Meld u op wachtwoord gebaseerde][4]

## <a name="linked-sign-on"></a>Gekoppelde aanmelding
Als voor de toepassing hello wordt ondersteund, kunt Hallo gekoppeld SSO-modus u tooenter Hallo URL die u wilt dat hello Azure AD-Toegangsvenster of Office 365 tooredirect toowhen gebruikers klikt u op deze app. Zie voor meer informatie over gekoppelde eenmalige aanmelding (voorheen bekend als 'bestaande SSO'), [hoe eenmalige aanmelding met Azure Active Directory work](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

![Gekoppelde aanmelding][5]

##<a name="feedback"></a>Feedback

We hopen dat u met behulp van Hallo verbeterde Azure AD-ervaring. Zorg ervoor dat Hallo feedback binnenkort! Plaats uw feedback en suggesties voor verbetering van de gebruikerservaring in Hallo **beheerportal** sectie van onze [Feedbackforum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  We enthousiast bent over het bouwen van cool nieuw per dag uit, en gebruik uw tooshape richtlijnen en definiëren wat we hierna bouwen.

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
