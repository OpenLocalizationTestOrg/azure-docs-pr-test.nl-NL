---
title: 'Zelfstudie: Azure Active Directory-integratie met Pingboard | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Pingboard.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a>Zelfstudie: Azure Active Directory-integratie met Pingboard

In deze zelfstudie leert u hoe toointegrate Pingboard met Azure Active Directory (Azure AD).

Pingboard integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooPingboard toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooPingboard (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Pingboard tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Pingboard eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Pingboard van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-pingboard-from-hello-gallery"></a>Het toevoegen van Pingboard van Hallo-galerie
tooconfigure hello integratie van Pingboard in Azure AD, moet u tooadd Pingboard uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Pingboard via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Pingboard**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. Selecteer in het deelvenster resultaten hello, **Pingboard**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Pingboard op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Pingboard is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Pingboard toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Pingboard.

tooconfigure en eenmalige aanmelding Azure AD-test met Pingboard, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Pingboard](#creating-a-pingboard-test-user)**  -toohave een equivalent van Britta Simon in Pingboard die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing Pingboard configureren.

**Azure AD tooconfigure eenmalige aanmelding met Pingboard, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **Pingboard** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. Op Hallo **Pingboard domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    a. In Hallo **id** textbox Hallo typewaarde als:`http://<entity-id>.pingboard.com/sp`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<entity-id>.pingboard.com/auth/saml/consume`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id. Neem contact op met [Pingboard Client ondersteuningsteam](https://support.pingboard.com/) tooget deze waarden. 

4. Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    a. In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`http://<sub-domain>.pingboard.com/sign_in`
     
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. tooconfigure SSO Pingboard zijde, open een nieuw browservenster en meld u tooyour Pingboard-Account. U moet een Pingboard admin tooset van eenmalige aanmelding op.

8. Selecteer in het bovenste menu Hallo **Apps > integraties**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  Op Hallo **integraties** pagina, Hallo zoeken **'Azure Active Directory'** tegel en klik erop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. In de modale Hallo klikt u op volgende **'Configureren'**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. Op Hallo na pagina, zult u merken dat ' Azure SSO-integratie is ingeschakeld.'. Open Hallo gedownload Metadata XML-bestand in een Hallo Kladblok en plak de inhoud van **IDP metagegevens**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. Hallo-bestand worden gevalideerd en als alles juist is eenmalige aanmelding nu worden ingeschakeld

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-pingboard-test-user"></a>Een testgebruiker Pingboard maken

In de volgorde tooenable Azure AD gebruikers toolog in Pingboard, moeten ze worden ingericht in Pingboard.  
In geval van Pingboard Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Aanmelden tooyour Pingboard bedrijf site als beheerder.

2. Klik op **'Werknemer toevoegen'** knop op **Directory** pagina.

    ![Werknemer toevoegen](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. Op Hallo **'Werknemer toevoegen'** dialoogvenster pagina, voert u Hallo stappen te volgen.

    ![Personen uitnodigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    a. In Hallo **volledige naam** textbox Hallo volledige typenaam van Britta Simon.

    b. In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.

    c. In Hallo **taaktitel** textbox type Hallo-functie van Britta Simon.

    d. In Hallo **locatie** vervolgkeuzelijst, selecteer Hallo-locatie van Britta Simon.
    
    e. Klik op **Add**.   

4. Tooconfirm hello toevoeging van de gebruiker wordt een bevestigingsvenster komen.
    
    ![Bevestigen](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooPingboard toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooPingboard, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Pingboard**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Pingboard tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Pingboard toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
