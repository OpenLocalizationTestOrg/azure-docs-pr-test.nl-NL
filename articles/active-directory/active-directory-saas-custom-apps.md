---
title: Azure AD SSO aaaConfigure voor toepassingen | Microsoft Docs
description: Meer informatie over hoe apps tooAzure Active Directory in tooself-service verbinding maken met behulp van SAML- en eenmalige aanmelding op basis van wachtwoorden
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Eenmalige aanmelding tooapplications die zich niet in de Azure Active Directory-toepassingsgalerie Hallo configureren
Dit artikel is over een functie waarmee beheerders tooconfigure eenmalige aanmelding tooapplications niet aanwezig in de app-galerie van Azure Active Directory Hallo *zonder code te schrijven*. Deze functie werd uitgebracht van technical preview op 18 November 2015 en is opgenomen in [Azure Active Directory Premium](active-directory-editions.md). Als u in plaats daarvan-handleiding voor ontwikkelaars over het zoekt toointegrate aangepaste apps met Azure AD via programmacode, Zie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

Hello Azure Active Directory-toepassingsgalerie biedt een overzicht van toepassingen die bekend zijn toosupport een vorm van eenmalige aanmelding bij Azure Active Directory, zoals beschreven in [in dit artikel](active-directory-appssoaccess-whatis.md). Als u (als een IT infrastructuurspecialist of system integrator in uw organisatie) hebt Hallo toepassing gevonden gewenste tooconnect, u kunt aan de slag door Hallo Stapsgewijze instructies die zijn gepresenteerd in hello Azure management portal tooenable eenmalige aanmelding.

Klanten met [Azure Active Directory Premium](active-directory-editions.md) licenties ook krijgen deze aanvullende mogelijkheden:

