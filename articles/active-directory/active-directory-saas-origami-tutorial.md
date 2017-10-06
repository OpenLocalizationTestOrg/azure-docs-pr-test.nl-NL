---
title: 'Zelfstudie: Azure Active Directory-integratie met Origami | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Origami.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a>Zelfstudie: Azure Active Directory-integratie met Origami

In deze zelfstudie leert u hoe toointegrate Origami met Azure Active Directory (Azure AD).

Origami integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooOrigami toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooOrigami (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Origami tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Origami eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Origami van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-origami-from-hello-gallery"></a>Het toevoegen van Origami van Hallo-galerie
tooconfigure hello integratie van Origami in Azure AD, moet u tooadd Origami uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Origami via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Origami**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. Selecteer in het deelvenster resultaten hello, **Origami**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Origami op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Origami is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Origami toobe tot stand gebracht.

Wijs in Origami, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Origami, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Origami](#creating-an-origami-test-user)**  -toohave een equivalent van Britta Simon in Origami die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Origami configureren.

**Azure AD tooconfigure eenmalige aanmelding met Origami, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Origami** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. Op Hallo **Origami domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://live.origamirisk.com/origami/account/login?account=<companyname>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [Origami Client ondersteuningsteam](https://wordpress.org/support/theme/origami) tooget Hallo waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. Op Hallo **Origami configuratie** sectie, klikt u op **Origami configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. Meld u bij toohello Origami account met beheerdersrechten.

8. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. Uitvoeren op Hallo Single Sign op Setup dialoogvenster pagina Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    a. Selecteer **eenmalige aanmelding inschakelen op**.

    b. In Hallo **van de identiteitsprovider aanmelden pagina-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    c. In Hallo **Sign-out pagina-URL van de identiteitsprovider** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    d. Klik op **Bladeren** tooupload Hallo certificaat u hebt gedownload van hello Azure-portal.

    e. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-origami-test-user"></a>Een testgebruiker Origami maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Origami maken. 

1. Meld u bij toohello Origami account met beheerdersrechten.

2. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. Op Hallo **gebruikers en beveiliging** dialoogvenster, klikt u op **gebruikers**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. Klik op **nieuwe gebruiker toevoegen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. Voer in het dialoogvenster van de nieuwe gebruiker toevoegen hello, Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    a. In Hallo **gebruikersnaam** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .

    b. In Hallo **wachtwoord** textbox, typ een wachtwoord.

    c. In Hallo **wachtwoord bevestigen** textbox type Hallo wachtwoord opnieuw.

    d. In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.

    e. In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.

    f. Klik op **Opslaan**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. Wijs **gebruikersrollen** en **clienttoegang** toohello gebruiker. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOrigami toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooOrigami, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Origami**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Origami tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Origami toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

