---
title: 'Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SciQuest besteden directeur.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Zelfstudie: Azure Active Directory-integratie met SciQuest besteden directeur
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SciQuest besteden directeur met Azure Active Directory (Azure AD).  
SciQuest besteden directeur integreren met Azure AD biedt Hallo volgende voordelen: 

* U kunt beheren in Azure AD die toegang tooSciQuest uitgaven directeur heeft 
* U kunt uw gebruikers tooautomatically get aangemelde tooSciQuest uitgaven directeur (Single Sign-On) met hun Azure AD-accounts inschakelen
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met SciQuest besteden directeur tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Een SciQuest besteden directeur eenmalige aanmelding ingeschakeld abonnement

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

1. Het toevoegen van SciQuest besteden directeur van Hallo-galerie 
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Het toevoegen van SciQuest besteden directeur van Hallo-galerie
tooconfigure hello integratie van SciQuest besteden directeur in Azure AD, moet u tooadd SciQuest besteden directeur uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SciQuest besteden directeur via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **sciQuest besteden directeur**.
   
    ![Toepassingen][5]

7. Selecteer in het deelvenster met resultaten Hallo **SciQuest besteden directeur**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Toepassingen][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en eenmalige aanmelding Azure AD-test met SciQuest besteden directeur op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SciQuest besteden directeur tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SciQuest besteden directeur toobe tot stand gebracht.  
Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SciQuest besteden directeur.

tooconfigure en eenmalige aanmelding Azure AD-test met SciQuest besteden directeur, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD één Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SciQuest besteden directeur](#creating-a-halogen-software-test-user)**  -toohave een equivalent van Britta Simon in SciQuest besteden directeur die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Azure AD één eenmalige aanmelding configureren
Hallo-doel van deze sectie is tooenable Azure AD eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure eenmalige aanmelding in uw toepassing SciQuest besteden directeur.

**tooconfigure eenmalige aanmelding Azure AD met SciQuest besteden directeur uitvoeren Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **SciQuest besteden directeur** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**dialoogvenster.
   
    ![Eenmalige aanmelding configureren][8]

2. Op Hallo **wilt u hoe gebruikers toosign op tooSciQuest uitgaven directeur** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][9]

3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![App-instellingen configureren][10]
   
     a. In Hallo **aanmelding op URL** textbox, typ uw URL wordt gebruikt door uw gebruikers toosign op tooyour SciQuest besteden directeur toepassing hello patroon volgen: *https://.* SciQuest.com/.**
   
     b. In Hallo **antwoord-URL** textbox, type Hallo dezelfde waarde als u hebt in Hallo hebt getypt **aanmelding op URL** textbox. 
   
     c. Klik op **Volgende**.

4. Op Hallo **eenmalige aanmelding configureren op SciQuest besteden directeur** pagina, klikt u op **metagegevens downloaden**, en sla het bestand met metagegevens Hallo lokaal op uw computer.
   
    ![Wat is Azure AD Connect?][11]

5. Neem contact op met SciQuest ondersteuning tooenable deze verificatiemethode met metagegevens voor de bovenstaande Hallo gedownload.

6. Op Hallo klassieke Azure-portal, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **Complete** tooclose hello **configureren eenmalige aanmelding** dialoogvenster. 
   
    ![Wat is Azure AD Connect?][15]

7. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Wat is Azure AD Connect?][100] 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Wat is Azure AD Connect?][101] 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**. 
   
    ![Wat is Azure AD Connect?][102] 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Wat is Azure AD Connect?][103] 
   
    a. Als **Type gebruiker**, selecteer **nieuwe gebruiker in uw organisatie**.
   
    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
   
    c. Klik op **Volgende**.

6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Wat is Azure AD Connect?][104] 
   
    a. In Hallo **voornaam** textbox type **Britta**.  
   
    b. In Hallo **achternaam** txtbox, type, **Simon**.
   
    c. In Hallo **weergavenaam** textbox type **Britta Simon**.
   
    d. In Hallo **rol** selecteert **gebruiker**.
   
    e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Wat is Azure AD Connect?][105]  

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Wat is Azure AD Connect?][106]   
   
    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   
    b. Klik op **Voltooien**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Een testgebruiker SciQuest besteden directeur maken
Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SciQuest besteden directeur van een gebruiker.

U moet toocontact ondersteuningsteam SciQuest besteden directeur en hen voorzien Hallo details over uw test account tooget die deze gemaakt.

U kunt ook kunt u gebruikmaken van just-in-time-inrichting, een eenmalige aanmelding functie die wordt ondersteund door SciQuest besteden directeur.  
Als just-in-time-inrichting is ingeschakeld, worden gebruikers automatisch gemaakt door SciQuest besteden directeur tijdens een poging voor aanmelding als ze nog niet bestaan. Deze functie Hallo overbodig toomanually gebruikers eenmalige aanmelding equivalent maken.

tooget just-in-time-inrichting is ingeschakeld, moet u toocontact je het ondersteuningsteam SciQuest besteden directeur.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooSciQuest uitgaven directeur verleent.

![Wat is Azure AD Connect?][200]

**tooassign Britta Simon tooSciQuest uitgaven directeur, Voer Hallo stappen te volgen:**

1. Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.
   
    ![Wat is Azure AD Connect?][201]

2. Selecteer in de lijst met de toepassingen van Hallo **SciQuest besteden directeur**.
   
    ![Wat is Azure AD Connect?][202]

3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Wat is Azure AD Connect?][203]

4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
   
    ![Wat is Azure AD Connect?][204]

5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Wat is Azure AD Connect?][205]

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  
Als u op Hallo SciQuest besteden directeur tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SciQuest besteden directeur toepassing.

## <a name="additional-resources"></a>Aanvullende resources
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

