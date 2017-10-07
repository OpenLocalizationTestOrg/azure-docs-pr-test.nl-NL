---
title: 'Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Questetra BPM Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Questetra BPM Suite met Azure Active Directory (Azure AD).  
Questetra BPM Suite integreren met Azure AD biedt Hallo volgende voordelen: 

* U kunt beheren in Azure AD wie toegang tot tooQuestetra BPM Suite heeft 
* U kunt uw gebruikers tooautomatically get aangemelde tooQuestetra BPM Suite (Single Sign-On) inschakelen met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met Questetra BPM Suite tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Een [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
> 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.  
Hallo scenario beschreven in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:

1. Het toevoegen van Questetra BPM Suite van Hallo-galerie 
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Het toevoegen van Questetra BPM Suite van Hallo-galerie
tooconfigure hello integratie van Questetra BPM Suite in Azure AD, moet u tooadd Questetra BPM Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Questetra BPM Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **Questetra BPM Suite**.
   
    ![Toepassingen][5]

7. Selecteer in het deelvenster met resultaten Hallo **Questetra BPM Suite**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test eenmalige aanmelding Azure AD met Questetra BPM Suite op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Questetra BPM Suite tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Questetra BPM Suite toobe tot stand gebracht.  
Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Questetra BPM Suite.

tooconfigure en test eenmalige aanmelding Azure AD met Questetra BPM Suite, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave een equivalent van Britta Simon in Questetra BPM-pakket dat is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD voor eenmalige aanmelding configureren
Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw toepassing Questetra BPM Suite.

**tooconfigure eenmalige aanmelding Azure AD met Questetra BPM Suite Hallo stappen uitvoeren:**

1. In de klassieke Azure-portal op Hallo Hallo **Questetra BPM Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.
   
    ![Eenmalige aanmelding configureren][8]

2. Op Hallo **wilt u hoe gebruikers toosign op tooQuestetra BPM Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][9]

3. In een ander browservenster, meld u aan bij uw **Questetra BPM Suite** bedrijf site als beheerder.

4. Klik in het menu bovenaan Hallo Hallo **systeeminstellingen**. 
   
    ![Azure AD voor eenmalige aanmelding][10]

5. Hallo tooopen **SingleSignOnSAML** pagina, klikt u op **eenmalige aanmelding (SAML)**. 
   
    ![Azure AD voor eenmalige aanmelding][11]

6. In de klassieke Azure-portal op Hallo Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![App-instellingen configureren][13]
   
    a. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **ACS URL**, en plak deze in Hallo **aanmelding op URL** textbox.
   
    b. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **entiteit-ID**, en plak deze in Hallo **URL-verlener** textbox.
   
    c. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP informatie hello, kopie Hallo **ACS URL**, en plak deze in Hallo **antwoord-URL** textbox.
   
    d. Klik op **Volgende**.

7. Op Hallo **op Questetra BPM Suite eenmalige aanmelding configureren** pagina, klikt u op **certificaat downloaden**, en sla Hallo certificaatbestand lokaal op uw computer.
   
    ![Eenmalige aanmelding configureren][14]

8. Op uw **Questetra BPM Suite** bedrijf site, voert u Hallo stappen te volgen: 
   
    ![Eenmalige aanmelding configureren][15]
   
    a. Selecteer **eenmalige aanmelding inschakelen**.
   
    b. Kopieer op Hallo klassieke Azure-portal, Hallo **URL-verlener** waarde en plak deze in Hallo **entiteit-ID** textbox.
   
    c. Kopieer op Hallo klassieke Azure-portal, Hallo **Single Sign-On Service-URL** waarde en plak deze in Hallo **aanmelden pagina-URL** textbox.
   
    d. Kopieer op Hallo klassieke Azure-portal, Hallo **Service-URL met eenmalige Sign-Out** waarde en plak deze in Hallo **afmelden pagina-URL** textbox.
   
    e. In Hallo **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.

    f. Maak een Base64-gecodeerde bestand uit het gedownloade certificaat. 

    >[!TIP] 
    >Zie voor meer informatie [hoe tooconvert een binair bestand van het certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).

    g. De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze in Hallo **validatiecertificaat** textbox. 

    h. Klik op **Opslaan**.

1. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**. 
   
    ![Wat is Azure AD Connect?][17]

2. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
   
    ![Wat is Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Azure AD-testgebruiker maken][100] 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Azure AD-testgebruiker maken][101] 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**. 
   
    ![Azure AD-testgebruiker maken][102] 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Azure AD-testgebruiker maken][103]
   
    a. Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.
   
    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op Volgende.

6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Azure AD-testgebruiker maken][104] 
   
    a. In Hallo **voornaam** textbox type **Britta**. 
   
    b. In Hallo **achternaam** textbox type, **Simon**.
   
    c. In Hallo **weergavenaam** textbox type **Britta Simon**.
   
    d. In Hallo **rol** selecteert **gebruiker**.
   
    e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Azure AD-testgebruiker maken][105]  

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Azure AD-testgebruiker maken][106]   
   
    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Maken van een testgebruiker Questetra BPM Suite
Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Questetra BPM Suite van een gebruiker.

**een gebruiker Britta Simon aangeroepen in Questetra BPM Suite toocreate uitvoeren Hallo stappen te volgen:**

1. Eenmalige aanmelding tooyour Questetra BPM Suite bedrijf site als beheerder.
2. Ga te**systeeminstellingen > gebruikerslijst > nieuwe gebruiker**. 
3. Voer in het dialoogvenster van de nieuwe gebruiker Hallo, Hallo stappen te volgen: 
   
    ![Testgebruiker maken][300] 
   
    a. In Hallo **naam** textbox, typ de gebruikersnaam van Britta in Azure AD.
   
    b. In Hallo **e** textbox, typ de gebruikersnaam van Britta in Azure AD.
   
    c. In Hallo **wachtwoord** textbox, typ een wachtwoord.

4. Klik op **nieuwe gebruiker toevoegen**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooQuestetra BPM Suite verleent.

![Wat is Azure AD Connect?][200]

**tooassign Britta Simon tooQuestetra BPM Suite Hallo stappen uitvoeren:**

1. Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.
   
    ![Wat is Azure AD Connect?][201]
2. Selecteer in de lijst met de toepassingen van Hallo **Questetra BPM Suite**.
   
    ![Wat is Azure AD Connect?][205]
3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Wat is Azure AD Connect?][202]
4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
   
    ![Wat is Azure AD Connect?][203]
5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Wat is Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  
Als u op Hallo Questetra BPM Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Questetra BPM Suite-toepassing.

## <a name="additional-resources"></a>Aanvullende resources
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
