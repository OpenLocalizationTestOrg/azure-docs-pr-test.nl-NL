---
title: 'Zelfstudie: Azure Active Directory-integratie met Litmos | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Litmos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 026fd10058760f2d63d185ef4aa9d7de3b82525e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a>Zelfstudie: Azure Active Directory-integratie met Litmos

In deze zelfstudie leert u hoe toointegrate Litmos met Azure Active Directory (Azure AD).

Litmos integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooLitmos toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooLitmos (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Litmos tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Litmos eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Litmos van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-litmos-from-hello-gallery"></a>Het toevoegen van Litmos van Hallo-galerie
tooconfigure hello integratie van Litmos in Azure AD, moet u tooadd Litmos uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Litmos via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Litmos**, selecteer **Litmos** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Litmos in de lijst met resultaten Hallo](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Litmos op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Litmos is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Litmos toobe tot stand gebracht.

Wijs in Litmos, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Litmos, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Litmos](#create-a-litmos-test-user)**  -toohave een equivalent van Britta Simon in Litmos die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Litmos configureren.

**Azure AD tooconfigure eenmalige aanmelding met Litmos, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Litmos** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. Op Hallo **Litmos domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Litmos domein eenmalige aanmelding informatie](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.litmos.com/account/Login`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.litmos.com/integration/samllogin`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden met Hallo werkelijke id en de antwoord-URL, die worden beschreven verderop in de zelfstudie of neem contact op met [Litmos ondersteuningsteam](https://www.litmos.com/contact-us/) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. Als onderdeel van Hallo configuratie, moet u toocustomize hello **SAML-Token kenmerken** voor uw toepassing Litmos.

    ![Kenmerk-sectie](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | Naam van kenmerk   | De waarde van kenmerk |   
    | ---------------  | ----------------|
    | Voornaam |User.givenName |
    | Achternaam  |User.surname |
    | E-mail |User.mail |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Kenmerk toevoegen](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Kenmerk Dailog toevoegen](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**.     

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. In een ander browservenster, aanmelding tooyour Litmos bedrijf site als administrator.

8. Klik in de navigatiebalk aan de linkerkant Hallo Hallo op **Accounts**.
   
    ![Het gedeelte accounts App-zijde][22] 

9. Klik op Hallo **integraties** tabblad.
   
    ![Tabblad-integratie][23] 

10. Op Hallo **integraties** tabblad, schuif naar beneden te**3e partij integraties**, en klik vervolgens op **SAML 2.0** tabblad.
   
    ![SAML 2.0 sectie][24] 

11. Kopieer Hallo waarde onder **Hallo SAML-eindpunt voor litmos is:** en plak deze in Hallo **antwoord-URL** textbox in Hallo **Litmos domein en de URL's** sectie in Azure-portal. 
   
    ![SAML-eindpunt][26] 

12. In uw **Litmos** -toepassing hello stappen uitvoeren:
    
     ![Litmos toepassing][25] 
     
     a. Klik op **SAML inschakelen**.
    
     b. De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **SAML X.509-certificaat** textbox.
     
     c. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
  
### <a name="create-a-litmos-test-user"></a>Een testgebruiker Litmos maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Litmos van een gebruiker.  
Hallo Litmos toepassing biedt ondersteuning voor Just-in-Time-inrichting. Dit betekent een gebruikersaccount wordt automatisch gemaakt indien nodig tijdens een poging tooaccess Hallo toepassing hello Toegangsvenster gebruiken.

**een gebruiker Britta Simon aangeroepen in Litmos, toocreate uitvoeren Hallo stappen te volgen:**

1. In een ander browservenster, aanmelding tooyour Litmos bedrijf site als administrator.

2. Klik in de navigatiebalk aan de linkerkant Hallo Hallo op **Accounts**.
   
    ![Het gedeelte accounts App-zijde][22] 

3. Klik op Hallo **integraties** tabblad.
   
    ![Tabblad integraties][23] 

4. Op Hallo **integraties** tabblad, schuif naar beneden te**3e partij integraties**, en klik vervolgens op **SAML 2.0** tabblad.
   
    ![SAML 2.0][24] 
    
5. Selecteer **Autogenerate gebruikers**
   
    ![Gebruikers automatisch genereren][27] 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLitmos toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooLitmos, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Litmos**.

    ![Hallo Litmos koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  

Als u op Hallo Litmos-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Litmos toepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

