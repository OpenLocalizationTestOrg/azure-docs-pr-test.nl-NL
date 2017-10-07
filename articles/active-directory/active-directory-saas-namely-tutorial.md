---
title: 'Zelfstudie: Azure Active Directory-integratie met namelijk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en namelijk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a>Zelfstudie: Azure Active Directory-integratie met namelijk

In deze zelfstudie leert u hoe toointegrate namelijk met Azure Active Directory (Azure AD).

Namelijk integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooNamely toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooNamely (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met namelijk u Hallo volgende items nodig:

- Een Azure AD-abonnement
- Een namelijk eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van namelijk van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-namely-from-hello-gallery"></a>Het toevoegen van namelijk van Hallo-galerie
tooconfigure hello integratie van namelijk in Azure AD, moet u tooadd namelijk van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd namelijk via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **namelijk**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. Selecteer in het deelvenster resultaten hello, **namelijk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met namelijk op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in namelijk is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker in Hallo namelijk toobe tot stand gebracht.

In waarde Hallo Hallo namelijk toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met namelijk u beschikken over toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een namelijk testgebruiker](#creating-a-namely-test-user)**  -toohave een equivalent van Britta Simon in namelijk die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing namelijk configureren.

**Azure AD tooconfigure eenmalige aanmelding met namelijk uitvoeren Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **namelijk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. Op Hallo **namelijk domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.namely.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<subdomain>.namely.com/saml/metadata`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [namelijk Client ondersteuningsteam](https://www.namely.com/contact/) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. Op Hallo **namelijk configuratie** sectie, klikt u op **namelijk configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. Een ander browservenster geopend Meld u aan bij tooyour namelijk bedrijf site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **bedrijf**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. Klik op Hallo **instellingen** tabblad.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. Klik op **SAML**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. Op Hallo **SAML instellingen** pagina, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    a. Klik op **SAML inschakelen**. 

    b. In Hallo **identiteit provider SSO url** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
    
    c. Open uw gedownloade certificaat in Kladblok, kopieer Hallo inhoud, en plak deze in Hallo **provider identiteitscertificaat** textbox.
     
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-namely-test-user"></a>Maken van een namelijk testgebruiker

Hallo-doel van deze sectie is toocreate Britta Simon namelijk naam in van een gebruiker.

**toocreate Britta Simon namelijk naam in van een gebruiker uitvoeren Hallo stappen te volgen:**

1. Eenmalige aanmelding tooyour bedrijf namelijk site als beheerder.

2. Klik in de werkbalk bovenaan Hallo Hallo op **mensen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. Klik op Hallo **Directory** tabblad.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. Klik op **toevoegen van nieuwe persoon**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. Op Hallo **nieuwe persoon toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:

    a. In Hallo **voornaam** textbox type **Britta**.

    b. In Hallo **achternaam** textbox type **Simon**.

    c. In Hallo **e** textbox type Hallo **e-mailadres** van BrittaSimon.

    d. Klik op **Opslaan**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooNamely toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooNamely, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **namelijk**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Wanneer u klikt op Hallo namelijk-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour namelijk toepassing

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

