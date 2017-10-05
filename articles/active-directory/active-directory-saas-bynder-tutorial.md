---
title: 'Zelfstudie: Azure Active Directory-integratie met Bynder | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Bynder.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Zelfstudie: Azure Active Directory-integratie met Bynder
Er is het doel van deze zelfstudie leert u Bynder integreren met Azure Active Directory (Azure AD).

Bynder integreren met Azure AD biedt de volgende voordelen:

* U kunt beheren in Azure AD die toegang tot Bynder heeft
* U kunt uw gebruikers automatisch ophalen aangemeld bij Bynder eenmalige aanmelding (SSO) met hun Azure AD-accounts inschakelen
* U kunt uw accounts op één centrale locatie - en de klassieke Azure portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Voor het configureren van Azure AD-integratie met Bynder, moet u de volgende items:

* Een Azure AD-abonnement
* Een Bynder eenmalige aanmelding (SSO) abonnement ingeschakeld

>[!NOTE]
>Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving. 
> 

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
Het doel van deze zelfstudie is zodat u kunt Microsoft Azure AD SSO testen in een testomgeving.

Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Bynder uit de galerie toevoegen
2. Configureren en testen van Microsoft Azure AD-SSO

## <a name="add-bynder-from-the-gallery"></a>Bynder uit de galerie toevoegen
Voor het configureren van de integratie van Bynder in Azure AD, moet u Bynder uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Bynder uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**. 
   
    ![Active Directory][1]
2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.
3. De weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
    ![Toepassingen][2]
4. Klik op **toevoegen** aan de onderkant van de pagina.
   
    ![Toepassingen][3]
5. Op de **wat wilt u doen** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie**.
   
    ![Toepassingen][4]
6. Typ in het zoekvak **Bynder**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Selecteer in het deelvenster resultaten **Bynder**, en klik vervolgens op **Complete** de toepassing toevoegen.
   
    ![De app selecteren in de galerie](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configureren en testen van Microsoft Azure AD-SSO
Het doel van deze sectie is het beschreven hoe u met het configureren en testen van Microsoft Azure AD-SSO met Bynder op basis van een testgebruiker 'Britta Simon' genoemd.

Azure AD moet weten wat de gebruiker van het bijbehorende equivalent in Bynder aan een gebruiker in Azure AD is voor eenmalige aanmelding werkt. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Bynder tot stand worden gebracht.

Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Bynder.

Als u wilt configureren en testen van Microsoft Azure AD-SSO met Bynder, moet u de volgende elementen voltooid:

1. **[Configureren van eenmalige aanmelding Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Microsoft Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Bynder](#creating-a-bynder-test-user)**  - Bynder die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Microsoft Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuratie van Microsoft Azure AD-SSO
In deze sectie maakt u Microsoft Azure AD eenmalige aanmelding inschakelen in de klassieke portal en eenmalige aanmelding configureren in uw toepassing Bynder.

**Als u wilt Microsoft Azure AD-SSO met Bynder configureert, moet u de volgende stappen uitvoeren:**

1. In de klassieke portal op de **Bynder** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** openen de **configureren Single Sign-On** dialoogvenster.
   
    ![Eenmalige aanmelding configureren][6] 
2. Op de **hoe wilt u dat gebruikers zich aanmelden op Bynder** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Op de **App-instellingen configureren** dialoogvenster pagina als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, voer de volgende stappen uit en klik op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Klik op **Volgende**.
4. Als u wilt configureren van de toepassing in **SP geïnitieerd modus** op de **App-instellingen configureren** dialoogvenster pagina, klikt u op de **"Weergeven geavanceerde instellingen (optioneel)"** en voer vervolgens de **aanmelding op URL** en klik op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.getbynder.com/login/`
  2. Klik op **Volgende**.
  
   >[!NOTE]
   >De waarde voor de aanmelding op de URL in deze zelfstudie is slechts een placeholfer. Als u de werkelijke vlaue voor uw omgeving, contact op met Bynder.
   >

5. Op de **eenmalige aanmelding configureren op Bynder** pagina, voer de volgende stappen uit en klik op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Klik op **metagegevens downloaden**, en sla het bestand op uw computer.
  2. Klik op **Volgende**.
6. Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, contact op met het ondersteuningsteam Bynder. Het metagegevensbestand van de gedownloade koppelen en delen met Bynder team voor het instellen van eenmalige aanmelding op hun kant.
7. In de klassieke portal, selecteert u de configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][10]
8. Op de **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
   
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de klassieke portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **klassieke Azure-Portal**, klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.
3. De lijst met gebruikers, in het menu bovenaan, klikt u op **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Openen van de **gebruiker toevoegen** dialoogvenster op de werkbalk aan de onderkant, klikt u op **gebruiker toevoegen**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Op de **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
  2. De gebruikersnaam **textbox**, type **BrittaSimon**.
  3. Klik op **Volgende**.
6. Op de **gebruikersprofiel** dialoogvenster pagina, voert u de volgende stappen uit:
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. In de **voornaam** textbox type **Britta**.  
  2. In de **achternaam** textbox type, **Simon**. 
  3. In de **weergavenaam** textbox type **Britta Simon**.
  4. In de **rol** selecteert **gebruiker**.
  5. Klik op **Volgende**.
7. Op de **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Op de **tijdelijk wachtwoord** dialoogvenster pagina, voert u de volgende stappen uit:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Noteer de waarde van de **nieuw wachtwoord**.
   2. Klik op **Voltooien**.   

### <a name="create-a-bynder-test-user"></a>Een testgebruiker Bynder maken
Het doel van deze sectie is het maken van een gebruiker Britta Simon in Bynder genoemd. Bynder ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot Bynder als deze nog niet bestaat.

>[!NOTE]
>Als u een gebruiker handmatig maken wilt, moet u contact op met het ondersteuningsteam Bynder. 
> 

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen
Het doel van deze sectie is het Britta Simon Bynder haar toegang verlenen voor het gebruik van Azure eenmalige aanmelding inschakelen.

   ![Gebruiker toewijzen][200]

**Britta Simon om aan te wijzen Bynder, moet u de volgende stappen uitvoeren:**

1. In de klassieke portal, de weergave toepassingen in de directoryweergave, klikt u op **toepassingen** in het menu bovenaan.
   
    ![Gebruiker toewijzen][201]
2. Selecteer in de lijst met toepassingen **Bynder**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Klik in het menu bovenaan op **gebruikers**.
   
    ![Gebruiker toewijzen][203]
4. Selecteer in de lijst gebruikers **Britta Simon**.
5. Klik in de werkbalk aan de onderkant op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding
Het doel van deze sectie is het testen van uw Microsoft Azure AD SSO-configuratie met behulp van het toegangsvenster.

Als u op de tegel Bynder in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Bynder.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
