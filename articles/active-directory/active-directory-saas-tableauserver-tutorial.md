---
title: 'Zelfstudie: Azure Active Directory-integratie met Tableau Server | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Tableau-Server.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Zelfstudie: Azure Active Directory-integratie met Tableau Server

In deze zelfstudie leert u hoe toointegrate Tableau Server met Azure Active Directory (Azure AD).

Tableau Server integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooTableau Server heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTableau Server (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Tableau Server tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Server Tableau eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Tableau Server uit de galerie Hallo toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-tableau-server-from-hello-gallery"></a>Tableau Server uit de galerie Hallo toevoegen
tooconfigure hello integratie van Tableau Server in Azure AD, moet u tooadd Tableau Server uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Tableau Server uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Tableau Server**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. Selecteer in het deelvenster resultaten hello, **Tableau Server**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tableau-Server op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tableau Server is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Tableau Server toobe tot stand gebracht.

In het vak Tableau Server Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Tableau Server, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Tableau Server](#creating-a-tableau-server-test-user)**  -toohave een equivalent van Britta Simon in Tableau-Server die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Tableau Server configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met de Server Tableau, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Tableau Server** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. Op Hallo **Tableau-serverdomein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link`
    
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Hallo voorgaande waarden zijn niet echte waarden. Later kunt bijwerken u Hallo waarden met de Hallo werkelijke URL en de id van de configuratiepagina voor Hallo Tableau Server. 

4. Hallo SAML asserties verwacht tableau servertoepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerken'** sectie op de pagina van de toepassing-integratie. Hallo volgende schermafbeelding ziet u een voorbeeld van Hallo dezelfde.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ---------------| --------------- |    
    | gebruikersnaam | *User.DisplayName* |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**


6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget SSO is geconfigureerd voor uw toepassing, moet u toosign op tooyour Tableau Server tenant als beheerder.
   
   a. In het Tableau serverconfiguratie hello, klikt u op Hallo **SAML** tabblad.
  
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Schakel dit selectievakje in Hallo van **gebruik SAML voor eenmalige aanmelding**.
   
   c. Tableau Server retour-URL-URL die Tableau Server-gebruikers toegang, zoals http://tableau_server tot krijgen Hallo. Gebruik http://localhost wordt niet aanbevolen. Via een URL met een slash (bijvoorbeeld http://tableau_server/) wordt niet ondersteund. Kopiëren **Tableau Server retour-URL** en plak deze tooAzure AD **aanmelding op URL** textbox in **Tableau-serverdomein en URL's** sectie.
   
   d. Entiteit-ID van SAML-Hallo entiteit-ID is uniek voor uw Server Tableau installatie toohello IdP. Hier geeft u de URL van de Server Tableau opnieuw, indien gewenst, maar er geen toobe uw Tableau Server-URL. Kopiëren **SAML entiteit-ID** en plak deze tooAzure AD **id** textbox in **Tableau-serverdomein en URL's** sectie.
     
   e. Klik op Hallo **metagegevensbestand exporteren** en open het in Hallo text editor-toepassing. Zoek Assertion Consumer Service-URL met Http Post en 0-Index en kopiëren Hallo-URL. Plak nu tooAzure AD **antwoord-URL** textbox in **Tableau-serverdomein en URL's** sectie.
   
   f. Zoek uw Federatiemetagegevens bestand gedownload van Azure-portal en uploadt u dit in Hallo **SAML Idp metagegevensbestand**.
   
   g. Klik op Hallo **OK** knop in Hallo Tableau configuratiepagina op de Server.
   
    >[!NOTE] 
    >Klant hebben tooupload alle certificaten in Hallo Tableau Server SAML SSO-configuratie en het in Hallo SSO stroom ophalen genegeerd.
    >Als u moet helpen SAML configureren op de Server Tableau Raadpleeg toothis artikel [SAML configureren](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-tableau-server-test-user"></a>Een testgebruiker Tableau Server maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Tableau Server van een gebruiker. U moet alle Hallo gebruikers in Hallo Tableau server tooprovision. 

Deze gebruikersnaam van de gebruiker Hallo moet overeenkomen met de Hallo-waarde die u hebt geconfigureerd in het aangepaste kenmerk hello Azure AD van **gebruikersnaam**. Met de juiste toewijzing Hallo integratie moet werken Hallo [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello Tableau Server-beheerder in uw organisatie.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTableau Server.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTableau Server, voert u Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Tableau Server**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Tableau Server tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Tableau servertoepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

