---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LinkedIn opzoeken.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup

In deze zelfstudie leert u hoe toointegrate LinkedIn Lookup met Azure Active Directory (Azure AD).

LinkedIn Lookup integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooLinkedIn Lookup heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooLinkedIn Lookup (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met LinkedIn Lookup tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LinkedIn Lookup eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van LinkedIn Lookup van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>Het toevoegen van LinkedIn Lookup van Hallo-galerie
tooconfigure hello integratie van LinkedIn zoeken in Azure AD, moet u tooadd LinkedIn Lookup uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd LinkedIn Lookup via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop bovenaan Hallo van Hallo dialoogvenster tooadd nieuwe toepassing.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **LinkedIn Lookup**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. Selecteer in het deelvenster resultaten hello, **LinkedIn Lookup**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met LinkedIn opzoeken op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LinkedIn Lookup is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in LinkedIn Lookup toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in LinkedIn opzoeken.

tooconfigure en eenmalige aanmelding Azure AD-test met LinkedIn opzoeken, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**  -toohave een equivalent van Britta Simon in LinkedIn Lookup die is gekoppeld toohello Azure AD-weergave.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LinkedIn Lookup configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met LinkedIn-Lookup, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **LinkedIn Lookup** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster in **modus** Selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. In een andere web-browservenster aanmelding tooyour **LinkedIn Lookup** website als beheerder.

4. In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**. Schakel ook **Lookup** uit de vervolgkeuzelijst Hallo.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Klik op **of Klik hier tooload en kopieert u afzonderlijke velden uit Hallo formulier** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. Op de Azure-portal onder **LinkedIn Lookup domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. In Hallo **id** textbox Voer Hallo **entiteit-ID** gekopieerd uit LinkedIn-Portal 

    b. In Hallo **antwoord-URL** textbox Voer Hallo **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal

7. Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Dit is geen echte waarde. Hallo gebruiker heeft tooupdate deze waarden Hello werkelijke aanmeldings-URL. Neem contact op met [LinkedIn Lookup Client ondersteuningsteam](https://business.LinkedIn.com/lookup) tooget deze waarde.

8. Uw **LinkedIn Lookup** toepassing hello SAML asserties verwacht in een specifieke indeling. Hallo gebruiker heeft tooadd aangepast kenmerk toewijzingen toohello SAML-token kenmerkconfiguratie. Hallo volgende Schermafbeelding toont een voorbeeld. Hallo standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Lookup deze toobe toegewezen met e-mailadres van de gebruiker Hallo verwacht. U kunt **user.mail** kenmerk uit de lijst Hallo of Hallo juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw gebruiken. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en Hallo kenmerken instellen. Hallo-gebruiker moet vier tooadd-claims met de naam **e**, **afdeling**, **firstname**, en **lastname** en Hallo-waarde is toegewezen met toobe **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | E-mail| User.mail |    
    | Afdeling| User.Department |
    | Voornaam| User.givenName |
    | Achternaam| User.surname |

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Klik op **kenmerk toevoegen** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

10. Uitvoeren van de volgende stappen uit op Hallo Hallo **naam** kenmerk -

    a. Klik op Hallo kenmerk tooopen hello **kenmerk bewerken** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Hallo URL waarde verwijderen uit Hallo **naamruimte**.
    
    c. Klik op **Ok** toosave Hallo-instelling.

10. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla Hallo XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Ga te**LinkedIn beheerdersinstellingen** sectie. U hebt gedownload van hello Azure-portal door te klikken op Hallo van uploaden Hallo XML-bestand **uploaden XML-bestand** optie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Klik op **op** tooenable eenmalige aanmelding. Status SSO wordt gewijzigd van **niet verbonden** te**verbonden**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Klik op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **Britta Simon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Maken van een testgebruiker LinkedIn Lookup

Gekoppelde Lookup toepassing ondersteunt Just in Time (Just in time) gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing hello gemaakt worden. Activeren **automatisch toewijzen van licenties** tooassign een licentie toohello gebruiker.
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooLinkedIn opzoeken.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLinkedIn-Lookup, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **LinkedIn Lookup**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.

    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u op Hallo LinkedIn Lookup-tegel in Hallo toegangsvenster klikt, moet u omgeleide tooOrganizational pagina waar u tooprovide de details van uw persoonlijke LinkedIn hebt. Uw persoonlijke account aan uw LinkedIn business-account worden gekoppeld. 

Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

