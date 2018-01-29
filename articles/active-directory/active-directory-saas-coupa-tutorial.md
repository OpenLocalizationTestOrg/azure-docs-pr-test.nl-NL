---
title: 'Zelfstudie: Azure Active Directory-integratie met Coupa | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Coupa.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2017
ms.author: jeedes
ms.openlocfilehash: 30149f181d8b0ebdc1ae6820da5d561f3a942fa3
ms.sourcegitcommit: aaba209b9cea87cb983e6f498e7a820616a77471
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/12/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Zelfstudie: Azure Active Directory-integratie met Coupa

In deze zelfstudie leert u hoe Coupa integreren met Azure Active Directory (Azure AD).

Coupa integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot Coupa heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij Coupa (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Coupa, moet u de volgende items:

- Een Azure AD-abonnement
- Een Coupa eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Coupa uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-coupa-from-the-gallery"></a>Coupa uit de galerie toevoegen
Voor het configureren van de integratie van Coupa in Azure AD, moet u Coupa uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Coupa uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop Nieuw toepassing][3]

4. Typ in het zoekvak **Coupa**, selecteer **Coupa** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Coupa in de lijst met resultaten](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Coupa op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Coupa is voor een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Coupa tot stand worden gebracht.

Wijs in Coupa, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met Coupa, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Coupa](#create-a-coupa-test-user)**  - Coupa die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Coupa configureren.

**Voor het configureren van Azure AD eenmalige aanmelding met Coupa, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Coupa** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_samlbase.png)

3. Op de **Coupa domein en de URL's** sectie, voert u de volgende stappen uit:

    ![URL's en Coupa domein eenmalige aanmelding informatie](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_url.png)

    a. In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://<companyname>.Coupa.com`

    b. In de **id** textbox, typ een URL met het volgende patroon volgen:`<companyname>.coupahost.com`

    c. In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.coupahost.com/sp/ACS.saml2`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met de werkelijke aanmeldings-URL, id en antwoord-URL. Neem contact op met [Coupa Client ondersteuningsteam](https://success.coupa.com/Support/Contact_Us?) ophalen van deze waarden. u krijgt de antwoord-URL-waarde van de metagegevens die verderop in de zelfstudie wordt beschreven.

4. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-coupa-tutorial/tutorial_general_400.png)

6. Meld u op met uw bedrijf Coupa site als een beheerder.

7. Ga naar **Setup \> beveiligingscontrole**.
   
   ![Beveiligingsmechanismen](./media/active-directory-saas-coupa-tutorial/ic791900.png "beveiligingsmechanismen")

8. In de **Meld u aan met referenties Coupa** sectie, voert u de volgende stappen uit:

    ![Coupa SP metagegevens](./media/active-directory-saas-coupa-tutorial/ic791901.png "Coupa SP metagegevens")
    
    a. Selecteer **aanmelden via SAML**.
    
    b. Het bestand te downloaden Coupa metagegevens op uw computer, klikt u op **downloaden en importeren SP metagegevens**. Open het metagegevens en kopieer de **AssertionConsumerService index/URL** waarde, plak de waarde in de **antwoord-URL** textbox in de **Coupa domein en de URL's** sectie. 
    
    c. Klik op **Bladeren** voor het uploaden van de metagegevens van de Azure portal hebt gedownload.
    
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/active-directory-saas-coupa-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-coupa-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/active-directory-saas-coupa-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-coupa-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-coupa-test-user"></a>Een testgebruiker Coupa maken

Om in te schakelen gebruikers van Azure AD aan te melden bij Coupa, moeten ze worden ingericht in Coupa.  

* In het geval van Coupa is inrichting een handmatige taak.

**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw **Coupa** bedrijf site als administrator.

2. Klik in het menu bovenaan op **Setup**, en klik vervolgens op **gebruikers**.
   
   ![Gebruikers](./media/active-directory-saas-coupa-tutorial/ic791908.png "gebruikers")

3. Klik op **Create**.
   
   ![Gebruikers maken](./media/active-directory-saas-coupa-tutorial/ic791909.png "gebruikers maken")

4. In de **gebruiker maken** sectie, voert u de volgende stappen uit:
   
   ![Details van gebruiker](./media/active-directory-saas-coupa-tutorial/ic791910.png "Gebruikersdetails")
   
   a. Typ de **aanmelding**, **voornaam**, **achternaam**, **Single Sign-On-ID**, **e** kenmerken van een geldige Azure Active Directory-account die u inrichten in de bijbehorende tekstvakken wilt.

   b. Klik op **Create**.   
   
   >[!NOTE]
   >De houder van Azure Active Directory-account ontvangt een e-mailbericht met een koppeling naar het account te bevestigen voordat deze geactiveerd wordt. 
   > 

>[!NOTE]
>U kunt andere Coupa gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Coupa aan inrichten AAD-gebruikersaccounts. 

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Coupa.

![Toewijzen van de gebruikersrol][200] 

**Britta Simon om aan te wijzen Coupa, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Coupa**.

    ![De koppeling Coupa in de lijst met toepassingen](./media/active-directory-saas-coupa-tutorial/tutorial_coupa_app.png)  

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Als u op de tegel Coupa in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Coupa.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-coupa-tutorial/tutorial_general_203.png

