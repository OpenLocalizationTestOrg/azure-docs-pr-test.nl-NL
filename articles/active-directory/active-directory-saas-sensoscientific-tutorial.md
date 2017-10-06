---
title: 'Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SensoScientific draadloze temperatuur Monitoring System.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Zelfstudie: Azure Active Directory-integratie met SensoScientific draadloze temperatuur Monitoring System

In deze zelfstudie leert u hoe toointegrate SensoScientific draadloze temperatuur Monitoring System met Azure Active Directory (Azure AD).

SensoScientific draadloze temperatuur Monitoring System integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSensoScientific draadloze temperatuur Monitoring System heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSensoScientific draadloze temperatuur Monitoring System (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SensoScientific draadloze temperatuur Monitoring System tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SensoScientific draadloze temperatuur Monitoring System eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SensoScientific draadloze temperatuur Monitoring System van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Het toevoegen van SensoScientific draadloze temperatuur Monitoring System van Hallo-galerie
tooconfigure hello integratie van SensoScientific draadloze temperatuur-bewakingssysteem in Azure AD, moet u tooadd SensoScientific draadloze temperatuur Monitoring System uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SensoScientific draadloze temperatuur Monitoring System via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SensoScientific draadloze temperatuur Monitoring System**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. Selecteer in het deelvenster resultaten hello, **SensoScientific draadloze temperatuur Monitoring System**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SensoScientific draadloze temperatuur Monitoring System op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SensoScientific draadloze temperatuur Monitoring System is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SensoScientific draadloze temperatuur Monitoring System toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SensoScientific draadloze temperatuur Monitoring System.

tooconfigure en eenmalige aanmelding Azure AD-test met SensoScientific draadloze temperatuur Monitoring System, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave een equivalent van Britta Simon in SensoScientific draadloze temperatuur bewakingssysteem die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SensoScientific draadloze temperatuur Monitoring System.

**tooconfigure eenmalige aanmelding Azure AD met SensoScientific draadloze temperatuur Monitoring System, Voer Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **SensoScientific draadloze temperatuur Monitoring System** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. Op Hallo **SensoScientific draadloze temperatuur bewaking systeemdomein en URL's** sectie geen noodzaak tooperform eventuele stappen als Hallo app al vooraf is geïntegreerd met Azure:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. Op Hallo **SensoScientific draadloze temperatuur bewaking systeemconfiguratie** sectie, klikt u op **configureren SensoScientific draadloze temperatuur Monitoring System** tooopen  **Eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, de entiteit-ID SAML** en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Meld u aan op tooyour SensoScientific draadloze temperatuur bewaking systeemtoepassing als beheerder.

8. Klik in het navigatiemenu Hallo Hallo bovenaan op **configuratie** en Ga naar **configureren** onder **eenmalige aanmelding** tooopen Hallo eenmalige aanmelding op instellingen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. In **eenmalige aanmelding op instellingen** formulier Hallo stappen uitvoeren:
 
    a. Selecteer **certificaatverlener** als Azure AD.
    
    b. Plakken Hallo **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in URL-verlener tekstvak.
    
    c. Plakken Hallo **SAML Single Sign-On Service-URL** die u in één Service-URL aanmelding tekstvak vanuit Azure-portal hebt gekopieerd.

    d. Plakken Hallo **Sign-Out URL** die u in het tekstvak voor de Service-URL met eenmalige Sign-Out vanuit Azure-portal hebt gekopieerd.

    e. Blader Hallo-certificaat dat u hebt gedownload vanuit Azure-portal en hier uploaden.
    
    f. Klik op **Opslaan**.
  
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Maken van een testgebruiker SensoScientific draadloze temperatuur Monitoring System

Azure AD tooenable gebruikers toolog in tooSensoScientific draadloze temperatuur Monitoring System, ze in SensoScientific draadloze temperatuur bewakingssysteem moeten worden ingericht. Werken met [SensoScientific draadloze temperatuur Monitoring System ondersteuningsteam](https://www.sensoscientific.com/contact-us/) Hallo gebruikers toevoegen in Hallo SensoScientific draadloze temperatuur Monitoring System platform. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSensoScientific draadloze temperatuur Monitoring System.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSensoScientific draadloze temperatuur Monitoring System Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SensoScientific draadloze temperatuur Monitoring System**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen. Klik op Hallo SensoScientific draadloze temperatuur Monitoring System tegel in het deelvenster toegang hello, kunt u zich automatisch aangemelde tooyour SensoScientific draadloze temperatuur Monitoring-toepassing. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

