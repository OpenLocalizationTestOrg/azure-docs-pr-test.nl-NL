---
title: 'Zelfstudie: Azure Active Directory-integratie met Slack | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en de toegestane vertraging.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>Zelfstudie: Azure Active Directory-integratie met Slack

In deze zelfstudie leert u hoe toointegrate vertraging bij Azure Active Directory (Azure AD).

Vertraging integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSlack toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSlack (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Slack tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een toegestane eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van vertraging van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-slack-from-hello-gallery"></a>Het toevoegen van vertraging van Hallo-galerie
Hallo-integratie tooconfigure vertraging met Azure AD, moet u tooadd Slack uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Slack via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Slack**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. Selecteer in het deelvenster resultaten hello, **Slack**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Slack op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Slack is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Slack toobe tot stand gebracht.

In Slack, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Slack, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een toegestane testgebruiker](#creating-a-slack-test-user)**  -toohave een equivalent van Britta Simon in Slack die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing toegestane configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met vertraging Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Slack** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. Op Hallo **Slack-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.slack.com`

    b. In Hallo **id** textbox type Hallo URL:`https://slack.com`

    > [!NOTE] 
    > Hallo-waarde is geen echte. U hebt tooupdate de waarde Hallo met Hallo werkelijke aanmelding op URL. Neem contact op met [toegestane ondersteuningsteam](https://slack.com/help/contact) tooget Hallo waarde
     
4. Toegestane toepassing verwacht Hallo SAML asserties in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **user.mail** als **gebruikers-id** en voor elke rij die wordt weergegeven Voer in Hallo onderstaande tabel Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | Voornaam | User.givenName |
    | Achternaam | User.surname |
    | User.Email | User.mail |  
    | User.Username | User.userPrincipalName |

    a. Klik op **kenmerk** tooopen **kenmerk bewerken** dialoogvenster vak en Hallo stappen uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    a. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    b. Van Hallo **waarde** wilt weergeven, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    c. Klik op **OK**

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. Op Hallo **Slack configuratie** sectie, klikt u op **Slack configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  In een ander browservenster, meld u aan tooyour toegestane bedrijf site als een beheerder.

10.  Navigeer te**Microsoft Azure AD** gaat u verder te**instellingen Team**.

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  In Hallo **instellingen Team** sectie, klikt u op Hallo **verificatie** tabblad en klik vervolgens op **Wijzigingsinstellingen**.

     ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. Op Hallo **SAML-verificatie-instellingen** dialoogvenster Hallo volgende stappen uit te voeren:

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    a.  In Hallo **SAML 2.0-eindpunt (HTTP)** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    b.  In Hallo **identiteit Provider verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.

    c.  Open uw gedownloade certificaat-bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **openbaar certificaat** textbox.

    d. Hallo bovenstaande drie instellingen geschikt is voor uw team toegestane configureren. Vinden voor meer informatie over instellingen voor Hallo Hallo **vertraging van SSO configuratiehandleiding** hier. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    e.  Klik op **configuratie op te slaan**.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-slack-test-user"></a>Een toegestane testgebruiker maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Slack van een gebruiker. Vertraging ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess Slack gemaakt als deze nog niet bestaat.

> [!NOTE]
> Als u een gebruiker toocreate handmatig nodig hebt, moet u tooContact [toegestane ondersteuningsteam](https://slack.com/help/contact).

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSlack toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSlack, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Slack**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u klikt op Hallo toegestane tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour toegestane toepassingen.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

