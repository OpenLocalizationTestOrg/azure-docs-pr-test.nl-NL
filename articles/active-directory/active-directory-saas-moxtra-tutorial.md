---
title: 'Zelfstudie: Azure Active Directory-integratie met Moxtra | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Moxtra.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Zelfstudie: Azure Active Directory-integratie met Moxtra

In deze zelfstudie leert u hoe toointegrate Moxtra met Azure Active Directory (Azure AD).

Moxtra integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooMoxtra toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooMoxtra (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Moxtra tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Moxtra eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Moxtra van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-moxtra-from-hello-gallery"></a>Het toevoegen van Moxtra van Hallo-galerie
tooconfigure hello integratie van Moxtra in Azure AD, moet u tooadd Moxtra uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Moxtra via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Moxtra**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. Selecteer in het deelvenster resultaten hello, **Moxtra**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Moxtra op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Moxtra is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Moxtra toobe tot stand gebracht.

Wijs in Moxtra, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Moxtra, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Moxtra](#creating-a-moxtra-test-user)**  -toohave een equivalent van Britta Simon in Moxtra die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Moxtra configureren.

**Azure AD tooconfigure eenmalige aanmelding met Moxtra, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Moxtra** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Op Hallo **Moxtra domein en de URL's** sectie, voert u Hallo stap:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://www.moxtra.com/service/#login`

4. Hallo SAML asserties verwacht Moxtra toepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze configuratie. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ------------------- | -------------------- |    
    | Voornaam | User.givenName |
    | Achternaam | User.surname |
    | idpid    | < SAML entiteit-ID > 

    > [!Note]
    > waarde van Hallo **idpid** -kenmerk is niet echt. U kunt de werkelijke waarde Hallo van opvragen **Naslaggids** onder sectie **Moxtra configuratie**.
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.

    d. Klik op **OK**.
    
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Op Hallo **Moxtra configuratie** sectie, klikt u op **configureren Moxtra** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. Een ander browservenster geopend Meld u aan bij tooyour Moxtra bedrijf site als beheerder.

9. Klik in de werkbalk aan de linkerkant Hallo Hallo op **-beheerconsole > SAML Single Sign-on**, en klik vervolgens op **nieuw**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Op Hallo **SAML** pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. In Hallo **naam** textbox, typ een naam voor uw configuratie (bijvoorbeeld: *SAML*). 
  
    b. In Hallo **IdP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal. 
 
    c. In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal. 
 
    d. In Hallo **AuthnContextClassRef** textbox type **urn: oasis: namen: tc: SAML:2.0:ac:classes:Password**. 
 
    e. In Hallo **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**. 
 
    f. Open certificaat dat u hebt gedownload vanuit Azure-portal in Kladblok Hallo inhoud kopieert en plakt u deze in Hallo **certificaat** textbox.    
 
    g. Typ uw e-maildomein SAML in Hallo SAML e domein textbox.    
  
    >[!NOTE]
    >toosee hello stappen tooverify Hallo domein, klikt u op Hallo '**ik**' hieronder.

    h. Klik op **Update**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-moxtra-test-user"></a>Een testgebruiker Moxtra maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Moxtra van een gebruiker.

**een gebruiker Britta Simon aangeroepen in Moxtra, toocreate uitvoeren Hallo stappen te volgen:**

1. Meld u op tooyour Moxtra bedrijf site als een beheerder.

2. Klik in de werkbalk aan de linkerkant Hallo Hallo op **-beheerconsole > Gebruikersbeheer**, en vervolgens **gebruiker toevoegen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:
  
    a. In Hallo **voornaam** textbox type **Britta**.
  
    b. In Hallo **achternaam** textbox type **Simon**.
  
    c. In Hallo **e** textbox type Britta van e-mailadres dezelfde als voor de Azure-portal.
  
    d. In Hallo **deling** textbox type **Dev**.
  
    e. In Hallo **afdeling** textbox type **IT**.
  
    f. Selecteer **beheerder**.
  
    g. Klik op **Add**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooMoxtra toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooMoxtra, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Moxtra**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Moxtra tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Moxtra toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

