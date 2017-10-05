---
title: 'Zelfstudie: Azure Active Directory-integratie met Soonr werkplek | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Soonr werkplek.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Zelfstudie: Azure Active Directory-integratie met Soonr werkplek

Het doel van deze zelfstudie is het ziet u hoe werkplek Soonr integreren met Azure Active Directory (Azure AD).  
Soonr werkplek integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Soonr werkplek heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij Soonr werkplek (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Soonr werkplek, moet u de volgende items:

- Een Azure AD-abonnement
- Een Soonr werkplek eenmalige aanmelding ingeschakeld abonnement


> [!NOTE] 
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
Het doel van deze zelfstudie is zodat u kunt eenmalige aanmelding Azure AD te testen in een testomgeving.  
Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Soonr werkplek toevoegen uit de galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-soonr-workplace-from-the-gallery"></a>Soonr werkplek toevoegen uit de galerie
Voor het configureren van de integratie van Soonr werkplek in Azure AD, moet u Soonr werkplek uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Soonr werkplek uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**. 

    ![Active Directory][1]

2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.

    ![Toepassingen][2]

4. Klik op **toevoegen** aan de onderkant van de pagina.

    ![Toepassingen][3]

5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.
 
    ![Toepassingen][4]

6. Typ in het zoekvak **Soonr werkplek**.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Selecteer in het deelvenster met resultaten **Soonr werkplek**, en klik vervolgens op **Complete** de toepassing toevoegen.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Het doel van deze sectie wordt beschreven hoe u met het configureren en testen Azure AD eenmalige aanmelding bij Soonr werkplek op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Soonr werkplek aan een gebruiker in Azure AD is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gebruiker op de werkplek Soonr tot stand worden gebracht.  

Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Soonr werkplek.

Om te configureren en testen van Azure AD eenmalige aanmelding bij Soonr werkplek, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Soonr werkplek](#creating-a-soonr-workplace-test-user)**  - Soonr werkplek die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Soonr werkplek.


**Voor het configureren van Azure AD eenmalige aanmelding bij Soonr werkplek, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure-portal op de **Soonr werkplek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.

    ![Eenmalige aanmelding configureren][6] 

2. Op de **hoe wilt u dat gebruikers zich aanmelden op de werkplek Soonr** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Klik op **Volgende**.

    > [!NOTE] 
    > Houd er rekening mee dat dit geen de feitelijke waarde is. U moet deze waarde met de werkelijke aanmelding op de URL bijwerken. Neem contact op met het ondersteuningsteam Soonr werkplek deze waarde op te halen.

4. Op de **eenmalige aanmelding configureren op de werkplek Soonr** pagina, klikt u op **metagegevens downloaden** en sla het bestand op uw computer:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. Neem contact op met het ondersteuningsteam Soonr werkplek om SSO is geconfigureerd voor uw toepassing, en geef met de volgende opties: 

    • De gedownloade **metagegevens** bestand

    • De **URL-verlener**

    • De **SAML SSO-URL**

    • De **eenmalige afmelden Service-URL**

    >[!NOTE]
    >Deze toepassing wordt vervangen door <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask werkplek</a> en u kunt verwijzen <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">dit</a> zelfstudie voor het configureren van de toepassing met Azure AD.
   
6. In de klassieke Azure portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.

    ![Azure AD voor eenmalige aanmelding][10]

7. Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
  
    ![Azure AD voor eenmalige aanmelding][11]



### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is een testgebruiker maken in de klassieke Azure portal Britta Simon aangeroepen.  

![Azure AD-gebruiker maken][20]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.

    b. De gebruikersnaam **textbox**, type **BrittaSimon**.

    c. Klik op **Volgende**.

6.  Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. In de **voornaam** textbox type **Britta**.  

    b. In de **achternaam** textbox type, **Simon**.

    c. In de **weergavenaam** textbox type **Britta Simon**.

    d. In de **rol** selecteert **gebruiker**.

    e. Klik op **Volgende**.

7. Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Noteer de waarde van de **nieuw wachtwoord**.

    b. Klik op **Voltooien**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Maken van een testgebruiker Soonr werkplek

Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in Soonr werkplek. Neem contact op met het ondersteuningsteam Soonr werkplek een gebruiker te maken van het platform. U kunt de ondersteuningsticket met Soonr van verhogen <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">hier</a>.


### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

Het doel van deze sectie is het Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang te verlenen aan de werkplek Soonr inschakelen.

![Gebruiker toewijzen][200] 

**Als u wilt toewijzen Britta Simon Soonr werkplek, moet u de volgende stappen uitvoeren:**

1. In de klassieke Azure portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Soonr werkplek**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Klik in het menu bovenaan op **gebruikers**.

    ![Gebruiker toewijzen][203] 

1. Selecteer in de lijst gebruikers **Britta Simon**.

2. Klik in de werkbalk aan de onderkant op **toewijzen**.

    ![Gebruiker toewijzen][205]



### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.  
Als u op de tegel Soonr werkplek in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Soonr werkplek.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
