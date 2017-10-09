---
title: 'Zelfstudie: Azure Active Directory-integratie met centraal Cerner | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Cerner centraal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a>Zelfstudie: Azure Active Directory-integratie met Cerner-centraal

In deze zelfstudie leert u hoe toointegrate Cerner centraal met Azure Active Directory (Azure AD).

Cerner centraal integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooCerner centraal heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooCerner centraal (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met centraal Cerner tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een goedgekeurde Cerner centrale systeemaccount

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Cerner centraal van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-cerner-central-from-hello-gallery"></a>Het toevoegen van Cerner centraal van Hallo-galerie
tooconfigure hello integratie van Cerner centraal in Azure AD, moet u tooadd Cerner centraal uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Cerner centraal via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop boven op Hallo dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Cerner centraal**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. Selecteer in het deelvenster resultaten hello, **Cerner centraal**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Cerner centraal op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Cerner centrale is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Cerner centrale toobe tot stand gebracht.

tooconfigure en eenmalige aanmelding Azure AD-test met Cerner centraal, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Cerner centraal](#creating-a-cerner-central-test-user)**  -toohave een equivalent van Britta Simon in Cerner centrale die is gekoppeld toohello Azure AD-weergave van Hallo-gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Cerner centraal configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met Cerner centraal, Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Cerner centraal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. Op Hallo **Cerner centrale domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    a. In Hallo **id** textbox Hallo typewaarde met Hallo patronen te volgen:
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    b. In Hallo **antwoord-URL** textbox, type patronen u een URL met hello te volgen: 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [Cerner centraal ondersteuningsteam](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget deze waarden.
 
4. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:

    a. Klik op **App registraties**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    b. Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    c. Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    d. Ga nu toohello eigenschappenpagina van **Cerner centraal** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    e. Hallo genereren **metagegevens-URL** met Hallo patroon volgen:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`

6. tooconfigure eenmalige aanmelding op **Cerner centraal** clientzijde, moet u toosend hello **metagegevens-URL** te[Cerner centraal ondersteuning](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations). Ze configureren Hallo eenmalige aanmelding op de integratie van toepassingen aan clientzijde toocomplete Hallo.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen. 

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen**.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-cerner-central-test-user"></a>Maken van een testgebruiker Cerner-centraal

**Cerner centraal** toepassing kunt verificatie van elke provider federatieve identiteiten. Als een gebruiker kan toolog in toohello toepassing startpagina is, wordt deze federatieve zijn en niet nodig is voor handmatige inrichting.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCerner centraal.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooCerner centraal, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Cerner centraal**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Cerner centraal-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Cerner centrale toepassing. Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

