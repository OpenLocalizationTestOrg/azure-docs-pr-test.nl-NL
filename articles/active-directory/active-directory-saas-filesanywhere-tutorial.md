---
title: 'Zelfstudie: Azure Active Directory-integratie met FilesAnywhere | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en FilesAnywhere.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>Zelfstudie: Azure Active Directory-integratie met FilesAnywhere

In deze zelfstudie leert u hoe toointegrate FilesAnywhere met Azure Active Directory (Azure AD).

FilesAnywhere integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooFilesAnywhere toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooFilesAnywhere (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met FilesAnywhere tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een FilesAnywhere eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van FilesAnywhere van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-filesanywhere-from-hello-gallery"></a>Het toevoegen van FilesAnywhere van Hallo-galerie
tooconfigure hello integratie van FilesAnywhere in Azure AD, moet u tooadd FilesAnywhere uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd FilesAnywhere via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **FilesAnywhere**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. Selecteer in het deelvenster resultaten hello, **FilesAnywhere**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met FilesAnywhere op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in FilesAnywhere is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in FilesAnywhere toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in FilesAnywhere.

tooconfigure en eenmalige aanmelding Azure AD-test met FilesAnywhere, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave een equivalent van Britta Simon in FilesAnywhere die is gekoppeld toohello Azure AD-weergave van haar.
3. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
4. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding in uw toepassing FilesAnywhere configureren.

**Azure AD tooconfigure eenmalige aanmelding met FilesAnywhere, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **FilesAnywhere** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. Op Hallo **FilesAnywhere domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    a. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> Houd er rekening mee dat waarde Hallo **215** is een **clientid** en is slechts een voorbeeld. U moet tooreplace met Hallo clientid Werkelijke waarde.

4. Op Hallo **FilesAnywhere domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **SP geïnitieerd modus**, Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie

    b. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke aanmelding op de URL en de antwoord-URL Hallo tooupdate. Neem contact op met [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) tooget deze waarden. 

5. Hallo SAML asserties verwacht FilesAnywhere softwaretoepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    Wanneer gebruikers zich up met FilesAnywhere ze Hallo-waarde van krijgen Hallo **clientid** kenmerk uit [FilesAnywhere team](mailto:support@FilesAnywhere.com). U hebt tooadd Hallo 'Client-Id-kenmerk met Hallo unieke waarde die door FilesAnywhere. Alle deze kenmerken die hierboven zijn vereist.
    > [!NOTE] 
    > Houd er rekening mee dat waarde Hallo **. 2331** van **clientid** is slechts een voorbeeld. U moet tooprovide Hallo werkelijke waarde.


6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in Hallo afbeelding hierboven en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ---------------| --------------- |    
    | clientid | *'uniquevalue'* |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. Op Hallo **FilesAnywhere configuratie** sectie, klikt u op **configureren FilesAnywhere** tooopen **eenmalige aanmelding configureren** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. tooget SSO configuratie voltooid voor uw toepassing aan het einde van FilesAnywhere contact [FilesAnywhere ondersteuningsteam](mailto:support@FilesAnywhere.com) en bieden ze Hallo gedownload ondertekenen certificaat en eenmalige aanmelding op (SSO) de URL van SAML-token.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 



### <a name="creating-a-filesanywhere-test-user"></a>Een testgebruiker FilesAnywhere maken

Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt. 


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooFilesAnywhere toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooFilesAnywhere, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **FilesAnywhere**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo FilesAnywhere tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour FilesAnywhere toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
