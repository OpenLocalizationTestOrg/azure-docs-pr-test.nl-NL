---
title: aaaConfigure SaaS-apps voor B2B-samenwerking in Azure Active Directory | Microsoft Docs
description: Voorbeelden van code en PowerShell voor Azure Active Directory B2B-samenwerking
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>SaaS-apps voor B2B-samenwerking configureren

Azure Active Directory (Azure AD) B2B-samenwerking werkt met de meeste apps die zijn geïntegreerd met Azure AD. In deze sectie doorlopen we instructies voor het configureren van een aantal populaire SaaS-apps voor gebruik met Azure AD B2B.

Voordat u de instructies van de app-specifiek bekijkt, hier een aantal regels van miniatuur te volgen:

* Voor de meeste Hallo apps moet gebruikersinstellingen toohappen handmatig. Dat wil zeggen, moeten gebruikers handmatig in Hallo app ook worden gemaakt.

* Voor apps die ondersteuning bieden voor automatische installatie, zoals Dropbox, worden afzonderlijke inschrijvingen van Hallo-apps gemaakt. Gebruikers ervoor tooaccept elke uitnodiging moet zijn.

* In gebruikerskenmerken hello, eventuele problemen met vervormde gebruikersprofielschijf (UDP) in gastgebruikers, toomitigate altijd ingesteld **gebruikers-id** te**user.mail**.


## <a name="dropbox-business"></a>Dropbox Business

tooenable gebruikers toosign met hun organisatieaccount, moet u handmatig configureren Dropbox Business toouse Azure AD als een id-provider Security Assertion Markup Language (SAML). Als Dropbox Business geconfigureerde toodo niet is dus kan het vragen of anders toestaan dat gebruikers toosign in met behulp van Azure AD.

1. tooadd hello Dropbox-Business-app in Azure AD, selecteer **bedrijfstoepassingen** in het linkerdeelvenster Hallo en klik vervolgens op **toevoegen**.

  ![Hallo "Toevoegen" knop op de pagina met toepassingen Hallo Enterprise](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. In Hallo **een toepassing toevoegen** venster invoeren **dropbox** in het zoekvak Hallo en selecteer vervolgens **Dropbox voor bedrijven** in de lijst met resultaten Hallo.

  ![Zoek naar 'dropbox' op Hallo-toepassingspagina voor een toevoegen](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. Op Hallo **eenmalige aanmelding** pagina **eenmalige aanmelding** in het linkerdeelvenster Hallo en voer vervolgens **user.mail** in Hallo **gebruikers-id** vak. (Het ingesteld als de UPN standaard.)

  ![Eenmalige aanmelding voor Hallo app configureren](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toodownload hello certificaat toouse voor configuratie van Dropbox, selecteer **DropBox configureren**, en selecteer vervolgens **SAML aanmelding op Service-URL met eenmalige** in Hallo-lijst.

  ![Hallo-certificaat voor de configuratie van Dropbox downloaden](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Aanmelden tooDropbox Hello aanmelding URL uit Hallo **eenmalige aanmelding** pagina.

  ![Hallo aanmeldingspagina Dropbox-pagina](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Selecteer Hallo menu **beheerconsole**.

  ![Hallo 'Admin Console' koppeling op Hallo Dropbox menu](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. In Hallo **verificatie** dialoogvenster, **meer**, Hallo-certificaat uploaden en klik vervolgens op Hallo **aanmelden URL** Voer Hallo eenmalige aanmelding SAML-URL.

  ![Hallo ' ' link in het dialoogvenster verificatie Hallo samengevouwen](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hallo 'Aanmelding in URL' in hello uitgevouwen dialoogvenster verificatie](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. Automatische gebruikersinstellingen tooconfigure in hello Azure-portal, selecteer **inrichten** selecteren in het linkerdeelvenster Hallo **automatische** in Hallo **modus inrichting** vak en selecteer vervolgens **Autoriseren**.

  ![Automatisch gebruikers inrichten in hello Azure-portal configureren](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

Nadat de gast of lid gebruikers zijn ingesteld in Hallo Dropbox-app, ontvangen ze een uitnodiging voor een afzonderlijke van Dropbox. toouse eenmalige aanmelding Dropbox genodigden moeten Hallo uitnodiging accepteren door te klikken op een koppeling in het.

## <a name="box"></a>Box
U kunt gebruikers tooauthenticate vak gastgebruikers met hun Azure AD-account inschakelen met behulp van de federatieserver die gebaseerd op Hallo SAML-protocol. In deze procedure moet u metagegevens tooBox.com uploaden.

1. Hallo-Box-app uit Hallo zakelijke apps toevoegen.

2. Eenmalige aanmelding in volgorde Hallo configureren:

  ![Eenmalige aanmelding vak configureren](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 a. In Hallo **aanmelden URL** Zorg dat Hallo aanmeldings-URL juist is ingesteld voor Box in hello Azure-portal. Deze URL is Hallo-URL van uw tenant Box.com. Deze moet voldoen aan de naamgevingsconventie Hallo *https://.box.com*.  
 Hallo **id** toothis is niet van toepassing app, maar nog steeds wordt weergegeven als een verplicht veld.

 b. In Hallo **gebruikers-id** Voer **user.mail** (voor eenmalige aanmelding voor gastaccounts).

 c. Onder **SAML-certificaat voor ondertekening van**, klikt u op **nieuw certificaat maken**.

 d. uw Box.com tenant toouse Azure AD configureren als een id-provider toobegin Hallo metagegevensbestand downloaden en sla vervolgens tooyour lokale schijf.

 e. Doorsturen Hallo metagegevens bestand toohello vak ondersteuningsteam, eenmalige aanmelding voor u te configureren.

3. Selecteer voor Azure AD automatische gebruikersinstellingen, in het linkerdeelvenster Hallo **inrichten**, en selecteer vervolgens **autoriseren**.

  ![Azure AD tooconnect tooBox autoriseren](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Zoals Dropbox-genodigden moeten vak genodigden gebruikmaken van hun uitnodiging van Hallo Box-app.

## <a name="next-steps"></a>Volgende stappen

Zie Hallo artikelen over Azure AD B2B-samenwerking te volgen:

* [Wat is Azure AD B2B-samenwerking?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Gebruikerseigenschappen B2B-samenwerking](active-directory-b2b-user-properties.md)
* [B2B-samenwerking tooa gebruikersrol toevoegen](active-directory-b2b-add-guest-to-role.md)
* [B2B-samenwerking uitnodigingen delegeren](active-directory-b2b-delegate-invitations.md)
* [Dynamische groepen en B2B-samenwerking](active-directory-b2b-dynamic-groups.md)
* [B2B-samenwerking code en PowerShell-voorbeelden](active-directory-b2b-code-samples.md)
* [B2B-samenwerking gebruikerstokens](active-directory-b2b-user-token.md)
* [Gebruikersclaims voor B2B-samenwerking toewijzing](active-directory-b2b-claims-mapping.md)
* [Office 365 extern delen](active-directory-b2b-o365-external-user.md)
* [Huidige beperkingen voor B2B-samenwerking](active-directory-b2b-current-limitations.md)
