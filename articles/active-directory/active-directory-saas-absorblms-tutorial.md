---
title: 'Zelfstudie: Azure Active Directory-integratie met kunnen LMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LMS opvangen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Zelfstudie: Azure Active Directory-integratie met LMS opnemen

In deze zelfstudie leert u hoe toointegrate Absorb LMS met Azure Active Directory (Azure AD).

LMS kunnen integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAbsorb LMS heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAbsorb LMS (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie. [Wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met LMS kunnen tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LMS kunnen eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Toe te voegen kunnen LMS uit Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-absorb-lms-from-hello-gallery"></a>Toe te voegen kunnen LMS uit Hallo-galerie
tooconfigure hello integratie van LMS opnemen in tooAzure AD, moet u tooadd Absorb LMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Absorb LMS via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **LMS kunnen**, selecteer **LMS kunnen** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![LMS opnemen in lijst met resultaten Hallo](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met kunnen LMS op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in kunnen LMS is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in kunnen LMS toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LMS opvangen.

tooconfigure en eenmalige aanmelding Azure AD-test met LMS opnemen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker kunnen LMS](#create-an-absorb-lms-test-user)**  -toohave een equivalent van Britta Simon in kunnen LMS gekoppelde toohello Azure AD-weergave van de gebruiker is.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LMS kunnen configureren.

**Azure AD tooconfigure eenmalige aanmelding met LMS kunnen uitvoeren Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **kunnen LMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Op Hallo **kunnen LMS domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![LMS domein en de URL's eenmalige aanmelding informatie opnemen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [kunnen LMS Client ondersteuningsteam](https://www.absorblms.com/support) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Op Hallo **LMS configuratie kunnen** sectie, klikt u op **kunnen LMS configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![LMS configuratie opnemen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. In een ander browservenster, meld u aan tooyour kunnen LMS bedrijf site als een beheerder.

9. Klik op Hallo **pictogram** op Hallo-beheerinterface. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Klik op **portalinstellingen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Klik op Hallo **gebruikers** tabblad.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Volgende stappen tooaccess Hallo Single Sign-On configuratievelden Hallo uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Selecteer Hallo juiste **modus**.

    b. Open Hallo certificaat dat u hebt gedownload van Azure-portal in Kladblok Hallo Hallo verwijderen **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---** code en plak Hallo resterende inhoud in Hallo **sleutel** textbox.
    
    c. In Hallo **Id-eigenschap**, selecteer Hallo juiste kenmerk dat u hebt geconfigureerd zoals Hallo gebruikers-id in hello Azure AD (bijvoorbeeld als Hallo userprinciplename is ingeschakeld in Azure AD en vervolgens de gebruikersnaam hier zou worden geselecteerd.)

    d. In Hallo **aanmeldings-URL**, plak Hallo **'SAML Single Sign-On Service URL'** waarde die u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.

    e. In Hallo **afmelding URL**, Hallo plakken **'Sign-Out URL'** waarde die u hebt gekopieerd uit Hallo **eenmalige aanmelding configureren** venster Hallo Azure-portal.

13. Schakel **'Alleen SSO aanmelden toestaan'**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Klik op **'Opgeslagen'.**

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.

### <a name="create-an-absorb-lms-test-user"></a>Een testgebruiker LMS kunnen maken

Azure AD tooenable gebruikers toolog in tooAbsorb LMS, ze in tooAbsorb LMS moeten worden ingericht.  
Inrichting is een handmatige taak voor LMS opvangen.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Aanmelden tooyour kunnen LMS bedrijf site als beheerder.

2. Klik op **gebruikers** tabblad.

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Klik op **gebruikers** onder Hallo **gebruikers** tabblad.

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Selecteer **gebruiker** van **nieuwe toevoegen** vervolgkeuzelijst.

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Op Hallo **gebruiker toevoegen** pagina, voert u Hallo stappen te volgen:

    ![Personen uitnodigen](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. In Hallo **voornaam** textbox type Hallo Voornaam zoals Britta.

    b. In Hallo **achternaam** textbox type Hallo achternaam zoals Simon.
    
    c. In Hallo **gebruikersnaam** textbox, typ de gebruikersnaam zoals Britta Simon Hallo.

    d. In Hallo **wachtwoord** textbox type wachtwoord op Hallo van Britta Simon.

    e. In Hallo **wachtwoord bevestigen** textbox type Hallo hetzelfde wachtwoord.
    
    f. Als u **ACTIVE**.   

6. Klik op **'Opgeslagen'.**
 
### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAbsorb LMS.

![Hallo-gebruikersrollen toewijzen][200]

**tooassign Britta Simon tooAbsorb LMS, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **kunnen LMS**.

    ![Hallo LMS kunnen koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Hallo kunnen LMS-tegel in Hallo paneel voor Apptoegang, klikt u op krijgt u automatisch aangemelde tooyour kunnen LMS toepassing. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

