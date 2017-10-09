---
title: 'Zelfstudie: Azure Active Directory-integratie met PagerDuty | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en PagerDuty.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Zelfstudie: Azure Active Directory-integratie met PagerDuty

In deze zelfstudie leert u hoe toointegrate PagerDuty met Azure Active Directory (Azure AD).

PagerDuty integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooPagerDuty toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooPagerDuty (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met PagerDuty tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een PagerDuty eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van PagerDuty van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-pagerduty-from-hello-gallery"></a>Het toevoegen van PagerDuty van Hallo-galerie
tooconfigure hello integratie van PagerDuty in Azure AD, moet u tooadd PagerDuty uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd PagerDuty via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **PagerDuty**, selecteer **PagerDuty** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met PagerDuty op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in PagerDuty is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in PagerDuty toobe tot stand gebracht.

Wijs in PagerDuty, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met PagerDuty, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker PagerDuty](#create-a-pagerduty-test-user)**  -toohave een equivalent van Britta Simon in PagerDuty die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing PagerDuty configureren.

**Azure AD tooconfigure eenmalige aanmelding met PagerDuty, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **PagerDuty** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. Op Hallo **PagerDuty domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en PagerDuty domein eenmalige aanmelding informatie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.pagerduty.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [PagerDuty Client ondersteuningsteam](https://www.pagerduty.com/support/) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. Op Hallo **PagerDuty configuratie** sectie, klikt u op **configureren PagerDuty** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![PagerDuty configuratie](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Pagerduty site als beheerder.

8. Klik in het menu bovenaan Hallo Hallo **Accountinstellingen**.
   
    ![Instellingen account](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Accountinstellingen")

9. Klik op **Single Sign-on**.
   
    ![Eenmalige aanmelding](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "eenmalige aanmelding")

10. Op Hallo **Schakel eenmalige aanmelding (SSO)** pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding inschakelen](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "eenmalige aanmelding inschakelen")
   
    a. Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **X.509-certificaat** tekstvak
  
    b. In Hallo **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
  
    c. In Hallo **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
 
    d. Selecteer **Single Sign-on inschakelen**.
 
    e. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-pagerduty-test-user"></a>Een testgebruiker PagerDuty maken

Azure AD tooenable gebruikers toolog in tooPagerDuty, ze in PagerDuty moeten worden ingericht.  
In geval van PagerDuty Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt andere Pagerduty gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Pagerduty tooprovision Azure Active Directory-gebruikersaccounts.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Pagerduty** tenant.

2. Klik in het menu bovenaan Hallo Hallo **gebruikers**.

3. Klik op **gebruikers toevoegen**.
   
    ![Gebruikers toevoegen](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "gebruikers toevoegen")

4.  Op Hallo **uitnodigen van uw team** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Uw team uitnodigen](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "uitnodigen van uw team")

    a. Type Hallo **eerste en laatste naam** van gebruiker zoals **Britta Simon**. 
   
    b. Voer **e** adres van de gebruiker, zoals  **brittasimon@contoso.com** .
   
    c. Klik op **toevoegen**, en klik vervolgens op **verzenden nodigt**.
   
    >[!NOTE]
    >Alle toegevoegde gebruikers ontvangen een uitnodiging toocreate een PagerDuty-account.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooPagerDuty toegang verleent.

![Hallo-gebruikersrollen toewijzen][200]

**tooassign Britta Simon tooPagerDuty, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **PagerDuty**.

    ![Hallo PagerDuty koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u klikt op deze Hallo PagerDuty tegel in Hallo Panelyou toegang krijgt automatisch aangemelde tooyour PagerDuty toepassing.

Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

