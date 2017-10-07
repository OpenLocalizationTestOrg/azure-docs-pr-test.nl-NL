---
title: 'Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Wizergos productiviteitssoftware.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Zelfstudie: Azure Active Directory-integratie met Wizergos productiviteitssoftware
Hallo-doel van deze zelfstudie is tooshow u hoe toointegrate Wizergos productiviteitssoftware met Azure Active Directory (Azure AD).

Wizergos productiviteitssoftware integreren met Azure AD biedt Hallo volgende voordelen:

* U kunt beheren in Azure AD wie toegang tot tooWizergos productiviteitssoftware heeft
* U kunt uw gebruikers tooautomatically get aangemelde tooWizergos productiviteitssoftware eenmalige aanmelding (SSO) inschakelen met hun Azure AD-accounts
* U kunt uw accounts op één centrale locatie - Hallo klassieke Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met Wizergos productiviteitssoftware tooconfigure, moet u Hallo volgende items:

* Een Azure AD-abonnement
* Een abonnement Wizergos productiviteit Software SSO-ingeschakeld

>[!NOTE]
>tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving. 
> 

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

* U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
* Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
Hallo-doel van deze zelfstudie is tooenable u tootest Azure AD-eenmalige aanmelding in een testomgeving.

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Wizergos productiviteitssoftware van Hallo-galerie
2. Configureren en testen van Azure AD-SSO

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Het toevoegen van Wizergos productiviteitssoftware van Hallo-galerie
tooconfigure hello integratie van Software voor Wizergos productiviteit in Azure AD, moet u tooadd Wizergos productiviteitssoftware uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Wizergos productiviteitssoftware uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**. 
   
    ![Active Directory][1]
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. tooopen hello toepassingen weergeven in de weergave van de directory hello, klikt u op **toepassingen** in het bovenste menu Hallo.
   
    ![Toepassingen][2]
4. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Toepassingen][3]
5. Op Hallo **wat wilt u wilt toodo** dialoogvenster, klikt u op **toevoegen van een toepassing uit de galerie Hallo**.
   
    ![Toepassingen][4]
