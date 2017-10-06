---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceNow | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ServiceNow en ServiceNow Express.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Zelfstudie: Azure Active Directory-integratie met ServiceNow
In deze zelfstudie leert u hoe toointegrate ServiceNow en ServiceNow Express met Azure Active Directory (Azure AD).

ServiceNow en ServiceNow Express integreren met Azure AD biedt Hallo volgende voordelen:

* U kunt beheren in Azure AD wie toegang tot tooServiceNow heeft en ServiceNow Express
* U kunt uw gebruikers tooautomatically get aangemelde tooServiceNow en ServiceNow Express (Single Sign-On) inschakelen met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met ServiceNow en ServiceNow Express tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Voor ServiceNow, een exemplaar of de tenant van ServiceNow, Calgary versie of hoger
* Voor ServiceNow snelle, een exemplaar van ServiceNow Express, Helsinki versie of hoger
* Hallo ServiceNow-tenant moet hebben Hallo [meerdere Provider eenmalige aanmelding op invoegtoepassing](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) ingeschakeld. Dit kan worden gedaan door [indienen van een serviceaanvraag](https://hi.service-now.com). 

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
> 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ServiceNow van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding voor ServiceNow of ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Het toevoegen van ServiceNow van Hallo-galerie
tooconfigure hello integratie van ServiceNow of ServiceNow Express in Azure AD, moet u tooadd ServiceNow uit Hallo galerie tooyour lijst met beheerde SaaS-apps. 

**tooadd ServiceNow via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]
6. Typ in het zoekvak Hallo **ServiceNow**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Selecteer in het deelvenster met resultaten Hallo **ServiceNow**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met ServiceNow of ServiceNow snelle op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ServiceNow is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in ServiceNow toobe tot stand gebracht.
Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ServiceNow. tooconfigure en eenmalige aanmelding Azure AD-test met ServiceNow, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren voor ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable uw toouse gebruikers deze functie.
2. **[Configureren van Azure AD eenmalige aanmelding voor snelle ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable uw toouse gebruikers deze functie.
3. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Maken van een testgebruiker ServiceNow](#creating-a-servicenow-test-user)**  -toohave een equivalent van Britta Simon in ServiceNow die is gekoppeld toohello Azure AD-weergave van haar.
5. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
6. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

> [!NOTE]
> Als u wilt weglaten tooconfigure ServiceNow stap 2. Op dezelfde manier als u wilt dat tooconfigure weglaten ServiceNow snelle stap 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Azure AD voor eenmalige aanmelding configureren voor ServiceNow
1. In de klassieke portal hello Azure AD op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster .
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")

2. Op Hallo **wilt u hoe gebruikers toosign op tooServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")

3. Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")
   
    a. in Hallo **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.
   
    b. In Hallo **id** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.
   
    c. Klik op **Volgende**

4. toohave Azure AD automatisch ServiceNow configureren voor verificatie op basis van SAML, Voer uw ServiceNow-instantienaam, beheerdersgebruikersnaam en beheerderswachtwoord in Hallo **automatisch eenmalige aanmelding configureren** vormen en klikt u op  *Configureer*. Opmerking die Hallo beheerder opgegeven gebruikersnaam moet hebben Hallo **security_admin** rol die is toegewezen in ServiceNow voor deze toowork. Anders toomanually ServiceNow toouse Azure AD als SAML-identiteitsprovider configureren, klikt u op **handmatig Hallo-toepassing voor eenmalige aanmelding configureren**, klikt u vervolgens op **volgende** en volledige Hallo volgende stappen uit.
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")

5. Op Hallo **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**, slaat u Hallo certificaatbestand lokaal op uw computer.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")

6. Eenmalige aanmelding tooyour ServiceNow-toepassing als beheerder.

7. Hallo activeren *integratie - meerdere Provider Single Sign-On-installatieprogramma* invoegtoepassing door Hallo volgende stappen:
   
    a. In het navigatievenster aan de linkerkant Hallo Hallo gaat te**System Definition** sectie en klik vervolgens op **Plugins**.
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "invoegtoepassing activeren")
   
    b. Zoeken naar *integratie - meerdere Provider Single Sign-On-installatieprogramma*.
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "invoegtoepassing activeren")
   
    c. Selecteer Hallo-invoegtoepassing. Rigth op en selecteer **activeren/Upgrade**.
   
    d. Klik op Hallo **activeren** knop.

8. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **eigenschappen**.  
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "app-URL configureren")

9. Op Hallo **meerdere eigenschappen van de Provider SSO** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "app-URL configureren")
   
    a. Als **provider voor meervoudige eenmalige aanmelding inschakelen**, selecteer **Ja**.
   
    b. Als **inschakelen, hebt u logboekregistratie voor foutopsporing Hallo provider voor meervoudige SSO-integratie**, selecteer **Ja**.
   
    c. In **Hallo veld op Hallo gebruiker tabel die...**  textbox type **gebruikersnaam**.
   
    d. Klik op **Opslaan**.

10. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **x509 certificaten**.
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "eenmalige aanmelding configureren")

11. Op Hallo **X.509-certificaten** dialoogvenster, klikt u op **nieuw**.
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "eenmalige aanmelding configureren")

12. Op Hallo **X.509-certificaten** dialoogvenster Hallo volgende stappen uit te voeren:
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")
    
     a. Klik op **Nieuw**.
    
     b. In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).
    
     c. Selecteer **Active**.
    
     d. Als **indeling**, selecteer **PEM**.
    
     e. Als **Type**, selecteer **vertrouwen Store Cert**.
    
     f. De met Base64 versleuteld certificaat openen in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PEM certificaat** textbox.
    
     g. Klik op **Update**.

13. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **identiteitsproviders**.
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "eenmalige aanmelding configureren")

14. Op Hallo **identiteitsproviders** dialoogvenster, klikt u op **nieuw**:
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "eenmalige aanmelding configureren")

15. Op Hallo **identiteitsproviders** dialoogvenster, klikt u op **SAML2 Update1?**:
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "eenmalige aanmelding configureren")

16. Op eigenschappenvenster Hallo SAML2 Update1, voert u Hallo stappen te volgen:
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "eenmalige aanmelding configureren")

    a. in Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).

    b. In Hallo **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt toouniquely gebruikers in uw ServiceNow-implementatie identificeren. 

    > [!NOTE] 
    > U kunt configue Azure AD tooemit beide hello Azure AD-gebruikers-ID (UPN) of Hallo e-mailadres als unieke id in het SAML-token Hallo Hallo door te gaan toohello **ServiceNow > kenmerken > eenmalige aanmelding** sectie klassieke Azure portal en toewijzing Hallo gewenst veld toohello Hallo **nameidentifier** kenmerk. Hallo-waarde voor het geselecteerde kenmerk Hallo opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de Hallo opgeslagen in ServiceNow voor Hallo ingevoerd veld (bijvoorbeeld gebruikersnaam)

    c. Kopieer in de klassieke portal hello Azure AD, Hallo **identiteit Provider-ID** waarde en plak deze in Hallo **identiteit Provider URL** textbox.

    d. Kopieer in de klassieke portal hello Azure AD, Hallo **aanvraag-URL voor webverificatie** waarde en plak deze in Hallo **van de identiteitsprovider AuthnRequest** textbox.

    e. Kopieer in de klassieke portal hello Azure AD, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **van de identiteitsprovider SingleLogoutRequest** textbox.

    f. In Hallo **ServiceNow Homepage** textbox type Hallo-URL van de startpagina van uw ServiceNow-exemplaar.

    > [!NOTE] 
    > startpagina van Hallo ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld:`https://fabrikam.service-now.com/navpage.do`).

    g. In Hallo **entiteit-ID / verlener** textbox type Hallo-URL van uw ServiceNow-tenant.

    h. In Hallo **doelgroep URL** textbox type Hallo-URL van uw ServiceNow-tenant. 

    ik. In Hallo **Protocol Binding voor Hallo van IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.

    j. Typ in het tekstvak NameID beleid hello, **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.

    k. Hef de selectie **maken van een AuthnContextClass**.

    l. In Hallo **AuthnContextClassRef methode**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Dit is alleen nodig als u alleen cloud-organisatie. Als u werkt met on-premises AD FS of MFA voor verificatie en vervolgens moet u deze waarde niet configureren. 

    m. In **klok leiden tot onjuiste** textbox type **60**.

    n. Als **eenmalige aanmelding op Script**, selecteer **MultiSSO_SAML2_Update1**.

    o. Als **x509 certificaat**, selecteert u hebt gemaakt in de vorige stap Hallo Hallo-certificaat.

    p. Klik op **indienen**. 

1. In de klassieke portal hello Azure AD, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")

2. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configureren van Azure AD voor eenmalige aanmelding voor snelle ServiceNow
1. In de klassieke portal hello Azure AD op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** dialoogvenster .
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749323.png "eenmalige aanmelding configureren")

2. Op Hallo **wilt u hoe gebruikers toosign op tooServiceNow** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749324.png "eenmalige aanmelding configureren")

3. Op Hallo **App-instellingen configureren** pagina, voert u Hallo stappen te volgen:
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC769497.png "app-URL configureren")
   
    a. in Hallo **ServiceNow aanmelding op URL** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen: `https://<instance-name>.service-now.com`.
   
    b. In Hallo **URL-verlener** textbox, typ de URL van uw gebruikt door uw gebruikers toosign op tooyour ServiceNow-toepassing hello patroon volgen `https://<instance-name>.service-now.com`.
   
    c. Klik op **Volgende**

4. Klik op **handmatig Hallo-toepassing voor eenmalige aanmelding configureren**, klikt u vervolgens op **volgende** en volledige Hallo stappen te volgen.
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "app-URL configureren")

5. Op Hallo **eenmalige aanmelding configureren op ServiceNow** pagina, klikt u op **certificaat downloaden**Hallo certificaatbestand lokaal op uw computer opgeslagen en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC749325.png "eenmalige aanmelding configureren")

6. Eenmalige aanmelding tooyour ServiceNow Express-toepassing als beheerder.

7. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **Single Sign-On**.  
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "app-URL configureren")

8. Op Hallo **Single Sign-On** dialoogvenster, klikt u op Hallo configuratiepictogram op Hallo rechterbovenhoek rechts en stel hello volgende eigenschappen:
   
    ![App-URL configureren](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "app-URL configureren")
   
    a. Wisselknop **provider voor meervoudige eenmalige aanmelding inschakelen** toohello rechts.
   
    b. Wisselknop **logboekregistratie voor Hallo provider voor meervoudige SSO-integratie voor het inschakelen van foutopsporing** toohello rechts.
   
    c. In **Hallo veld op Hallo gebruiker tabel die...**  textbox type **gebruikersnaam**.
9. Op Hallo **Single Sign-On** dialoogvenster, klikt u op **nieuw certificaat toevoegen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "eenmalige aanmelding configureren")
10. Op Hallo **X.509-certificaten** dialoogvenster Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "eenmalige aanmelding configureren")
    
    a. In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **TestSAML2.0**).
    
    b. Selecteer **Active**.
    
    c. Als **indeling**, selecteer **PEM**.
    
    d. Als **Type**, selecteer **vertrouwen Store Cert**.
    
    e. Maak een Base64-gecodeerde bestand uit het gedownloade certificaat.
    
    > [!NOTE]
    > Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. De met Base64 versleuteld certificaat openen in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PEM certificaat** textbox.
    
    g. Klik op **Update**.
11. Op Hallo **Single Sign-On** dialoogvenster, klikt u op **toevoegen van nieuwe IdP**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "eenmalige aanmelding configureren")
12. Op Hallo **identiteitsprovider toevoegen** dialoogvenster onder **id-Provider configureren**, Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "eenmalige aanmelding configureren")

    a. in Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: **SAML 2.0**).

    b. Kopieer in de klassieke portal hello Azure AD, Hallo **identiteit Provider-ID** waarde en plak deze in Hallo **identiteit Provider URL** textbox.

    c. Kopieer in de klassieke portal hello Azure AD, Hallo **aanvraag-URL voor webverificatie** waarde en plak deze in Hallo **van de identiteitsprovider AuthnRequest** textbox.

    d. Kopieer in de klassieke portal hello Azure AD, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **van de identiteitsprovider SingleLogoutRequest** textbox.

    e. Als **Provider identiteitscertificaat**, selecteert u hebt gemaakt in de vorige stap Hallo Hallo-certificaat.


1. Klik op **geavanceerde instellingen**, en klikt u onder **extra identiteitseigenschappen Provider**, Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "eenmalige aanmelding configureren")
   
    a. In Hallo **Protocol Binding voor Hallo van IDP SingleLogoutRequest** textbox type **urn: oasis: namen: tc: SAML:2.0:bindings:HTTP-omleiden**.
   
    b. In Hallo **NameID beleid** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: niet-gespecificeerde**.    
   
    c. In Hallo **AuthnContextClassRef methode**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Hef de selectie **maken van een AuthnContextClass**.

