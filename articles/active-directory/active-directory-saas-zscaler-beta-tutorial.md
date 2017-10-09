---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler Beta | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zscaler Beta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 1471c2b51ca5684a11acd40f4e450521605bb786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a>Zelfstudie: Azure Active Directory-integratie met Zscaler Beta

In deze zelfstudie leert u hoe toointegrate Zscaler Beta met Azure Active Directory (Azure AD).

Zscaler Beta integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooZscaler Beta heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooZscaler Beta (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Zscaler Beta tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Zscaler Beta eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Zscaler Beta van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-zscaler-beta-from-hello-gallery"></a>Het toevoegen van Zscaler Beta van Hallo-galerie
tooconfigure hello integratie van Zscaler Beta in Azure AD, moet u tooadd Zscaler Beta uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Zscaler Beta via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Zscaler Beta**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

5. Selecteer in het deelvenster resultaten hello, **Zscaler Beta**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Zscaler Beta op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zscaler Beta is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo Zscaler bètaversie toobe tot stand gebracht.

In Zscaler Bèta, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Zscaler Bèta, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Proxy-instellingen configureren](#configuring-proxy-settings)**  -tooconfigure Hallo proxy-instellingen in Internet Explorer
3. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Maken van een testgebruiker Zscaler Beta](#creating-a-zscaler-beta-test-user)**  -toohave een equivalent van Britta Simon Zscaler bètaversie die gekoppelde toohello Azure AD-weergave van de gebruiker.
5. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
6. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Zscaler Beta.

**Voer tooconfigure Azure AD eenmalige aanmelding met Zscaler Bèta, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Zscaler Beta** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

3. Op Hallo **Zscaler Beta domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    Typ in het tekstvak URL gebruikersportal Hallo eenmalige aanmelding, Hallo-URL die door uw gebruikers toosign op tooyour Zscaler Beta-toepassing gebruikt.

    > [!NOTE] 
    > U hebt tooupdate deze waarde Hello werkelijke aanmeldings-URL. Neem contact op met [Zscaler bèta-Client-ondersteuningsteam](https://www.zscaler.com/company/contact) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_400.png)

6. Op Hallo **Zscaler Beta configuratie** sectie, klikt u op **configureren Zscaler Beta** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

7. In een ander browservenster aanmelden tooyour Zscaler Beta bedrijf site als beheerder.

8. Klik in het menu bovenaan Hallo Hallo **beheer**.
   
    ![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic800206.png "beheer")

9. Onder **beheerders beheren en rollen**, klikt u op **gebruikers beheren & verificatie**.   
            
    ![Gebruikers & verificatie beheren](./media/active-directory-saas-zscaler-beta-tutorial/ic800207.png "gebruikers & verificatie beheren")

10. In Hallo **verificatie-opties kiezen voor uw organisatie** sectie, voert u Hallo stappen te volgen:   
                
    ![Verificatie](./media/active-directory-saas-zscaler-beta-tutorial/ic800208.png "verificatie")
   
    a. Selecteer **verificatie met eenmalige aanmelding SAML**.

    b. Klik op **één SAML aanmelding Parameters configureren**.

11. Op Hallo **configureren SAML Single Sign-On Parameters** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **gedaan**

    ![Eenmalige aanmelding](./media/active-directory-saas-zscaler-beta-tutorial/ic800209.png "eenmalige aanmelding")
    
    a. Plakken Hallo **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **URL Hallo SAML Portal toowhich gebruikers worden verzonden voor verificatie** textbox.
    
    b. In Hallo **kenmerk met naam van de aanmelding** textbox type **NameID**.
    
    c. tooupload uw gedownloade certificaat, klik op **Zscaler pem**.
    
    d. Selecteer **SAML automatische inrichting inschakelen**.

12. Op Hallo **gebruikersverificatie configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic800210.png "beheer")
    
    a. Klik op **Opslaan**.

    b. Klik op **nu activeren**.

## <a name="configuring-proxy-settings"></a>Proxy-instellingen configureren
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>tooconfigure hello proxy-instellingen in Internet Explorer

1. Start **Internet Explorer**.

2. Selecteer **Internetopties** van Hallo **extra** menu voor open Hallo **Internetopties** dialoogvenster.   
    
     ![Internetopties](./media/active-directory-saas-zscaler-beta-tutorial/ic769492.png "Internetopties")

3. Klik op Hallo **verbindingen** tabblad.   
  
     ![Verbindingen](./media/active-directory-saas-zscaler-beta-tutorial/ic769493.png "verbindingen")

4. Klik op **LAN-instellingen** tooopen hello **LAN-instellingen** dialoogvenster.

5. Voer in Hallo sectie Proxy-server, Hallo stappen te volgen:   
   
    ![Proxyserver](./media/active-directory-saas-zscaler-beta-tutorial/ic769494.png "proxyserver")

    a. Selecteer **een proxyserver gebruiken voor uw LAN**.

    b. Typ in het tekstvak voor het adres van Hallo **gateway.zscalerbeta.net**.

    c. Typ in het tekstvak poort Hallo **80**.

    d. Selecteer **proxyserver niet gebruiken voor lokale adressen**.

    e. Klik op **OK** tooclose hello **Local Area Network (LAN)-instellingen** dialoogvenster.

6. Klik op **OK** tooclose hello **Internetopties** dialoogvenster.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zscaler-beta-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-zscaler-beta-test-user"></a>Maken van een testgebruiker Zscaler Beta

Azure AD tooenable gebruikers toolog in tooZscaler Bèta, moeten ze ingerichte tooZscaler Beta. In geval van Zscaler Beta Hallo is inrichting een handmatige taak.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:

1. Meld u bij tooyour **Zscaler Beta** tenant.

2. Klik op **beheer**.   
   
    ![Beheer](./media/active-directory-saas-zscaler-beta-tutorial/ic781035.png "beheer")

3. Klik op **Gebruikersbeheer**.   
        
     ![Voeg](./media/active-directory-saas-zscaler-beta-tutorial/ic781036.png "toevoegen")

4. In Hallo **gebruikers** tabblad **toevoegen**.
      
    ![Voeg](./media/active-directory-saas-zscaler-beta-tutorial/ic781037.png "toevoegen")

5. Voer in Hallo sectie gebruiker toevoegen, Hallo stappen te volgen:
        
    ![Gebruiker toevoegen](./media/active-directory-saas-zscaler-beta-tutorial/ic781038.png "gebruiker toevoegen")
   
    a. Type Hallo **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en Hallo **afdeling** van een geldig Azure AD-account die u wilt dat tooprovision.

    b. Klik op **Opslaan**.

> [!NOTE]
> U kunt andere Zscaler Beta gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Zscaler Beta tooprovision Azure AD-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooZscaler Beta.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooZscaler Bèta, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Zscaler Beta**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Zscaler Beta-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zscaler Beta-toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-beta-tutorial/tutorial_general_203.png

