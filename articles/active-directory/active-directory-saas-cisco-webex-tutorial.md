---
title: 'Zelfstudie: Azure Active Directory-integratie met Cisco Webex | Microsoft Docs'
description: Lees hoe toouse Cisco Webex met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Zelfstudie: Azure Active Directory-integratie met Cisco Webex
Hallo-doel van deze zelfstudie is tooshow Hallo integratie van Azure en Cisco Webex.  
Hallo scenario beschreven in deze zelfstudie wordt ervan uitgegaan dat u al hebt Hallo volgende items:

* Een geldige Azure-abonnement
* Een tenant Cisco Webex

Na het voltooien van deze zelfstudie hello Azure AD-gebruikers die u hebt toegewezen tooCisco Webex worden kunnen toosingle teken in de toepassing hello op uw Cisco Webex bedrijf site (serviceprovider geïnitieerd aanmelding) of met behulp van Hallo [inleiding toohello Toegang tot Configuratiescherm](active-directory-saas-access-panel-introduction.md).

Hallo scenario beschreven in deze zelfstudie bestaat uit Hallo bouwstenen te volgen:

* Hallo toepassingsintegratie voor Cisco Webex inschakelen
* Configureren van eenmalige aanmelding (SSO)
* Configuratie van gebruikers inrichten
* Gebruikers toewijzen

![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Hallo toepassingsintegratie voor Cisco Webex inschakelen
Hallo-doel van deze sectie is het toooutline hoe tooenable Hallo toepassingsintegratie voor Cisco Webex.

**tooenable hello toepassingsintegratie voor Cisco Webex, Voer Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo navigatiedeelvenster links Hallo op **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
   ![Toepassingen](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "toepassingen")
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
   ![Toepassing toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "toepassing toevoegen")
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
   ![Een toepassing toevoegen van gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "een toepassing van gallerry toevoegen")
6. In Hallo **zoekvak**, type **Cisco Webex**.
   
   ![Toepassingsgalerie](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "-Toepassingsgalerie")
7. Selecteer in het deelvenster met resultaten Hallo **Cisco Webex**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Eenmalige aanmelding configureren

Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooCisco Webex aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.  

Als onderdeel van deze procedure bent u vereiste toocreate een Base64-gecodeerde certificaat. Als u niet bekend met deze procedure bent, raadpleegt u [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure eenmalige aanmelding, voert u Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Cisco Webex** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "eenmalige aanmelding configureren")
2. Op Hallo **wilt u hoe gebruikers toosign op tooCisco Webex** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "eenmalige aanmelding configureren")
3. Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.
   
   ![App-URL configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "app-URL configureren")   
   1. In Hallo **Sing op URL** textbox, typt u uw Cisco Webex tenant-URL (bijvoorbeeld: *http://contoso.webex.com*).
   2. In Hallo **Cisco Webex antwoord-URL** textbox type uw **Cisco Webex AssertionConsumerService URL** (bijvoorbeeld: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Op Hallo **op Cisco Webex eenmalige aanmelding configureren** pagina, toodownload uw certificaat, klik op **certificaat downloaden**, en sla het Hallo-certificaatbestand op uw computer.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "eenmalige aanmelding configureren")
5. In een ander browservenster, meld u bij uw bedrijf Cisco Webex site als beheerder.
6. Klik in het menu bovenaan Hallo Hallo **Sitebeheer**.
   
   ![Sitebeheer](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Sitebeheer")
7. In Hallo **-Site beheren** sectie, klikt u op **SSO configuratie**.
   
   ![Configuratie van de SSO-](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO-configuratie")
8. Voer in Hallo federatieve Web-SSO configuratiesectie, Hallo stappen te volgen:
   
   ![Federatieve SSO configuratie](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "federatieve SSO-configuratie")  
   1. Van Hallo **Protocol Federation** selecteert **SAML 2.0**.
   2. Maak een **Base 64-codering** bestand van uw gedownloade certificaat.  
    >[!TIP]
    >Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Open uw base-64 gecodeerde certificaat in Kladblok en kopiëren Hallo inhoud ervan.
   4. Klik op **SAML-metagegevens importeren**, en plak de base-64 gecodeerde certificaat.
   5. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **URL-verlener** waarde en plak deze in Hallo **verlener voor SAML (IdP-ID)** textbox.
   6. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **externe aanmeldings-URL** waarde en plak deze in Hallo **klant SSO Service Login URL** textbox.
   7. Van Hallo **NameID indeling** selecteert **e-mailadres**.
   8. In Hallo **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**.
   9. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, kopie Hallo **externe URL voor afmelden** waarde en plak deze in Hallo **klant SSO Service afmelden URL** textbox.
   10. Klik op **Update**.
9. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding configureren op Cisco Webex** dialoogvenster pagina, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "eenmalige aanmelding configureren")
   
## <a name="configure-user-provisioning"></a>Gebruikers inrichten configureren

In volgorde tooenable Azure AD gebruikers toolog in Cisco Webex, moeten ze worden ingericht in Cisco Webex.  

* In geval van Cisco Webex Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u bij tooyour **Cisco Webex** tenant.
2. Ga te**gebruikers beheren \> gebruiker toevoegen**.
   
   ![Gebruikers toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "gebruikers toevoegen")
3. Op Hallo sectie gebruiker toevoegen, voert u Hallo stappen te volgen:
   
   ![Gebruiker toevoegen](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "gebruiker toevoegen")   
   1. Als **accounttype**, selecteer **Host**.
   2. Hallo-informatie van een bestaande Azure AD-gebruiker in Hallo tekstvakken volgende typen: **voornaam, achternaam**, **gebruikersnaam**, **e**, **wachtwoord**, **Wachtwoord bevestigen**.
   3. Klik op **Add**.

>[!NOTE]
>U kunt andere Cisco Webex gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Cisco Webex tooprovision AAD-gebruikersaccounts. 
> 

## <a name="assign-users"></a>Gebruikers toewijzen
tootest uw configuratie, moet u toogrant hello Azure AD-gebruikers gewenste tooallow met behulp van uw toepassing toegang tooit door toe te wijzen.

**tooassign gebruikers tooCisco Webex, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal hello, een testaccount te maken.
2. Op Hallo **Cisco Webex** toepassing Integratiepagina, klikt u op **gebruikers toewijzen**.
   
   ![Gebruikers toewijzen](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "gebruikers toewijzen")
3. Selecteer uw testgebruiker, klik op **toewijzen**, en klik vervolgens op **Ja** tooconfirm de toewijzing.
   
   ![Ja](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Ja")

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

