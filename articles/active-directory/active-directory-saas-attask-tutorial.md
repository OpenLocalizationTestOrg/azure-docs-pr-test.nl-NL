---
title: 'Zelfstudie: Azure Active Directory-integratie met @Task| Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en @Task.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Zelfstudie: Azure Active Directory-integratie met@Task
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate @Task met Azure Active Directory (Azure AD).  
Integratie van @Task met Azure AD biedt u Hallo volgende voordelen: 

* U kunt beheren in Azure AD die toegang heefttoo@Task
* U kunt uw tooautomatically ophalen aangemelde gebruikers inschakelen too@Task (Single Sign-On) met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-Portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
tooconfigure Azure AD-integratie met @Task, moet u de volgende items Hallo:

* Een Azure AD-abonnement
* Een @Task eenmalige aanmelding ingeschakeld abonnement

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

1. Toe te voegen @Task uit Hallo-galerie 
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-task-from-hello-gallery"></a>Toe te voegen @Task uit Hallo-galerie
tooconfigure hello integratie van @Task in Azure AD, moet u tooadd @Task uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd @Task uitvoeren via Hallo gallery Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1] 
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2] 
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3] 
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4] 
6. Typ in het zoekvak Hallo  **@Task** .
   
    ![Toepassingen][5] 
7. Selecteer in het deelvenster met resultaten Hallo  **@Task** , en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Toepassingen][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Hallo doel van deze sectie is tooshow u hoe tooconfigure en Azure AD test eenmalige aanmelding met @Task op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork Azure AD moet tooknow welke gebruiker Hallo equivalent in @Task tooan gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in @Task moet toobe tot stand gebracht.   
Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in @Task.

tooconfigure en Azure AD test eenmalige aanmelding met @Task, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een @Tasktest gebruiker](#creating-a-halogen-software-test-user)**  -toohave een equivalent van Britta Simon in @Taskthat gekoppelde toohello Azure AD-weergave van haar is.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD voor eenmalige aanmelding configureren
Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw @Task toepassing.

**tooconfigure eenmalige aanmelding Azure AD met @Task, Hallo volgende stappen uit te voeren:**

1. In de klassieke Azure-portal op Hallo Hallo  **@Task**  toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.
   
    ![Eenmalige aanmelding configureren][6] 
2. Op Hallo **hoe wilt u gebruikers toosign op too@Task**  pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][7] 
3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![App-instellingen configureren][8] 
   
     a. In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour @Task toepassing (bijvoorbeeld:*https://<Tenant name>.attask ondemand.com*).
   
     b. Klik op **Volgende**.
4. Op Hallo **configureren eenmalige aanmelding op @Task**  pagina, klikt u op **metagegevens downloaden**, Hallo metagegevensbestand lokaal op uw computer opslaan en klik vervolgens op **volgende**.
   
    ![Wat is Azure AD Connect?][9] 
5. Eenmalige aanmelding tooyour @Task bedrijf site als administrator.
6. Ga te**aanmelding op configuratie voor één**.
7. Op Hallo **Single Sign-On** dialoogvenster Hallo volgende stappen uit te voeren
   
    ![Eenmalige aanmelding configureren][23]
   
    a. Als **Type**, selecteer **SAML 2.0**.
   
    b. Selecteer **Service Provider-ID**.
   
    c. Kopieer op Hallo klassieke Azure-portal, Hallo **externe aanmeldings-URL**, en plak deze in Hallo **Portal de aanmeldings-URL** textbox.
   
    d. Kopieer op Hallo klassieke Azure-portal, Hallo **Service-URL met eenmalige Sign-Out**, en plak deze in Hallo **Sign-Out URL** textbox.
   
    e. Kopieer op Hallo klassieke Azure-portal, Hallo **URL van wijzigen wachtwoord**, en plak deze in Hallo **URL van wijzigen wachtwoord** textbox.
   
    f. Klik op **Opslaan**.
8. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**. 
   
    ![Wat is Azure AD Connect?][10]
9. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
   
    ![Wat is Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.  

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**. 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
   
    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op **Volgende**.
6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. In Hallo **voornaam** textbox type **Britta**.  
   
    b. In Hallo **achternaam** textbox type, **Simon**.
   
    c. In Hallo **weergavenaam** textbox type **Britta Simon**.
   
    d. In Hallo **rol** selecteert **gebruiker**.

    e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.   

### <a name="creating-an-task-test-user"></a>Maken van een @Task testgebruiker
Hallo-doel van deze sectie is toocreate een gebruiker Britta Simon aangeroepen in @Task.

**een gebruiker Britta Simon aangeroepen in toocreate @Task, Hallo volgende stappen uit te voeren:**

1. Meld u aan bij tooyour @Task bedrijf site als administrator.
2. Klik in het menu bovenaan Hallo Hallo **mensen**.
3. Klik op **nieuwe persoon**. 
4. Voer in het dialoogvenster van de nieuwe persoon Hallo, Hallo stappen te volgen:
   
    ![Maak een @Task testgebruiker][21] 
   
    a. In Hallo **voornaam** textbox, typt u 'Britta'.
   
    b. In Hallo **achternaam** textbox, typt u 'Simon'.
   
    c. In Hallo **e-mailadres** textbox Britta Simon van e-mailadres typt in Azure Active Directory.
   
    d. Klik op **persoon toevoegen**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding door haar toegang te verlenen too@Task.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon too@Task, Hallo volgende stappen uit te voeren:**

1. Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][201] 
2. Selecteer in de lijst met de toepassingen van Hallo  **@Task** .
   
    ![Gebruiker toewijzen][202] 
3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][203] 
4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  
Wanneer u klikt op Hallo @Task tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour @Task toepassing.

## <a name="additional-resources"></a>Aanvullende resources
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






