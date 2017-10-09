---
title: 'Zelfstudie: Azure Active Directory-integratie met ThousandEyes | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ThousandEyes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Zelfstudie: Azure Active Directory-integratie met ThousandEyes

In deze zelfstudie leert u hoe toointegrate ThousandEyes met Azure Active Directory (Azure AD).

ThousandEyes integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooThousandEyes toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooThousandEyes (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ThousandEyes tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ThousandEyes eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ThousandEyes van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-thousandeyes-from-hello-gallery"></a>Het toevoegen van ThousandEyes van Hallo-galerie
tooconfigure hello integratie van ThousandEyes in Azure AD, moet u tooadd ThousandEyes uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ThousandEyes via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **ThousandEyes**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. Selecteer in het deelvenster resultaten hello, **ThousandEyes**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met ThousandEyes op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ThousandEyes is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ThousandEyes toobe tot stand gebracht.

Wijs in ThousandEyes, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met ThousandEyes, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave een equivalent van Britta Simon in ThousandEyes die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ThousandEyes configureren.

**Azure AD tooconfigure eenmalige aanmelding met ThousandEyes, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ThousandEyes** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. Op Hallo **ThousandEyes domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL als:`https://app.thousandeyes.com/login/sso`

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. Op Hallo **ThousandEyes configuratie** sectie, klikt u op **configureren ThousandEyes** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. Een ander browservenster, meld u aan bij tooyour **ThousandEyes** bedrijf site als beheerder.

8. Klik in het menu bovenaan Hallo Hallo **instellingen**.
   
    ![Instellingen](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "instellingen")

9. Klik op **Account**
   
    ![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")

10. Klik op Hallo **beveiliging & verificatie** tabblad.
   
    ![Beveiliging en verificatie](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "beveiliging en verificatie")

11. In Hallo **Setup Single Sign-On** sectie, voert u Hallo stappen te volgen:
   
    ![Instellen van eenmalige aanmelding](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "eenmalige aanmelding instellen")
  
    a. Selecteer **eenmalige aanmelding inschakelen**.
  
    b. In **URL aanmeldingspagina** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
  
    c. In **pagina-URL voor afmelden** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
  
    d. **ID-Provider verlener** textbox plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
  
    e. In **verificatiecertificaat**, klikt u op **bestand kiezen**, en u hebt gedownload vanuit Azure-portal Hallo-certificaat uploaden.
  
    f. Klik op **Opslaan**.
 
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Een testgebruiker ThousandEyes maken

In de volgorde tooenable Azure AD gebruikers toolog in ThousandEyes, moeten ze worden ingericht in ThousandEyes.  
In geval van ThousandEyes Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt andere ThousandEyes gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door ThousandEyes tooprovision Azure Active Directory-gebruikersaccounts.

**een gebruiker account-tooThousandEyes tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u aan bij uw bedrijf ThousandEyes site als beheerder.

2. Klik op **instellingen**.
   
    ![Instellingen](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "instellingen")

3. Klik op **Account**.
   
    ![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")

4. Klik op Hallo **Accounts gebr & uikers** tabblad.
   
    ![Accounts gebr & uikers](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts gebr & uikers")

5. In Hallo **gebruikers toevoegen & Accounts** sectie, voert u Hallo stappen te volgen:
   
    ![Gebruikersaccounts toevoegen](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "gebruikersaccounts toevoegen")   
  
    a. In **naam** textbox Hallo-typenaam van de gebruiker zoals **Britta Simon**.

    b. In **e** textbox type Hallo e-mailadres van de gebruiker, zoals  **brittasimon@contoso.com** .
   
    b. Klik op **nieuwe gebruiker toevoegen tooAccount**.
      
     >[!NOTE]
     >Hello Azure Active Directory-accounthouder wordt een e-mailbericht een koppeling tooconfirm inclusief ophalen en activeer Hallo-account.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooThousandEyes toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooThousandEyes, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ThousandEyes**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo ThousandEyes-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ThousandEyes toepassing.

Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

