---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn daarvan te leren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Zelfstudie: Azure Active Directory-integratie met LinkedIn Learning

In deze zelfstudie leert u hoe toointegrate LinkedIn Learning met Azure Active Directory (Azure AD).

LinkedIn Learning integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooLinkedIn heeft leren
- U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn inschakelen Learning (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met LinkedIn Learning tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LinkedIn Learning eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van LinkedIn Learning van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Het toevoegen van LinkedIn Learning van Hallo-galerie
tooconfigure hello integratie van LinkedIn Learning in Azure AD, moet u tooadd LinkedIn Learning uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd LinkedIn leren van Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **LinkedIn Learning**. Klik in het deelvenster met resultaten, op **LinkedIn Learning** tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met LinkedIn Learning op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn Learning is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn Learning toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** LinkedIn weten.

tooconfigure en test eenmalige aanmelding Azure AD met LinkedIn Learning, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing LinkedIn Learning.

**Voer tooconfigure Azure AD eenmalige aanmelding met LinkedIn-Learning Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **LinkedIn Learning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. In een ander browservenster, aanmelding tooyour LinkedIn Learning tenant als beheerder.

4. In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**. Schakel ook **Learning - standaard** uit de vervolgkeuzelijst Hallo.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. Op de Azure-portal onder **LinkedIn Learning domein en de URL's**, uitvoeren van de volgende stappen uit als u wilt dat tooconfigure SSO Hallo in **IdP geïnitieerd** modus

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal 

    b. In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal

7. Als u wilt dat tooconfigure SSO in **SP geïnitieerd**, klikt u op geavanceerde URL weergeven instelling optie in de configuratiesectie Hallo en Hallo aanmeldings-URL configureren met Hallo patroon volgen:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. Uw toepassing LinkedIn Learning verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token kenmerken-configuratie is vereist. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. Hallo standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Learning deze toobe toegewezen met e-mailadres van de gebruiker Hallo verwacht. Die u kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen. Hallo-gebruiker moet vier tooadd-claims met de naam **e**, **afdeling**, **firstname**, en **lastname** en Hallo-waarde is toegewezen met toobe **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | E-mail| User.mail |    
    | Afdeling| User.Department |
    | Voornaam| User.givenName |
    | Achternaam| User.surname |
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Klik op **kenmerk toevoegen** dialoogvenster tooopen Hallo-kenmerk.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

10. Uitvoeren van de volgende stappen uit op Hallo Hallo **naam** kenmerk -

    a. Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Hallo URL waarde verwijderen uit Hallo **naamruimte**.
    
    c. Klik op **Ok** toosave Hallo-instelling.

11. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Klik op **Opslaan**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Ga te**LinkedIn beheerdersinstellingen** sectie. Hallo XML-bestand die u hebt gedownload van hello Azure-portal door te klikken op de optie Hallo uploaden XML-bestand uploaden.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Klik op **op** tooenable eenmalige aanmelding. Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Een testgebruiker LinkedIn Learning maken

Gekoppelde Learning toepassing ondersteunt. Alleen bij tijd gebruikers inrichten en na verificatie zijn gebruikers in de toepassing hello automatisch gemaakt. Op Hallo beheerder instellingenpagina op Hallo LinkedIn Learning portal spiegelen Hallo switch **automatisch toewijzen van licenties** tooactive tooenable NET tijd inrichten en dit wordt ook een licentie toohello gebruiker toewijzen.
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLinkedIn leren.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLinkedIn leren, Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **LinkedIn Learning**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo LinkedIn Learning tegel in Hallo Toegangsvenster, krijgt u hello Azure aanmelding pagina en op na geslaagde aanmelding, krijgt u in uw toepassing LinkedIn Learning.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png