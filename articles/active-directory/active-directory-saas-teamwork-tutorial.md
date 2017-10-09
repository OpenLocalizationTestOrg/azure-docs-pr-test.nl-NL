---
title: 'Zelfstudie: Azure Active Directory-integratie met werken als een team | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en werken als een team.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a>Zelfstudie: Azure Active Directory-integratie met werken als een team

In deze zelfstudie leert u hoe toointegrate werken als een team met Azure Active Directory (Azure AD).

Werken als een team integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTeamwork toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTeamwork (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met werken als een team tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een werken als een team eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van werken als een team van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-teamwork-from-hello-gallery"></a>Het toevoegen van werken als een team van Hallo-galerie
tooconfigure hello integratie van werken als een team in Azure AD, moet u tooadd werken als een team van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd werken als een team via Hallo gallery Hallo stappen uitvoeren:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **werken als een team**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. Selecteer in het deelvenster resultaten hello, **werken als een team**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met werken als een team op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in werken als een team is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in werken als een team toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in werken als een team.

tooconfigure en eenmalige aanmelding Azure AD-test met werken als een team, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker werken als een team](#creating-a-teamwork-test-user)**  -toohave een equivalent van Britta Simon in werken als een team dat is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing werken als een team.

**Azure AD tooconfigure eenmalige aanmelding met werken als een team, voert Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **werken als een team** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. Op Hallo **werken als een team domein en de URL's** sectie in Hallo **aanmelding op URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.teamwork.com`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > Houd er rekening mee dat dit geen Hallo echte waarde is. U hebt deze waarde Hello werkelijke aanmelden URL tooupdate. Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**. Klik vervolgens op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. tooget SSO geconfigureerd voor uw toepassing, neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) en voorzien Hallo gedownload **metagegevens**.
  

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 



### <a name="creating-a-teamwork-test-user"></a>Een testgebruiker werken als een team maken

In deze sectie maakt maken u een gebruiker Britta Simon aangeroepen in werken als een team. Neem contact op met [werken als een team ondersteuningsteam](mailto:support@teamwork.com) tooadd Hallo gebruikers in Hallo werken als een team platform.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooTeamwork toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTeamwork, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **werken als een team**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo werken als een team tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour werken als een team toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png