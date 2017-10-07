---
title: 'Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en xMatters OnDemand.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Zelfstudie: Azure Active Directory-integratie met xMatters OnDemand

In deze zelfstudie leert u hoe toointegrate xMatters OnDemand met Azure Active Directory (Azure AD).

XMatters OnDemand integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooxMatters OnDemand heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooxMatters OnDemand (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met xMatters OnDemand tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een xMatters eenmalige aanmelding OnDemand abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van xMatters OnDemand van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Het toevoegen van xMatters OnDemand van Hallo-galerie
tooconfigure hello integratie van xMatters OnDemand in Azure AD, moet u tooadd xMatters OnDemand uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd xMatters OnDemand via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **xMatters OnDemand**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. Selecteer in het deelvenster resultaten hello, **xMatters OnDemand**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met xMatters die OnDemand op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork Azure AD moet tooknow welke Hallo equivalent in xMatters OnDemand is tooa gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in xMatters moet OnDemand toobe tot stand gebracht.

In xMatters OnDemand, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met xMatters OnDemand, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een gebruiker xMatters OnDemand test](#creating-a-xmatters-ondemand-test-user)**  -toohave een equivalent van Britta Simon in xMatters OnDemand die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw xMatters OnDemand-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met xMatters OnDemand, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **xMatters OnDemand** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. Op Hallo **xMatters OnDemand domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [ondersteuningsteam voor OnDemand xMatters](https://www.xmatters.com/company/contact-us/) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het certificaatbestand van Hallo lokaal als **c:\\XMatters OnDemand.cer**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > U moet tooforward Hallo certificaat toohello [ondersteuningsteam voor OnDemand xMatters](https://www.xmatters.com/company/contact-us/). Hallo-certificaat moet toobe geüpload door Hallo xMatters ondersteuningsteam voordat u kunt één Hallo aanmelding configuratie voltooien. 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. Op Hallo **xMatters OnDemand configuratie** sectie, klikt u op **xMatters OnDemand configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. In een ander browservenster aanmelden tooyour XMatters OnDemand bedrijf site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **Admin**, en klik vervolgens op **bedrijfsgegevens** in de navigatiebalk Hallo op Hallo linkerkant.
   
    ![Beheerder](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")

9. Op Hallo **SAML-configuratie** pagina, voert u Hallo stappen te volgen:
   
    ![De SAML-configuratie](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML-configuratie")
   
    a. Selecteer **SAML inschakelen**.
   
    b. Plakken **SAML entiteit-ID**, die u hebt gekopieerd uit hello Azure-portal in Hallo **identiteit Provider-ID** textbox.
   
    c. Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **eenmalige aanmelding op URL** textbox.
   
    d. Plakken **Sign-Out URL**, die u hebt gekopieerd uit hello Azure-portal in Hallo **-URL met eenmalige afmelding** textbox.
   
    e. Klik op Hallo bedrijfsgegevens pagina boven Hallo op **wijzigingen opslaan**.
    
    ![Details voor de bedrijfsportal](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "details voor de bedrijfsportal")

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>Maken van een gebruiker xMatters OnDemand testen

In volgorde tooenable Azure AD gebruikers toolog in tooXMatters OnDemand, moeten ze worden ingericht in XMatters OnDemand. In geval van XMatters OnDemand Hallo is inrichting een handmatige taak.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:
1. Meld u bij tooyour **XMatters OnDemand** tenant.

2.  Klik op **gebruikers** tabblad en klik vervolgens op **gebruiker toevoegen**.
  
    ![Gebruikers](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "gebruikers")

3. In Hallo **toevoegen van een gebruiker** sectie, voert u Hallo stappen te volgen:
   
    ![Een gebruiker toevoegen](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "een gebruiker toevoegen")

    a. Selecteer **Active**.

    b. In Hallo **gebruikers-ID** textbox type Hallo id van gebruiker zoals Brittasimon@contoso.com.
   
    c. In Hallo **voornaam** textbox type voornaam van de gebruiker Hallo zoals Britta.

    d. In Hallo **achternaam** textbox achternaam van de gebruiker Hallo zoals Simon type.
    
    e. In Hallo **Site** textbox Enter Hallo geldige site van een geldig Azure AD-account die u wilt dat tooprovision.
    
    f. Klik op **Opslaan**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooxMatters OnDemand.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooxMatters OnDemand, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **xMatters OnDemand**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo xMatters OnDemand-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour xMatters OnDemand-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

