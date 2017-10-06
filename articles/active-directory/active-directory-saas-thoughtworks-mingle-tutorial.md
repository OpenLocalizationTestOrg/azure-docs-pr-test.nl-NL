---
title: 'Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Thoughtworks Singleplayer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a>Zelfstudie: Azure Active Directory-integratie met Thoughtworks Singleplayer

In deze zelfstudie leert u hoe toointegrate Thoughtworks Singleplayer met Azure Active Directory (Azure AD).

Thoughtworks Singleplayer integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooThoughtworks Mingle heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooThoughtworks Mingle (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Thoughtworks Singleplayer tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Thoughtworks Singleplayer eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Thoughtworks Singleplayer van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a>Het toevoegen van Thoughtworks Singleplayer van Hallo-galerie
tooconfigure hello integratie van Thoughtworks Singleplayer in Azure AD, moet u tooadd Thoughtworks Singleplayer uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Thoughtworks Singleplayer via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Thoughtworks Singleplayer**, selecteer **Thoughtworks Singleplayer** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Thoughtworks Singleplayer in de lijst met resultaten Hallo](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met Thoughtworks Singleplayer op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Thoughtworks Singleplayer is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Thoughtworks Singleplayer toobe tot stand gebracht.

Wijs in het Thoughtworks Singleplayer, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Thoughtworks Singleplayer, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Thoughtworks Singleplayer](#create-a-thoughtworks-mingle-test-user)**  -toohave een equivalent van Britta Simon in Thoughtworks Singleplayer die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Thoughtworks Singleplayer configureren.

**Azure AD tooconfigure eenmalige aanmelding met Thoughtworks Singleplayer, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Thoughtworks Singleplayer** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. Op Hallo **Thoughtworks Singleplayer domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Thoughtworks Singleplayer domein eenmalige aanmelding informatie](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.mingle.thoughtworks.com`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [Thoughtworks Singleplayer Client ondersteuningsteam](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget Hallo waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. Meld u bij tooyour **Thoughtworks Singleplayer** bedrijf site als administrator.

7. Klik op Hallo **Admin** tabblad en klik vervolgens op **SSO-Config**.
   
    ![Tabblad beheer](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO-configuratie")

8. In Hallo **SSO-Config** sectie, voert u Hallo stappen te volgen:
   
    ![SSO-Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO-configuratie")
    
    a. metagegevensbestand tooupload hello, klikt u op **bestand kiezen**. 

    b. Klik op **wijzigingen opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-thoughtworks-mingle-test-user"></a>Een testgebruiker Thoughtworks Singleplayer maken

Voor Azure AD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello Thoughtworks Singleplayer toepassing met behulp van de namen van de Azure Active Directory-gebruiker zijn. In geval van Thoughtworks Singleplayer Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Aanmelden tooyour Thoughtworks Singleplayer bedrijf site als administrator.

2. Klik op **profiel**.
   
    ![Uw eerste Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "uw eerste Project")

3. Klik op Hallo **Admin** tabblad en klik vervolgens op **gebruikers**.
   
    ![Gebruikers](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "gebruikers")

4. Klik op **nieuwe gebruiker**.
   
    ![Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "nieuwe gebruiker")

5. Op Hallo **nieuwe gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Dialoogvenster Nieuwe gebruiker](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "nieuwe gebruiker")  
 
    a. Type Hallo **aanmeldingsnaam**, **weergavenaam**, **Kies wachtwoord**, **wachtwoord bevestigen** van een geldig Azure AD-account die u wilt dat tooprovision gerelateerde in Hallo tekstvakken. 

    b. Als **gebruikerstype**, selecteer **volledige gebruiker**.

    c. Klik op **maken van dit profiel**.

>[!NOTE]
>U kunt andere Thoughtworks Singleplayer gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door tooprovision Thoughtworks Singleplayer AAD-gebruikersaccounts.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooThoughtworks Mingle.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooThoughtworks Mingle, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Thoughtworks Singleplayer**.

    ![Hallo Thoughtworks Singleplayer koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Thoughtworks Singleplayer tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Thoughtworks Singleplayer toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

