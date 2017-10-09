---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP Cloud voor de klant.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Zelfstudie: Azure Active Directory-integratie met SAP Cloud voor klant

In deze zelfstudie leert u hoe toointegrate SAP Cloud voor klanten met Azure Active Directory (Azure AD).

Integratie van SAP Cloud voor klanten met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooSAP Cloud voor de klant heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSAP Cloud inschakelen voor de klant (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SAP Cloud voor klant tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Cloud SAP voor eenmalige aanmelding klant abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. SAP Cloud toe te voegen voor de klant uit Hallo galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>SAP Cloud toe te voegen voor de klant uit Hallo galerie
tooconfigure hello integratie van SAP Cloud voor klanten met Azure AD, moet u tooadd SAP-Cloud van Hallo galerie tooyour lijst met beheerde SaaS-apps voor de klant.

**tooadd SAP Cloud voor klant via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SAP Cloud voor klant**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. Selecteer in het deelvenster resultaten hello, **SAP Cloud voor klant**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAP Cloud voor klant op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Cloud SAP voor de klant is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Cloud voor klant SAP Hallo toobe tot stand gebracht.

In de Cloud SAP voor de klant, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met SAP Cloud voor de klant, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Cloud SAP voor klant testgebruiker](#creating-a-sap-cloud-for-customer-test-user)**  -toohave een equivalent van Britta Simon in SAP Cloud voor de klant die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Cloud SAP voor toepassing van de klant.

**tooconfigure eenmalige aanmelding Azure AD met SAP Cloud voor klant, voert u Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **SAP Cloud voor klant** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. Op Hallo **SAP Cloud voor domein van de klant en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server name>.crm.ondemand.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [SAP Cloud voor klant Client ondersteuningsteam](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget deze waarden. 

4. Op Hallo **gebruikerskenmerken** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    a. In **gebruikers-id** lijst, selecteer Hallo **ExtractMailPrefix()** functie.

    b. Van Hallo **Mail** lijst, selecteer Hallo gebruikerskenmerk gewenste toouse voor uw implementatie.
    Bijvoorbeeld, als u wilt dat toouse Hallo werknemer-id als unieke gebruikers-id en u Hallo-kenmerkwaarde in Hallo ExtensionAttribute2 hebt opgeslagen, selecteert u user.extensionattribute2.  

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. Op Hallo **SAP Cloud voor de configuratie van de klant** sectie, klikt u op **SAP Cloud configureren voor de klant** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO is geconfigureerd, voert u Hallo stappen te volgen:
   
    a. De aanmelding in de Cloud SAP voor Customer portal met beheerdersrechten.
   
    b. Navigeer toohello **toepassings- en algemene beheertaak gebruiker** en klik op Hallo **identiteitsprovider** tabblad.
   
    c. Klik op **nieuwe identiteitsprovider** en selecteer Hallo metagegevens XML-bestand die u hebt gedownload van hello Azure-portal. Door het importeren van metagegevens Hallo uploadt Hallo systeem automatisch Hallo vereist handtekeningcertificaat en -versleutelingscertificaat.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory vereist Hallo element Assertion Consumer Service-URL in Hallo SAML-aanvraag, dus selecteer Hallo **Assertion Consumer Service-URL opnemen** selectievakje.
   
    e. Klik op **activeren Single Sign-On**.
   
    f. Sla uw wijzigingen op.
   
    g. Klik op Hallo **mijn systeem** tabblad.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. In **Azure AD aanmelding URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    ik. Opgeven of Hallo werknemer handmatig kiezen kunt tussen het aanmelden met gebruikersnaam en wachtwoord of eenmalige aanmelding door het selecteren van Hallo **handmatige identiteit Provider selectie**.
   
    j. In Hallo **URL SSO** sectie Hallo URL opgeven die moet worden gebruikt door uw werknemers toosign op toohello systeem. 
    In Hallo **tooEmployee URL verzonden** lijst, kunt u kiezen tussen Hallo volgende opties:
   
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

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Maken van een Cloud SAP voor klant testgebruiker

In deze sectie maakt u Britta Simon aangeroepen in SAP Cloud voor klant van een gebruiker. Neem contact op met [SAP Cloud voor afdeling Klantenondersteuning](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd Hallo gebruikers in Hallo SAP Cloud voor klant-platform. 

> [!NOTE]
> Zorg dat NameID waarde met de Hallo gebruikersnaam veld in Hallo SAP Cloud voor klant-platform overeenkomen moet.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP Cloud voor de klant.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSAP Cloud voor de klant, voert u Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SAP Cloud voor klant**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo SAP Cloud voor klant-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour SAP Cloud voor de toepassing van de klant.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

