---
title: 'Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en LinkedIn opzoeken.
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
ms.openlocfilehash: e296431866a8611b30e72f286884890adf0f7e50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Zelfstudie: Azure Active Directory-integratie met LinkedIn Lookup

In deze zelfstudie leert u hoe LinkedIn om Lookup te integreren met Azure Active Directory (Azure AD).

LinkedIn Lookup integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot LinkedIn Lookup heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij LinkedIn Lookup (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met LinkedIn opzoeken, moet u de volgende items:

- Een Azure AD-abonnement
- Een LinkedIn Lookup eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. LinkedIn Lookup uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-linkedin-lookup-from-the-gallery"></a>LinkedIn Lookup uit de galerie toevoegen
Voor het configureren van de integratie van LinkedIn zoeken in Azure AD, moet u LinkedIn Lookup uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen LinkedIn Lookup uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop boven aan het dialoogvenster nieuwe toepassing toevoegen.

    ![Toepassingen][3]

4. Typ in het zoekvak **LinkedIn Lookup**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. Selecteer in het deelvenster resultaten **LinkedIn Lookup**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met LinkedIn opzoeken op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in LinkedIn Lookup is voor een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de zoekactie LinkedIn tot stand worden gebracht.

Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in LinkedIn opzoeken.

Als u wilt configureren en testen Azure AD eenmalige aanmelding met LinkedIn opzoeken, moet u voltooien van de volgende elementen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LinkedIn Lookup](#creating-an-linkedin-lookup-test-user)**  - LinkedIn Lookup die is gekoppeld aan de Azure AD-weergave van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing LinkedIn Lookup configureren.

**Voor het configureren van Azure AD eenmalige aanmelding met LinkedIn opzoeken, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **LinkedIn Lookup** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster in **modus** Selecteer **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. In een ander browservenster aanmelding bij uw **LinkedIn Lookup** website als beheerder.

4. In **Accountcentrum**, klikt u op **globale instellingen** onder **instellingen**. Schakel ook **Lookup** uit de vervolgkeuzelijst.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Klik op **of Klik hier om te laden en afzonderlijke velden van het formulier kopiëren** en kopieer **entiteit-Id** en **Url Assertion Consumer Access (ACS)**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. Op de Azure-portal onder **LinkedIn Lookup domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    a. In de **id** textbox, voer de **entiteit-ID** gekopieerd uit LinkedIn-Portal 

    b. In de **antwoord-URL** textbox, voer de **Assertion Consumer Access (ACS) Url** gekopieerd uit LinkedIn-Portal

7. Controleer **weergeven geavanceerde instellingen voor URL**, als u wilt configureren van de toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Dit is geen echte waarde. De gebruiker heeft deze waarden bijwerken met de werkelijke URL voor eenmalige aanmelding. Neem contact op met [LinkedIn Lookup Client ondersteuningsteam](https://business.LinkedIn.com/lookup) deze waarde op te halen.

8. Uw **LinkedIn Lookup** toepassing de SAML-asserties verwacht in een specifieke indeling. De gebruiker heeft het aangepaste kenmerktoewijzingen toevoegen aan de configuratie van de SAML-token kenmerken. De volgende Schermafbeelding toont een voorbeeld. De standaardwaarde van **gebruikers-id** is **user.userprincipalname** maar LinkedIn Lookup verwacht dit met het e-mailadres van de gebruiker worden toegewezen. U kunt **user.mail** kenmerk uit de lijst of gebruik de juiste kenmerkwaarde op basis van de organisatieconfiguratie van uw. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en kenmerken instellen. De gebruiker moet vier claims met de naam toe te voegen **e**, **afdeling**, **firstname**, en **lastname** en de waarde moet worden toegewezen met **user.mail**, **user.department**, **user.givenname**, en **user.surname** respectievelijk

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | E-mail| User.mail |    
    | Afdeling| User.Department |
    | Voornaam| User.givenName |
    | Achternaam| User.surname |

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    a. Klik op **kenmerk toevoegen** openen de **kenmerk toevoegen** dialoogvenster.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.
    
    c. Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

10. Voer de volgende stappen uit op de **naam** kenmerk -

    a. Klik op het kenmerk openen de **kenmerk bewerken** venster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Verwijder de URL-waarde van de **naamruimte**.
    
    c. Klik op **Ok** om op te slaan van de instelling.

10. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Ga naar **LinkedIn beheerdersinstellingen** sectie. Uploaden van het XML-bestand dat u hebt gedownload van de Azure-portal door te klikken op de **uploaden XML-bestand** optie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Klik op **op** eenmalige aanmelding inschakelen. Status SSO wordt gewijzigd van **niet verbonden** naar **verbonden**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Ga naar **gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Klik op **toevoegen** openen de **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **Britta Simon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Maken van een testgebruiker LinkedIn Lookup

Gekoppelde Lookup toepassing ondersteunt Just in Time (Just in time) gebruikers inrichten en na verificatie gebruikers automatisch in de toepassing gemaakt worden. Activeren **automatisch toewijzen van licenties** een licentie toewijzen aan de gebruiker.
   
   ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan LinkedIn-Lookup.

![Gebruiker toewijzen][200] 

**Als u wilt toewijzen Britta Simon LinkedIn opzoeken, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **LinkedIn Lookup**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.

    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel LinkedIn opzoeken in het deelvenster toegang, moet u naar organisatie pagina waar u de details van uw persoonlijke LinkedIn moet worden omgeleid. Uw persoonlijke account aan uw LinkedIn business-account worden gekoppeld. 

Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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