* Selfservice integratie van alle toepassingen die ondersteuning biedt voor SAML 2.0 id-providers (Serviceprovider geïnitieerde of IdP gestart)
* Integratie van een webtoepassing met een op basis van een HTML-aanmeldingspagina met selfservice [eenmalige aanmelding op basis van wachtwoorden](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Verbinding van toepassingen die gebruikmaken van Hallo SCIM protocol voor gebruikers inrichten selfservice ([hier beschreven](active-directory-scim-provisioning.md))
* Mogelijkheid tooadd koppelingen tooany toepassing in Hallo [Office 365 app linksboven](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) of Hallo [deelvenster Azure AD access](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Dit kunnen bijvoorbeeld niet alleen SaaS-toepassingen dat u gebruikt, maar geïntegreerde toohello galerie van Azure AD-toepassing nog niet zijn, maar van derden webtoepassingen die u, hetzij in Hallo cloud of on-premises beheert tooservers, uw organisatie is geïmplementeerd.

Deze mogelijkheden, ook wel bekend als *app integratie sjablonen*, geeft u op standaarden gebaseerde verbindingspunten voor apps die ondersteuning bieden voor SAML, SCIM of verificatie op basis van formulieren en flexibele opties en instellingen voor compatibiliteit met een groot aantal toepassingen bevatten. 

## <a name="adding-an-unlisted-application"></a>Een niet-vermelde toepassing toevoegen
een toepassing met een sjabloon van de integratie app tooconnect melden bij hello Azure-beheerportal met administrator-account van uw Azure Active Directory en bladeren toohello **Active Directory > [Directory] > toepassingen**sectie **toevoegen**, en vervolgens **toevoegen van een toepassing uit de galerie Hallo**. 

![][1]

In app-galerie hello, kunt u een niet-vermelde-app met Hallo toevoegen **aangepaste** categorie aan de linkerkant Hallo of door het selecteren van Hallo **een niet-vermelde toepassing toevoegen** koppeling die wordt weergegeven in de zoekopdracht Hallo resulteert als uw app in de gewenste is niet gevonden. U kunt na het invoeren van een naam voor uw toepassing hello één opties voor aanmelding en het gedrag configureren. 

**Snelle tip**: gebruiken als een best practice Hallo zoeken functie toocheck toosee als Hallo toepassing al in Hallo-toepassingsgalerie bestaat. Als het Hallo-app wordt gevonden en de beschrijving noemt 'eenmalige aanmelding' en vervolgens de toepassing hello wordt al voor federatieve eenmalige aanmelding ondersteund. 

![][2]

Toevoegen van een toepassing op deze manier biedt een vergelijkbaar ervaring toohello beschikbaar voor vooraf geïntegreerde toepassingen. toostart, selecteer **configureren Single Sign-On**. het volgende scherm Hallo geeft Hallo na drie opties voor het configureren van eenmalige aanmelding op, die worden beschreven in Hallo uit te voeren.

![][3]

## <a name="azure-ad-single-sign-on"></a>Azure AD voor eenmalige aanmelding
Selecteer deze optie tooconfigure SAML-verificatie voor de toepassing hello. Hiervoor moet Hallo toepassingsondersteuning SAML 2.0 en u dient informatie te verzamelen over hoe toouse Hallo SAML-mogelijkheden van de toepassing hello voordat u doorgaat. Na het selecteren van **volgende**, kunt u zich na vragen aan gebruiker tooenter drie verschillende URL's toohello SAML eindpunten voor de toepassing hello overeenkomt. 

![][4]

Dit zijn:

* **Meld u op de URL (Serviceprovider geïnitieerde alleen)** – indien Hallo gebruiker toosign in toothis toepassing gaat. Als de toepassing hello is geconfigureerd tooperform service provider geïnitieerde één aanmelding, vervolgens wanneer een gebruiker toothis URL navigeert, Hallo serviceprovider wordt Hallo nodig omleiding tooAzure AD tooauthenticate en aanmelden Hallo-gebruiker in. Als dit veld is ingevuld, wordt deze URL toolaunch Hallo toepassing vanuit Office 365 en Azure AD-Toegangsvenster Hallo gebruikt door Azure AD. Als dit veld ommited is, voer vervolgens de Azure AD wordt in plaats daarvan id-provider-geïnitieerd aanmelding wanneer Hallo app wordt gestart vanuit Office 365, Azure AD-Toegangsvenster Hallo of vanuit hello Azure AD eenmalige aanmelding URL (copiable van tabblad Hallo-Dashboard).
* **URL-verlener** -URL-verlener Hallo moet een unieke identificatie van de toepassing hello voor welke één aanmelding wordt geconfigureerd. Dit is Hallo waarde dat Azure AD back tooapplication als Hallo verzendt **doelgroep** parameter van Hallo SAML-token en de toepassing hello verwachte toovalidate is het. Deze waarde wordt ook weergegeven als Hallo **entiteit-ID** in een SAML-metagegevens door Hallo toepassing geleverd. Raadpleeg de documentatie van de toepassing hello SAML voor meer informatie over wat het entiteit-ID is of waarde van de doelgroep is. Hieronder volgt een voorbeeld van hoe Hallo doelgroep URL wordt weergegeven in Hallo SAML-token geretourneerde toohello toepassing:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **Antwoord-URL** -Hallo antwoord-URL is waar de toepassing hello tooreceive Hallo SAML-token verwacht. Dit is ook bedoeld tooas hello **Assertion Consumer Service (ACS) URL**. Raadpleeg de documentatie van de toepassing hello SAML voor meer informatie over wat het SAML-token antwoord-URL of de ACS-URL is.
  Nadat deze zijn ingevoerd, klikt u op **volgende** tooproceed toohello volgende scherm. Dit scherm bevat informatie over welke toobe behoeften deze heeft geconfigureerd op Hallo toepassing side tooenable tooaccept een SAML-token van Azure AD. 

![][5]

Waarden die zijn vereist variëren afhankelijk van de toepassing hello, dus controleer van de toepassing hello SAML-documentatie voor meer informatie. Hallo **aanmelding** en **afmeldingsaanvragen** service-URL beide oplossen toohello hetzelfde eindpunt dat Hallo SAML verwerken van aanvragen eindpunt voor uw exemplaar van Azure AD. Hallo URL-verlener is Hallo-waarde die wordt weergegeven als 'Verlener' hello binnen Hallo SAML-token uitgegeven toohello toepassing. 

Nadat u uw toepassing is geconfigureerd, klikt u op **volgende** knop en vervolgens Hallo **Complete** tooclose Hallo dialoogvenster. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Toewijzen van gebruikers en groepen tooyour SAML-toepassing
Als uw toepassing geconfigureerde toouse Azure AD als een op basis van SAML-identiteitsprovider is, wordt het tootest bijna klaar. Als een beveiligingscontrole geeft Azure AD geen token van een zodat ze toosign in toepassing hello tenzij ze gebruikmaken van Azure AD toegang hebben gekregen. Gebruikers kunnen toegang verleend rechtstreeks of via een groep waarvan ze lid zijn van. 

tooassign een gebruiker of groep tooyour toepassing, klikt u op Hallo **gebruikers toewijzen** knop. Selecteer Hallo-gebruiker of groep die u wenst dat tooassign en selecteer vervolgens Hallo **toewijzen** knop. 

![][6]

Een gebruiker toewijzen, kunnen Azure AD-tooissue een token voor de gebruiker hello, evenals een tegel voor deze toepassing tooappear veroorzaakt in het toegangsvenster Hallo van de gebruiker. De tegel van een toepassing wordt ook weergegeven in startprogramma voor toepassingen van Office 365 Hallo als Hallo gebruiker via de Office 365. 

U kunt een logo in tegel voor Hallo toepassing hello uploaden **Logo uploaden** knop op Hallo **configureren** tabblad voor de toepassing hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Hallo uitgegeven claims in Hallo SAML-token aanpassen
Als een gebruiker zich toohello toepassing verifieert, geeft Azure AD een SAML-token toohello-app met informatie (of claims) over Hallo-gebruiker die uniek wordt geïdentificeerd. Dit omvat standaard gebruikersnaam, e-mailadres, voornaam en achternaam op Hallo van de gebruiker. 

U kunt weergeven of bewerken Hallo claims in Hallo SAML-token toohello toepassing onder Hallo verzonden **kenmerken** tabblad. 

![][7]

Er zijn twee mogelijke redenen waarom u tooedit Hallo uitgegeven claims in Hallo SAML-token wellicht: •hello toepassing is geschreven toorequire een andere set claim URI's of claim waarden •Your toepassing is geïmplementeerd op een manier die Hallo vereist NameIdentifier claim toobe iets anders dan van Hallo gebruikersnaam (AKA UPN-naam) opgeslagen in Azure Active Directory. 

Voor informatie over hoe tooadd en bewerken van de claims voor deze scenario's, Bekijk dit [artikel op claims aanpassing](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Hallo SAML toepassing testen
Zodra Hallo SAML-URL's en certificaten zijn geconfigureerd in Azure AD en in de toepassing hello, toohello toepassing in Azure, is toegewezen aan gebruikers of groepen hebt en Hallo claims zijn gecontroleerd en bewerkt, indien nodig, en vervolgens Hallo gebruiker is gereed toosign in Hallo de toepassing. 

tootest, gewoon sign-in Azure AD-Toegangsvenster op https://myapps.microsoft.com met een gebruikersaccount toegewezen van toohello toepassing hello en klik vervolgens op Hallo tegel voor Hallo toepassing tookick uit één Hallo aanmelding proces. Ook kunt u bladeren rechtstreeks toohello aanmeldings-URL voor de toepassing hello en meld u daar. 

Zie voor foutopsporing tips, [artikel over het toodebug op basis van SAML eenmalige aanmelding tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Eenmalige aanmelding wachtwoord
Selecteer deze optie tooconfigure [op basis van wachtwoorden eenmalige aanmelding](active-directory-appssoaccess-whatis.md) voor een webtoepassing met een HTML-aanmeldingspagina. Op basis van wachtwoorden SSO, ook waarnaar wordt verwezen tooas wachtwoord vaulting, kunt u toomanage toegang en wachtwoorden tooweb toepassingen die geen ondersteuning voor identiteitsfederatie. Het is ook nuttig voor scenario's waarbij meerdere gebruikers tooshare één account, zoals van tooyour organisatie sociale media app accounts moeten. 

Na het selecteren van **volgende**, kunt u zich na vragen aan gebruiker tooenter Hallo-URL van de van toepassing hello web gebaseerde aanmeldingspagina. Houd er rekening mee dat dit Hallo-pagina waarop Hallo velden gebruikersnaam en wachtwoord invoer moet zijn. Eenmaal worden ingevoerd, Azure AD wordt gestart van een proces tooparse Hallo aanmeldingspagina voor de invoer van een gebruikersnaam en een wachtwoord voor invoer. Als Hallo niet voltooid is, klikt u vervolgens leidt het u door een alternatief proces van het installeren van een Browseruitbreiding (vereist Internet Explorer, Chrome of Firefox) waarmee u toomanually vastleggen Hallo velden.

Zodra de aanmeldingspagina hello wordt vastgelegd, gebruikers en groepen kunnen worden toegewezen en referentie beleidsregels kunnen worden ingesteld net als normale [wachtwoord SSO apps](active-directory-appssoaccess-whatis.md).

Opmerking: U kunt een logo in tegel voor Hallo toepassing hello uploaden **Logo uploaden** knop op Hallo **configureren** tabblad voor de toepassing hello. 

## <a name="existing-single-sign-on"></a>Bestaande eenmalige aanmelding
Selecteer deze optie tooadd een koppeling tooan toepassing tooyour van organisatie Azure AD-Toegangsvenster of Office 365-portal. U kunt deze tooadd koppelingen toocustom web-apps die momenteel gebruikmaken van Azure Active Directory Federation Services (of een andere federatieservice) gebruiken in plaats van Azure AD voor verificatie. Of u kunt dieptekoppelingen toospecific SharePoint-pagina's of andere webpagina's die u zojuist hebt tooappear op van uw gebruikers toegang panelen wilt toevoegen. 

Na het selecteren van **volgende**, kunt u zich na vragen aan gebruiker tooenter Hallo-URL van Hallo toepassing toolink aan. Zodra de voltooid, gebruikers en groepen kunnen worden toegewezen toohello toepassing, waardoor Hallo toepassing tooappear in Hallo [Office 365 app linksboven](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) of Hallo [Azure AD-Toegangsvenster](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) voor gebruikers.

Opmerking: U kunt een logo in tegel voor Hallo toepassing hello uploaden **Logo uploaden** knop op Hallo **configureren** tabblad voor de toepassing hello.

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Hoe tooCustomize Claims uitgegeven hello SAML-Token voor Pre-Integrated Apps](active-directory-saml-claims-customization.md)
* [Het oplossen van problemen op basis van SAML eenmalige aanmelding](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
