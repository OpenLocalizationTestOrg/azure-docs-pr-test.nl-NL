---
title: 'Zelfstudie: Azure Active Directory-integratie met Halosys | Microsoft Docs'
description: Meer informatie over het gebruik van Halosys met Azure Active Directory voor het inschakelen van eenmalige aanmelding, geautomatiseerde inrichting en meer!
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18c5cd8eb4ca211f8ae2b8dd994c0e8c48625a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Zelfstudie: Azure Active Directory-integratie met Halosys

In deze zelfstudie leert u hoe Halosys integreren met Azure Active Directory (Azure AD).

Halosys integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Halosys heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij Halosys (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Halosys, moet u de volgende items:

- Een Azure AD-abonnement
- Een Halosys eenmalige aanmelding ingeschakeld abonnement


> [!NOTE] 
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.

Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Halosys uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-halosys-from-the-gallery"></a>Halosys uit de galerie toevoegen
Voor het configureren van de integratie van Halosys in Azure AD, moet u Halosys uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Halosys uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.

    ![Active Directory][1]
2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.

    ![Toepassingen][2]

4. Klik op **toevoegen** aan de onderkant van de pagina.

    ![Toepassingen][3]

5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.

    ![Toepassingen][4]

6. Typ in het zoekvak **Halosys**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Selecteer in het deelvenster met resultaten **Halosys**, en klik vervolgens op **Complete** de toepassing toevoegen.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Halosys op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Halosys is voor een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Halosys tot stand worden gebracht.

Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Halosys.

Om te configureren en testen van Azure AD eenmalige aanmelding met Halosys, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Halosys](#creating-a-halosys-test-user)**  - Halosys die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Halosys.


**Voor het configureren van Azure AD eenmalige aanmelding met Halosys, moet u de volgende stappen uitvoeren:**

1. In de klassieke portal op de **Halosys** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.
     
    ![Eenmalige aanmelding configureren][6] 

2. Op de **hoe wilt u dat gebruikers zich aanmelden op Halosys** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Op de **App-instellingen configureren** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. In de **aanmelding op URL** textbox, typ de URL moet worden gebruikt door uw gebruikers eenmalige aanmelding voor uw toepassing Halosys is met het volgende patroon volgen: `https://<company-name>.Halosys.com/client-api/api`.

    b.In de **identificatie-URL** textbox, typ de URL in het volgende patroon volgen: `https://<company-name>.Halosys.com`.   
         
4. Op de **eenmalige aanmelding configureren op Halosys** pagina, klikt u op **metagegevens downloaden**, en sla het bestand op uw computer:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. Neem contact op met het ondersteuningsteam Halosys om SSO is geconfigureerd voor uw toepassing, en geef met de volgende opties:

    • De gedownloade **metagegevensbestand**
    
    • De **SAML SSO-URL**
    

6. In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
    
    ![Azure AD voor eenmalige aanmelding][10]

7. Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
 
    ![Azure AD voor eenmalige aanmelding][11]


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie maakt u een testgebruiker in de klassieke portal Britta Simon aangeroepen.


![Azure AD-gebruiker maken][20]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-portal**, klik op het navigatiedeelvenster links **Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.

3. De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.

    b. De gebruikersnaam **textbox**, type **BrittaSimon**.

    c. Klik op **Volgende**.

6.  Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. In de **voornaam** textbox type **Britta**.  

    b. In de **achternaam** textbox type, **Simon**.

    c. In de **weergavenaam** textbox type **Britta Simon**.

    d. In de **rol** selecteert **gebruiker**.

    e. Klik op **Volgende**.

7. Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Noteer de waarde van de **nieuw wachtwoord**.

    b. Klik op **Voltooien**.   



### <a name="creating-a-halosys-test-user"></a>Een testgebruiker Halosys maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Halosys maken. Neem contact op met het ondersteuningsteam Halosys de gebruikers van het platform Halosys toevoegen.


### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Halosys.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen Halosys, moet u de volgende stappen uitvoeren:**

1. In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Halosys**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Klik in het menu bovenaan op **gebruikers**.

    ![Gebruiker toewijzen][203]

4. Selecteer in de lijst gebruikers **Britta Simon**.

5. Klik in de werkbalk aan de onderkant op **toewijzen**.

    ![Gebruiker toewijzen][205]


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel Halosys in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Halosys.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
