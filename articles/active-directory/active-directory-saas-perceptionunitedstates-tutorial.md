---
title: 'Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro) | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en perceptie Verenigde Staten (niet-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro)

In deze zelfstudie leert u hoe toointegrate perceptie Verenigde Staten (niet-UltiPro) met Azure Active Directory (Azure AD).

Perceptie Verenigde Staten (niet-UltiPro) integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooPerception Verenigde Staten (niet-UltiPro) heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooPerception Verenigde Staten (niet-UltiPro) (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met perceptie Verenigde Staten (niet-UltiPro), moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een perceptie Verenigde Staten (niet-UltiPro) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Perceptie Verenigde Staten (niet-UltiPro) uit de galerie Hallo toe te voegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Perceptie Verenigde Staten (niet-UltiPro) uit de galerie Hallo toe te voegen
tooconfigure hello integratie van perceptie Verenigde Staten (niet-UltiPro) in Azure AD, moet u tooadd perceptie Verenigde Staten (niet-UltiPro) uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd perceptie Verenigde Staten (niet-UltiPro) uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **perceptie Verenigde Staten (niet-UltiPro)**, selecteer **perceptie Verenigde Staten (niet-UltiPro)** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Perceptie Verenigde Staten (niet-UltiPro) in de lijst met resultaten Hallo](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro) op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in perceptie Verenigde Staten (niet-UltiPro) is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in de perceptie Verenigde Staten (niet-UltiPro) toobe tot stand gebracht.

In perceptie Verenigde Staten (niet-UltiPro), wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met perceptie Verenigde Staten (niet-UltiPro), moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave een equivalent van Britta Simon in perceptie Verenigde Staten (niet-UltiPro) die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing perceptie Verenigde Staten (niet-UltiPro).

**Azure AD tooconfigure eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro) uitvoeren Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **perceptie Verenigde Staten (niet-UltiPro)** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. Op Hallo **perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. In Hallo **id** textbox type Hallo URL:`https://perception.kanjoya.com/sp`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Hallo-waarde wordt bijgewerkt met Hallo werkelijke antwoord-URL, die verderop in Hallo zelfstudie wordt beschreven.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. Op Hallo **perceptie Verenigde Staten (niet-UltiPro) configuratie** sectie, klikt u op **configureren perceptie Verenigde Staten (niet-UltiPro)** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**

    a. Hallo **perceptie Verenigde Staten (niet-UltiPro)** toepassing hello vereist **SAML entiteit-ID** waarde, die u hebt gekopieerd, toobe uri-codering. tooget hello uri-gecodeerde waarde gebruik Hallo volgende koppeling:**http://www.url-encode-decode.com/**.

    b. Nadat u de uri Hallo gecodeerde waarde combineren met Hallo **antwoord-URL** zoals vermeld hieronder -

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Plakken Hallo hierboven waarde in Hallo **antwoord-URL** textbox in **perceptie Verenigde Staten (niet-UltiPro)-domein en de URL's** sectie.

    ![Perceptie Verenigde Staten (niet-UltiPro)-configuratie](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. Een ander browservenster geopend Meld u aan bij tooyour perceptie Verenigde Staten (niet-UltiPro) bedrijf site als beheerder.

8. Klik in het Hallo hoofdwerkbalk op **Accountinstellingen**.

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. Op Hallo **Accountinstellingen** pagina, voert u Hallo stappen te volgen:

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. In Hallo **bedrijfsnaam** textbox Hallo typenaam Hallo **bedrijf**.
    
    b. In Hallo **accountnaam** textbox Hallo typenaam Hallo **Account**.

    c. In **standaard antwoord-tooEmail** tekstvak, type Hallo geldig **e**.

    d. Selecteer **SSO-identiteitsprovider** als **SAML 2.0**.

10. Op Hallo **SSO configuratie** pagina, voert u Hallo stappen te volgen:

    ![Perceptie Verenigde Staten (niet-UltiPro) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Selecteer **SAML NameID Type** als **e**.

    b. In Hallo **SSO configuratienaam** textbox Hallo-typenaam van uw **configuratie**.
    
    c. In **identiteit providernaam** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal. 

    d. In **SAML domein textbox**, Voer Hallo domein zoals  **@contoso.com** .

    e. Klik op **opnieuw uploaden** tooupload hello **Metadata XML** bestand.

    f. Klik op **Update**.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)

In deze sectie maakt u een gebruiker met de naam Britta Simon in perceptie Verenigde Staten (niet-UltiPro). Werken met [ondersteuningsteam perceptie Verenigde Staten (niet-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd Hallo gebruikers in Hallo perceptie Verenigde Staten (niet-UltiPro) platform.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooPerception Verenigde Staten (niet-UltiPro).

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooPerception Verenigde Staten (niet-UltiPro), Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **perceptie Verenigde Staten (niet-UltiPro)**.

    ![Hallo perceptie Verenigde Staten (niet-UltiPro) koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo perceptie Verenigde Staten (niet-UltiPro)-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour perceptie Verenigde Staten (niet-UltiPro)-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

