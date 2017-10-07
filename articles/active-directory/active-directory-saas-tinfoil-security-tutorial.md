---
title: 'Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TINFOIL SECURITY.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Zelfstudie: Azure Active Directory-integratie met TINFOIL SECURITY

In deze zelfstudie leert u hoe toointegrate TINFOIL SECURITY met Azure Active Directory (Azure AD).

TINFOIL SECURITY integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooTINFOIL beveiliging heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTINFOIL beveiliging (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met TINFOIL SECURITY tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een TINFOIL SECURITY eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. TINFOIL SECURITY van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>TINFOIL SECURITY van Hallo galerie toevoegen
tooconfigure hello integratie van TINFOIL SECURITY in Azure AD, moet u tooadd TINFOIL SECURITY uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**TINFOIL SECURITY via Hallo gallery tooadd uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **TINFOIL SECURITY**, selecteer **TINFOIL SECURITY** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![TINFOIL SECURITY vanuit galerie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met TINFOIL SECURITY op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TINFOIL SECURITY is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TINFOIL SECURITY toobe tot stand gebracht.

Wijs in TINFOIL SECURITY Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met behulp van TINFOIL SECURITY, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave een equivalent van Britta Simon in TINFOIL SECURITY die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TINFOIL SECURITY configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met TINFOIL SECURITY Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **TINFOIL SECURITY** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![SAML op basis van eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. Op Hallo **TINFOIL SECURITY domein en de URL's** sectie, hello gebruiker beschikt niet over tooperform eventuele stappen zoals Hallo app al vooraf is geïntegreerd met Azure.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde.

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. Kenmerktoewijzingen tooadd Hallo vereist, voert u Hallo stappen te volgen:
    
    ![Kenmerken](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "kenmerken")
    
    | Naam van kenmerk    |   De waarde van kenmerk |
    | ------------------- | -------------------- |
    | AccountId | UXXXXXXXXXXXXX |
    
    a. Klik op **gebruikerskenmerk toevoegen**.
    
    ![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "kenmerken")
    
    ![Kenmerk toevoegen](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "kenmerken")
    
    b. In Hallo **kenmerknaam** textbox type **accountid**.
    
    c. In Hallo **kenmerkwaarde** textbox plakken Hallo account id-waarde die u later op Hallo zelfstudie krijgt.
    
    d. Klik op **OK**.    

6. Klik op **opslaan** knop.

    ![knop Opslaan](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. Op Hallo **TINFOIL SECURITY Configuration** sectie, klikt u op **TINFOIL SECURITY configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![TINFOIL SECURITY Configuration](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. In een ander browservenster, meld u bij uw bedrijf TINFOIL SECURITY site als beheerder.

9. Klik in de werkbalk bovenaan Hallo Hallo op **Mijn Account**.
   
    ![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")

10. Klik op **beveiliging**.
   
    ![Beveiliging](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "beveiliging")

11. Op Hallo **Single Sign-On** configuratie pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "eenmalige aanmelding")
   
    a. Selecteer **SAML inschakelen**.
   
    b. Klik op **handmatige configuratie**.
   
    c. In **SAML Post URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal
   
    d. In **SAML certificaat vingerafdruk** textbox plakken Hallo-waarde van **vingerafdruk** die u hebt gekopieerd uit **certificaat voor ondertekening van SAML** sectie.
  
    e. Kopiëren **uw Account-ID** waarde en plak Hallo-waarde in **kenmerkwaarde** textbox onder **kenmerk toevoegen** sectie in Azure-portal.
   
    f. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Gebruikers en groepen -> alle gebruikers ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Gebruiker](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Een testgebruiker TINFOIL SECURITY maken

In volgorde tooenable Azure AD gebruikers toolog in TINFOIL SECURITY, moeten ze worden ingericht in TINFOIL SECURITY. In geval van TINFOIL SECURITY Hallo is inrichting een handmatige taak.

**een gebruiker die zijn ingericht, tooget uitvoeren Hallo stappen te volgen:**

1. Als het Hallo-gebruiker deel uitmaakt van een Enterprise-account, moet u deze te[Neem contact op met het ondersteuningsteam van Hallo TINFOIL SECURITY](https://www.tinfoilsecurity.com/contact) tooget Hallo-gebruikersaccount is gemaakt.

2. Als Hallo gebruiker een gewone TINFOIL SECURITY SaaS-gebruiker, kan Hallo gebruiker een tooany medewerker van de gebruiker van het Hallo-sites toevoegen. Deze triggers een proces toosend een uitnodiging toohello opgegeven e-toocreate een nieuw TINFOIL SECURITY-gebruikersaccount.

> [!NOTE]
> U kunt andere TINFOIL SECURITY gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TINFOIL SECURITY tooprovision Azure AD-gebruikersaccounts.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTINFOIL beveiliging.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTINFOIL beveiliging, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **TINFOIL SECURITY**.

    ![TINFOIL SECURITY selecteren](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo TINFOIL SECURITY-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TINFOIL SECURITY-toepassing. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

