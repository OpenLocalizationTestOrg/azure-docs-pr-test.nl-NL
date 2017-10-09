---
title: 'Zelfstudie: Azure Active Directory-integratie met RunMyProcess | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en RunMyProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f02acda015aeb8d131d8e3ef88bf50c4e8e94750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a>Zelfstudie: Azure Active Directory-integratie met RunMyProcess

In deze zelfstudie leert u hoe toointegrate RunMyProcess met Azure Active Directory (Azure AD).

RunMyProcess integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooRunMyProcess toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooRunMyProcess (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met RunMyProcess tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een RunMyProcess eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden:[proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van RunMyProcess van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-runmyprocess-from-hello-gallery"></a>Het toevoegen van RunMyProcess van Hallo-galerie
tooconfigure hello integratie van RunMyProcess in Azure AD, moet u tooadd RunMyProcess uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd RunMyProcess via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **RunMyProcess**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. Selecteer in het deelvenster resultaten hello, **RunMyProcess**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met RunMyProcess op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in RunMyProcess is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in RunMyProcess toobe tot stand gebracht.

Wijs in RunMyProcess, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met RunMyProcess, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker RunMyProcess](#creating-a-runmyprocess-test-user)**  -toohave een equivalent van Britta Simon in RunMyProcess die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing RunMyProcess configureren.

**Azure AD tooconfigure eenmalige aanmelding met RunMyProcess, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **RunMyProcess** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. Op Hallo **RunMyProcess domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://live.runmyprocess.com/live/<tenant id>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [RunMyProcess Client ondersteuningsteam](mailto:support@runmyprocess.com) tooget Hallo waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. Op Hallo **RunMyProcess configuratie** sectie, klikt u op **configureren RunMyProcess** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. In een ander browservenster, aanmelding tooyour RunMyProcess tenant als beheerder.

8. Klik in het linkernavigatievenster, **Account** en selecteer **configuratie**.
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. Ga te**verificatiemethode** sectie en Voer onderstaande stappen te volgen:
   
    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    a. Als **methode**, selecteer **-SSO met Samlv2**. 

    b. In Hallo **SSO omleiding** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    c. In Hallo **afmelding omleiding** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    d. In Hallo **indeling naam-Id** textbox Hallo typewaarde van **indeling van de id** als **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.

    e. Hallo-inhoud van het gedownloade bestand Hallo Kopieer en plak deze in Hallo **certificaat** textbox. 
 
    f. Klik op **opslaan** pictogram.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-runmyprocess-test-user"></a>Een testgebruiker RunMyProcess maken

In de volgorde tooenable Azure AD gebruikers toolog in tooRunMyProcess, moeten ze worden ingericht in RunMyProcess. In geval van RunMyProcess Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Aanmelden tooyour RunMyProcess bedrijf site als beheerder.

2. Klik op **Account** en selecteer **gebruikers** in het linkernavigatievenster, klik vervolgens op **nieuwe gebruiker**.
   
    ![Nieuwe gebruiker](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "nieuwe gebruiker")

3. In Hallo **gebruikersinstellingen** sectie, voert u Hallo stappen te volgen:
   
    ![Profiel](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "profiel") 
  
    a. Type Hallo **naam** en **e** van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo. 

    b. Selecteer een **IDE taal**, **taal**, en **profiel**. 

    c. Selecteer **verzenden account maken van het e-toome**. 

    d. Klik op **Opslaan**.
   
    >[!NOTE]
    >U kunt andere RunMyProcess gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door RunMyProcess tooprovision Azure Active Directory-gebruikersaccounts. 
    > 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRunMyProcess toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooRunMyProcess, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **RunMyProcess**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo RunMyProcess-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RunMyProcess toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

