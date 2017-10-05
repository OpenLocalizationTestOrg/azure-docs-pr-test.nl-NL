---
title: 'Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Questetra BPM Suite.
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
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Zelfstudie: Azure Active Directory-integratie met Questetra BPM Suite
Er is het doel van deze zelfstudie leert u Questetra BPM Suite integreren met Azure Active Directory (Azure AD).  
Questetra BPM Suite integreren met Azure AD biedt de volgende voordelen: 

* U kunt beheren in Azure AD die toegang tot Questetra BPM Suite heeft 
* U kunt uw gebruikers automatisch ophalen aangemeld bij Questetra BPM Suite (Single Sign-On) inschakelen met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Voor het configureren van Azure AD-integratie met Questetra BPM Suite, moet u de volgende items:

* Een Azure AD-abonnement
* Een [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
> 
> 

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenariobeschrijving
Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.  
Het scenario in deze zelfstudie bestaat uit drie belangrijkste bouwstenen:

1. Questetra BPM Suite uit de galerie toevoegen 
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a>Questetra BPM Suite uit de galerie toevoegen
Voor het configureren van de integratie van Questetra BPM Suite in Azure AD, moet u Questetra BPM Suite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Questetra BPM Suite uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**. 
   
    ![Active Directory][1]

2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
    ![Toepassingen][2]

4. Klik op **toevoegen** aan de onderkant van de pagina.
   
    ![Toepassingen][3]

5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.
   
    ![Toepassingen][4]

6. Typ in het zoekvak **Questetra BPM Suite**.
   
    ![Toepassingen][5]

7. Selecteer in het deelvenster met resultaten **Questetra BPM Suite**, en klik vervolgens op **Complete** de toepassing toevoegen.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Het doel van deze sectie is het beschreven hoe u met het configureren en testen eenmalige aanmelding Azure AD met Questetra BPM Suite op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker van het bijbehorende equivalent in Questetra BPM Suite aan een gebruiker in Azure AD is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Questetra BPM Suite tot stand worden gebracht.  
Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Questetra BPM Suite.

Om te configureren en testen van Azure AD eenmalige aanmelding met Questetra BPM Suite, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  - Questetra BPM Suite die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD voor eenmalige aanmelding configureren
Het doel van deze sectie is Azure AD eenmalige aanmelding inschakelen in de klassieke Azure portal en eenmalige aanmelding configureren in uw toepassing Questetra BPM Suite.

**Voor het configureren van Azure AD eenmalige aanmelding met Questetra BPM Suite, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure-portal op de **Questetra BPM Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.
   
    ![Eenmalige aanmelding configureren][8]

2. Op de **hoe wilt u dat gebruikers zich aanmelden op Questetra BPM Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][9]

3. In een ander browservenster, meld u aan bij uw **Questetra BPM Suite** bedrijf site als beheerder.

4. Klik in het menu bovenaan op **systeeminstellingen**. 
   
    ![Azure AD voor eenmalige aanmelding][10]

5. Openen van de **SingleSignOnSAML** pagina, klikt u op **eenmalige aanmelding (SAML)**. 
   
    ![Azure AD voor eenmalige aanmelding][11]

6. In de klassieke Azure-portal op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit: 
   
    ![App-instellingen configureren][13]
   
    a. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **ACS URL**, en plak deze in de **aanmelding op URL** textbox.
   
    b. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **entiteit-ID**, en plak deze in de **URL-verlener** textbox.
   
    c. Op uw **Questetra BPM Suite** bedrijf site in de sectie SP gegevens kopiëren de **ACS URL**, en plak deze in de **antwoord-URL** textbox.
   
    d. Klik op **Volgende**.

7. Op de **op Questetra BPM Suite eenmalige aanmelding configureren** pagina, klikt u op **certificaat downloaden**, en sla het certificaatbestand lokaal op uw computer.
   
    ![Eenmalige aanmelding configureren][14]

