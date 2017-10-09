---
title: 'Zelfstudie: Azure Active Directory-integratie met Envoy | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Envoy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a>Zelfstudie: Azure Active Directory-integratie met Envoy

In deze zelfstudie leert u hoe toointegrate Envoy met Azure Active Directory (Azure AD).

Envoy integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooEnvoy toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooEnvoy (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Envoy tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Envoy eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Envoy van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-envoy-from-hello-gallery"></a>Het toevoegen van Envoy van Hallo-galerie
tooconfigure hello integratie van Envoy in Azure AD, moet u tooadd Envoy uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Envoy via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Envoy**, selecteer **Envoy** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Lijst met zoekresultaten Envoy in Hallo](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Envoy op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Envoy is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Envoy toobe tot stand gebracht.

Wijs in Envoy, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Envoy, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Envoy](#create-an-envoy-test-user)**  -toohave een equivalent van Britta Simon in Envoy die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Envoy configureren.

**Azure AD tooconfigure eenmalige aanmelding met Envoy, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Envoy** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. Op Hallo **Envoy-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Envoy-domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.Envoy.com`
    
    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Envoy Client ondersteuningsteam](https://envoy.com/contact/) tooget deze waarde.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat...

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. Op Hallo **Envoy configuratie** sectie, klikt u op **Envoy configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Envoy-configuratie](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. In een ander browservenster, meld u bij uw bedrijf Envoy site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**.

    ![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")

9. Klik op **bedrijf**.

    ![Bedrijf](./media/active-directory-saas-envoy-tutorial/ic776783.png "bedrijf")

10. Klik op **SAML**.

    ![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")

11. In Hallo **SAML-verificatie** configuratie sectie, voert u Hallo stappen te volgen:

    ![SAML-verificatie](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML-verificatie")
    
    >[!NOTE]
    >Hallo-waarde voor Hallo hoofdkantoor locatie-ID is automatisch gegenereerd door de toepassing hello.
    
    a. In **vingerafdruk** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.
    
    b. Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd formulier hello Azure portal naar Hallo **identiteit PROVIDER HTTP-URL voor SAML** textbox.
    
    c. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-an-envoy-test-user"></a>Een testgebruiker Envoy maken

Er is geen actie-item voor u tooconfigure gebruikers inrichten tooEnvoy. Wanneer een toegewezen gebruiker toolog in Envoy met behulp van het toegangsvenster hello probeert, controleert Envoy of Hallo gebruiker bestaat. Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Envoy.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEnvoy toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooEnvoy, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Envoy**.

    ![Hallo Envoy-koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Envoy-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Envoy-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

