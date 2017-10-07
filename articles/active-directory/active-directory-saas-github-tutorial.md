---
title: 'Zelfstudie: Azure Active Directory-integratie met GitHub | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Zelfstudie: Azure Active Directory-integratie met GitHub

In deze zelfstudie leert u hoe toointegrate GitHub met Azure Active Directory (Azure AD).

GitHub integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooGitHub toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooGitHub (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met GitHub, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een GitHub-eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van GitHub van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-github-from-hello-gallery"></a>Het toevoegen van GitHub van Hallo-galerie
tooconfigure hello integratie van GitHub in Azure AD, moet u tooadd GitHub uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd GitHub via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **GitHub.com**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. Selecteer in het deelvenster resultaten hello, **GitHub**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met GitHub op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in GitHub is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in GitHub toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in GitHub.

tooconfigure en eenmalige aanmelding Azure AD-test met GitHub, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker GitHub](#creating-a-GitHub-test-user)**  -toohave een equivalent van Britta Simon in GitHub die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw GitHub-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met GitHub, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **GitHub** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. Op Hallo **GitHub-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://github.com/orgs/<entity-id>/sso`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden met Hallo werkelijke Kana-URL en id tooupdate. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id. Ga tooGitHub Admin sectie tooretrieve deze waarden. 

4. Op Hallo **gebruikerskenmerken** sectie **gebruikers-id** als user.mail.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. Op Hallo **nieuw certificaat maken** dialoogvenster, klikt u op Hallo agenda-pictogram en selecteer een **vervaldatum**. Klik vervolgens op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. Op Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Op Hallo pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. Op Hallo **GitHub configuratie** sectie, klikt u op **configureren GitHub** tooopen **eenmalige aanmelding configureren** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. Meld u in een ander browservenster in uw organisatie GitHub site als beheerder.

12. Navigeer te**instellingen** en klik op **beveiliging**

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Controleer Hallo **inschakelen SAML-verificatie** vak Hallo Single Sign-on configuratievelden weer te geven. Gebruik vervolgens Hallo eenmalige aanmelding URL waarde tooupdate Hallo één aanmeldings-URL op Azure AD-configuratie.

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Hallo velden volgende configureren:

    a. **Meld u aan op de URL voor**: Voer **SAML eenmalige aanmelding Service-URL** van Hallo **GitHub configureren** sectie over Azure AD

    b. **Certificaatverlener**: Voer **SAML entiteit-ID** van Hallo **GitHub configureren** sectie over Azure AD

    c. **Openbaar certificaat**: Open Hallo certificaat gedownload vanuit Azure AD in Kladblok en kopieer Hallo inhoud zoals 'BEGIN CERTIFICATE' en 'END CERTIFICATE'

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Klik op **Test SAML-configuratie** tooconfirm die geen validatiefouten of fouten tijdens eenmalige aanmelding.

    ![Instellingen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Klik op **opslaan**

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 


### <a name="creating-a-github-test-user"></a>De gebruiker van een GitHub-test maken

In de volgorde tooenable Azure AD gebruikers toolog in GitHub, moeten ze worden ingericht in GitHub.  
In geval van GitHub Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Aanmelden tooyour GitHub bedrijf site als beheerder.

2. Klik op **mensen**.

    ![Mensen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "personen")

3. Klik op **uitnodiging lid**.

    ![Gebruikers uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "gebruikers uitnodigen")

4. Op Hallo **uitnodiging lid** dialoogvenster pagina, voert u Hallo stappen te volgen:

    a. In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.

    ![Personen uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "personen uitnodigen")
    
    b. Klik op **uitnodiging**.

    ![Personen uitnodigen](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "personen uitnodigen")

    > [!NOTE]
    > Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooGitHub toegang verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooGitHub, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **GitHub.com**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    


### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo GitHub-tegel in Hallo Toegangsvenster, krijgt u aangemelde tooyour GitHub-toepassing. U moet als een organisatie-account maar moeten toolog worden aanmelden met uw persoonlijke account.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
