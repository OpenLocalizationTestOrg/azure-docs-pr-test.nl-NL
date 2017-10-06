---
title: 'Zelfstudie: Azure Active Directory-integratie met Voyance | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Voyance.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a>Zelfstudie: Azure Active Directory-integratie met Voyance

In deze zelfstudie leert u hoe toointegrate Voyance met Azure Active Directory (Azure AD).

Voyance integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooVoyance toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooVoyance (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Voyance tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Voyance eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Voyance van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-voyance-from-hello-gallery"></a>Het toevoegen van Voyance van Hallo-galerie
tooconfigure hello integratie van Voyance in Azure AD, moet u tooadd Voyance uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Voyance via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Voyance**, selecteer **Voyance** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Voyance in de lijst met resultaten Hallo](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Voyance op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Voyance is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Voyance toobe tot stand gebracht.

Wijs in Voyance, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Voyance, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Voyance](#create-a-voyance-test-user)**  -toohave een equivalent van Britta Simon in Voyance die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Voyance configureren.

**Azure AD tooconfigure eenmalige aanmelding met Voyance, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Voyance** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. Op Hallo **Voyance domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com/saml/create/`

4. Controleer **weergeven geavanceerde instellingen voor URL** en uitvoeren van de volgende stap als u wilt dat tooconfigure Hallo toepassing in Hallo **SP** modus gestart:

    ![Voyance domein en URL's eenmalige aanmelding-informatie voor SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.nyansa.com/`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Neem contact op met [Voyance Client ondersteuningsteam](mailto:support@nyansa.com) tooget deze waarden. 

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. Op Hallo **Voyance configuratie** sectie, klikt u op **configureren Voyance** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Voyance configuratie](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. In een ander browservenster, aanmelding tooyour Voyance tenant als beheerder.

9. Ga toohello rechtsboven Hallo navigatiebalk en klik op Hallo vervolgkeuzelijst met de tekst "**Top universiteit**'.
    
    ![Eenmalige aanmelding op App aan clientzijde Top universiteit configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. Klik op '**beheerdersinstellingen**'.

    ![Eenmalige aanmelding op App aan clientzijde beheerdersinstellingen configureren](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. Klik op '**gebruikerstoegang**' tabblad.

    ![Eenmalige aanmelding configureren voor toegang voor App-zijde van gebruiker](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. Klik op Hallo '**SSO is uitgeschakeld**' knop tooconfigure Azure AD als een IdP SAML 2.0 gebruikt.

    ![Configureren van eenmalige aanmelding op App aan clientzijde SSO is uitgeschakeld knop](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. Ga te**SAML v2** sectie en Voer onderstaande stappen te volgen:

    ![Eenmalige aanmelding configureren op App aan clientzijde SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    a. Selecteer **ingeschakeld**.
    
    b. Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **IdP aanmeldings-URL** textbox.

    c. Het gedownloade Base64-gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IdP Cert** textbox.
    
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-voyance-test-user"></a>Een testgebruiker Voyance maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Voyance van een gebruiker. Voyance ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld. Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess Voyance gemaakt als deze nog niet bestaat.

>[!NOTE]
>Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [Voyance ondersteuningsteam](maiLto:support@nyansa.com).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooVoyance toegang verleent.

![Hallo-gebruikersrollen toewijzen][200]

**tooassign Britta Simon tooVoyance, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Voyance**.

    ![Hallo Voyance koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Voyance tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Voyance toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

