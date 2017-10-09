---
title: 'Zelfstudie: Azure Active Directory-integratie met Direct | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Direct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a>Zelfstudie: Azure Active Directory-integratie met Direct

In deze zelfstudie leert u hoe toointegrate Direct met Azure Active Directory (Azure AD).

Directe integratie met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooDirect toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooDirect (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Direct, moet u de volgende items Hallo:

- Een Azure AD-abonnement
- Een directe eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Direct uit de galerie Hallo toe te voegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-direct-from-hello-gallery"></a>Direct uit de galerie Hallo toe te voegen
tooconfigure hello integratie van Direct in Azure AD, moet u tooadd Direct uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Direct uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Direct**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. Selecteer in het deelvenster resultaten hello, **Direct**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Direct op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Direct is tooa gebruiker in Azure AD. Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in directe behoeften toobe tot stand gebracht.

In de directe, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en Azure AD test eenmalige aanmelding met Direct, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een directe testgebruiker](#creating-a-direct-test-user)**  -toohave een equivalent van Britta Simon in rechtstreeks die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing rechtstreeks configureren.

**tooconfigure eenmalige aanmelding Azure AD met Direct kunnen uitvoeren Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Direct** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. Op Hallo **Direct domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    In Hallo **id** textbox type Hallo URL:`https://direct4b.com/`

4. Controleer **weergeven geavanceerde instellingen voor URL**, indien gewenst tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://direct4b.com/sso` 
    
5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. tooconfigure eenmalige aanmelding op **Direct** zijde, moet u toosend Hallo gedownload **Metadata XML** te[Direct ondersteuningsteam](https://direct4b.com/ja/support.html#inquiry). 

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-direct-test-user"></a>Een rechtstreekse testversie van de gebruiker maken

In deze sectie maakt u Britta Simon aangeroepen in rechtstreeks van een gebruiker. Werken met [Direct ondersteuningsteam](https://direct4b.com/ja/support.html#inquiry) Hallo gebruikers toevoegen in directe Hallo-platform. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDirect toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooDirect, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Direct**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

1. U kunt eventueel tootest in **IDP geïnitieerd modus**:

    Wanneer u klikt op Hallo **Direct** tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour **Direct** toepassing.

2. U kunt eventueel tootest in **SP geïnitieerd modus**:
    
    a. Klik op Hallo **directe** -tegel in Hallo Toegangspaneel en kunt u omgeleide toohello aanmelding toepassingspagina.

    b. Voer uw `subdomain` in Hallo textbox weergegeven en druk op '次へ (volgende)' u moet ophalen en automatisch aangemelde tooyour **Direct** toepassing.
    
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

