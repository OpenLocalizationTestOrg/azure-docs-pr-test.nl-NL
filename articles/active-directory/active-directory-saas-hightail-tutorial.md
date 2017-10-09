---
title: 'Zelfstudie: Azure Active Directory-integratie met Hightail | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Hightail.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Zelfstudie: Azure Active Directory-integratie met Hightail

In deze zelfstudie leert u hoe toointegrate Hightail met Azure Active Directory (Azure AD).

Hightail integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooHightail toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooHightail (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Hightail tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Hightail eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Hightail van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-hightail-from-hello-gallery"></a>Het toevoegen van Hightail van Hallo-galerie
tooconfigure hello integratie van Hightail in Azure AD, moet u tooadd Hightail uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Hightail via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Hightail**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. Selecteer in het deelvenster resultaten hello, **Hightail**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Hightail op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Hightail is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Hightail toobe tot stand gebracht.

Wijs in Hightail, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Hightail, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Hightail](#creating-a-hightail-test-user)**  -toohave een equivalent van Britta Simon in Hightail die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Hightail configureren.

**Azure AD tooconfigure eenmalige aanmelding met Hightail, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Hightail** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. Op Hallo **Hightail domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     In Hallo **antwoord-URL** textbox type Hallo URL als:`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Hallo voorgaande waarde is geen echte waarde. Hallo-waarde wordt bijgewerkt met Hallo werkelijke antwoord-URL, die verderop in Hallo zelfstudie wordt beschreven.
 
4. Op Hallo **Hightail domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL**.

    b. In Hallo **aanmelding op URL** textbox type Hallo URL als:`https://www.hightail.com/loginSSO`

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail toepassing hello SAML asserties verwacht in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Atrribute'** tabblad van de toepassing hello. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ------------------- | -------------------- |
    | Voornaam | User.givenName |
    | Achternaam | User.surname |
    | E-mail | User.mail |    
    | UserIdentity | User.mail |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.

    d. Hallo laat **Namespace** leeg.
    
    e. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. Op Hallo **Hightail configuratie** sectie, klikt u op **configureren Hightail** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Voordat u configureert Hallo eenmalige aanmelding op Hightail app, kunt witte lijst uw e-maildomein met Hightail team, zodat alle gebruikers met dit domein Hallo gebruik functionaliteit voor eenmalige aanmelding.


9. tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour Hightail tenant als beheerder.
   
    a. Klik op Hallo in het menu bovenaan Hallo Hallo **Account** tabblad en selecteer **SAML configureren**.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Schakel dit selectievakje in Hallo van **SAML-verificatie inschakelen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **handtekeningcertificaat van SAML-Token** textbox.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. In Hallo **SAML-instantie (id-Provider)** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Als u wilt dat tooconfigure Hallo toepassing in **IDP geïnitieerd modus** selecteren **'Identiteitsprovider (IdP) geïnitieerd aanmelden'**. Als **SP geïnitieerd modus** Selecteer **'Serviceprovider (SP) geïnitieerd aanmelden'**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Hallo SAML consumer-URL voor uw exemplaar Kopieer en plak deze in **antwoord-URL** textbox in **Hightail domein en de URL's** sectie op Azure-portal.
    
    g. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-hightail-test-user"></a>Een testgebruiker Hightail maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Hightail van een gebruiker. 

Er is geen actie-item voor u in deze sectie. Hightail ondersteunt just in time gebruikers inrichten op basis van Hallo aangepaste claims. Als u aangepaste claims Hallo hebt geconfigureerd, zoals wordt weergegeven in de sectie Hallo  **[eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on)**  , een gebruiker is gemaakt in Hallo toepassing nog niet bestaat. 

>[!NOTE]
>Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [Hightail ondersteuningsteam](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooHightail toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooHightail, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Hightail**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Hightail tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Hightail toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

