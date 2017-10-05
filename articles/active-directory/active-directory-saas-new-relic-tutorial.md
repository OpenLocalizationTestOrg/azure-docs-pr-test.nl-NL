---
title: 'Zelfstudie: Azure Active Directory-integratie met New Relic | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en de New Relic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a>Zelfstudie: Azure Active Directory-integratie met New Relic

In deze zelfstudie leert u hoe New Relic integreren met Azure Active Directory (Azure AD).

New Relic integreren met Azure AD biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot de New Relic heeft
- U kunt uw gebruikers automatisch ophalen aangemeld bij New Relic (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met New Relic, moet u de volgende items:

- Een Azure AD-abonnement
- Een New Relic eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. New Relic uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-new-relic-from-the-gallery"></a>New Relic uit de galerie toevoegen
Voor het configureren van de integratie van New Relic in Azure AD, moet u New Relic uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen New Relic uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak **New Relic**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. Selecteer in het deelvenster resultaten **New Relic**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met New Relic op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in New Relic in Azure AD voor een gebruiker is. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante New Relic-gebruiker worden gemaakt.

Wijs in New Relic de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met New Relic, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een New Relic-testgebruiker](#creating-a-new-relic-test-user)**  - New Relic die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing New Relic.

**Voor het configureren van Azure AD eenmalige aanmelding met New Relic, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **New Relic** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. Op de **nieuwe Relic domein en URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.newrelic.com`

    > [!NOTE] 
    > De waarde is geen echte. Werk de waarde met de werkelijke URL voor eenmalige aanmelding. Neem contact op met [nieuwe Relic Client ondersteuningsteam](https://support.newrelic.com/) de waarde op te halen. 
 
4. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. Op de **nieuwe Relic configuratie** sectie, klikt u op **New Relic configureren** openen **eenmalige aanmelding configureren** venster. Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. In een ander browservenster, meld u aan bij uw **New Relic** bedrijf site als administrator.

8. Klik in het menu bovenaan op **Accountinstellingen**.
   
    ![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Accountinstellingen")

9. Klik op de **beveiligings- en** tabblad en klik vervolgens op de **eenmalige aanmelding** tabblad.
   
    ![Eenmalige aanmelding](./media/active-directory-saas-new-relic-tutorial/ic797037.png "eenmalige aanmelding")

10. Voer de volgende stappen uit op de pagina van het dialoogvenster SAML:
   
    ![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")
   
   a. Klik op **bestand kiezen** om uw gedownloade Azure Active Directory-certificaat te uploaden.

   b. In de **externe aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
   
   c. In de **afmelding aanvoer URL** textbox, plak de waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

   d. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    a. In de **naam** textbox type **BrittaSimon**.

    b. In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-new-relic-test-user"></a>De gebruiker van een New Relic-test maken

Om Azure Active Directory-gebruikers zich aanmelden bij de New Relic inschakelt, moeten ze worden ingericht in New Relic. In het geval van New Relic is inrichting een handmatige taak.

**Voor het inrichten van een New Relic-gebruikersaccount, moet u de volgende stappen uitvoeren:**

1. Meld u aan bij uw **New Relic** bedrijf site als administrator.

2. Klik in het menu bovenaan op **Accountinstellingen**.
   
    ![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Accountinstellingen")

3. In de **Account** deelvenster aan de linkerkant te klikken op **samenvatting**, en klik vervolgens op **gebruiker toevoegen**.
   
    ![Instellingen account](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Accountinstellingen")

4. Op de **actieve gebruikers** dialoogvenster de volgende stappen uitvoeren:
   
    ![Actieve gebruikers](./media/active-directory-saas-new-relic-tutorial/ic797042.png "actieve gebruikers")
   
    a. In de **e** textbox, typ de e-mailadres van een geldige Azure Active Directory-gebruiker die u inrichten wilt.

    b. Als **rol** Selecteer **gebruiker**.

    c. Klik op **deze gebruiker toevoegen**.

>[!NOTE]
>U kunt andere New Relic gebruiker account hulpmiddelen voor het maken of API's die door New Relic inrichten AAD-gebruikersaccounts.
> 

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen van de testgebruiker Azure AD

In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan New Relic.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen New Relic, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **New Relic**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Als u op de New Relic-tegel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw New Relic-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

