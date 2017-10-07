---
title: 'Zelfstudie: Azure Active Directory-integratie met Syncplicity | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Syncplicity.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Zelfstudie: Azure Active Directory-integratie met Syncplicity

In deze zelfstudie leert u hoe toointegrate Syncplicity met Azure Active Directory (Azure AD).

Syncplicity integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSyncplicity toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSyncplicity (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Syncplicity tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Syncplicity eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Syncplicity van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-syncplicity-from-hello-gallery"></a>Het toevoegen van Syncplicity van Hallo-galerie
tooconfigure hello integratie van Syncplicity in Azure AD, moet u tooadd Syncplicity uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Syncplicity via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Syncplicity**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. Selecteer in het deelvenster resultaten hello, **Syncplicity**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Syncplicity op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Syncplicity is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Syncplicity toobe tot stand gebracht.

Wijs in Syncplicity, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Syncplicity, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Syncplicity](#creating-a-syncplicity-test-user)**  -toohave een equivalent van Britta Simon in Syncplicity die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Syncplicity configureren.

**Azure AD tooconfigure eenmalige aanmelding met Syncplicity, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Syncplicity** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. Op Hallo **Syncplicity domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.syncplicity.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Syncplicity Client ondersteuningsteam](https://www.syncplicity.com/contact-us) tooget deze waarden. 
 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. Op Hallo **Syncplicity configuratie** sectie, klikt u op **configureren Syncplicity** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. Meld u aan tooyour **Syncplicity** tenant.

8. Klik in het menu bovenaan Hallo Hallo **admin**, selecteer **instellingen**, en klik vervolgens op **aangepaste domeinen en eenmalige aanmelding**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. Op Hallo **eenmalige aanmelding (SSO)** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding \(eenmalige aanmelding\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. In Hallo **aangepaste domeinen** textbox Hallo-typenaam van uw domein.
  
    b. Selecteer **ingeschakeld** als **Single Sign-On Status**.

    c. In Hallo **entiteit-Id** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    d. In Hallo **aanmelden pagina-URL** textbox plakken Hallo **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    e. In Hallo **pagina-URL voor afmelden** textbox plakken Hallo **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

    f. In **Provider identiteitscertificaat**, klikt u op **bestand kiezen**, en vervolgens uploaden Hallo-certificaat dat u hebt gedownload van hello Azure-portal. 

    g. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-syncplicity-test-user"></a>Een testgebruiker Syncplicity maken
Voor AAD gebruikers toobe kunnen toosign in, moeten ze ingerichte tooSyncplicity toepassing zijn. Deze sectie beschrijft hoe toocreate AAD gebruikersaccounts in Syncplicity.

**een gebruiker account-tooSyncplicity tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Syncplicity** tenant (bijvoorbeeld: `https://company.Syncplicity.com`).

2. Klik op **admin** en selecteer **gebruikersaccounts**.

3. Klik op **toevoegen van een gebruiker**.
   
    ![Gebruikers beheren](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "gebruikers beheren")

4. Type Hallo **e adressen** van een AAD-account dat u wilt dat tooprovision, selecteer **gebruiker** als **rol**, en klik vervolgens op **volgende**.
   
    ![Accountgegevens](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "accountgegevens")
   
    >[!NOTE]
    >Hallo AAD accounthouder opgehaald van een e-mailbericht met inbegrip van een koppeling tooconfirm en Hallo account activeren. 
    > 

5. Selecteer een groep in uw bedrijf dat de nieuwe gebruiker moet lid van en klik vervolgens op **volgende**.
   
    ![Groepslidmaatschap](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "groepslidmaatschap")
   
    >[!NOTE]
    >Als er geen groepen die zijn vermeld zijn, klikt u op **volgende**. 
    > 

6. Selecteer Hallo mappen u wilt tooplace onder het beheer van Syncplicity op Hallo van de gebruiker, computer, en klik vervolgens op **volgende**.
   
    ![Syncplicity mappen](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity mappen")

>[!NOTE]
>U kunt andere Syncplicity gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Syncplicity tooprovision AAD-gebruikersaccounts. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSyncplicity toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSyncplicity, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Syncplicity**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Syncplicity tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Syncplicity toepassing.
## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

