---
title: 'Zelfstudie: Azure Active Directory-integratie met TalentLMS | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TalentLMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Zelfstudie: Azure Active Directory-integratie met TalentLMS

In deze zelfstudie leert u hoe toointegrate TalentLMS met Azure Active Directory (Azure AD).

TalentLMS integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooTalentLMS toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTalentLMS (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met TalentLMS tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een TalentLMS eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van TalentLMS van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-talentlms-from-hello-gallery"></a>Het toevoegen van TalentLMS van Hallo-galerie
tooconfigure hello integratie van TalentLMS in Azure AD, moet u tooadd TalentLMS uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd TalentLMS via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **TalentLMS**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. Selecteer in het deelvenster resultaten hello, **TalentLMS**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met TalentLMS op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in TalentLMS is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TalentLMS toobe tot stand gebracht.

Wijs in TalentLMS, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met TalentLMS, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker TalentLMS](#creating-a-talentlms-test-user)**  -toohave een equivalent van Britta Simon in TalentLMS die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing TalentLMS configureren.

**Azure AD tooconfigure eenmalige aanmelding met TalentLMS, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **TalentLMS** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. Op Hallo **TalentLMS domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.TalentLMSapp.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [TalentLMS Client ondersteuningsteam](https://www.talentlms.com/contact) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van Hallo-certificaat.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. Op Hallo **TalentLMS configuratie** sectie, klikt u op **configureren TalentLMS** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. In een ander browservenster, meld u aan tooyour TalentLMS bedrijf site als een beheerder.

8. In Hallo **& Accountinstellingen** sectie, klikt u op Hallo **gebruikers** tabblad.
   
    ![& Accountinstellingen](./media/active-directory-saas-talentlms-tutorial/IC777296.png "& Accountinstellingen")

9. Klik op **eenmalige aanmelding (SSO)**,

10. Voer in Hallo Single Sign-On sectie, Hallo stappen te volgen:
   
    ![Eenmalige aanmelding](./media/active-directory-saas-talentlms-tutorial/IC777297.png "eenmalige aanmelding")   

    a. Van Hallo **SSO-Integratietype** selecteert **SAML 2.0**.

    b. In Hallo **identiteitsprovider (IDP)** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.
 
    c. Plakken Hallo **vingerafdruk** waarde van de Azure-portal in Hallo **vingerafdruk van certificaat** textbox.    

    d.  In Hallo **extern aanmelden URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.
 
    e. In Hallo **externe URL voor afmelden** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    f. Vul Hallo volgende in: 

    * In Hallo **TargetedID** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * In Hallo **voornaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * In Hallo **achternaam** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * In Hallo **e** textbox type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
11. Klik op **Opslaan**.
 
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-talentlms-test-user"></a>Een testgebruiker TalentLMS maken

Azure AD tooenable gebruikers toolog in tooTalentLMS, ze in TalentLMS moeten worden ingericht. In geval van TalentLMS Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **TalentLMS** tenant.

2. Klik op **gebruikers**, en klik vervolgens op **gebruiker toevoegen**.

3. Op Hallo **gebruiker toevoegen** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
    ![Gebruiker toevoegen](./media/active-directory-saas-talentlms-tutorial/IC777299.png "gebruiker toevoegen")  

    a. In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.

    b. In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.
 
    c. In Hallo **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .

    d. Klik op **gebruiker toevoegen**.

>[!NOTE]
>U kunt andere TalentLMS gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door TalentLMS tooprovision AAD-gebruikersaccounts.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooTalentLMS toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTalentLMS, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **TalentLMS**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo TalentLMS-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TalentLMS toepassing

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

