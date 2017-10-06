---
title: 'Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en MOVEit overdracht - Azure AD-integratie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Zelfstudie: Azure Active Directory-integratie met MOVEit overdracht - Azure AD-integratie

In deze zelfstudie leert u hoe toointegrate MOVEit overdracht - Azure AD-integratie met Azure Active Directory (Azure AD).

Integratie van MOVEit overdracht - Azure AD-integratie met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooMOVEit overdracht - Azure AD-integratie heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooMOVEit overdracht - Azure AD-integratie met hun Azure AD-accounts (Single Sign-On) inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met MOVEit overdracht - integratie van Azure AD, moet u Hallo volgende items:

- Een Azure AD-abonnement
- De overdracht van een MOVEit - Azure AD-integratie eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. MOVEit overdracht - Azure AD-integratie uit Hallo galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>MOVEit overdracht - Azure AD-integratie uit Hallo galerie toevoegen
tooconfigure hello integratie van MOVEit overdracht - Azure AD-integratie met Azure AD, moet u tooadd MOVEit overdracht - Azure AD-integratie in Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd MOVEit overdracht - Azure AD-integratie uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **MOVEit overdracht - Azure AD-integratie**, selecteer **MOVEit overdracht - Azure AD-integratie** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo de toepassing.

    ![Overdracht van MOVEit - Azure AD-integratie in de lijst met resultaten Hallo](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie op basis van een testgebruiker 'Britta Simon' genoemd.

Azure AD moet tooknow welke gebruiker Hallo equivalent in overdrachts-MOVEit voor eenmalige aanmelding toowork - Azure AD-integratie is tooa gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in overdrachts-MOVEit - moet Azure AD-integratie toobe tot stand gebracht.

In MOVEit overdrachts - Azure AD-integratie Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met MOVEit overdracht - integratie van Azure AD, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een overdracht MOVEit - Azure AD-integratie testgebruiker](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave een equivalent van Britta Simon in overdrachts-MOVEit - Azure AD-integratie die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in de overdracht van uw MOVEit - toepassing voor Azure AD-integratie.

**Voer tooconfigure Azure AD eenmalige aanmelding met MOVEit overdracht - Azure AD-integratie Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **MOVEit overdracht - Azure AD-integratie** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Op Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com/<tenatid>`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. U kunt deze waarden later in verwijzen **metagegevens-URL voor Service Provider** sectie of neem contact op met [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Meld u aan op tooyour MOVEit overdracht tenant als beheerder.

7. Klik op Hallo navigatiedeelvenster links **instellingen**.

    ![Instellingen sectie op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Klik op **eenmalige aanmelding** koppeling, die zich onder **beveiligingsbeleid-gebruikersverificatie >**.

    ![Security-beleid op App aan clientzijde](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Klik op Hallo metagegevens-URL koppeling toodownload hello metagegevensdocument.

    ![Serviceprovider metagegevens-URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Controleer of **id van de entiteit** overeenkomt met **id** in Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.
    * Controleer of **AssertionConsumerService** locatie-URL overeenkomt met **antwoord-URL** in Hallo **MOVEit overdracht - URL's en Azure AD-integratie domein** sectie.
    
    ![Eenmalige aanmelding op App aan clientzijde configureren](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Klik op **identiteitsprovider toevoegen** tooadd knop een nieuwe federatieve id-Provider.

    ![ID-Provider toevoegen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Klik op **bladeren...**  tooselect Hallo metagegevensbestand dat u hebt gedownload van Azure-portal en klik vervolgens op **identiteitsprovider toevoegen** tooupload Hallo bestand hebt gedownload.

    ![SAML-identiteitsprovider](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Selecteer "**Ja**' als **ingeschakeld** in Hallo **federatieve identiteit Providerinstellingen bewerken...**  pagina en klik op **opslaan**.

    ![Federatieve identiteiten Providerinstellingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. In Hallo **bewerken federatieve identiteit Provider gebruikersinstellingen** pagina, voert u Hallo van de volgende activiteiten:
    
    ![Federatieve identiteiten Providerinstellingen bewerken](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Selecteer **SAML NameID** als **aanmeldingsnaam**.
    
    b. Selecteer **andere** als **volledige naam** en in Hallo **kenmerknaam** textbox plaatsen Hallo-waarde: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Selecteer **andere** als **e** en in Hallo **kenmerknaam** textbox plaatsen Hallo-waarde: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Selecteer **Ja** als **automatisch maken van account aanmeldt**.
    
    e. Klik op **opslaan** knop.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Een MOVEit Transfer - Azure AD-integratie testgebruiker maken

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in MOVEit overdracht - Azure AD-integratie van een gebruiker. Overdracht van MOVEit - Azure AD-integratie ondersteunt just-in-time-inrichting, die u hebt ingeschakeld. Er is geen actie-item voor u in deze sectie. Een nieuwe gebruiker is gemaakt tijdens een poging tooaccess MOVEit overdracht - Azure AD-integratie als deze nog niet bestaat.

>[!NOTE]
>Als u handmatig een gebruiker toocreate nodig, moet u toocontact hello [MOVEit overdracht - ondersteuningsteam van Azure AD-integratie Client](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooMOVEit overdracht - Azure AD-integratie.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooMOVEit overdracht - Azure AD-integratie Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **MOVEit overdracht - Azure AD-integratie**.

    ![Hallo MOVEit overdracht - Azure AD-integratie koppelen in de lijst met Hallo-toepassingen](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Wanneer u klikt op Hallo MOVEit overdracht - tegel van Azure AD-integratie in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour MOVEit overdracht - toepassing voor Azure AD-integratie. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