8. Op uw **Questetra BPM Suite** bedrijf site, voert u de volgende stappen uit: 
   
    ![Eenmalige aanmelding configureren][15]
   
    a. Selecteer **eenmalige aanmelding inschakelen**.
   
    b. Kopieer op de klassieke Azure portal, de **URL-verlener** waarde en plak deze in de **entiteit-ID** textbox.
   
    c. Kopieer op de klassieke Azure portal, de **Single Sign-On Service-URL** waarde en plak deze in de **aanmelden pagina-URL** textbox.
   
    d. Kopieer op de klassieke Azure portal, de **Service-URL met eenmalige Sign-Out** waarde en plak deze in de **afmelden pagina-URL** textbox.
   
    e. In de **NameID indeling** textbox type **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.

    f. Maak een Base64-gecodeerde bestand uit het gedownloade certificaat. 

    >[!TIP] 
    >Zie voor meer informatie [het converteren van een binaire certificaat naar een tekstbestand](http://youtu.be/PlgrzUZ-Y1o).

    g. Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze in de **validatiecertificaat** textbox. 

    h. Klik op **Opslaan**.

1. Bij de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik op **volgende**. 
   
    ![Wat is Azure AD Connect?][17]

2. Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
   
    ![Wat is Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Azure AD-testgebruiker maken][100] 

2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.
   
    ![Azure AD-testgebruiker maken][101] 

4. Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**. 
   
    ![Azure AD-testgebruiker maken][102] 

5. Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
   
    ![Azure AD-testgebruiker maken][103]
   
    a. Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.
   
    b. De gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op Volgende.

6. Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit: 
   
    ![Azure AD-testgebruiker maken][104] 
   
    a. In de **voornaam** textbox type **Britta**. 
   
    b. In de **achternaam** textbox type, **Simon**.
   
    c. In de **weergavenaam** textbox type **Britta Simon**.
   
    d. In de **rol** selecteert **gebruiker**.
   
    e. Klik op **Volgende**.

7. Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Azure AD-testgebruiker maken][105]  

8. Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:
   
    ![Azure AD-testgebruiker maken][106]   
   
    a. Noteer de waarde van de **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Maken van een testgebruiker Questetra BPM Suite
Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Questetra BPM Suite.

**Als u wilt een gebruiker Britta Simon aangeroepen in Questetra BPM Suite maakt, moet u de volgende stappen uitvoeren:**

1. Aanmelding bij uw bedrijf Questetra BPM Suite site als beheerder.
2. Ga naar **systeeminstellingen > gebruikerslijst > nieuwe gebruiker**. 
3. In het dialoogvenster Nieuwe gebruiker de volgende stappen uitvoeren: 
   
    ![Testgebruiker maken][300] 
   
    a. In de **naam** textbox, typ de gebruikersnaam van Britta in Azure AD.
   
    b. In de **e** textbox, typ de gebruikersnaam van Britta in Azure AD.
   
    c. In de **wachtwoord** textbox, typ een wachtwoord.

4. Klik op **nieuwe gebruiker toevoegen**.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD
Het doel van deze sectie is het Britta Simon haar toegang verlenen aan Questetra BPM Suite gebruikt Azure eenmalige aanmelding inschakelen.

![Wat is Azure AD Connect?][200]

**Als u wilt toewijzen Britta Simon Questetra BPM Suite, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
    ![Wat is Azure AD Connect?][201]
2. Selecteer in de lijst met toepassingen **Questetra BPM Suite**.
   
    ![Wat is Azure AD Connect?][205]
3. Klik in het menu bovenaan op **gebruikers**.
   
    ![Wat is Azure AD Connect?][202]
4. Selecteer in de lijst gebruikers **Britta Simon**.
   
    ![Wat is Azure AD Connect?][203]
5. Klik in de werkbalk aan de onderkant op **toewijzen**.
   
    ![Wat is Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.  
Als u op de tegel Questetra BPM Suite in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Questetra BPM Suite.

## <a name="additional-resources"></a>Aanvullende resources
* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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
