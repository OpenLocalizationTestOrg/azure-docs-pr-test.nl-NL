---
title: 'Zelfstudie: Azure Active Directory-integratie met TimeOffManager | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TimeOffManager.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Zelfstudie: Azure Active Directory-integratie met TimeOffManager

In deze zelfstudie leert u hoe toointegrate TimeOffManager met Azure Active Directory (Azure AD).

TimeOffManager integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTimeOffManager toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTimeOffManager (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met TimeOffManager tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een TimeOffManager eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. TimeOffManager van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-timeoffmanager-from-hello-gallery"></a>TimeOffManager van Hallo galerie toevoegen
tooconfigure hello integratie van TimeOffManager in Azure AD, moet u tooadd TimeOffManager uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd TimeOffManager via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **TimeOffManager**, selecteer **TimeOffManager** van resultaat deelvenster en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Uit de galerie toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met TimeOffManager op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TimeOffManager is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TimeOffManager toobe tot stand gebracht.

Wijs in TimeOffManager, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met TimeOffManager, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave een equivalent van Britta Simon in TimeOffManager die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TimeOffManager configureren.

**Azure AD tooconfigure eenmalige aanmelding met TimeOffManager, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **TimeOffManager** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. Op Hallo **TimeOffManager domein en de URL's** sectie, voert u de volgende Hallo:

     ![Sectie TimeOffManager domein en URL 's](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde met de werkelijke antwoord-URL Hallo bijwerken. U krijgt deze waarde van **voor eenmalige aanmelding instellingenpagina** die wordt uitgelegd later in de zelfstudie Hallo of neem contact op met [TimeOffManager ondersteuningsteam](http://www.timeoffmanager.com/contact-us.aspx).
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooTimeOffManger aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.
    
    Uw toepassing TimeOffManger verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

    ![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml-token kenmerken")
    
    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | Voornaam |User.givenName |
    | Achternaam |User.surname |
    | E-mail |User.mail |
    
    a.  Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.
    
    ![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml-token kenmerken")
    
    ![SAML-token kenmerken](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml-token kenmerken")
    
    b.  In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c.  In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d.  Klik op **OK**.
    
6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. Op Hallo **TimeOffManager configuratie** sectie, klikt u op **configureren TimeOffManager** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Configuratiesectie TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. In een ander browservenster, meld u bij uw bedrijf TimeOffManager site als beheerder.

9. Ga te**Account \> accountopties \> instellingen voor eenmalige aanmelding**.
   
   ![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "eenmalige aanmelding-instellingen")
7. In Hallo **instellingen voor eenmalige aanmelding** sectie, voert u Hallo stappen te volgen:
   
   ![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "eenmalige aanmelding-instellingen")
   
   a. De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak Hallo gehele certificaat in **X.509-certificaat** textbox.
   
   b. In **Idp verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
   
   c. In **IdP eindpunt-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
   d. Als **afdwingen SAML**, selecteer **Nee**.
   
   e. Als **gebruikers automatisch maken**, selecteer **Ja**.
   
   f. In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
   
   g. Klik op **wijzigingen opslaan**.

11. In **voor eenmalige aanmelding instellingen** pagina kopiëren Hallo-waarde van **Assertion Consumer Service-URL** en plak deze in Hallo **antwoord-URL** in het tekstvak onder **TimeOffManager Domein- en URL's** sectie in Azure-portal. 

      ![Eenmalige aanmelding instellingen](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "eenmalige aanmelding-instellingen")

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Gebruikers en groepen--> alle gebruikers](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Knop toevoegen](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Een testgebruiker TimeOffManager maken

In de volgorde tooenable Azure AD gebruikers toolog in TimeOffManager, moeten ze ingerichte tooTimeOffManager zijn.  

TimeOffManager ondersteunt alleen in de tijd van gebruikersinrichting. Er is geen actie-item voor u.  

Hallo gebruikers worden automatisch toegevoegd tijdens de eerste aanmelding Hallo met eenmalige aanmelding op.

>[!NOTE]
>U kunt andere TimeOffManager gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TimeOffManager tooprovision Azure AD-gebruikersaccounts.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTimeOffManager toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTimeOffManager, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **TimeOffManager**.

    ![TimeOffManager in lijst met Apps](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo TimeOffManager tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TimeOffManager toepassing. Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

