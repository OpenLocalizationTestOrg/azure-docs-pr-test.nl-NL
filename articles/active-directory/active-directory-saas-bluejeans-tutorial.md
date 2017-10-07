---
title: 'Zelfstudie: Azure Active Directory-integratie met BlueJeans | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en BlueJeans.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dfc634fd-1b55-4ba8-94a8-b8288429b6a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: jeedes
ms.openlocfilehash: 67613303a9f854afbf4619418cc1607d329caf94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bluejeans"></a>Zelfstudie: Azure Active Directory-integratie met BlueJeans

In deze zelfstudie leert u hoe toointegrate BlueJeans met Azure Active Directory (Azure AD).

BlueJeans integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooBlueJeans toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooBlueJeans (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met BlueJeans tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een BlueJeans eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van BlueJeans van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-bluejeans-from-hello-gallery"></a>Het toevoegen van BlueJeans van Hallo-galerie
tooconfigure hello integratie van BlueJeans in Azure AD, moet u tooadd BlueJeans uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd BlueJeans via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **BlueJeans**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_search.png)

5. Selecteer in het deelvenster resultaten hello, **BlueJeans**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met BlueJeans op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in BlueJeans is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in BlueJeans toobe tot stand gebracht.

Wijs in BlueJeans, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met BlueJeans, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker BlueJeans](#creating-a-bluejeans-test-user)**  -toohave een equivalent van Britta Simon in BlueJeans die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing BlueJeans configureren.

**Azure AD tooconfigure eenmalige aanmelding met BlueJeans, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **BlueJeans** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_samlbase.png)

3. Op Hallo **BlueJeans domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.BlueJeans.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.BlueJeans.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [BlueJeans Client ondersteuningsteam](https://support.bluejeans.com/contact) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_general_400.png)

6. Op Hallo **BlueJeans configuratie** sectie, klikt u op **configureren BlueJeans** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, de URL van wijzigen wachtwoord en de SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_configure.png) 

7. Aanmelden in een ander browservenster tooyour **BlueJeans** bedrijf site als beheerder.

8. Ga te**ADMIN \> groepsinstellingen \> beveiliging**.
   
   ![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785868.png "Admin")

9. In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:
   
   ![SAML voor eenmalige aanmelding](./media/active-directory-saas-bluejeans-tutorial/IC785869.png "SAML voor eenmalige aanmelding")   
   
   a. Selecteer **SAML voor eenmalige aanmelding**.
  
   b. Selecteer **automatische inrichting inschakelen**.

10. Verplaatsen op Hello stappen te volgen:

    ![Pad van het certificaat](./media/active-directory-saas-bluejeans-tutorial/IC785870.png "pad van het certificaat")
    
    a. Klik op **bestand kiezen**, en vervolgens Hallo gedownload certificaat te uploaden.
   
    b. Plakken **SAML Single Sign-On Service-URL** in Hallo **aanmeldings-URL** textbox.
   
    c. Plakken **URL van wijzigen wachtwoord** in Hallo **URL voor wachtwoord wijzigen** textbox.
   
    d. Plakken **Sign-Out URL** in Hallo **afmelding URL** textbox.

11. Verplaatsen op Hello stappen te volgen:
    
    ![Wijzigingen opslaan](./media/active-directory-saas-bluejeans-tutorial/IC785874.png "wijzigingen opslaan")
    
    a. In Hallo **gebruikers-id** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    b. In Hallo **e** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
   
    c. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bluejeans-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-bluejeans-test-user"></a>Een testgebruiker BlueJeans maken

Azure AD tooenable gebruikers toolog in tooBlueJeans, ze in BlueJeans moeten worden ingericht.  

In geval van een BlueJeans is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u bij tooyour **BlueJeans** bedrijf site als beheerder.

2. Ga te**ADMIN \> gebruikers beheren \> gebruiker toevoegen**.
   
   ![Beheerder](./media/active-directory-saas-bluejeans-tutorial/IC785877.png "Admin")
   
   >[!IMPORTANT]
   >Hallo **gebruiker toevoegen** tabblad is alleen beschikbaar als in Hallo **tabblad Beveiliging**, **automatische inrichting inschakelen** is uitgeschakeld. 
   
3. In Hallo **gebruiker toevoegen** sectie, voert u Hallo stappen te volgen:

    ![Gebruiker toevoegen](./media/active-directory-saas-bluejeans-tutorial/IC785886.png "gebruiker toevoegen")
    
    a. Typ een **BlueJeans gebruikersnaam**, een **e-mailadres**, een **BlueJeans vergadering ID**, een **beheerder wachtwoordcode**, een **volledige naam** , Hallo **bedrijf** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.
    
    b. Klik op **gebruiker toevoegen**.

>[!NOTE]
>U kunt andere BlueJeans gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door BlueJeans tooprovision AAD-gebruikersaccounts. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBlueJeans toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooBlueJeans, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **BlueJeans**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bluejeans-tutorial/tutorial_bluejeans_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo BlueJeans-tegel in Hallo Toegangsvenster, krijgt u de aanmeldingspagina van BlueJeans toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bluejeans-tutorial/tutorial_general_203.png

