---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Business ByDesign.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Zelfstudie: Azure Active Directory-integratie met SAP Business ByDesign

In deze zelfstudie leert u hoe toointegrate SAP Business ByDesign met Azure Active Directory (Azure AD).

SAP Business ByDesign integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooSAP Business ByDesign heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooSAP Business ByDesign (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SAP Business ByDesign tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SAP Business ByDesign eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SAP Business ByDesign van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Het toevoegen van SAP Business ByDesign van Hallo-galerie
tooconfigure hello integratie van SAP Business ByDesign in Azure AD, moet u tooadd SAP Business ByDesign uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SAP Business ByDesign via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **SAP Business ByDesign**, selecteer **SAP Business ByDesign** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![SAP Business ByDesign in de lijst met resultaten Hallo](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met SAP Business ByDesign op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SAP Business ByDesign is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in een SAP Business ByDesign Hallo toobe tot stand gebracht.

In een SAP Business ByDesign, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met SAP Business ByDesign, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SAP Business ByDesign testgebruiker](#create-an-sap-business-bydesign-test-user)**  -toohave een equivalent van Britta Simon in SAP Business ByDesign die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SAP Business ByDesign configureren.

**tooconfigure eenmalige aanmelding Azure AD met SAP Business ByDesign, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **SAP Business ByDesign** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. Op Hallo **SAP Business ByDesign domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en SAP Business ByDesign domein eenmalige aanmelding informatie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.sapbydesign.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) tooget deze waarden.

4. Op Hallo **gebruikerskenmerken** sectie, voert u Hallo stappen te volgen:

    ![SAP Business ByDesign kenmerk sectie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    a. In **gebruikers-id** lijst, selecteer Hallo **ExtractMailPrefix()** functie.
    
    b. Van Hallo **Mail** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie. Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.   

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. Op Hallo **SAP Business ByDesign configuratie** sectie, klikt u op **configureren SAP Business ByDesign** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![SAP Business ByDesign-configuratie](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget SSO is geconfigureerd voor uw toepassing hello stappen uitvoeren:
   
    a. Meld u aan op tooyour SAP Business ByDesign portal met beheerdersrechten.
   
    b. Navigeer te**toepassings- en algemene beheertaak gebruiker** en klik op Hallo **identiteitsprovider** tabblad.
   
    c. Klik op **nieuwe identiteitsprovider** en selecteer Hallo metagegevens XML-bestand dat u hebt gedownload van hello Azure-portal. Door het importeren van metagegevens Hallo uploadt Hallo systeem automatisch Hallo vereist handtekeningcertificaat en -versleutelingscertificaat.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. Hallo tooinclude **Assertion Consumer Service-URL** in Hallo SAML-aanvraag, selecteer **Assertion Consumer Service-URL opnemen**.
   
    e. Klik op **activeren Single Sign-On**.
   
    f. Sla uw wijzigingen op.
   
    g. Klik op Hallo **mijn systeem** tabblad.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal het in Hallo **Azure AD aanmelding URL** textbox.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    ik. Opgeven of de werknemer Hallo handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door te selecteren **handmatige identiteit Provider selectie**.
   
    j. In Hallo **URL SSO** sectie Hallo URL opgeven die moet worden gebruikt door Hallo werknemer toologon toohello systeem. 
    In Hallo URL verzonden tooEmployee vervolgkeuzelijst wordt weergegeven, kunt u kiezen tussen Hallo volgende opties:
   
    **Niet-SSO-URL**
   
    Hallo system verzendt alleen Hallo normale system URL toohello werknemer. Hallo werknemer kan niet aanmelden met eenmalige aanmelding, en moet gebruik wachtwoord of certificaat in plaats daarvan.
   
    **URL VOOR EENMALIGE AANMELDING** 
   
    Hallo system verzendt alleen Hallo URL SSO toohello werknemer. Hallo werknemers kan zich aanmelden met behulp van eenmalige aanmelding. Authenticatie-aanvraag wordt omgeleid via Hallo IdP.
   
    **Automatische selectie**
   
    Als eenmalige aanmelding niet actief is, verzendt het afdruksysteem van Hallo Hallo normale system URL toohello werknemer. Als eenmalige aanmelding actief is, controleert Hallo system of Hallo werknemer een wachtwoord heeft. Als een wachtwoord beschikbaar is, worden zowel de URL van de SSO- en Non-SSO-toohello werknemer verzonden. Als Hallo werknemer geen wachtwoord heeft, is alleen Hallo URL SSO echter toohello werknemer verzonden.
   
    k. Sla uw wijzigingen op.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Een SAP Business ByDesign testgebruiker maken

In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in een SAP Business ByDesign. Neem contact op met [SAP Business ByDesign Client ondersteuningsteam](https://www.sap.com/products/cloud-analytics.support.html) tooadd Hallo gebruikers in Hallo SAP Business ByDesign platform. 

> [!NOTE]
> Zorg dat NameID waarde met de Hallo gebruikersnaam veld in Hallo SAP Business ByDesign platform overeenkomen moet.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP Business ByDesign.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooSAP Business ByDesign, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SAP Business ByDesign**.

    ![Hallo SAP Business ByDesign koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo SAP Business ByDesign tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAP Business ByDesign toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

