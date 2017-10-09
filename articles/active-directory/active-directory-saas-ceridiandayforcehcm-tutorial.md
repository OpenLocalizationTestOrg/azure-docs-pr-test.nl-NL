---
title: 'Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Ceridian Dayforce HCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a>Zelfstudie: Azure Active Directory-integratie met Ceridian Dayforce HCM

In deze zelfstudie leert u hoe toointegrate Ceridian Dayforce HCM met Azure Active Directory (Azure AD).

Ceridian Dayforce HCM integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooCeridian Dayforce HCM heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooCeridian Dayforce HCM (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Ceridian Dayforce HCM tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Ceridian Dayforce HCM eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Ceridian Dayforce HCM van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a>Het toevoegen van Ceridian Dayforce HCM van Hallo-galerie
tooconfigure hello integratie van Ceridian Dayforce HCM in Azure AD, moet u tooadd Ceridian Dayforce HCM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Ceridian Dayforce HCM via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Ceridian Dayforce HCM**, selecteer **Ceridian Dayforce HCM** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Ceridian Dayforce HCM in de lijst met resultaten Hallo](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Ceridian Dayforce HCM op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Ceridian Dayforce HCM is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Ceridian Dayforce HCM toobe tot stand gebracht.

Wijs in Ceridian Dayforce HCM, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Ceridian Dayforce HCM, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave een equivalent van Britta Simon in Ceridian Dayforce HCM die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Ceridian Dayforce HCM configureren.

**tooconfigure eenmalige aanmelding Azure AD met Ceridian Dayforce HCM, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Ceridian Dayforce HCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. Op Hallo **Ceridian Dayforce HCM domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    a. In Hallo **aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign op tooyour Ceridian Dayforce HCM toepassing gebruikt.
    
    | Omgeving | URL |
    | :-- | :-- |
    | Voor productie | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | Voor de tests voor | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:
    
    | Omgeving | URL |
    | :-- | :-- |
    | Voor productie | `https://ncpingfederate.dayforcehcm.com/sp` |
    | Voor de tests voor | `https://fs-test.dayforcehcm.com/sp` |
    
    c. In Hallo **antwoord-URL** textbox type Hallo-URL die door Azure AD toopost Hallo antwoord gebruikt.
    
    | Omgeving | URL |
    | :-- | :-- |
    | Voor productie | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | Voor de tests voor | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Neem contact op met [Ceridian Dayforce HCM Client ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. Uw toepassing Ceridian Dayforce HCM verwacht Hallo SAML asserties in een specifieke indeling. Werken met [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) eerste tooidentify Hallo juiste gebruikers-id. Microsoft raadt u Hallo **'name'** kenmerk als gebruikers-id. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerken** sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk  | De waarde van kenmerk |
    | --------------- | -------------------- |    
    | naam  | User.extensionattribute2 |    

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. In Hallo **waarde** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie.
    Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u **user.extensionattribute2**.
    
    d. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. Op Hallo **Ceridian Dayforce HCM configuratie** sectie, klikt u op **configureren Ceridian Dayforce HCM** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Ceridian Dayforce HCM configuratie](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. tooconfigure eenmalige aanmelding op **Ceridian Dayforce HCM** zijde, moet u toosend Hallo gedownload **Metadata XML** en **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** te[Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html).

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a>Een testgebruiker Ceridian Dayforce HCM maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Ceridian Dayforce HCM van een gebruiker. Werken met Hallo [Ceridian Dayforce HCM ondersteuningsteam](https://www.ceridian.com/contact-us/index.html) tooget gebruikers toegevoegd in Hallo Ceridian Dayforce HCM toepassing. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCeridian Dayforce HCM.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Ceridian Dayforce HCM**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCeridian Dayforce HCM.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Ceridian Dayforce HCM**.

    ![Hallo Ceridian Dayforce HCM koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  
Als u op Hallo Ceridian Dayforce HCM tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Ceridian Dayforce HCM toepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

