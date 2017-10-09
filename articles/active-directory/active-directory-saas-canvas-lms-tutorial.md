---
title: 'Zelfstudie: Azure Active Directory-integratie met Canvas Lms | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Canvas LMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Zelfstudie: Azure Active Directory-integratie met Canvas LMS

In deze zelfstudie leert u hoe toointegrate Canvas met Azure Active Directory (Azure AD).

Canvas integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooCanvas toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooCanvas (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Canvas tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Canvas eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Canvas van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-canvas-from-hello-gallery"></a>Het toevoegen van Canvas van Hallo-galerie
tooconfigure hello integratie van Canvas in Azure AD, moet u tooadd Canvas uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Canvas via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Canvas**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. Selecteer in het deelvenster resultaten hello, **Canvas**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Canvas op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in het Canvas is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in het Canvas Hallo toobe tot stand gebracht.

In het canvas past, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Canvas, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Canvas](#creating-a-canvas-test-user)**  -toohave een equivalent van Britta Simon in die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Canvas.

**Voer tooconfigure Azure AD eenmalige aanmelding met Canvas Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Canvas** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. Op Hallo **Canvas domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.instructure.com`

    b. In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Canvas Client ondersteuningsteam](https://community.canvaslms.com/community/help) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. Op Hallo **configuratie tekenpapier** sectie, klikt u op **Canvas configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **URL van wijzigen wachtwoord, Sign-Out URL SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. In een ander browservenster, meld u aan tooyour Canvas bedrijf site als een beheerder.

8. Ga te**cursussen \> beheerde Accounts \> Microsoft**.
   
    ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

9. Selecteer in het navigatievenster aan de linkerkant Hallo Hallo **verificatie**, en klik vervolgens op **nieuwe SAML-configuratie toevoegen**.
   
    ![Verificatie](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "verificatie")

10. Voer op Hallo integratie van de huidige pagina Hallo stappen te volgen:
   
    ![Huidige integratie](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "huidige integratie")

    a. In **IdP entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    b. In **logboek URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    c. In **afmeldings-URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

    d. In **koppeling van wijzigen wachtwoord** textbox plakken Hallo-waarde van **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal. 

    e. In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.      
        
    f. Van Hallo **aanmelding kenmerk** selecteert **NameID**.

    g. Van Hallo **id indeling** selecteert **emailAddress**.

    h. Klik op **verificatie-instellingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-canvas-test-user"></a>Maken van een testgebruiker Canvas

Azure AD tooenable gebruikers toolog in tooCanvas, moeten ze worden ingericht in Canvas.

In geval van een Canvas is gebruikersaanvragen een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Canvas** tenant.

2. Ga te**cursussen \> beheerde Accounts \> Microsoft**.
   
   ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

3. Klik op **gebruikers**.
   
   ![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "gebruikers")

4. Klik op **nieuwe gebruiker toevoegen**.
   
   ![Gebruikers](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "gebruikers")

5. Op Hallo pagina dialoogvenster Nieuwe gebruiker toevoegen, voert u Hallo stappen te volgen:
   
   ![Gebruiker toevoegen](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "gebruiker toevoegen")
   
   a. In Hallo **volledige naam** textbox Voer Hallo-naam van gebruiker zoals **BrittaSimon**.

   b. In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .

   c. In Hallo **aanmelding** textbox Voer van Hallo gebruiker Azure AD e-mailadres zoals  **brittasimon@contoso.com** .

   d. Selecteer **e-mailadres Hallo gebruikersnaam over het maken van dit account**.

   e. Klik op **gebruiker toevoegen**.

>[!NOTE]
>U kunt andere Canvas gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Canvas tooprovision AAD-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCanvas toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooCanvas, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Canvas**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Canvas tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Canvas toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

