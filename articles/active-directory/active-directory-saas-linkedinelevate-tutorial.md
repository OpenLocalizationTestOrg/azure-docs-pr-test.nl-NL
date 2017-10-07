---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn uitbreiden | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn uitbreiden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Zelfstudie: Azure Active Directory-integratie met LinkedIn uitbreiden

In deze zelfstudie leert u hoe toointegrate LinkedIn uitbreiden met Azure Active Directory (Azure AD).

LinkedIn bevoegdheden integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooLinkedIn uitbreiden heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn uitbreiden (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met LinkedIn uitbreiden, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LinkedIn bevoegdheden eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van LinkedIn worden de bevoegdheden van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Het toevoegen van LinkedIn worden de bevoegdheden van Hallo-galerie
tooconfigure hello integratie van LinkedIn bevoegdheden in Azure AD, moet u tooadd LinkedIn worden de bevoegdheden van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd LinkedIn bevoegdheden uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **LinkedIn bevoegdheden**. Klik in het deelvenster met resultaten, op **LinkedIn bevoegdheden** tooadd Hallo toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met LinkedIn worden de bevoegdheden op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn worden de bevoegdheden is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn bevoegdheden toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LinkedIn uitbreiden.

tooconfigure en eenmalige aanmelding Azure AD-test met LinkedIn uitbreiden, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LinkedIn bevoegdheden](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing LinkedIn uitbreiden.

**Voer tooconfigure Azure AD eenmalige aanmelding met de bevoegdheden LinkedIn, Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **LinkedIn bevoegdheden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. In een ander browservenster, aanmelding tooyour tenant LinkedIn bevoegdheden als beheerder.

4. In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**. Schakel ook **uitbreiden - AAD-Test worden de bevoegdheden** uit de vervolgkeuzelijst Hallo.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. Op de Azure-Portal onder **LinkedIn bevoegdheden domein en de URL's**, uitvoeren van de volgende stappen uit als u wilt dat tooconfigure SSO Hallo in **IdP geïnitieerd** modus

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    a. In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal 

    b. In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal

7. Als u wilt dat tooconfigure SSO in **SP geïnitieerd**, klikt u op geavanceerde URL weergeven instelling optie in de configuratiesectie Hallo en Hallo aanmeldingsopties configureren op de URL voor Hello patroon volgen:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. Uw toepassing LinkedIn bevoegdheden verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. de standaardwaarde van Hallo **gebruikers-id** is **user.userprincipalname** , maar deze toobe toegewezen met e-mailadres van de gebruiker Hallo LinkedIn bevoegdheden verwacht. Die u kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen. U moet tooadd een andere claim met de naam **afdeling** en Hallo-waarde moet toobe te toegewezen**user.department**.

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |    
    | Afdeling| User.Department |

      ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      a. Klik op de detailpagina toevoegen kenmerk tooopen Hallo kenmerk Hallo afdeling kenmerk toevoegen, zoals hieronder-

      ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Klik op **Ok** toosave Hallo-kenmerk.

      c. Hallo naam wijzigen van Hallo kenmerk **emailaddress** te**e**.


10. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Klik op **Opslaan**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Ga te**LinkedIn beheerdersinstellingen** sectie. Hallo XML-bestand die u zojuist hebt gedownload van hello Azure-portal door te klikken op Hallo optie uploaden XML-bestand uploaden.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Klik op **op** tooenable eenmalige aanmelding. Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Maken van een testgebruiker LinkedIn uitbreiden

Gekoppelde bevoegdheden toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing hello automatisch gemaakt. Op Hallo beheerder instellingenpagina op Hallo LinkedIn bevoegdheden portal spiegelen Hallo switch **automatisch toewijzen van licenties** tooactive tooenable NET tijd inrichten en dit wordt ook een licentie toohello gebruiker toewijzen.

   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door toe te kennen haar toegang tooLinkedIn uitbreiden.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLinkedIn uitbreiden, Voer Hallo stappen te volgen:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **LinkedIn bevoegdheden**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo LinkedIn bevoegdheden tegel in Hallo Toegangsvenster, krijgt u hello Azure aanmelding pagina en op na geslaagde aanmelding, krijgt u in uw toepassing LinkedIn uitbreiden.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Zelfstudie: LinkedIn bevoegdheden configureren voor automatisch gebruikers inrichten met Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
