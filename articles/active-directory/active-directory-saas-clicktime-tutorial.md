---
title: 'Zelfstudie: Azure Active Directory-integratie met ClickTime | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ClickTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Zelfstudie: Azure Active Directory-integratie met ClickTime

In deze zelfstudie leert u hoe toointegrate ClickTime met Azure Active Directory (Azure AD).

ClickTime integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooClickTime toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooClickTime (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ClickTime tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ClickTime eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ClickTime van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-clicktime-from-hello-gallery"></a>Het toevoegen van ClickTime van Hallo-galerie
tooconfigure hello integratie van ClickTime in Azure AD, moet u tooadd ClickTime uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ClickTime via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **ClickTime**, selecteer **ClickTime** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![ClickTime in de lijst met resultaten Hallo](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met ClickTime op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ClickTime is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ClickTime toobe tot stand gebracht.

Wijs in ClickTime, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met ClickTime, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker ClickTime](#create-a-clicktime-test-user)**  -toohave een equivalent van Britta Simon in ClickTime die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ClickTime configureren.

**Azure AD tooconfigure eenmalige aanmelding met ClickTime, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ClickTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. Op Hallo **ClickTime domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en ClickTime domein eenmalige aanmelding informatie](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. In Hallo **id** textbox, typ een URL als:`https://app.clicktime.com/sp/`
    
    b. In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. Op Hallo **ClickTime configuratie** sectie, klikt u op **configureren ClickTime** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![ClickTime configuratie](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf ClickTime site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **voorkeuren**, en klik vervolgens op **beveiligingsinstellingen**.

9. In Hallo **voorkeuren voor eenmalige aanmelding** configuratie sectie, voert u Hallo stappen te volgen:
   
    ![Beveiligingsinstellingen](./media/active-directory-saas-clicktime-tutorial/tic777280.png "beveiligingsinstellingen")
   
    a.  Selecteer **toestaan** aanmelden met eenmalige aanmelding (SSO) met **Azure AD**.
   
    b. In Hallo **eindpunt van de Provider identiteit** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    c.  Open Hallo **base-64 gecodeerde certificaat** gedownload van Azure-portal op **Kladblok**Hallo inhoud kopieert en plakt u deze in Hallo **X.509-certificaat** textbox.
   
    d.  Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-clicktime-test-user"></a>Een testgebruiker ClickTime maken

In de volgorde tooenable Azure AD gebruikers toolog in ClickTime, moeten ze worden ingericht in ClickTime.  
In geval van ClickTime Hallo is inrichting een handmatige taak.

> [!NOTE]
> U kunt andere ClickTime gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ClickTime tooprovision Azure AD-gebruikersaccounts.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**
1. Meld u bij tooyour **ClickTime** tenant.
2. Klik in de werkbalk bovenaan Hallo Hallo op **bedrijf**, en klik vervolgens op **mensen**.
   
    ![Mensen](./media/active-directory-saas-clicktime-tutorial/tic777282.png "personen")
3. Klik op **persoon toevoegen**.
   
    ![Persoon toevoegen](./media/active-directory-saas-clicktime-tutorial/tic777283.png "persoon toevoegen")
4. Voer in de sectie nieuwe persoon Hallo, Hallo stappen te volgen:
   
    ![Mensen](./media/active-directory-saas-clicktime-tutorial/tic777284.png "personen")
   
    a.  In Hallo **volledige naam** textbox type volledige naam van gebruiker zoals **Britta Simon**. 
  
    b.  In Hallo **e-mailadres** textbox type Hallo e-mailadres van de gebruiker, zoals  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Als u wilt, kunt u extra eigenschappen van het nieuwe persoon object Hallo instellen.
   
    c.  Klik op **Opslaan**.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooClickTime toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooClickTime, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ClickTime**.

    ![ClickTimne koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo ClickTime tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ClickTime toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

