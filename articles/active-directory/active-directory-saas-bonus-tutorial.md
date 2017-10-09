---
title: 'Zelfstudie: Azure Active Directory-integratie met Bonusly | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Zelfstudie: Azure Active Directory-integratie met Bonusly

In deze zelfstudie leert u hoe toointegrate Bonusly met Azure Active Directory (Azure AD).

Bonusly integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooBonusly toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooBonusly (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Bonusly tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Bonusly eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Bonusly van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-bonusly-from-hello-gallery"></a>Het toevoegen van Bonusly van Hallo-galerie
tooconfigure hello integratie van Bonusly in Azure AD, moet u tooadd Bonusly uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Bonusly via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Bonusly**, selecteer **Bonusly** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![In de lijst met resultaten Hallo bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met Bonusly op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Bonusly is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Bonusly toobe tot stand gebracht.

Wijs in Bonusly, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Bonusly, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een Bonusly testgebruiker](#create-a-bonusly-test-user)**  -toohave een equivalent van Britta Simon in Bonusly die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Bonusly configureren.

**Azure AD tooconfigure eenmalige aanmelding met Bonusly, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Bonusly** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. Op Hallo **Bonusly domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Bonusly domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke antwoord-URL. Neem contact op met [Bonusly ondersteuningsteam](https://Bonusly/contact) tooget Hallo waarde.
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van Hallo-certificaat.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. Op Hallo **Bonusly configuratie** sectie, klikt u op **Bonusly configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Bonusly configuratie](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. Aanmelden in een ander browservenster tooyour **Bonusly** tenant.

8. Klik in de werkbalk bovenaan Hallo Hallo op **instellingen**, en selecteer vervolgens **integraties en apps**.
   
    ![Bonusly sociale sectie](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. Onder **Single Sign-On**, selecteer **SAML**.

10. Op Hallo **SAML** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Bonusly Saml dialoogvenster pagina](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    a. In Hallo **doel-URL voor eenmalige aanmelding IdP** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
   
    b. In Hallo **IdP verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal. 

    c. In Hallo **IdP aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    d. Plak de **vingerafdruk** waarde gekopieerd vanuit Azure-portal naar Hallo **Cert vingerafdruk** textbox.
   
11. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-bonusly-test-user"></a>Een Bonusly testgebruiker maken

In de volgorde tooenable Azure AD gebruikers toolog in tooBonusly, moeten ze worden ingericht in Bonusly. In geval van Bonusly Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt een andere gebruiker Bonusly account hulpmiddelen voor het maken of API's die worden geleverd door Bonusly tooprovision AAD gebruikersaccounts.
>  

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Aanmelden tooyour Bonusly tenant in een browservenster.

2. Klik op **instellingen**.
 
    ![Instellingen](./media/active-directory-saas-bonus-tutorial/ic781041.png "instellingen")

3. Klik op Hallo **gebruikers en bonussen** tabblad.
   
    ![Gebruikers en bonussen](./media/active-directory-saas-bonus-tutorial/ic781042.png "gebruikers en bonussen")

4. Klik op **gebruikers beheren**.
   
    ![Gebruikers beheren](./media/active-directory-saas-bonus-tutorial/ic781043.png "gebruikers beheren")

5. Klik op **gebruiker toevoegen**.
   
    ![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781044.png "gebruiker toevoegen")

6. Op Hallo **gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Gebruiker toevoegen](./media/active-directory-saas-bonus-tutorial/ic781045.png "gebruiker toevoegen")  

    a. In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.

    b. In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.
 
    c. In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .

    d. Klik op **Opslaan**.
   
     >[!NOTE]
     >Hello Azure AD-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.
     >  

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBonusly toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooBonusly, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Bonusly**.

    ![Hallo Bonusly koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Wanneer u klikt op Hallo Bonusly tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Bonusly toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

