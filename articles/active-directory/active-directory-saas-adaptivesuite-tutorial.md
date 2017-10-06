---
title: 'Zelfstudie: Azure Active Directory-integratie met adaptieve Suite | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en adaptieve Suite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Zelfstudie: Azure Active Directory-integratie met adaptieve Suite

In deze zelfstudie leert u hoe toointegrate adaptieve Suite met Azure Active Directory (Azure AD).

Adaptieve Suite integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAdaptive Suite heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAdaptive Suite (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met adaptieve Suite tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een adaptieve Suite eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van adaptieve Suite van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Het toevoegen van adaptieve Suite van Hallo-galerie
tooconfigure hello integratie van adaptieve Suite in Azure AD, moet u tooadd adaptieve Suite van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd adaptieve Suite van Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **adaptieve Suite**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. Selecteer in het deelvenster resultaten hello, **adaptieve Suite**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met adaptieve Suite op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in adaptieve Suite is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in adaptieve Suite toobe tot stand gebracht.

In adaptieve Suite Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met adaptieve Suite, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker adaptieve Suite](#creating-an-adaptive-suite-test-user)**  -toohave een equivalent van Britta Simon in adaptieve-pakket dat is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing adaptieve Suite.

**Voer tooconfigure Azure AD eenmalige aanmelding met adaptieve Suite Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **adaptieve Suite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. Op Hallo **adaptieve Suite domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > U kunt deze waarde niet ophalen uit Hallo adaptieve Suite van **SAML SSO instellingen** pagina.
    >  

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. Op Hallo **geavanceerde configuratie van de Suite** sectie, klikt u op **adaptieve Suite configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. In een ander browservenster, meld u aan tooyour adaptieve Suite bedrijf site als een beheerder.

8. Ga te**Admin**.
   
    ![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")

9. In Hallo **gebruikers en rollen** sectie, klikt u op **SAML SSO-instellingen beheren**.
   
    ![SAML SSO-instellingen beheren](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "SAML SSO-instellingen beheren")

10. Op Hallo **SAML SSO instellingen** pagina, voert u Hallo stappen te volgen:
   
    ![Instellingen voor eenmalige aanmelding SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO-instellingen")

    a. In Hallo **identiteit providernaam** textbox, typ een naam voor uw configuratie.
    
    b. Plakken Hallo **SAML entiteit-ID** waarde gekopieerd vanuit Azure-portal naar Hallo **identiteitsprovider entiteit-ID** textbox.
  
    c. Plakken Hallo **SAML Single Sign-On Service-URL** waarde gekopieerd vanuit Azure-portal naar Hallo **identiteitsprovider URL SSO** textbox.
  
    d. Plakken Hallo **SAML Single Sign-On Service-URL** waarde gekopieerd vanuit Azure-portal naar Hallo **aangepaste afmelding URL** textbox.
  
    e. tooupload uw gedownloade certificaat, klik op **bestand kiezen**.
  
    f. Selecteer de volgende hello, voor:
    * **Gebruikers-id van SAML**, selecteer **adaptieve Insights gebruiker gebruikersnaam**.
    * **Locatie van het SAML-id**, selecteer **gebruikers-id in NameID van onderwerp**.
    * **SAML NameID indeling**, selecteer **e-mailadres**.
    * **SAML inschakelen**, selecteer **toestaan SAML SSO en direct adaptieve Insights aanmelden**.
    
    g. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Maken van een testgebruiker adaptieve Suite

Azure AD tooenable gebruikers toolog in tooAdaptive Suite, moeten ze worden ingericht in adaptieve Suite.  

* In geval van adaptieve Suite Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:** 

1. Meld u bij tooyour **adaptieve Suite** bedrijf site als beheerder.
2. Ga te**Admin**.
   
   ![Beheerder](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")
3. In Hallo **gebruikers en rollen** sectie, klikt u op **gebruiker toevoegen**.
   
   ![Gebruiker toevoegen](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "gebruiker toevoegen")
4. In Hallo **nieuwe gebruiker** sectie, voert u Hallo stappen te volgen:
   
   ![Indienen](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "verzenden")   

   a. Type Hallo **naam**, **aanmelding**, **e**, **wachtwoord** van een geldige Azure Active Directory-gebruiker gewenste tooprovision in Hallo gerelateerd tekstvakken.
  
   b. Selecteer een **rol**.
  
   c. Klik op **indienen**.

>[!NOTE]
>U kunt andere adaptieve Suite gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door adaptieve Suite tooprovision AAD-gebruikersaccounts.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAdaptive Suite.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAdaptive Suite Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **adaptieve Suite**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Microsoft Azure AD Single Sign-On configuratie met Hallo Toegangsvenster.

Als u op Hallo adaptieve Suite tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour adaptieve Suite-toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

