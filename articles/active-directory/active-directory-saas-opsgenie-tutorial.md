---
title: 'Zelfstudie: Azure Active Directory-integratie met OpsGenie | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 50d31c234fb9716d05d681b9bc4164740a3a662b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>Zelfstudie: Azure Active Directory-integratie met OpsGenie

In deze zelfstudie leert u hoe toointegrate OpsGenie met Azure Active Directory (Azure AD).

OpsGenie integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooOpsGenie toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooOpsGenie (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met OpsGenie tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een OpsGenie eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van OpsGenie van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-opsgenie-from-hello-gallery"></a>Het toevoegen van OpsGenie van Hallo-galerie
tooconfigure hello integratie van OpsGenie in Azure AD, moet u tooadd OpsGenie uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd OpsGenie via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **OpsGenie**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. Selecteer in het deelvenster resultaten hello, **OpsGenie**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met OpsGenie op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in OpsGenie is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in OpsGenie toobe tot stand gebracht.

Wijs in OpsGenie, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met OpsGenie, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker OpsGenie](#creating-a-opsgenie-test-user)**  -toohave een equivalent van Britta Simon in OpsGenie die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing OpsGenie configureren.

**Azure AD tooconfigure eenmalige aanmelding met OpsGenie, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **OpsGenie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. Op Hallo **OpsGenie domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://app.opsgenie.com/auth/login`

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. Op Hallo **OpsGenie configuratie** sectie, klikt u op **configureren OpsGenie** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. Open een ander browserexemplaar, en vervolgens aanmelden tooOpsGenie als beheerder.

8. Klik op **instellingen**, en klik vervolgens op Hallo **eenmalige aanmelding** tabblad.
   
    ![OpsGenie voor eenmalige aanmelding](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. tooenable SSO, selecteer **ingeschakeld**.
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. In Hallo **Provider** sectie, klikt u op Hallo **Azure Active Directory** tabblad.
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. Voer op Hallo Azure Active Directory dialoogvenster pagina Hallo stappen te volgen:
   
    ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. Plakken **aanmelding op Service-URL met eenmalige**, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML 2.0 eindpunt** textbox.
    
    b. De gedownloade base-64 gecodeerde certificaat Open in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze in Hallo **X.500 certificaat** textbox.
    
    c. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-opsgenie-test-user"></a>Een testgebruiker OpsGenie maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in OpsGenie van een gebruiker. 

1. Meld u aan bij uw tenant OpsGenie als een beheerder in een browservenster.

2. Navigeer tooUsers lijst door te klikken op **gebruiker** in het linkerdeelvenster.
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. Klik op **gebruiker toevoegen**.

4. Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:
   
   ![OpsGenie instellingen](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. In Hallo **e** textbox type Hallo e-mailadres van BrittaSimon behandeld in Azure Active Directory.
   
   b. In Hallo **volledige naam** textbox type **Britta Simon**.
   
   c. Klik op **Opslaan**. 

>[!NOTE]
>Britta Hiermee haalt u een e-mailbericht met instructies voor het instellen van haar profiel.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOpsGenie toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooOpsGenie, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **OpsGenie**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo OpsGenie tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour OpsGenie toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

