---
title: 'Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Dropbox voor bedrijven.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Zelfstudie: Azure Active Directory-integratie met Dropbox voor bedrijven

In deze zelfstudie leert u hoe toointegrate Dropbox voor bedrijven gebruiken met Azure Active Directory (Azure AD).

Dropbox voor bedrijven integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooDropbox voor bedrijven heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooDropbox voor bedrijven (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Dropbox voor bedrijven, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Dropbox voor eenmalige aanmelding Business abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Dropbox voor bedrijven van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Het toevoegen van Dropbox voor bedrijven van Hallo-galerie
tooconfigure hello integratie van Dropbox voor bedrijven met Azure AD, moet u tooadd Dropbox uit Hallo galerie tooyour lijst met beheerde SaaS-apps voor bedrijven.

**tooadd Dropbox voor bedrijven via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Dropbox voor bedrijven**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. Selecteer in het deelvenster resultaten hello, **Dropbox voor bedrijven**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Dropbox voor bedrijven op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Dropbox voor bedrijven is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Dropbox voor bedrijven toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Dropbox voor bedrijven.

tooconfigure en test eenmalige aanmelding Azure AD met Dropbox voor bedrijven, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Dropbox voor zakelijke testgebruiker](#creating-a-dropbox-for-business-test-user)**  -toohave een equivalent van Britta Simon in Dropbox voor bedrijven die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw dropbox geplaatst voor Business-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met Dropbox voor bedrijven, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Dropbox voor bedrijven** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Op Hallo **Dropbox voor Business-domein en URL's** sectie, voert u Hallo stappen te volgen:

    a. Meld u aan op tooyour Dropbox voor bedrijven-tenant. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "eenmalige aanmelding configureren")
   
    b. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beheerconsole**. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "eenmalige aanmelding configureren")
   
    c. Op Hallo **beheerconsole**, klikt u op **verificatie** in het linkernavigatievenster Hallo. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "eenmalige aanmelding configureren")
   
    d. In Hallo **eenmalige aanmelding** sectie **eenmalige aanmelding inschakelen**, en klik vervolgens op **meer** tooexpand in deze sectie.  
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "eenmalige aanmelding configureren")
   
    e. Kopieer de URL Hallo naast te**kunnen gebruikers zich aanmelden door te voeren van het e-mailadres of kunnen ze rechtstreeks naar**. 
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. Op de Azure-portal, op Hallo Hallo **aanmeldings-URL** textbox plakken Hallo-URL.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Deze waarde is geen echte waarde. Hallo waarde bijwerken met Hallo werkelijke aanmeldings-URL u via een sectie voor eenmalige aanmelding krijgen. Neem contact op met [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Op Hallo **Dropbox voor zakelijke configuratie** sectie, klikt u op **Dropbox configureren voor bedrijven** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure eenmalige aanmelding op **Dropbox voor bedrijven** zijde, gaat u op uw Dropbox voor bedrijven-tenant in Hallo **eenmalige aanmelding** sectie Hallo **verificatie** pagina Voer Hallo stappen te volgen: 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "eenmalige aanmelding configureren")
   
    a. Klik op **vereist**.
   
    b. In de Azure-portal op Hallo Hallo **eenmalige aanmelding configureren** venster, kopie Hallo **SAML Single Sign-On Service-URL** waarde en plak deze in Hallo **aanmelden URL** textbox.

    c. Klik op **certificaat kiezen**, en blader vervolgens tooyour **Base64-gecodeerde certificaatbestand**.

    d. Klik op **wijzigingen opslaan** toocomplete Hallo-configuratie op uw DropBox voor bedrijven-tenant.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Een Dropbox voor zakelijke testgebruiker maken

In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Dropbox voor bedrijven. Dropbox voor bedrijven ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.

Er is geen actie-item voor u in deze sectie. Als een gebruiker niet al in Dropbox voor bedrijven bestaat, wordt een nieuw gemaakt wanneer u tooaccess Dropbox voor bedrijven probeert.

>[!Note]
>Als u een gebruiker handmatig, neem contact op met toocreate moet [Dropbox voor Business Client ondersteuningsteam](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooDropbox voor bedrijven.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooDropbox voor bedrijven, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Dropbox voor bedrijven**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Dropbox hello voor bedrijven-tegel in Hallo toegangsvenster klikt, krijgt u de aanmeldingspagina van uw Dropbox voor Business-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

