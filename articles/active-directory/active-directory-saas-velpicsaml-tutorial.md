---
title: 'Zelfstudie: Azure Active Directory-integratie met Velpic SAML | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Velpic SAML.
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
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a>Zelfstudie: Azure Active Directory-integratie met Velpic SAML

In deze zelfstudie leert u hoe toointegrate Velpic SAML met Azure Active Directory (Azure AD).

Velpic SAML integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooVelpic SAML heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooVelpic SAML (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Velpic SAML tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Velpic SAML-eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Velpic SAML van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-velpic-saml-from-hello-gallery"></a>Het toevoegen van Velpic SAML van Hallo-galerie
tooconfigure hello integratie van Velpic SAML in Azure AD, moet u tooadd Velpic SAML uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Velpic SAML via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Velpic SAML**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. Selecteer in het deelvenster resultaten hello, **Velpic SAML**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Velpic SAML op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Velpic SAML is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Velpic SAML toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Velpic SAML.

tooconfigure en eenmalige aanmelding Azure AD-test met Velpic SAML, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave een equivalent van Britta Simon in Velpic SAML die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Velpic SAML.

**Azure AD tooconfigure eenmalige aanmelding met Velpic SAML, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **Velpic SAML** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. Voer Hallo-gegevens in Hallo **Velpic SAML-domein en de URL's** sectie -

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    a. In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://<sub-domain>.velpicsaml.net`

    b. In Hallo **id** textbox plakken Hallo **'Eenmalige op URL'** waarde`https://auth.velpic.com/saml/v2/<entity-id>/login`
    
    > [!NOTE]
    > Houd er rekening mee dat Hallo aanmelding URL worden geleverd door Hallo Velpic SAML-team en id-waarde beschikbaar zijn bij het configureren van SSO-invoegtoepassing Hallo Velpic SAML-zijde. U moet toocopy die de waarde uit de pagina Velpic SAML-toepassing en plakt u deze hier.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. Klik op Hallo Velpic SAML-configuratiesectie, configureer Velpic SAML tooopen configureren aanmelding venster. Hallo SAML entiteit-ID van Hallo Naslaggids punt kopiëren.

7. In een ander browservenster, meld u bij uw bedrijf Velpic SAML site als beheerder.

8. Klik op **beheren** tabblad en ga te**integratie** sectie waarin u tooclick moet op **Plugins** knop toocreate nieuwe-invoegtoepassing voor aanmelden.

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. Klik op Hallo **'Add invoegtoepassing'** knop.
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. Klik op Hallo **SAML** -tegel in Hallo invoegtoepassing toevoegen pagina.
    
    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. Hallo-naam van de nieuwe SAML-invoegtoepassing Hallo en klik op Hallo **'Add-** knop.

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. Voer Hallo gegevens als volgt in:

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    a. In Hallo **naam** textbox Hallo-typenaam van SAML-invoegtoepassing.

    b. In Hallo **URL-verlener** textbox plakken Hallo **SAML entiteit-ID** u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.

    c. In Hallo **Provider metagegevens Config** Hallo Metadata XML-bestand dat u hebt gedownload van Azure-portal uploaden.

    d. U kunt ook tooenable SAML in tijd inrichten door in te schakelen Hallo **'Automatische Maak nieuwe gebruikers'** selectievakje. Als een gebruiker niet in Velpic bestaat en deze markering niet is ingeschakeld, mislukt de Hallo aanmelding van Azure. Als het Hallo-vlag is ingeschakeld Hallo gebruiker wordt automatisch worden ingericht in Velpic op Hallo-tijd van de aanmelding. 

    e. Kopiëren Hallo **eenmalige op URL** vanuit Hallo tekstvak en plakt Hallo in Azure-portal.
    
    f. Klik op **Opslaan**.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-velpic-saml-test-user"></a>Een testgebruiker Velpic SAML maken

Deze stap is meestal niet vereist als toepassing hello alleen in de tijd gebruikersaanvragen ondersteunt. Als Hallo automatisch gebruikers inrichten niet is ingeschakeld kan vervolgens maken van een handmatige gebruikersaccount worden uitgevoerd zoals hieronder wordt beschreven.

Meld u aan bij uw site van het bedrijf Velpic SAML als beheerder en voert u de volgende stappen:
    
1. Klik op het tabblad beheren en ga tooUsers sectie en klik vervolgens op de nieuwe knop tooadd gebruikers.

    ![gebruiker toevoegen](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. Op Hallo **'Nieuwe gebruiker maken'** dialoogvenster pagina, voert u Hallo stappen te volgen.

    ![Gebruiker](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    a. In Hallo **voornaam** textbox type Hallo voornaam van Britta Simon.

    b. In Hallo **achternaam** textbox type Hallo achternaam van Britta Simon.

    c. In Hallo **gebruikersnaam** textbox, typ de gebruikersnaam van Britta Simon Hallo.

    d. In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.

    e. Overige Hallo informatie is optioneel, vult u deze indien nodig.
    
    f. Klik op **OPSLAAN**.  

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooVelpic SAML verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooVelpic SAML, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Velpic SAML**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

1. Als u op Hallo Velpic SAML-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Velpic SAML-toepassing. U ziet Hallo **'Aanmelden met Azure AD'** knop op de aanmeldingspagina Hallo.

    ![Invoegtoepassing](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. Klik op Hallo **'Aanmelden met Azure AD'** knop toolog in tooVelpic met behulp van uw Azure AD-account.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

