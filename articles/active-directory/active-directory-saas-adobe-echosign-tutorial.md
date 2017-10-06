---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe teken | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Adobe aanmelding.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Zelfstudie: Azure Active Directory-integratie met Adobe teken

In deze zelfstudie leert u hoe toointegrate Adobe Meld u aan bij Azure Active Directory (Azure AD).

Meld u Adobe integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAdobe aanmelding heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAdobe aanmelding (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Adobe teken tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Adobe aanmelding eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Adobe aanmelding van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-adobe-sign-from-hello-gallery"></a>Het toevoegen van Adobe aanmelding van Hallo-galerie
tooconfigure hello integratie van Adobe aanmelding in Azure AD, moet u tooadd Adobe aanmelding uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Adobe teken uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Adobe aanmelding**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. Selecteer in het deelvenster resultaten hello, **Adobe aanmelding**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Adobe aanmelding op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Adobe aanmelding is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Adobe aanmelding toobe tot stand gebracht.

In Adobe teken, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Adobe ondertekenen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Adobe aanmelding](#creating-an-adobe-sign-test-user)**  -toohave een equivalent van Britta Simon in Adobe aanmelding die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Adobe aanmelding.

**Voer tooconfigure Azure AD eenmalige aanmelding met Adobe-teken Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **Adobe aanmelding** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. Op Hallo **Adobe aanmelding domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.echosign.com/`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Adobe aanmelding Client ondersteuningsteam](https://helpx.adobe.com/in/contact/support.html) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. Op Hallo **Adobe aanmelding configuratie** sectie, klikt u op **Adobe aanmelding configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. In een ander browservenster, meld u aan tooyour Adobe aanmelding bedrijf site als een beheerder.

8. Klik in het menu bovenaan Hallo Hallo **Account**, en klik vervolgens in het navigatievenster aan de linkerkant Hallo Hallo op **SAML instellingen** onder **Accountinstellingen**.
   
   ![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")

9. Voer in Hallo sectie SAML-instellingen, Hallo stappen te volgen:
   
   ![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML-instellingen")
   
   a. Als **SAML modus**, selecteer **SAML verplichte**.
   
   b. Selecteer **EchoSign accountbeheerders toestaan toolog aan met hun referenties EchoSign**.
   
   c. Als **maken van een gebruikersaccount**, selecteer **automatisch toevoegen van gebruikers worden geverifieerd via SAML**.

10. Verplaatsen, uitvoeren Hallo volgende stappen:

       ![Instellingen voor SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML-instellingen")

    a. Plakken **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP entiteit-ID** textbox.
    
    b. Plakken **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP aanmeldings-URL** textbox.
   
    c. Plakken **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal in Hallo **IdP afmelding URL** textbox.

    d. Open uw gedownloade **Certificate(Base64)** -bestand in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **IdP certificaat** tekstvak

    e. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Een testgebruiker Adobe aanmelding maken

Azure AD tooenable gebruikers toolog in tooAdobe aanmelding, ze in Adobe aanmelding moeten worden ingericht. In geval van Adobe aanmelding Hallo is inrichting een handmatige taak.

>[!NOTE]
>U kunt andere Adobe aanmelding gebruiker account hulpmiddelen voor het maken of API's geleverd door Adobe aanmelding tooprovision AAD-gebruikersaccounts. 

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Adobe aanmelding** bedrijf site als administrator.

2. Klik in het menu bovenaan Hallo Hallo **Account**, en klik vervolgens in het navigatievenster aan de linkerkant Hallo Hallo op **gebruikers en groepen**, en klik vervolgens op **Maak een nieuwe gebruiker**.
   
   ![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")
   
3. In Hallo **nieuwe gebruiker maken** sectie, voert u Hallo stappen te volgen:
   
   ![Gebruiker maken](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "gebruiker maken")
   
   a. Type Hallo **e-mailadres**, **voornaam**, en **achternaam** van tekstvakken met betrekking tot een geldige AAD-account u wilt dat tooprovision in Hallo.
   
   b. Klik op **gebruiker maken**.

>[!NOTE]
>Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAdobe aanmelding.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAdobe teken, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Adobe aanmelding**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u op Hallo Adobe aanmelding-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour programma Adobe ondertekenen.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

