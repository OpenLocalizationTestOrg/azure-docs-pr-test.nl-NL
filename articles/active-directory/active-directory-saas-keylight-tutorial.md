---
title: 'Zelfstudie: Azure Active Directory-integratie met LockPath Keylight | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LockPath Keylight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Zelfstudie: Azure Active Directory-integratie met LockPath Keylight

In deze zelfstudie leert u hoe toointegrate LockPath Keylight met Azure Active Directory (Azure AD).

LockPath Keylight integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooLockPath Keylight heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooLockPath Keylight (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met LockPath Keylight tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LockPath Keylight eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van LockPath Keylight van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Het toevoegen van LockPath Keylight van Hallo-galerie
tooconfigure hello integratie van LockPath Keylight in Azure AD, moet u tooadd LockPath Keylight uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd LockPath Keylight via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **LockPath Keylight**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. Selecteer in het deelvenster resultaten hello, **LockPath Keylight**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met LockPath Keylight op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LockPath Keylight is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LockPath Keylight toobe tot stand gebracht.

Wijs in LockPath Keylight, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met LockPath Keylight, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave een equivalent van Britta Simon in LockPath Keylight die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LockPath Keylight configureren.

**Azure AD tooconfigure eenmalige aanmelding met LockPath Keylight, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **LockPath Keylight** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. Op Hallo **LockPath Keylight domein en de URL's** sectie, voert u stappen te volgen Hallo::

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com/`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Neem contact op met [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. Op Hallo **LockPath Keylight configuratie** sectie, klikt u op **configureren LockPath Keylight** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO in LockPath Keylight, Voer Hallo stappen te volgen:
   
    a. Eenmalige aanmelding tooyour LockPath Keylight account als administrator.
    
    b. Klik in het menu bovenaan Hallo Hallo **persoon**, en selecteer **Keylight Setup**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. In de structuurweergave Hallo op Hallo links, klikt u op **SAML**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. Op Hallo **SAML instellingen** dialoogvenster, klikt u op **bewerken**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/404.png) 

8. Op Hallo **SAML-instellingen bewerken** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Stel **SAML-verificatie** te**Active**.

    b. Plakken Hallo **SAML Single Sign-On Service-URL** waarde die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider aanmeldings-URL** textbox.

    c. Plakken Hallo **Service-URL met eenmalige Sign-Out** waarde die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider afmelding URL** textbox.

    d. Klik op **bestand kiezen** tooselect uw gedownloade LockPath Keylight van het certificaat, en klik vervolgens op **Open** tooupload Hallo certificaat.

    e. Ingesteld **SAML-gebruikersnaam locatie** te**NameIdentifier-element van Hallo onderwerp instructie**.
    
    f. Hallo bieden **Keylight serviceprovider** met Hallo patroon volgen: **https://&lt;NaamBedrijf&gt;. keylightgrc.com**.
    
    g. Stel **automatisch inrichten gebruikers** te**Active**.

    h. Stel **automatisch inrichten accounttype** te**volledige gebruiker**.

    ik. Stel **automatisch inrichten beveiligingsrol**, selecteer **standaardgebruiker met SAML**.
    
    j. Stel **automatisch inrichten beveiliging config**, selecteer **standaardconfiguratie van de gebruiker**.
     
    k. In Hallo **e kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. In Hallo **voornaam kenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. In Hallo **laatste naamkenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Een testgebruiker LockPath Keylight maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in LockPath Keylight maken. LockPath Keylight ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt gemaakt bij het openen van LockPath Keylight als Hallo gebruiker nog niet bestaat. 

>[!NOTE]
>Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [LockPath Keylight Client ondersteuningsteam](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLockPath Keylight.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLockPath Keylight, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **LockPath Keylight**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo LockPath Keylight-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour LockPath Keylight toepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

