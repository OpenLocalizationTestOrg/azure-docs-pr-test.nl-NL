---
title: 'Zelfstudie: Azure Active Directory-integratie met OfficeSpace Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en OfficeSpace Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a>Zelfstudie: Azure Active Directory-integratie met OfficeSpace Software

In deze zelfstudie leert u hoe toointegrate OfficeSpace Software met Azure Active Directory (Azure AD).

OfficeSpace Software integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooOfficeSpace Software heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooOfficeSpace Software (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met OfficeSpace Software tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een OfficeSpace Software eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van OfficeSpace Software van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-officespace-software-from-hello-gallery"></a>Het toevoegen van OfficeSpace Software van Hallo-galerie
tooconfigure hello integratie van OfficeSpace Software in Azure AD, moet u tooadd OfficeSpace Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd OfficeSpace Software uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **OfficeSpace Software**, selecteer **OfficeSpace Software** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Lijst met zoekresultaten OfficeSpace Software in Hallo](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met OfficeSpace Software op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in OfficeSpace Software is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in OfficeSpace Software toobe tot stand gebracht.

In OfficeSpace Software, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met OfficeSpace Software, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave een equivalent van Britta Simon in OfficeSpace-Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing OfficeSpace Software.

**Voer tooconfigure Azure AD eenmalige aanmelding met OfficeSpace Software Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **OfficeSpace Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. Op Hallo **OfficeSpace Software domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en OfficeSpace Software domein eenmalige aanmelding informatie](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.officespacesoftware.com/users/sign_in/saml`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`<company name>.officespacesoftware.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [OfficeSpace Software Client ondersteuningsteam](mailto:support@officespacesoftware.com) tooget deze waarden. 

4. Hallo SAML asserties verwacht OfficeSpace softwaretoepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Kenmerk configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **user.mail** als **gebruikers-id** en voor elke rij die wordt weergegeven Voer in Hallo onderstaande tabel Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |    
    | E-mail | User.mail |
    | naam | User.DisplayName |
    | Voornaam | User.givenName |
    | Achternaam | User.surname |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Configureer toevoegen ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Kenmerk configureren](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**
 
6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het Hallo-certificaat.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. Op Hallo **OfficeSpace softwareconfiguratie** sectie, klikt u op **OfficeSpace Software configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![De softwareconfiguratie voor OfficeSpace](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. Meld u aan bij uw tenant OfficeSpace Software als een beheerder in een ander browservenster.

10. Ga te**instellingen** en klik op **Connectors**.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. Klik op **SAML-verificatie**.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. In Hallo **SAML-verificatie** sectie, voert u Hallo stappen te volgen:

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    a. In Hallo **afmelding provider url** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

    b. In Hallo **Client idp doel-url** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    c. Plakken Hallo **vingerafdruk** waarde die u hebt gekopieerd vanuit Azure-portal in Hallo **Client IDP certificaat vingerafdruk** textbox. 

    d. Klik op **instellingen opslaan**.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-officespace-software-test-user"></a>Een testgebruiker OfficeSpace Software maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in OfficeSpace Software van een gebruiker. OfficeSpace Software ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess OfficeSpace Software gemaakt als deze nog niet bestaat.

> [!NOTE]
> Als u een gebruiker toocreate handmatig nodig hebt, moet u tooContact [OfficeSpace Software ondersteuningsteam](mailto:support@officespacesoftware.com).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooOfficeSpace Software.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooOfficeSpace Software, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **OfficeSpace Software**.

    ![Hallo OfficeSpace Software koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo OfficeSpace Software-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour OfficeSpace softwaretoepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

