---
title: 'Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en houder wachtwoordbeheer & digitale kluis.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a>Zelfstudie: Azure Active Directory-integratie met wachtwoordbeheer houder & digitale kluis

In deze zelfstudie leert u hoe houder wachtwoordbeheer & digitale kluis integreren met Azure Active Directory (Azure AD).

Wachtwoordbeheer houder & digitale kluis integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot de houder wachtwoordbeheer & digitale kluis heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij houder wachtwoordbeheer & digitale kluis (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met wachtwoordbeheer houder & digitale kluis, moet u de volgende items:

- Een Azure AD-abonnement
- Een houder wachtwoordbeheer & digitale kluis eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a>Wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen
Voor het configureren van de integratie van houder wachtwoordbeheer & digitale kluis in Azure AD, moet u wachtwoordbeheer houder & digitale kluis uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen houder wachtwoordbeheer & digitale kluis uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak **houder wachtwoordbeheer & digitale kluis**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. Selecteer in het deelvenster resultaten **houder wachtwoordbeheer & digitale kluis**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in houder wachtwoordbeheer & digitale kluis in Azure AD voor een gebruiker is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de houder wachtwoordbeheer & digitale kluis tot stand worden gebracht.

Wijs in houder wachtwoordbeheer & digitale kluis, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker houder wachtwoordbeheer & digitale kluis](#creating-a-keeperpasswordmanager-test-user)**  - hebben een equivalent van Britta Simon in houder wachtwoordbeheer & digitale kluis die is gekoppeld aan de Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing houder wachtwoordbeheer & digitale kluis.

**Voor het configureren van Azure AD eenmalige aanmelding met wachtwoordbeheer houder & digitale kluis, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **houder wachtwoordbeheer & digitale kluis** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. Op de **houder wachtwoordbeheer & digitale kluis domein en URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    a. In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`

    b. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`

    c. In de **id** textbox, typ een URL met het volgende patroon volgen:`https://{SSO CONNECT SERVER}/sso-connect`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met de werkelijke antwoord-URL en de aanmeldings-URL. Neem contact op met [houder wachtwoordbeheer & digitale kluis Client ondersteuningsteam](https://keepersecurity.com/contact.html) ophalen van deze waarden. 

4. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. Op de **houder wachtwoordbeheer & digitale kluis configuratie** sectie, klikt u op **houder wachtwoordbeheer configureren & digitale kluis** openen **eenmalige aanmelding configureren** venster. Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. Eenmalige aanmelding configureren op **houder wachtwoordbeheer & digitale kluis configuratie** zijde, volg de richtlijnen gegeven op [houder Support Guide](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **BrittaSimon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a>Een testgebruiker houder wachtwoordbeheer & digitale kluis maken

Om Azure AD-gebruikers zich aanmelden bij de houder wachtwoordbeheer & digitale kluis, moeten ze worden ingericht in houder wachtwoordbeheer & digitale kluis. Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt. U kunt contact opnemen met [houder ondersteuning](https://keepersecurity.com/contact.html), als u wilt gebruikers handmatig instellen.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan houder wachtwoordbeheer & digitale kluis.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen houder wachtwoordbeheer & digitale kluis, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **houder wachtwoordbeheer & digitale kluis**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel houder wachtwoordbeheer & digitale kluis in het deelvenster toegang, krijgt u de aanmeldingspagina van houder wachtwoordbeheer & digitale kluis toepassing. Op de geslaagde verificatie, moet u in de toepassing ophalen. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

