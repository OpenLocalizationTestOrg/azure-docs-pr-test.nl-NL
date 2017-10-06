---
title: 'Zelfstudie: Azure Active Directory-integratie met Evernote | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Evernote.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 4d7017e571ed12a0b155aa188c6b0ecb3c9898a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a>Zelfstudie: Azure Active Directory-integratie met Evernote

In deze zelfstudie leert u hoe toointegrate Evernote met Azure Active Directory (Azure AD).

Evernote integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooEvernote toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooEvernote (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Evernote tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Evernote eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Evernote van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-evernote-from-hello-gallery"></a>Het toevoegen van Evernote van Hallo-galerie
tooconfigure hello integratie van Evernote in Azure AD, moet u tooadd Evernote uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Evernote via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Evernote**, selecteer **Evernote** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Evernote in de lijst met resultaten Hallo](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Evernote op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Evernote is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Evernote toobe tot stand gebracht.

Wijs in Evernote, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Evernote, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Evernote](#create-an-evernote-test-user)**  -toohave een equivalent van Britta Simon in Evernote die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Evernote configureren.

**Azure AD tooconfigure eenmalige aanmelding met Evernote, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Evernote** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. Op Hallo **Evernote domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wenst tooconfigure Hallo toepassing in de IDP geïnitieerd modus:

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    In Hallo **id** textbox type Hallo URL:`https://www.evernote.com/saml2`

4. Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:

    ![URL's en Evernote domein eenmalige aanmelding informatie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    In Hallo **aanmelden URL** textbox type Hallo URL:`https://www.evernote.com/Login.action`   

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. Op Hallo **Evernote configuratie** sectie, klikt u op **configureren Evernote** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Evernote configuratie](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. In een ander browservenster, meld u bij uw bedrijf Evernote site als beheerder.

9. Ga te**Admin-Console**

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. Van Hallo **Admin-Console**, gaat u te**'Security'** en selecteer **' Single Sign-On'**

    ![SSO-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. Configureer Hallo volgende waarden:

    ![Certificaat-instelling](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    a.  **Eenmalige aanmelding inschakelen:** eenmalige aanmelding is standaard ingeschakeld (Klik op **uitschakelen Single Sign-on** tooremove Hallo SSO vereiste)

    b. Plakken **SAML eenmalige aanmelding Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **SAML HTTP-verzoek-URL** textbox.

    c. Hallo gedownloade certificaat openen vanuit Azure AD in Kladblok en kopieer Hallo inhoud zoals 'BEGIN CERTIFICATE' en 'END CERTIFICATE' en plak deze in Hallo **X.509-certificaat** textbox. 

    d.Click **wijzigingen opslaan**

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-an-evernote-test-user"></a>Een testgebruiker Evernote maken

In de volgorde tooenable Azure AD gebruikers toolog in Evernote, moeten ze worden ingericht in Evernote.  
In geval van Evernote Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Aanmelden tooyour Evernote bedrijf site als beheerder.

2. Klik op Hallo **Admin-Console**.

    ![-Beheerconsole](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. Van Hallo **Admin-Console**, gaat u te**toevoegen van gebruikers**.

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. **Teamleden toevoegen** in Hallo **e** textbox, typ de e-mailadres Hallo van gebruikersaccount en klik op **uit te nodigen.**

    ![Voeg testgebruiker](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. Nadat uitnodiging is verzonden, is het hello Azure Active Directory-accounthouder ontvangt een e-mailadres tooaccept Hallo uitnodiging.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEvernote toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooEvernote, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Evernote**.

    ![Hallo Evernote koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Evernote tegel in Hallo Toegangsvenster, krijgt u aangemelde tooyour Evernote toepassing. U moet als een organisatie-account maar moeten toolog worden aanmelden met uw persoonlijke account. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

