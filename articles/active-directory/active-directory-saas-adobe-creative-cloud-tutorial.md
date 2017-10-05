---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 3d13608612c77236346b0e98551d7fc427d602e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud

In deze zelfstudie leert u hoe Adobe Creative Cloud integreren met Azure Active Directory (Azure AD).

Adobe Creative Cloud integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Adobe Creative Cloud heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij Adobe Creative Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Adobe Creative Cloud, moet u de volgende items:

- Een Azure AD-abonnement
- Een Adobe Creative Cloud eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Adobe Creative Cloud uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-adobe-creative-cloud-from-the-gallery"></a>Adobe Creative Cloud uit de galerie toevoegen
Voor het configureren van de integratie van Adobe Creative Cloud met Azure AD, moet u Adobe Creative Cloud uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Adobe Creative Cloud uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak **Adobe Creative Cloud**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Selecteer in het deelvenster resultaten **Adobe Creative Cloud**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Adobe Creative Cloud op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Adobe Creative Cloud is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Adobe Creative Cloud worden gemaakt.

Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Adobe Creative Cloud.

Om te configureren en testen van Azure AD eenmalige aanmelding met Adobe Creative Cloud, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**  : een equivalent van Britta Simon in Adobe Creative Cloud die is gekoppeld aan de Azure AD-representatie van haar hebben.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Adobe Creative Cloud.

**Om eenmalige aanmelding Azure AD met Adobe Creative Cloud configureert, moet u de volgende stappen uitvoeren:**

1. In de Azure-beheerportal op de **Adobe Creative Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Op de **Adobe Creative Cloud-domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. In de **id** textbox, typ de waarde als:`https://www.okta.com/saml2/service-provider/<token>`

    b. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet de werkelijke waarden zijn. U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL. Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id. Als u een gebruiker handmatig maken wilt, moet u contact op met het ondersteuningsteam van Adobe Creative Cloud.

4. Op de **Adobe Creative Cloud-domein en de URL's** sectie, voert u de volgende stappen uit als u wilt configureren, de toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Klik op de **weergeven geavanceerde instellingen voor URL** optie

    b. In de **aanmeldings-URL** textbox, typ de waarde als:`https://adobe.com`

5. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Op de **Adobe Creative Cloudconfiguratie** sectie, klikt u op **Adobe Creative Cloud configureren** openen **eenmalige aanmelding configureren** venster. Kopieer de **SAML entiteit-Id** en **SAML SSO Service URL** van naslag-sectie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. In een ander browservenster aanmelding bij uw cloudtenant van Adobe Creative als beheerder.

8.  Ga naar **identiteit** in het navigatiedeelvenster links en klikt u op uw domein. Voer de volgende stappen uit op **eenmalige aanmelding op configuratie vereist** sectie.

    ![Instellingen](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "instellingen")

9. Klik op **Bladeren** voor het uploaden van het gedownloade certificaat uit Azure AD **IDP certificaat**.

10. In de **IDP verlener** textbox, plaatst u de waarde van **SAML entiteit-Id** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.

11. In de **IDP aanmeldings-URL** textbox, plaatst u de waarde van **SAML SSO Service URL** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.

12. Selecteer **HTTP - omleiding** als **IDP Binding**.

13. Selecteer **e-mailadres** als **aanmelding gebruikersinstelling**.
 
14. Klik op **opslaan** knop.

15. Het dashboard biedt nu de XML **'Metagegevens downloaden'** bestand. Het bevat van Adobe EntityDescriptor URL's en AssertionConsumerService. Open het bestand en configureer deze in de Azure AD-toepassing.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Gebruik de waarde van de EntityDescriptor Adobe geleverd, kunt u voor **id** op de **App-instellingen configureren** dialoogvenster.

    b. Gebruik de waarde van de AssertionConsumerService Adobe geleverd, kunt u voor **antwoord-URL** op de **App-instellingen configureren** dialoogvenster.
 
### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **BrittaSimon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Een testgebruiker Adobe Creative Cloud maken

Om in te schakelen gebruikers van Azure AD aan te melden bij Adobe Creative Cloud, moeten ze worden ingericht in Adobe Creative Cloud.  
In het geval van Adobe Creative Cloud is inrichting een handmatige taak.

**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw bedrijf Adobe Creative Cloud site als beheerder.

2. Klik op **mensen**.

    ![Mensen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "personen")

3. Klik op **gebruiker uitnodigen**.

    ![Gebruikers uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "gebruikers uitnodigen")

4. Op de **personen uitnodigen** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Personen uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "personen uitnodigen")

    a. In de **e** textbox, typ de e-mailadres van Britta Simon account.
    
    b. Klik op **uitnodigen**.

    > [!NOTE]
    > De accounthouder Azure Active Directory wordt een e-mailbericht ontvangen en Ga als volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan Adobe Creative Cloud.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen Adobe Creative Cloud, moet u de volgende stappen uitvoeren:**

1. In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Adobe Creative Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel Adobe Creative Cloud in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Adobe Creative Cloud.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png