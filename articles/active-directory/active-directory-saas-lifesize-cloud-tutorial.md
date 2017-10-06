---
title: 'Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Lifesize Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>Zelfstudie: Azure Active Directory-integratie met Lifesize Cloud

In deze zelfstudie leert u hoe toointegrate Lifesize Cloud met Azure Active Directory (Azure AD).

Lifesize Cloud integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooLifesize Cloud heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooLifesize Cloud (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Lifesize Cloud tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Lifesize Cloud eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Lifesize Cloud van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-lifesize-cloud-from-hello-gallery"></a>Het toevoegen van Lifesize Cloud van Hallo-galerie
tooconfigure hello integratie van Lifesize Cloud met Azure AD, moet u tooadd Lifesize Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Lifesize Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Lifesize Cloud**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. Selecteer in het deelvenster resultaten hello, **Lifesize Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Lifesize Cloud op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Lifesize Cloud is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in de Lifesize Cloud hello toobe tot stand gebracht.

In de Lifesize Cloud, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Lifesize Cloud, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Lifesize Cloud](#creating-a-lifesize-cloud-test-user)**  -toohave een equivalent van Britta Simon in Lifesize Cloud die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Lifesize Cloud.

**Voer tooconfigure Azure AD eenmalige aanmelding met Lifesize Cloud, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Lifesize Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. Op Hallo **Lifesize Cloud-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.lifesizecloud.com/ls/?acs`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://login.lifesizecloud.com/<companyname>`

     
4. Controleer **weergeven geavanceerde instellingen voor URL**, Hallo stap uitvoeren:  
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    In Hallo **Relay-status** textbox, typ een URL met Hallo patroon volgen:`https://webapp.lifesizecloud.com/?ent=<identifier>`
   
   > [!NOTE] 
   >Houd er rekening mee dat deze niet Hallo echte waarden zijn. u hebt tooupdate deze waarden Hello werkelijke aanmeldings-URL, de Relay-status en -id. Neem contact op met [Lifesize Cloud Client ondersteuningsteam](https://www.lifesize.com/support) tooget aanmeldings-URL, en id-waarden en u kunt benutten Relay status SSO-configuratie die later in Hallo zelfstudie wordt uitgelegd.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. Op Hallo **Lifesize Cloudconfiguratie** sectie, klikt u op **Lifesize Cloud configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. tooget SSO is geconfigureerd voor uw toepassing, aanmelding bij Hallo Lifesize cloudtoepassing met beheerdersbevoegdheden.

8. Klik op de naam van uw in Hallo rechterbovenhoek en klik vervolgens op Hallo **geavanceerde instellingen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. In de geavanceerde instellingen Klik nu op Hallo Hallo **SSO configuratie** koppeling. Hallo SSO-configuratiepagina voor uw exemplaar wordt geopend.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. Nu configureren Hallo volgende waarden in de gebruikersinterface voor Hallo SSO-configuratie.    
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    a. In **identiteit Provider verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    b.  In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    c. De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** textbox.
  
    d. Toewijzingen voor Hallo voornaam tekstvak Voer Hallo-waarde als in Hallo SAML-kenmerk **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
    
    e. In de toewijzing van de Hallo SAML-kenmerk voor Hallo **achternaam** tekstvak Voer Hallo-waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
    
    f. In de toewijzing van de Hallo SAML-kenmerk voor Hallo **e** tekstvak Voer Hallo-waarde als **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**

11. toocheck hello configuratie kunt u Hallo op **Test** knop.
   
    >[!NOTE]
    >Voor het testen van geslaagde toocomplete Hallo-configuratiewizard moet in Azure AD en bieden ook toegang toousers of -groepen die Hallo test kunnen uitvoeren.

12. Hallo eenmalige aanmelding inschakelen door te controleren op Hallo **eenmalige aanmelding inschakelen** knop.

13. Klik nu op Hallo **Update** knop zodat alle Hallo-instellingen worden opgeslagen. Hierdoor wordt Hallo RelayState waarde gegenereerd. Kopiëren Hallo RelayState waarde, die wordt gegenereerd in het tekstvak hello, plak deze in Hallo **Relay status** textbox onder **Lifesize Cloud-domein en de URL's** sectie. 

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-lifesize-cloud-test-user"></a>Een testgebruiker Lifesize Cloud maken

In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in de Lifesize Cloud. Lifesize cloud biedt ondersteuning voor automatisch gebruikers inrichten. Na de geslaagde verificatie op Azure AD worden Hallo gebruiker automatisch ingericht in Hallo-toepassing. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLifesize Cloud.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLifesize Cloud, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Lifesize Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Lifesize Cloud-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van Lifesize Cloud-toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