2. Onder **extra eigenschappen van de Service Provider**, Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "eenmalige aanmelding configureren")
   
    a. In Hallo **ServiceNow Homepage** textbox type Hallo-URL van de startpagina van uw ServiceNow-exemplaar.
   
    > [!NOTE]
    > startpagina van Hallo ServiceNow-exemplaar is een samenvoeging van uw **ServieNow tenant-URL** en **/navpage.do** (bijvoorbeeld: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. In Hallo **entiteit-ID / verlener** textbox type Hallo-URL van uw ServiceNow-tenant.
   
    c. In Hallo **doelgroep-URI** textbox type Hallo-URL van uw ServiceNow-tenant. 
   
    d. In **klok leiden tot onjuiste** textbox type **60**.
   
    e. In Hallo **Gebruikersveld** textbox type **e** of **gebruikersnaam**, afhankelijk van welk veld wordt gebruikt toouniquely gebruikers in uw ServiceNow-implementatie identificeren.
   
    > [!NOTE]
    > U kunt configue Azure AD tooemit beide hello Azure AD-gebruikers-ID (UPN) of Hallo e-mailadres als unieke id in het SAML-token Hallo Hallo door te gaan toohello **ServiceNow > kenmerken > eenmalige aanmelding** sectie klassieke Azure portal en toewijzing Hallo gewenst veld toohello Hallo **nameidentifier** kenmerk. Hallo-waarde voor het geselecteerde kenmerk Hallo opgeslagen in Azure AD (bijvoorbeeld gebruiker principal name) moet overeenkomen met de Hallo opgeslagen in ServiceNow voor Hallo ingevoerd veld (bijvoorbeeld gebruikersnaam)
    > 
    > 
   
    f. Klik op **Opslaan**. 

3. In de klassieke portal hello Azure AD, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "eenmalige aanmelding configureren")

4. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "eenmalige aanmelding configureren")

## <a name="configuring-user-provisioning"></a>Configuratie van gebruikers inrichten
Hallo-doel van deze sectie is het toooutline hoe tooServiceNow tooenable gebruikers inrichten van Active Directory-gebruiker accounts.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:
1. In hello Azure Management klassieke portal op Hallo **ServiceNow** toepassing Integratiepagina, klikt u op **configureren gebruikersaanvragen**. 
   
    ![Gebruikers inrichten](./media/active-directory-saas-servicenow-tutorial/IC769498.png "gebruikers inrichten")

2. Op Hallo **Voer uw ServiceNow referenties tooenable automatisch gebruikers inrichten** pagina, bieden Hallo na configuratie-instellingen:
   
     a. In Hallo **ServiceNow-exemplaarnaam** textbox typenaam Hallo ServiceNow-exemplaar.
   
     b. In Hallo **ServiceNow-Beheerdersgebruikersnaam** textbox Hallo typenaam Hallo ServiceNow-beheeraccount.
   
     c. In Hallo **ServiceNow-beheerderswachtwoord** textbox Hallo een wachtwoord op voor dit account.
   
     d. Klik op **valideren** tooverify uw configuratie.
   
     e. Klik op Hallo **volgende** knop tooopen hello **Vervolgstappen** pagina.
   
     f. Als u wilt dat tooprovision alle gebruikers toothis toepassing, selecteert u '**automatisch inrichten van alle gebruikersaccounts in de directory toothis-toepassing hello**'. 
   
    ![Volgende stappen](./media/active-directory-saas-servicenow-tutorial/IC698804.png "volgende stappen")
   
     g. Op Hallo **Vervolgstappen** pagina, klikt u op **Complete** toosave uw configuratie.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
   
    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op **Volgende**.

6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. In Hallo **voornaam** textbox type **Britta**.  
   
   b. In Hallo **achternaam** textbox type, **Simon**.
   
   c. In Hallo **weergavenaam** textbox type **Britta Simon**.
   
   d. In Hallo **rol** selecteert **gebruiker**.
   
   e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.   

### <a name="creating-a-servicenow-test-user"></a>Maken van een testgebruiker ServiceNow
In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow. In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in ServiceNow. Als u niet hoe tooadd een gebruiker in uw ServiceNow of ServiceNow Express-account weet, moet u contact op met ServiceNow-ondersteuningsteam.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooServiceNow toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooServiceNow, Voer Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ServiceNow**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][203] 

4. Selecteer in de lijst met alle gebruikers van hello, **Britta Simon**.

5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo ServiceNow-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ServiceNow-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
