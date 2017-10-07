---
title: 'Zelfstudie: Azure Active Directory-integratie met Veracode | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Veracode.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Zelfstudie: Azure Active Directory-integratie met Veracode

In deze zelfstudie leert u hoe toointegrate Veracode met Azure Active Directory (Azure AD).

Veracode integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooVeracode toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooVeracode (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Veracode tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Veracode eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Veracode van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-veracode-from-hello-gallery"></a>Veracode van Hallo galerie toevoegen
tooconfigure hello integratie van Veracode in Azure AD, moet u tooadd Veracode uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Veracode via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Veracode**, selecteer **Veracode** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Veracode in de lijst met resultaten Hallo](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Veracode op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Veracode is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Veracode toobe tot stand gebracht.

Wijs in Veracode, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Veracode, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Veracode](#create-a-veracode-test-user)**  -toohave een equivalent van Britta Simon in Veracode die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Veracode configureren.

**Azure AD tooconfigure eenmalige aanmelding met Veracode, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Veracode** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. Op Hallo **Veracode domein en de URL's** sectie van de gebruiker heeft geen tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. Hallo-doel van deze sectie is toooutline hoe tooenable gebruikers tooauthenticate tooVeracode aan hun account in Azure AD dat gebruikmaakt van Federatie gebaseerd op Hallo SAML-protocol.

    Uw toepassing Veracode Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **saml-token kenmerken** configuratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "kenmerken")

6. Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:

    | Naam van kenmerk | De waarde van kenmerk |
    |--- |--- |
    | Voornaam |User.givenName |
    | Achternaam |User.surname |
    | E-mail |User.mail |
    
    a. Klik voor elke gegevensrij in bovenstaande tabel voor Hallo **gebruikerskenmerk toevoegen**.
    
    ![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "kenmerken")
    
    ![Kenmerken](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "kenmerken")
    
    b. In Hallo **kenmerknaam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. In Hallo **kenmerkwaarde** textbox, selecteer Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. Op Hallo **Veracode configuratie** sectie, klikt u op **configureren Veracode** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID** van Hallo **Naslaggids punt.**

    ![Veracode configuratie](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. In een ander browservenster, meld u bij uw bedrijf Veracode site als beheerder.

10. Klik in het menu bovenaan Hallo Hallo **instellingen**, en klik vervolgens op **Admin**.
   
    ![Beheer](./media/active-directory-saas-veracode-tutorial/ic802911.png "beheer")

11. Klik op Hallo **SAML** tabblad.

12. In Hallo **organisatie SAML-instellingen** sectie, voert u Hallo stappen te volgen:
   
    ![Beheer](./media/active-directory-saas-veracode-tutorial/ic802912.png "beheer")
   
    a.  In **verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
    
    b. Klik op tooupload uw gedownloade certificaat vanuit Azure-portal **bestand kiezen**.
   
    c. Selecteer **Self-registratie inschakelen**.

13. In Hallo **Self-instellingen voor statusregistratie** sectie, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **opslaan**:
   
    ![Beheer](./media/active-directory-saas-veracode-tutorial/ic802913.png "beheer")
   
    a. Als **nieuwe gebruikersactivering**, selecteer **Nee activering vereist**.
   
    b. Als **gebruiker Gegevensupdates**, selecteer **voorkeur Veracode gebruikersgegevens**.
   
    c. Voor **Details van SAML-kenmerk**, selecteer Hallo volgende:
      * **Gebruikersrollen**
      * **Beleid beheerder**
      * **Revisor**
      * **Beveiliging Lead**
      * **Executive**
      * **Indienings**
      * **Maker**
      * **Alle scannen typen**
      * **Lidmaatschap van een team**
      * **Standaardteam**

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-veracode-test-user"></a>Een testgebruiker Veracode maken
In de volgorde tooenable Azure AD gebruikers toolog in Veracode, moeten ze worden ingericht in Veracode. In geval van Veracode Hallo is inrichting een geautomatiseerde taak. Er is geen actie-item voor u. Gebruikers worden automatisch gemaakt indien nodig tijdens Hallo eerste eenmalige aanmelding poging.

> [!NOTE]
> U kunt andere Veracode gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Veracode tooprovision Azure AD-gebruikersaccounts.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooVeracode toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooVeracode, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Veracode**.

    ![Hallo Veracode koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Veracode tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Veracode toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

