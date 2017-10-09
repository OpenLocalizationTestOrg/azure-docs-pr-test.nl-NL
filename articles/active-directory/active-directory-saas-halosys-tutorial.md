---
title: 'Zelfstudie: Azure Active Directory-integratie met Halosys | Microsoft Docs'
description: Lees hoe toouse Halosys met Azure Active Directory tooenable eenmalige aanmelding, geautomatiseerde inrichting en meer.
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
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Zelfstudie: Azure Active Directory-integratie met Halosys

In deze zelfstudie leert u hoe toointegrate Halosys met Azure Active Directory (Azure AD).

Halosys integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooHalosys toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooHalosys (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Halosys tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Halosys eenmalige aanmelding ingeschakeld abonnement


> [!NOTE] 
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Halosys van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-halosys-from-hello-gallery"></a>Het toevoegen van Halosys van Hallo-galerie
tooconfigure hello integratie van Halosys in Azure AD, moet u tooadd Halosys uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Halosys via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.

    ![Active Directory][1]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.

    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.

    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.

    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **Halosys**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Selecteer in het deelvenster met resultaten Hallo **Halosys**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Halosys op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Halosys is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Halosys toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Halosys.

tooconfigure en eenmalige aanmelding Azure AD-test met Halosys, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Halosys](#creating-a-halosys-test-user)**  -toohave een equivalent van Britta Simon in Halosys die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Halosys.


**Azure AD tooconfigure eenmalige aanmelding met Halosys, Voer Hallo stappen te volgen:**

1. In de klassieke portal Hallo op Hallo **Halosys** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.
     
    ![Eenmalige aanmelding configureren][6] 

2. Op Hallo **wilt u hoe gebruikers toosign op tooHalosys** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour Halosys toepassing met behulp van Hallo patroon volgen: `https://<company-name>.Halosys.com/client-api/api`.

    Hallo b.In **identificatie-URL** textbox, typ de URL van de Hallo in Hallo patroon volgen: `https://<company-name>.Halosys.com`. 
         
4. Op Hallo **eenmalige aanmelding configureren op Halosys** pagina, klikt u op **metagegevens downloaden**, en sla Hallo-bestand op uw computer:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO is geconfigureerd voor uw toepassing, neem contact op met het ondersteuningsteam Halosys en voorzien Hallo volgende:

    • Hallo gedownload **metagegevensbestand**
    
    • Hallo **SAML-URL voor eenmalige aanmelding**
    

6. In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
    
    ![Azure AD voor eenmalige aanmelding][10]

7. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
 
    ![Azure AD voor eenmalige aanmelding][11]


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.


![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.

    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.

    c. Klik op **Volgende**.

6.  Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen: ![maken van een Azure AD-testgebruiker](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. In Hallo **voornaam** textbox type **Britta**.  

    b. In Hallo **achternaam** textbox type, **Simon**.

    c. In Hallo **weergavenaam** textbox type **Britta Simon**.

    d. In Hallo **rol** selecteert **gebruiker**.

    e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.

    b. Klik op **Voltooien**.   



### <a name="creating-a-halosys-test-user"></a>Een testgebruiker Halosys maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Halosys maken. Neem contact op met Halosys support team tooadd Hallo gebruikers in Hallo Halosys platform.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooHalosys toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooHalosys, Voer Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Halosys**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Gebruiker toewijzen][203]

4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.

5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.

    ![Gebruiker toewijzen][205]


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Halosys-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Halosys toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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
