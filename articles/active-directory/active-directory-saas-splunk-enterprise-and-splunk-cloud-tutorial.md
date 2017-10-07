---
title: 'Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Splunk Enterprise en Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Zelfstudie: Azure Active Directory-integratie met Splunk Enterprise en Splunk Cloud

In deze zelfstudie leert u hoe toointegrate Splunk Enterprise en Splunk Cloud met Azure Active Directory (Azure AD).

Splunk Enterprise en Splunk Cloud integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang heeft tooSplunk Enterprise en Splunk Cloud
- U kunt uw gebruikers tooautomatically get aangemelde tooSplunk Enterprise en Splunk Cloud eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Splunk Enterprise en Splunk Cloud tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Splunk Enterprise of Splunk Cloud SSO ingeschakeld abonnement


>[!NOTE]
>tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.
>

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Splunk Enterprise en Splunk Cloud toe te voegen uit Hallo-galerie
2. Configureren en testen van Azure AD-SSO


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Splunk Enterprise en Splunk Cloud uit Hallo galerie toevoegen
tooconfigure hello integratie van Splunk Enterprise en Splunk Cloud met Azure AD, moet u tooadd Splunk Enterprise en Splunk Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Splunk Enterprise en Splunk Cloud uit de galerie hello, voert Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.

    ![Active Directory][1]

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.

    ![Toepassingen][2]

4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.

    ![Toepassingen][3]

5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.

    ![Toepassingen][4]

6. Typ in het zoekvak Hallo **Splunk Enterprise of Splunk Cloud**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Selecteer in het deelvenster met resultaten Hallo **Splunk Enterprise en Splunk Cloud**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Splunk voor ondernemingen en Splunk Cloud op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Splunk Enterprise en Splunk Cloud is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Splunk Enterprise en Splunk Cloud toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Splunk Enterprise en Splunk Cloud.

tooconfigure en eenmalige aanmelding Azure AD-test met Splunk Enterprise en Splunk Cloud, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Splunk Enterprise en Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave een equivalent van Britta Simon in de onderneming Splunk en Splunk Cloud die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in de klassieke portal Hallo en eenmalige aanmelding configureren in uw toepassing Splunk Enterprise en Splunk Cloud.


**tooconfigure eenmalige aanmelding Azure AD met Splunk Enterprise en Splunk Cloud, Voer Hallo stappen te volgen:**

1. In de klassieke portal Hallo op Hallo **Splunk Enterprise en Splunk Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On** dialoogvenster.
     
    ![Eenmalige aanmelding configureren][6] 

2. Op Hallo **hoe wilt u dat gebruikers toosign op tooSplunk Enterprise en Splunk Cloud** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. In Hallo **aanmelding op URL** textbox type Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour Splunk Enterprise en Splunk cloudtoepassing met Hallo patroon volgen:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. In Hallo **id** textbox type Hallo-URL van uw Splunk Server.
  3. In Hallo **antwoord-URL** textbox, typ de URL van de Hallo Hello patroon volgen:`https://<splunkserver>/saml/acs`
  4. Klik op **Volgende**.
 
4. Op Hallo **op Splunk Enterprise- en Splunk Cloud eenmalige aanmelding configureren** pagina, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Klik op **metagegevens downloaden**, en sla Hallo-bestand op uw computer.
  2. Klik op **Volgende**.

5. tooget SSO is geconfigureerd voor uw toepassing contact opnemen met Splunk Enterprise en Splunk Cloud ondersteuningsteam en voorzien Hallo volgende:

    * Hallo gedownload **federaton metagegevens**
6. In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
    
    ![Azure AD voor eenmalige aanmelding][10]

7. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
 
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie kunt u een testgebruiker maken in de klassieke portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.

3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
  2. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
  3. Klik op **Volgende**.

6.  Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:
  
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. In Hallo **voornaam** textbox type **Britta**.  
  2. In Hallo **achternaam** textbox type, **Simon**.
  3. In Hallo **weergavenaam** textbox type **Britta Simon**.
  4. In Hallo **rol** selecteert **gebruiker**.
  5. Klik op **Volgende**.

7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
  2. Klik op **Voltooien**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Een Splunk Enterprise en Splunk Cloud testgebruiker maken

In deze sectie maakt u een gebruiker met de naam Britta Simon in de onderneming Splunk en Splunk Cloud. Neem contact op met Splunk Enterprise en Splunk Cloud support team tooadd Hallo gebruikers in Hallo Splunk Enterprise en Splunk Cloud-platform.


### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie maakt inschakelen u Britta Simon toouse Azure SSOy verlenen haar toegang tooSplunk Enterprise en Splunk Cloud.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSplunk Enterprise en Splunk Cloud uitvoeren Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Splunk Enterprise en Splunk Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.

    ![Gebruiker toewijzen][203]

4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.

5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.

    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD-SSOonfiguration Hallo Toegangsvenster met testen.

Wanneer u hello Splunk Enterprise- en Splunk Cloud-tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Splunk Enterprise en Splunk Cloud-toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
