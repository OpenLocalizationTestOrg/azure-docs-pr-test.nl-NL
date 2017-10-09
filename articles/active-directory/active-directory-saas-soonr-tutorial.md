---
title: 'Zelfstudie: Azure Active Directory-integratie met Soonr werkplek | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Soonr werkplek.
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
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Zelfstudie: Azure Active Directory-integratie met Soonr werkplek

Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Soonr werkplek met Azure Active Directory (Azure AD).  
Soonr werkplek integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSoonr werkplek heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSoonr werkplek (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Soonr werkplek tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Soonr werkplek eenmalige aanmelding ingeschakeld abonnement


> [!NOTE] 
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD eenmalige aanmelding in een testomgeving.  
Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Soonr werkplek van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Het toevoegen van Soonr werkplek van Hallo-galerie
tooconfigure hello integratie van Soonr werkplek in Azure AD, moet u tooadd Soonr werkplek uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Soonr werkplek via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 

    ![Active Directory][1]

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.

    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.

    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
 
    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **Soonr werkplek**.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Selecteer in het deelvenster met resultaten Hallo **Soonr werkplek**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test eenmalige aanmelding Azure AD bij Soonr werkplek op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Soonr werkplek tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Soonr werkplek toobe tot stand gebracht.  

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Soonr werkplek.

tooconfigure en test eenmalige aanmelding Azure AD bij Soonr werkplek, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Soonr werkplek](#creating-a-soonr-workplace-test-user)**  -toohave een equivalent van Britta Simon in Soonr werkplek die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Soonr werkplek.


**Voer tooconfigure Azure AD eenmalige aanmelding bij Soonr werkplek, Hallo stappen te volgen:**

1. In de klassieke Azure-portal op Hallo Hallo **Soonr werkplek** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**  het dialoogvenster.

    ![Eenmalige aanmelding configureren][6] 

2. Op Hallo **wilt u hoe gebruikers toosign op tooSoonr werkplek** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo volgende stappen uit:.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. In Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Klik op **Volgende**.

    > [!NOTE] 
    > Houd er rekening mee dat dit geen Hallo echte waarde is. U hebt deze waarde Hello werkelijke aanmelden URL tooupdate. Neem contact op met de werkplek Soonr support team tooget deze waarde.

4. Op Hallo **eenmalige aanmelding configureren op de werkplek Soonr** pagina, klikt u op **metagegevens downloaden** en sla Hallo-bestand op uw computer:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO is geconfigureerd voor uw toepassing, neem contact op met het ondersteuningsteam Soonr werkplek en voorzien Hallo volgende: 

    • Hallo gedownload **metagegevens** bestand

    • Hallo **URL-verlener**

    • Hallo **SAML-URL voor eenmalige aanmelding**

    • Hallo **Service-URL met eenmalige Sign-Out**

    >[!NOTE]
    >Deze toepassing wordt vervangen door <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask werkplek</a> en u kunt verwijzen <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">dit</a> zelfstudie voor het configureren van de toepassing hello met Azure AD.
   
6. In de klassieke Azure-portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.

    ![Azure AD voor eenmalige aanmelding][10]

7. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
  
    ![Azure AD voor eenmalige aanmelding][11]



### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in Hallo klassieke Azure-portal Britta Simon aangeroepen.  

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.

    b. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.

    c. Klik op **Volgende**.

6.  Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. In Hallo **voornaam** textbox type **Britta**.  

    b. In Hallo **achternaam** textbox type, **Simon**.

    c. In Hallo **weergavenaam** textbox type **Britta Simon**.

    d. In Hallo **rol** selecteert **gebruiker**.

    e. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.

    b. Klik op **Voltooien**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Maken van een testgebruiker Soonr werkplek

Hallo-doel van deze sectie is toocreate een gebruiker Britta Simon aangeroepen in Soonr werkplek. Neem contact op met de werkplek Soonr support team toocreate een gebruiker in het Hallo-platform. U kunt verhogen Hallo ondersteuningsticket met Soonr van <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">hier</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure eenmalige aanmelding haar toegang tooSoonr werkplek verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSoonr werkplek, Voer Hallo stappen te volgen:**

1. Klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, klik op Hallo Azure **toepassingen** in het bovenste menu Hallo.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Soonr werkplek**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Klik in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Gebruiker toewijzen][203] 

1. Selecteer in de lijst gebruikers Hallo **Britta Simon**.

2. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.

    ![Gebruiker toewijzen][205]



### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.  
Als u op Hallo Soonr werkplek-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Soonr werkplek toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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
