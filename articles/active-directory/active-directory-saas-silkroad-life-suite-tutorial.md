---
title: 'Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SilkRoad levensduur Suite.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Zelfstudie: Azure Active Directory-integratie met SilkRoad levensduur Suite
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate SilkRoad levensduur Suite met Azure Active Directory (Azure AD). 

SilkRoad levensduur Suite integreren met Azure AD biedt Hallo volgende voordelen: 

* U kunt beheren in Azure AD wie toegang tot tooSilkRoad levensduur Suite heeft 
* U kunt uw gebruikers tooautomatically get aangemelde tooSilkRoad Suite levensduur van eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met SilkRoad levensduur Suite tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Een abonnement SilkRoad levensduur Suite SSO-ingeschakeld

>[!NOTE]
>tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving. 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD-eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SilkRoad levensduur Suite van Hallo-galerie 
2. Configureren en testen van Azure AD-SSO

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>SilkRoad levensduur Suite van Hallo galerie toevoegen
tooconfigure hello integratie van SilkRoad levensduur Suite in Azure AD, moet u tooadd SilkRoad levensduur Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SilkRoad levensduur Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **SilkRoad levensduur Suite**.
   
    ![Toepassingen][5]

7. Selecteer in het deelvenster met resultaten Hallo **SilkRoad levensduur Suite**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Toepassingen][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Azure AD-SSO met SilkRoad levensduur Suite op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SilkRoad leven Suite tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SilkRoad leven Suite toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in SilkRoad leven Suite.

tooconfigure en test eenmalige aanmelding Azure AD met SilkRoad levensduur Suite, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SilkRoad levensduur Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave een equivalent van Britta Simon in SilkRoad levensduur-pakket dat is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren
Hallo-doel van deze sectie is tooenable Azure AD-eenmalige aanmelding in de klassieke Azure-portal Hallo en tooconfigure SSO in uw toepassing SilkRoad levensduur Suite.

**tooconfigure eenmalige aanmelding Azure AD met SilkRoad levensduur Suite uitvoeren Hallo stappen te volgen:**

1. Eenmalige aanmelding tooyour SilkRoad bedrijf site als administrator. 

  >[!NOTE] 
  > tooobtain toegang toohello SilkRoad levensduur Suite verificatie-toepassing voor federatie configureren met Microsoft Azure AD en neem contact op met ondersteuning voor SilkRoad of uw vertegenwoordiger SilkRoad Services.
  > 

2. Ga te**serviceprovider**, en klik vervolgens op **Federation Details**. 
   
    ![Azure AD voor eenmalige aanmelding][10] 

3. Klik op **Federatiemetagegevens downloaden**, en sla het bestand met metagegevens Hallo op uw computer.
   
    ![Azure AD voor eenmalige aanmelding][11] 

4. In de klassieke Azure-portal op Hallo Hallo **SilkRoad levensduur Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.
   
    ![Eenmalige aanmelding configureren][6] 

5. Op Hallo **wilt u hoe gebruikers toosign op tooSilkRoad levensduur Suite** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][7] 

6. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Azure AD voor eenmalige aanmelding][8]   
 1. In Hallo **aanmelding op URL** textbox type Hallo-URL die door uw gebruikers toosign op tooyour SilkRoad levensduur Suite site gebruikt (bijvoorbeeld: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Open Hallo gedownload **Silkroad** bestand met metagegevens. 
 3. Zoek Hallo **AssertionConsumerService** label en kopiëren Hallo **locatie** kenmerk.         
   
    ![Azure AD voor eenmalige aanmelding][21] 
 4. Hallo-waarde in Hallo plakken **antwoord-URL** textbox.  
 5. Klik op **Volgende**.

6. Op Hallo **op SilkRoad levensduur Suite eenmalige aanmelding configureren** pagina, voert u Hallo stappen te volgen:
   
    ![Azure AD voor eenmalige aanmelding][9]  
 1. Klik op downloaden certificaat en sla Hallo-bestand op uw computer.  
 2. Klik op **Volgende**.

7. In uw **SilkRoad** toepassing, klikt u op **verificatie bronnen**.
   
    ![Azure AD voor eenmalige aanmelding][12] 

8. Klik op **verificatiebron toevoegen**. 
   
    ![Azure AD voor eenmalige aanmelding][13] 

9. In Hallo **verificatie-bron toevoegen** sectie, voert u Hallo stappen te volgen: 
   
    ![Azure AD voor eenmalige aanmelding][14]  
 1. Onder **optie 2 - bestand met metagegevens**, klikt u op **Bladeren** tooupload Hallo gedownload bestand met metagegevens.  
 2. Klik op **maken id-Provider met behulp van bestandsgegevens**.

10. In Hallo **verificatie bronnen** sectie, klikt u op **bewerken**. 
    
     ![Azure AD voor eenmalige aanmelding][15] 

11. Op Hallo **verificatiebron bewerken** dialoogvenster Hallo volgende stappen uit te voeren: 
    
     ![Azure AD voor eenmalige aanmelding][16] 
 1. Als **ingeschakeld**, selecteer **Ja**.   
 2. In Hallo **IdP beschrijving** textbox, typ een beschrijving voor uw configuratie (bijvoorbeeld: *Azure AD SSO*).  
 3. In Hallo **IdP naam** textbox, typ een naam die specifieke tooyour configuratie (bijvoorbeeld: *Azure SP*).  
 4. Klik op **Opslaan**.

12. Uitschakelen voor alle andere verificatie-bronnen. 
    
     ![Azure AD voor eenmalige aanmelding][17]

13. In de klassieke Azure-portal op Hallo Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **volgende**.  
    
     ![Azure AD voor eenmalige aanmelding][18]

14. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.
    
     ![Azure AD voor eenmalige aanmelding][19]

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**. 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.  
 2. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**. 
 3. Klik op **Volgende**.

6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. In Hallo **voornaam** textbox type **Britta**.    
 2. In Hallo **achternaam** textbox type, **Simon**. 
 3. In Hallo **weergavenaam** textbox type **Britta Simon**. 
 4. In Hallo **rol** selecteert **gebruiker**.
 5. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**. 
 2. Klik op **Voltooien**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Maak een testgebruiker SilkRoad levensduur Suite
Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SilkRoad leven Suite van een gebruiker. De Britta moet een SSO-ID hebben (dit wordt soms aangeduid tooas een *AuthParam*) die overeenkomt met de Britta **emailaddress** in Azure AD.

**toocreate een gebruiker Britta Simon aangeroepen in SilkRoad leven Suite uitvoeren Hallo stappen te volgen:**

- Vraag uw SilkRoad levensduur Suite support team toocreate een gebruiker die als heeft **SSO-ID** kenmerk Hallo dezelfde als Hallo waarde **emailaddress** van Britta Simon in Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo doel van deze sectie is tooenable Britta Simon toouse Azure SSO haar toegang tooSilkRoad levensduur Suite verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSilkRoad levensduur Suite uitvoeren Hallo stappen te volgen:**

1. Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SilkRoad levensduur Suite**.
   
    ![Gebruiker toewijzen][202] 

3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][203] 

4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.

5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.  

Als u op Hallo SilkRoad levensduur Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SilkRoad levensduur Suite-toepassing.

## <a name="additional-resources"></a>Aanvullende resources
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





