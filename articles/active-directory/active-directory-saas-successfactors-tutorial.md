---
title: 'Zelfstudie: Azure Active Directory-integratie met SuccessFactors | Microsoft Docs'
description: Lees hoe toouse SuccessFactors met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Zelfstudie: Azure Active Directory-integratie met SuccessFactors
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SuccessFactors met Azure Active Directory (Azure AD).

SuccessFactors integreren met Azure AD biedt Hallo volgende voordelen:

* U kunt beheren in Azure AD die tooSuccessFactors toegang heeft
* U kunt uw gebruikers tooautomatically get aangemelde tooSuccessFactors (Single Sign-On) met hun Azure AD-accounts inschakelen
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met SuccessFactors tooconfigure, moet u Hallo volgende items:

* Een geldige Azure-abonnement
* Een tenant in SuccessFactors

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
> 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SuccessFactors van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-successfactors-from-hello-gallery"></a>Het toevoegen van SuccessFactors van Hallo-galerie
tooconfigure hello integratie van SuccessFactors in Azure AD, moet u tooadd SuccessFactors uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SuccessFactors via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. Klik in de klassieke Azure-portal op Hallo linkernavigatievenster, Hallo op **Active Directory**.
   
    ![Eenmalige aanmelding configureren][1]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Eenmalige aanmelding configureren][2]
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Eenmalige aanmelding configureren][4]
6. In Hallo **zoekvak**, type **SuccessFactors**.
   
    ![Eenmalige aanmelding configureren][5]
7. Selecteer in het deelvenster resultaten hello, **SuccessFactors**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Eenmalige aanmelding configureren][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en eenmalige aanmelding Azure AD-test met SuccessFactors op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SuccessFactors tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SuccessFactors toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SuccessFactors.

tooconfigure en eenmalige aanmelding Azure AD-test met SuccessFactors, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SuccessFactors](#creating-a-successfactors-test-user)**  -toohave een equivalent van Britta Simon in SuccessFactors die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren
In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing SuccessFactors.

**Azure AD tooconfigure eenmalige aanmelding met SuccessFactors, Voer Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **SuccessFactors** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren eenmalige aanmelding** het dialoogvenster.
   
    ![Eenmalige aanmelding configureren][7]
2. Op Hallo **wilt u hoe gebruikers toosign op tooSuccessFactors** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren][8]
3. Op Hallo **App-URL configureren** pagina, het uitvoeren van Hallo volgende stappen uit en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren][9]
   
    a. In Hallo **aanmelding op URL** textbox, typ een URL met een Hallo patronen te volgen: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. In Hallo **antwoord-URL** textbox, typ een URL met een Hallo patronen te volgen: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Klik op **Volgende**. 

    > [!NOTE]
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke aanmelding op de URL en de antwoord-URL Hallo tooupdate. Neem contact op met tooget deze waarden [SuccessFactors ondersteuningsteam](https://www.successfactors.com/en_us/support.html).

1. Op Hallo **eenmalige aanmelding configureren op SuccessFactors** pagina, klikt u op **certificaat downloaden**, en sla Hallo certificaatbestand lokaal op uw computer.
   
    ![Eenmalige aanmelding configureren][10]

2. In een ander browservenster, meld u aan bij uw **SuccessFactors-beheerportal** als beheerder.

3. Ga naar **Toepassingsbeveiliging** en systeemeigen te**eenmalige aanmelding op functie**. 

4. De waarde van een plaats in Hallo **Token opnieuw** en klik op **Token opslaan** tooenable SAML SSO.
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][11]

    > [!NOTE] 
    > Deze waarde wordt alleen gebruikt als Hallo aan/uit-knop. Als een willekeurige waarde wordt opgeslagen, is Hallo SAML SSO ingeschakeld. Als een lege waarde wordt opgeslagen is Hallo SAML SSO uitgeschakeld.

