---
title: 'Zelfstudie: Azure Active Directory-integratie met LearnUpon | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en LearnUpon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Zelfstudie: Azure Active Directory-integratie met LearnUpon

In deze zelfstudie leert u hoe toointegrate LearnUpon met Azure Active Directory (Azure AD).

LearnUpon integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooLearnUpon toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooLearnUpon (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met LearnUpon tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een LearnUpon eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van LearnUpon van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-learnupon-from-hello-gallery"></a>Het toevoegen van LearnUpon van Hallo-galerie
tooconfigure hello integratie van LearnUpon in Azure AD, moet u tooadd LearnUpon uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd LearnUpon via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **LearnUpon**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. Selecteer in het deelvenster resultaten hello, **LearnUpon**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met LearnUpon op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in LearnUpon is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in LearnUpon toobe tot stand gebracht.

Wijs in LearnUpon, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met LearnUpon, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker LearnUpon](#creating-a-learnupon-test-user)**  -toohave een equivalent van Britta Simon in LearnUpon die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing LearnUpon configureren.

**Azure AD tooconfigure eenmalige aanmelding met LearnUpon, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **LearnUpon** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. Op Hallo **LearnUpon domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Houd er rekening mee dat dit geen Hallo echte waarde is. u hebt deze waarde met de werkelijke antwoord-URL Hallo tooupdate. Neem contact op met tooget deze waarde [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/).



4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Raw)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. Op Hallo **LearnUpon configuratie** sectie, klikt u op **configureren LearnUpon** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Open een ander browserexemplaar en meld u aan bij LearnUpon met een administratoraccount. 

8. Klik op Hallo **instellingen** tabblad.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Klik op **eenmalige aanmelding - SAML**, en klik vervolgens op **algemene instellingen** tooconfigure SAML-instellingen.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. In Hallo **algemene instellingen** sectie, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    a. Selecteer **ingeschakeld**.

    b. Selecteer **versie** als **2.0**.

    c. Selecteer **overslaan voorwaarden** als **Nee**.

    d. In Hallo **SAML-Token boeken param naam** textbox Hallo-typenaam van de aanvraag post parameter toohello SAML consumer URL hierboven genoemde met Hallo van SAML-verklaring toobe gecontroleerd en geverifieerd - bijvoorbeeld  **SAMLResponse**.

    e. In Hallo **indeling van de id** textbox type Hallo waarde die waar uw gebruikers van SAML-verklaring Hallo id (e-mailadres) zich bevindt aangeeft-bijvoorbeeld **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.
  
    f. In Hallo **Providerlocatie identificeren** textbox, type Hallo waarde die aangeeft waar hello gebruikers worden verzonden tooif ze klikt u op uw geüploade pictogram van het scherm van uw Azure-portal aanmelding.
  
    g. In Hallo **afmelden URL** textbox plakken Hallo **Sign-Out URL** die u hebt gekopieerd uit hello Azure-portal.
    
    h. Klik op **vinger afdrukken bestellen beheren**, en vervolgens de vingerafdruk Hallo van uw gedownloade certificaat uploaden.

11. Klik op **gebruikersinstellingen**, en klik vervolgens op Hallo stappen te volgen:
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    a. In Hallo **voornaam id indeling** textbox Hallo typewaarde die vertellen waar in uw voornaam SAML-verklaring Hallo gebruikers zich bevindt - voorbeeld: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. In Hallo **laatste naamnotatie id** textbox Hallo typewaarde die vertellen waar in uw achternaam SAML-verklaring Hallo gebruikers zich bevindt - voorbeeld: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-learnupon-test-user"></a>Een testgebruiker LearnUpon maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in LearnUpon van een gebruiker. LearnUpon ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker wordt tijdens een poging tooaccess LearnUpon gemaakt als deze nog niet bestaat. [Configureren van Azure AD voor eenmalige aanmelding](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Als u een gebruiker toocreate handmatig nodig hebt, moet u toocontact [LearnUpon ondersteuningsteam](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooLearnUpon toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooLearnUpon, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **LearnUpon**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo LearnUpon tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour LearnUpon toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

