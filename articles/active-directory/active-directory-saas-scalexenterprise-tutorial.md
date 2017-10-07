---
title: 'Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ScaleX Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Zelfstudie: Azure Active Directory-integratie met ScaleX Enterprise

In deze zelfstudie leert u hoe toointegrate ScaleX Enterprise met Azure Active Directory (Azure AD).

ScaleX-onderneming integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooScaleX Enterprise heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooScaleX Enterprise (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie. Wat is er toegang tot toepassingen en eenmalige aanmelding met [Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met ScaleX voor ondernemingen, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ScaleX Enterprise eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ScaleX Enterprise van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Het toevoegen van ScaleX Enterprise van Hallo-galerie
tooconfigure hello integratie van ScaleX onderneming in tooAzure AD, moet u tooadd ScaleX Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ScaleX Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **ScaleX Enterprise**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. Selecteer in het deelvenster resultaten hello, **ScaleX Enterprise**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met ScaleX Enterprise op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de onderneming ScaleX is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de onderneming ScaleX Hallo toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in ScaleX onderneming.

tooconfigure en test eenmalige aanmelding Azure AD met ScaleX voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave een equivalent van Britta Simon in ScaleX onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing ScaleX Enterprise.

**Voer tooconfigure Azure AD eenmalige aanmelding met ScaleX Enterprise, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ScaleX Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. Op Hallo **ScaleX Enterprise domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    a. In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Deze zijn niet Hallo echte waarden. Werk deze waarden met Hallo werkelijke id, de antwoord-URL of de aanmeldings-URL. Neem contact op met [ScaleX Enterprise Client ondersteuningsteam](http://info.rescale.com/contact_sales) tooget deze waarden. 

5. Uw toepassing ScaleX verwacht Hallo SAML asserties in een specifieke indeling waarvoor u toomodify aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Klik op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje tooopen Hallo aangepaste kenmerken instellingen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    a. Klik met de rechtermuisknop op Hallo kenmerk **naam** en klik op verwijderen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Klik op **emailaddress** venster kenmerk tooopen Hallo-kenmerk bewerken. Wijzig de waarde van **user.mail** te**user.userprincipalname** en klik op Ok.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. Op Hallo **ScaleX Ondernemingsconfiguratie** sectie, klikt u op **configureren ScaleX Enterprise** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure eenmalige aanmelding op **ScaleX Enterprise** side, aanmelding toohello ScaleX Enterprise bedrijfswebsite als beheerder.

9. Klik rechts op Hallo in Hallo bovenste menu en selecteer **Contoso beheer**.

    > [!NOTE] 
    > Contoso is slechts een voorbeeld. Dit moet de werkelijke naam van uw bedrijf. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Selecteer **integraties** van Hallo bovenste menu en selecteer **Single Sign-On**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Voer Hallo formulier als volgt:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    a. Selecteer **'Alle gebruikers die kan worden geverifieerd met eenmalige aanmelding maken'.**

    b. **Service Provider saml**: de waarde van de Hallo plakken ***urn: oasis: namen: tc: SAML:2.0:nameid-indeling: permanente***

    c. **Naam van identiteitsprovider e veld in de ACS-antwoord**: de waarde van de Hallo plakken`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **Identiteit EntityDescriptor entiteit-ID van Provider:** plakken Hallo **SAML entiteit-ID** waarde gekopieerd uit hello Azure-portal.

    e. **ID-Provider SingleSignOnService URL:** plakken Hallo **SAML Single Sign-On Service-URL** van hello Azure-portal.

    f. **Provider openbare X509 identiteitscertificaat:** Open Hallo X509 certificaat gedownload van hello Azure in Kladblok en plak Hallo-inhoud in dit vak. Zorg ervoor dat er dat geen regeleinden in Hallo middelste Hallo certificaat inhoud.
    
    g. Hallo selectievakjes volgende controleren: **ingeschakeld, NameID versleutelen en aanmelding AuthnRequests.**

    h. Klik op **SSO-Update-instellingen** toosave Hallo instellingen.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Maken van een testgebruiker ScaleX Enterprise

Azure AD tooenable gebruikers toolog in tooScaleX Enterprise, moeten ze worden ingericht in tooScaleX Enterprise. In geval van ScaleX onderneming Hallo inrichting is een automatische taak en er zijn geen handmatige stappen vereist. Elke gebruiker die kan worden geverifieerd met eenmalige aanmelding referenties worden automatisch ingericht op Hallo ScaleX aan clientzijde.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door de gebruiker toegang tooScaleX Enterprise verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooScaleX Enterprise, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ScaleX Enterprise**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Klik op Hallo ScaleX Enterprise-tegel in Hallo paneel voor Apptoegang, wordt u automatisch aangemelde tooyour ScaleX bedrijfstoepassing. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

