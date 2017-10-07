---
title: 'Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Adobe Creative Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Zelfstudie: Azure Active Directory-integratie met Adobe Creative Cloud

In deze zelfstudie leert u hoe toointegrate Adobe advertentie Cloud met Azure Active Directory (Azure AD).

Adobe Creative Cloud integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAdobe Creative Cloud heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAdobe Creative Cloud (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure Management portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Adobe Creative Cloud tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Adobe Creative Cloud eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Adobe Creative Cloud van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Het toevoegen van Adobe Creative Cloud van Hallo-galerie
tooconfigure hello integratie van Adobe Creative Cloud met Azure AD, moet u tooadd Adobe Creative Cloud uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Adobe Creative Cloud via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Management Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **toevoegen** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Adobe Creative Cloud**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Selecteer in het deelvenster resultaten hello, **Adobe Creative Cloud**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Adobe Creative Cloud op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Adobe Creative Cloud is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Adobe Creative Cloud toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Adobe Creative Cloud.

tooconfigure en eenmalige aanmelding Azure AD-test met Adobe Creative Cloud, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user)**  -toohave een equivalent van Britta Simon in Adobe Creative Cloud die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-beheerportal en eenmalige aanmelding configureren in uw toepassing Adobe Creative Cloud.

**tooconfigure eenmalige aanmelding Azure AD met Adobe Creative Cloud, Voer Hallo stappen te volgen:**

1. In hello Azure Management portal op Hallo **Adobe Creative Cloud** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** tooenable voor eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Op Hallo **Adobe Creative Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. In Hallo **id** textbox Hallo typewaarde als:`https://www.okta.com/saml2/service-provider/<token>`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Houd er rekening mee dat deze niet Hallo echte waarden zijn. U hebt deze waarden door de werkelijke id en de antwoord-URL Hallo tooupdate. We raden hier u toouse Hallo unieke waarde van een tekenreeks in Hallo id. Als u handmatig een gebruiker toocreate nodig, moet u toocontact Hallo Adobe Creative Cloud ondersteuningsteam.

4. Op Hallo **Adobe Creative Cloud-domein en de URL's** sectie, voert u Hallo volgende stappen uit als u wilt dat tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Klik op Hallo **weergeven geavanceerde instellingen voor URL** optie

    b. In Hallo **aanmeldings-URL** textbox Hallo typewaarde als:`https://adobe.com`

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Op Hallo **Adobe Creative Cloudconfiguratie** sectie, klikt u op **Adobe Creative Cloud configureren** tooopen **eenmalige aanmelding configureren** venster. Kopieer Hallo **SAML entiteit-Id** en **SAML SSO Service URL** van naslag-sectie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. In een ander browservenster, aanmelding tooyour Adobe Creative cloudtenant als beheerder.

8.  Ga te**identiteit** Hallo navigatiedeelvenster links en klikt u op uw domein. Voert de volgende stappen uit op Hallo **eenmalige aanmelding op configuratie vereist** sectie.

    ![Instellingen](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "instellingen")

9. Klik op **Bladeren** tooupload Hallo certificaat gedownload vanuit Azure AD te**IDP certificaat**.

10. In Hallo **IDP verlener** textbox Hallo-waarde van **SAML entiteit-Id** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.

11. In Hallo **IDP aanmeldings-URL** textbox Hallo-waarde van **SAML SSO Service URL** die u hebt gekopieerd uit **eenmalige aanmelding configureren** sectie in Azure-portal.

12. Selecteer **HTTP - omleiding** als **IDP Binding**.

13. Selecteer **e-mailadres** als **aanmelding gebruikersinstelling**.
 
14. Klik op **opslaan** knop.

15. Hallo dashboard biedt nu Hallo XML **'Metagegevens downloaden'** bestand. Het bevat van Adobe EntityDescriptor URL's en AssertionConsumerService. Hallo-bestand openen en deze configureren in Azure AD-toepassing hello.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Gebruik Hallo EntityDescriptor waarde Adobe geleverd, kunt u voor **id** op Hallo **App-instellingen configureren** dialoogvenster.

    b. Gebruik Hallo AssertionConsumerService waarde Adobe geleverd, kunt u voor **antwoord-URL** op Hallo **App-instellingen configureren** dialoogvenster.
 
### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-beheerportal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure Management portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Ga te**gebruikers en groepen** en klik op **alle gebruikers** toodisplay Hallo lijst met gebruikers.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Een testgebruiker Adobe Creative Cloud maken

In de volgorde tooenable Azure AD gebruikers toolog in Adobe Creative Cloud, moeten ze worden ingericht in Adobe Creative Cloud.  
In geval van Adobe Creative Cloud Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Aanmelden tooyour Adobe Creative Cloud bedrijf site als beheerder.

2. Klik op **mensen**.

    ![Mensen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "personen")

3. Klik op **gebruiker uitnodigen**.

    ![Gebruikers uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "gebruikers uitnodigen")

4. Op Hallo **personen uitnodigen** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Personen uitnodigen](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "personen uitnodigen")

    a. In Hallo **e** textbox type Hallo e-mailadres van Britta Simon account.
    
    b. Klik op **uitnodigen**.

    > [!NOTE]
    > Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar toegang tooAdobe Creative Cloud verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAdobe Creative Cloud Hallo stappen uitvoeren:**

1. Open in Hallo Azure Management portal Hallo toepassingen weergeven, en toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Adobe Creative Cloud**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Adobe Creative Cloud-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Adobe Creative Cloud-toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png