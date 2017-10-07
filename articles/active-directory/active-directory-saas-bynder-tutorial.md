---
title: 'Zelfstudie: Azure Active Directory-integratie met Bynder | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Bynder.
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
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Zelfstudie: Azure Active Directory-integratie met Bynder
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Bynder met Azure Active Directory (Azure AD).

Bynder integreren met Azure AD biedt Hallo volgende voordelen:

* U kunt beheren in Azure AD die tooBynder toegang heeft
* U kunt uw gebruikers tooautomatically get aangemelde tooBynder eenmalige aanmelding (SSO) met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met Bynder tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Een Bynder eenmalige aanmelding (SSO) abonnement ingeschakeld

>[!NOTE]
>tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving. 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Microsoft Azure AD SSO in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Bynder van Hallo-galerie
2. Configureren en testen van Microsoft Azure AD-SSO

## <a name="add-bynder-from-hello-gallery"></a>Bynder van Hallo galerie toevoegen
tooconfigure hello integratie van Bynder in Azure AD, moet u tooadd Bynder uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Bynder via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]
6. Typ in het zoekvak Hallo **Bynder**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Selecteer in het deelvenster resultaten hello, **Bynder**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Hallo-app in de galerie Hallo selecteren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configureren en testen van Microsoft Azure AD-SSO
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Microsoft Azure AD-SSO met Bynder op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Bynder tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Bynder toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Bynder.

tooconfigure en test Microsoft Azure AD-SSO met Bynder, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van eenmalige aanmelding Microsoft Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Bynder](#creating-a-bynder-test-user)**  -toohave een equivalent van Britta Simon in Bynder die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse eenmalige aanmelding Microsoft Azure AD.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuratie van Microsoft Azure AD-SSO
In deze sectie die u kunt Microsoft Azure AD eenmalige aanmelding inschakelen in de klassieke portal Hallo en eenmalige aanmelding in uw toepassing Bynder configureert.

**Microsoft Azure AD-SSO met Bynder, tooconfigure uitvoeren Hallo stappen te volgen:**

1. In de klassieke portal Hallo op Hallo **Bynder** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.
   
    ![Eenmalige aanmelding configureren][6] 
2. Op Hallo **wilt u hoe gebruikers toosign op tooBynder** pagina **Microsoft Azure AD Single Sign-On**, en klik vervolgens op **volgende**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, indien gewenst tooconfigure Hallo toepassing in **IDP geïnitieerd modus**, het uitvoeren van Hallo volgende stappen uit en klik op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Klik op **Volgende**.
4. U kunt eventueel tooconfigure Hallo toepassing in **SP geïnitieerd modus** op Hallo **App-instellingen configureren** dialoogvenster pagina, klikt u op Hallo **'Geavanceerde instellingen (optioneel) weergeven'**en voer vervolgens Hallo **aanmelding op URL** en klik op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.getbynder.com/login/`
  2. Klik op **Volgende**.
  
   >[!NOTE]
   >Hallo-waarde voor Hallo aanmelding op de URL in deze zelfstudie is slechts een placeholfer. tooget hello werkelijke vlaue voor uw omgeving contact op met Bynder.
   >

5. Op Hallo **eenmalige aanmelding configureren op Bynder** pagina, het uitvoeren van Hallo volgende stappen uit en klik op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Klik op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.
  2. Klik op **Volgende**.
6. tooget SSO is geconfigureerd voor uw toepassing contact op met het ondersteuningsteam Bynder. Hallo metagegevens van het gedownloade bestand toevoegen en delen met Bynder team tooset van eenmalige aanmelding op hun kant.
7. In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][10]
8. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
   
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
  2. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
  3. Klik op **Volgende**.
6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. In Hallo **voornaam** textbox type **Britta**.  
  2. In Hallo **achternaam** textbox type, **Simon**. 
  3. In Hallo **weergavenaam** textbox type **Britta Simon**.
  4. In Hallo **rol** selecteert **gebruiker**.
  5. Klik op **Volgende**.
7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
   2. Klik op **Voltooien**.   

### <a name="create-a-bynder-test-user"></a>Een testgebruiker Bynder maken
Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Bynder van een gebruiker. Bynder ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess Bynder gemaakt als deze nog niet bestaat.

>[!NOTE]
>Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello Bynder ondersteuningsteam. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure SSO haar tooBynder toegang verleent.

   ![Gebruiker toewijzen][200]

**tooassign Britta Simon tooBynder, Voer Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][201]
2. Selecteer in de lijst met de toepassingen van Hallo **Bynder**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][203]
4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Microsoft Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo Bynder tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Bynder toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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