1. Systeemeigen toobelow schermafbeelding en Hallo van de volgende activiteiten uit te voeren.
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][12]
   
    a. Selecteer Hallo **SAML v2 SSO** keuzerondje
   
    b. Hallo SAML aantonen partij Name(e.g. SAml issuer + company name) ingesteld.
   
    c. In Hallo **SAML verlener** textbox plaatsen Hallo-waarde van **URL-verlener** van de configuratiewizard voor Azure AD-toepassing.
   
    d. Selecteer **(klant gegenereerd/IdP/AP) antwoord** als **verplichte handtekening vereisen**.
   
    e. Selecteer **ingeschakeld** als **inschakelen SAML vlag**.
   
    f. Selecteer **Nee** als **aanmelding Aanvraaghandtekening (SF gegenereerd/SP/RP)**.
   
    g. Selecteer **Browser/Post profiel** als **SAML profiel**.
   
    h. Selecteer **Nee** als **geldigheidsduur van certificaat afdwingen**.
   
    ik. Hallo-inhoud van de gedownloade certificaatbestand Hallo kopiëren en plak deze in Hallo **SAML verifiëren certificaat** textbox.

    > [!NOTE] 
    > inhoud van de certificaten Hallo moet certificaat en certificaat afsluitcodes hebben beginnen.

1. Navigeer tooSAML V2 en voer vervolgens Hallo stappen te volgen:
   
    ![Configureren van eenmalige aanmelding op app aan clientzijde][13]
   
    a. Selecteer **Ja** als **ondersteuning voor globale afmelding Serviceprovider geïnitieerde**.
   
    b. In Hallo **globale afmelding Service-URL (LogoutRequest doel)** textbox plaatsen Hallo-waarde van **externe URL voor afmelden** van de configuratiewizard voor Azure AD-toepassing.
   
    c. Selecteer **Nee** als **vereisen sp alle NameID element moet versleutelen**.
   
    d. Selecteer **niet nader omschreven** als **NameID indeling**.
   
    e. Selecteer **Ja** als **inschakelen geïnitieerd sp aanmelding (AuthnRequest)**.
   
    f. In Hallo **Verzendaanvraag als uitgever van het hele bedrijf** textbox plaatsen Hallo-waarde van **externe aanmeldings-URL** van de configuratiewizard voor Azure AD-toepassing.
2. Voer deze stappen uit als u wilt dat toomake Hallo aanmelding gebruikersnamen niet hoofdlettergevoelig.
   
    a. Ga naar **Bedrijfsinstellingen**(aan de onderkant van de Hallo).
   
    b. Schakel dit selectievakje in bij **inschakelen niet hoofdlettergevoelig gebruikersnaam**.
   
    c.Click **opslaan**.
   
    ![Eenmalige aanmelding configureren][29]

    > [!NOTE] 
    > Als u tooenable dit probeert, systeemcontroles Hallo als een dubbele naam van de SAML-aanmelding wordt gemaakt. Bijvoorbeeld als de klant Hallo heeft gebruikersnamen Gebruiker1 als Gebruiker1. Blijf de hoofdlettergevoeligheid, kunt u deze dubbele vermeldingen. Hallo-systeem, krijgt u een foutbericht weergegeven en wordt het Hallo-functie niet inschakelt. Hallo-klant moet toochange een Hallo gebruikersnamen zodat deze daadwerkelijk gespeld verschillende. 

1. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster.
   
    ![Toepassingen][14]
2. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.
   
    ![Toepassingen][15]

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][16]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken][17]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken][18]
4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.
   
    ![Een Azure AD-testgebruiker maken][19]
5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken][20]
   
    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
   
    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op **Volgende**.
6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken][21]
   
    a. In Hallo **voornaam** textbox type **Britta**.  
   
    b. In Hallo **achternaam** textbox type, **Simon**.
   
    c. In Hallo **weergavenaam** textbox type **Britta Simon**.
   
    d. In Hallo **rol** selecteert **gebruiker**.
   
    e. Klik op **Volgende**.
7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken][22]
8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken][23]
   
    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.  

### <a name="creating-a-successfactors-test-user"></a>Een testgebruiker SuccessFactors maken
In de volgorde tooenable Azure AD gebruikers toolog in SuccessFactors, moeten ze worden ingericht in SuccessFactors.  
In geval van SuccessFactors Hallo is inrichting een handmatige taak.

tooget gebruikers in SuccessFactors hebt gemaakt, moet u toocontact hello [SuccessFactors ondersteuningsteam](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar tooSuccessFactors toegang verleent.

![Gebruiker toewijzen][24]

**tooassign Britta Simon tooSuccessFactors, Voer Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][25]
2. Selecteer in de lijst met de toepassingen van Hallo **SuccessFactors**.
   
    ![Eenmalige aanmelding configureren][26]
3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][27]
4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][28]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo SuccessFactors-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SuccessFactors toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
