---
title: 'Zelfstudie: Azure Active Directory-integratie met e-mailadres SkyDesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SkyDesk e-mailbericht.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a>Zelfstudie: Azure Active Directory-integratie met SkyDesk e-mailadres

In deze zelfstudie leert u hoe het e-toointegrate SkyDesk met Azure Active Directory (Azure AD).

E-mailadres SkyDesk integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSkyDesk e heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSkyDesk e (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met e-mailadres SkyDesk tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een e-mailadres SkyDesk eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u hier een proefversie van één maand krijgen [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SkyDesk e van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-skydesk-email-from-hello-gallery"></a>Het toevoegen van SkyDesk e van Hallo-galerie
tooconfigure hello integratie van SkyDesk E-mail in Azure AD, moet u tooadd SkyDesk e uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SkyDesk E-mail via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SkyDesk e**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. Selecteer in het deelvenster resultaten hello, **SkyDesk e**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met SkyDesk e-mailadres op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SkyDesk e-mailbericht is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SkyDesk e-mailbericht toobe tot stand gebracht.

In het e-mailadres SkyDesk Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met SkyDesk e-mailadres, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SkyDesk e](#creating-a-skydesk-email-test-user)**  -toohave een equivalent van Britta Simon in SkyDesk e-mailbericht is gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw SkyDesk e-mailtoepassing configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met e-mailadres SkyDesk Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **SkyDesk e** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. Op Hallo **SkyDesk e-maildomein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://mail.skydesk.jp/portal/<companyname>`

    > [!NOTE] 
    > Hallo-waarde is geen echte. Waarde van de update Hallo met Hallo werkelijke aanmeldings-URL. Neem contact op met [SkyDesk e-mailclient ondersteuningsteam](https://www.skydesk.sg/support/) tooget Hallo waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. Op Hallo **SkyDesk e-mailconfiguratie** sectie, klikt u op **configureren SkyDesk e** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. tooenable SSO in **SkyDesk e**, Hallo volgende stappen uit te voeren:

    a. Eenmalige aanmelding tooyour SkyDesk e-mailaccount als administrator.

    b. Klik in het menu bovenaan Hallo Hallo **Setup**, en selecteer **Org**. 
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    c. Klik op **domeinen** van het linkerpaneel Hallo.
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    d. Klik op **domein toevoegen**.
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    e. Voer uw domeinnaam en controleer vervolgens Hallo domein.
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    f. Klik op **SAML-verificatie** van het linkerpaneel Hallo.
    
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. Op Hallo **SAML-verificatie** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    >toouse SAML gebaseerde verificatie, hebt u ofwel **gecontroleerde domein** of **portal URL** setup. U kunt instellen Hallo portal URL met Hallo unieke naam.
    > 
    > 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    a. In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
   
    b. In Hallo **afmelding** tekstvak URL plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    c. **De URL van het wachtwoord wijzigen** is optioneel dus laat dit veld leeg.

    d. Klik op **sleutelbestand ophalen** tooselect uw gedownloade certificaat van de Azure-portal en klik vervolgens op **Open** tooupload Hallo certificaat.

    e. Als **algoritme**, selecteer **RSA**.

    f. Klik op **Ok** toosave Hallo wijzigingen.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-skydesk-email-test-user"></a>Maken van een testgebruiker SkyDesk e

In deze sectie kunt u een gebruiker met de naam van Britta Simon in SkyDesk E-mail maken.

1. Klik op **gebruikerstoegang** van Hallo links van het deelvenster in SkyDesk e-mailbericht en voer uw gebruikersnaam. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
>Als u toocreate bulksgewijs gebruikers moet, moet u toocontact hello [SkyDesk e-mailclient ondersteuningsteam](https://www.skydesk.sg/support/).


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSkyDesk e-mailbericht.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSkyDesk e-mailadres Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SkyDesk e**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD SSO-configuratie met Hallo Toegangsvenster.

Als u op Hallo SkyDesk e-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SkyDesk e-mailtoepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