6. Typ in het zoekvak Hallo **Wizergos productiviteitssoftware**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. Selecteer in het deelvenster resultaten hello, **Wizergos productiviteitssoftware**, en klik vervolgens op **Complete** tooadd Hallo-toepassing.
   
    ![Hallo-app in de galerie Hallo selecteren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configureren en testen van Azure AD-SSO
Hallo-doel van deze sectie is tooshow u hoe tooconfigure en test Azure AD-SSO met Wizergos productiviteitssoftware op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in Wizergos productiviteitssoftware tooan gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Wizergos productiviteitssoftware toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Wizergos productiviteitssoftware.

tooconfigure en eenmalige aanmelding Azure AD-test met BynWizergos productiviteit Softwareder, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van eenmalige aanmelding Azure AD](#configuring-azure-ad-single-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Wizergos productiviteitssoftware](#creating-a-wizergos-productivity-software-test-user)**  -toohave een equivalent van Britta Simon in Wizergos productiviteitssoftware die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-sso"></a>Configuratie van Azure AD-SSO
In deze sectie Azure AD eenmalige aanmelding in de klassieke portal Hallo inschakelen en configureren van eenmalige aanmelding in uw toepassing Wizergos productiviteit.

**tooconfigure eenmalige aanmelding Azure AD met Wizergos productiviteitssoftware, Voer Hallo stappen te volgen:**

1. In de klassieke portal Hallo op Hallo **Wizergos productiviteitssoftware** toepassing Integratiepagina, klikt u op **eenmalige aanmelding configureren** tooopen hello **configureren Single Sign-On**dialoogvenster.
   
    ![Eenmalige aanmelding configureren][6] 
2. Op Hallo **wilt u hoe gebruikers toosign op tooWizergos productiviteitssoftware** pagina **Azure AD Single Sign-On**, en klik vervolgens op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. Op Hallo **App-instellingen configureren** dialoogvenster pagina, klikt u op **volgende**:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. Op Hallo **eenmalige aanmelding op Wizergos productiviteitssoftware configureren** pagina, klikt u op **certificaat downloaden**, en sla Hallo-bestand op uw computer:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. In een ander browservenster, aanmelding tooyour Wizergos productiviteitssoftware tenant als beheerder.
6. Hallo hamburger menu en selecteer **Admin**.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Selecteer in de beheerpagina linkerkant menu **verificatie** en klik op **Azure AD**.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Uitvoeren van de volgende stappen uit op Hallo **verificatie** sectie.
   
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Klik op **uploaden** knop tooupload Hallo certificaat gedownload vanuit Azure AD. 
  2. In Hallo **URL-verlener** textbox plaatsen Hallo-waarde van **URL-verlener** van de configuratiewizard voor Azure AD-toepassing.
  3. In Hallo **-URL met eenmalige aanmelding** textbox plaatsen Hallo-waarde van **één Service-URL aanmelding** van de configuratiewizard voor Azure AD-toepassing.
  4. In Hallo **-URL met eenmalige Sign-Out** textbox plaatsen Hallo-waarde van **Service-URL met eenmalige Sign-out** van de configuratiewizard voor Azure AD-toepassing.
  5. Klik op **opslaan** knop.
9. In de klassieke portal hello, selecteert u Hallo configuratie voor één aanmelding bevestiging en klik vervolgens op **volgende**.
   
    ![Azure AD voor eenmalige aanmelding][10]
10. Op Hallo **eenmalige aanmelding bevestiging** pagina, klikt u op **Complete**.  
    
    ![Azure AD voor eenmalige aanmelding][11]

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in de klassieke portal Hallo Britta Simon aangeroepen.

![Azure AD-gebruiker maken][20]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **klassieke Azure-Portal**, op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
3. Klik op toodisplay Hallo lijst van gebruikers, in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. Hallo tooopen **gebruiker toevoegen** dialoogvenster in Hallo-werkbalk op Hallo onder, klikt u op **gebruiker toevoegen**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. Op Hallo **Vertel ons meer over deze gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. Selecteer de nieuwe gebruiker in uw organisatie als Type gebruiker.
  2. In Hallo gebruikersnaam **textbox**, type **BrittaSimon**.
  3. Klik op **Volgende**.
6. Op Hallo **gebruikersprofiel** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. In Hallo **voornaam** textbox type **Britta**.  
  2. In Hallo **achternaam** textbox type, **Simon**.
  3. In Hallo **weergavenaam** textbox type **Britta Simon**.
  4. In Hallo **rol** selecteert **gebruiker**.
  5. Klik op **Volgende**.
7. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, klikt u op **maken**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. Op Hallo **tijdelijk wachtwoord** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Schrijf Hallo-waarde van Hallo **nieuw wachtwoord**.
  2. Klik op **Voltooien**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Een testgebruiker Wizergos productiviteitssoftware maken
In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Wizergos productiviteitssoftware maken. Neem contact op met het ondersteuningsteam Wizergos productiviteitssoftware via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd Hallo gebruikers in Hallo Wizergos productiviteitssoftware platform.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Hallo-doel van deze sectie is tooenabling Britta Simon toouse Azure SSO verleent haar toegang tooWizergos productiviteitssoftware.

  ![Gebruiker toewijzen][200]

**tooassign Britta Simon tooWizergos productiviteitssoftware, Voer Hallo stappen te volgen:**

1. Klik op Hallo klassieke portal tooopen Hallo toepassingen weergeven in de weergave van de directory hello, **toepassingen** in het bovenste menu Hallo.
   
    ![Gebruiker toewijzen][201]
2. Selecteer in de lijst met de toepassingen van Hallo **Wizergos productiviteitssoftware**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. Klik in het menu bovenaan Hallo Hallo **gebruikers**.
   
    ![Gebruiker toewijzen][203]
4. Selecteer in de lijst gebruikers Hallo **Britta Simon**.
5. Klik in de werkbalk Hallo Hallo onder, op **toewijzen**.
   
    ![Gebruiker toewijzen][205]

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding
Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo Wizergos productiviteitssoftware tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Wizergos productiviteit softwaretoepassing.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
