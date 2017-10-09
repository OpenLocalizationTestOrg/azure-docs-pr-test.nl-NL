---
title: 'Zelfstudie: Azure Active Directory-integratie met etouches | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en etouches.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Zelfstudie: Azure Active Directory-integratie met etouches

In deze zelfstudie leert u hoe toointegrate etouches met Azure Active Directory (Azure AD).

Etouches integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooetouches toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooetouches (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met etouches tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een etouches eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van etouches van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-etouches-from-hello-gallery"></a>Het toevoegen van etouches van Hallo-galerie
tooconfigure hello integratie van etouches in Azure AD, moet u tooadd etouches uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd etouches via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **etouches**, selecteer **etouches** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![etouches in de lijst met resultaten Hallo](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met etouches op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in etouches is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in etouches toobe tot stand gebracht.

Wijs in etouches, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met etouches, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker etouches](#create-an-etouches-test-user)**  -toohave een equivalent van Britta Simon in etouches die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing etouches configureren.

**Azure AD tooconfigure eenmalige aanmelding met etouches, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **etouches** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. Op Hallo **etouches domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![etouches domein en de URL's eenmalige aanmelding informatie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Deze waarden zijn niet echt. U Hallo waarde bijwerken met de werkelijke Hallo Meld u aan bij de URL en de id, die verderop in Hallo zelfstudie wordt beschreven.
    > 

4. Hallo SAML asserties verwacht etouches toepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **gebruikerskenmerk** van Hallo-toepassing. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. 

    ![Gebruikerskenmerk](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ------------------- | -------------------- |
    | E-mail | User.mail |    
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Dialoogvenster kenmerk toevoegen](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**. 

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget SSO is geconfigureerd voor uw toepassing hello stappen te volgen in Hallo etouches toepassing uitvoeren: 

    ![etouches configuratie](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. Aanmelding te**etouches** toepassing met behulp van Hallo-beheerdersrechten.
   
    b. Ga toohello **SAML** configuratie.

    c. In Hallo **algemene instellingen** sectie en opent u het gedownloade certificaat vanuit Azure-portal in Kladblok, kopieer Hallo inhoud, plakt u deze in Hallo IDP metagegevens textbox. 

    d. Klik op Hallo **opslaan & blijven** knop.
  
    e. Klik op Hallo **updatemetagegevens** knop in Hallo sectie SAML-metagegevens. 

    f. Deze wordt geopend pagina Hallo en SSO worden uitgevoerd. Eenmaal Hallo SSO werkt u Hallo gebruikersnaam kunt instellen.

    g. Selecteer in het veld Username hello, Hallo **emailaddress** zoals weergegeven in onderstaande Hallo-afbeelding. 

    h. Kopiëren Hallo **SP entiteit-ID** waarde en plak deze in Hallo **id** textbox in **etouches domein en de URL's** sectie op Azure-portal.

    ik. Kopiëren Hallo **SSO URL / ACS** waarde en plak deze in Hallo **URL aanmelden** textbox in **etouches domein en de URL's** sectie op Azure-portal.
   
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-an-etouches-test-user"></a>Een testgebruiker etouches maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in etouches maken. Werken met [etouches Client ondersteuningsteam](https://www.etouches.com/event-software/support/customer-support/) tooadd Hallo gebruikers in Hallo etouches platform.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooetouches toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooetouches, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **etouches**.

    ![Hallo etouches koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding


Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo etouches-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour etouches toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

