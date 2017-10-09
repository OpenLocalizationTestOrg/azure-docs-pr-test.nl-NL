---
title: 'Zelfstudie: Azure Active Directory-integratie met SpringCM | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a>Zelfstudie: Azure Active Directory-integratie met SpringCM

In deze zelfstudie leert u hoe toointegrate SpringCM met Azure Active Directory (Azure AD).

SpringCM integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSpringCM toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSpringCM (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SpringCM tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SpringCM eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SpringCM van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-springcm-from-hello-gallery"></a>Het toevoegen van SpringCM van Hallo-galerie
tooconfigure hello integratie van SpringCM in Azure AD, moet u tooadd SpringCM uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SpringCM via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SpringCM**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. Selecteer in het deelvenster resultaten hello, **SpringCM**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SpringCM op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SpringCM is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SpringCM toobe tot stand gebracht.

Wijs in SpringCM, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met SpringCM, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker SpringCM](#creating-a-springcm-test-user)**  -toohave een equivalent van Britta Simon in SpringCM die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing SpringCM configureren.

**Azure AD tooconfigure eenmalige aanmelding met SpringCM, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **SpringCM** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. Op Hallo **SpringCM domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [SpringCM Client ondersteuningsteam](https://knowledge.springcm.com/support) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Raw)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. Op Hallo **SpringCM configuratie** sectie, klikt u op **configureren SpringCM** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. Een ander browservenster, meld u aan bij tooyour **SpringCM** bedrijf site als administrator.

8. Klik in het menu bovenaan Hallo Hallo **Ga naar**, klikt u op **voorkeuren**, en klikt u op Hallo **accountvoorkeuren** sectie, klikt u op **SAML SSO**.
   
    ![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML EENMALIGE AANMELDING")

9. Uitvoeren in Hallo identiteit Provider-configuratiesectie, Hallo stappen te volgen:
   
    ![Configuratie van de Provider identiteit](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "providerconfiguratie identiteit")
    
    a. tooupload uw gedownloade certificaat van de Azure Active Directory, klikt u op **uitgeverscertificaat selecteren** of **wijziging uitgeverscertificaat**.
    
    b. Plakken **SAML entiteit-ID** waarde, die u hebt gekopieerd vanuit Azure-portal in Hallo **verlener** textbox.
    
    c. Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **Service Provider (SP) geïnitieerd eindpunt** textbox.
            
    d. Selecteer **SAML ingeschakeld** als **inschakelen**.

    e. Klik op **Opslaan**.
 
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-springcm-test-user"></a>Een testgebruiker SpringCM maken

tooenable Azure Active Directory-gebruikers toolog in tooSpringCM, ze in SpringCM moeten worden ingericht. In geval van SpringCM Hallo is inrichting een handmatige taak.

>[!NOTE]
>Zie voor meer informatie [maken en bewerken van een gebruiker SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user). 

**een gebruiker account-tooSpringCM tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **SpringCM** bedrijf site als administrator.

2. Klik op **GOTO**, en klik vervolgens op **ADRESBOEK**.
   
    ![Gebruiker maken](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "gebruiker maken")

3. Klik op **gebruiker maken**.

4. Selecteer een **gebruikersrol**.

5. Selecteer **activering E-mail verzenden**.

6. Type Hallo voornaam en achternaam e-mailadres van een geldige Azure Active Directory-gebruikersaccount gewenste tooprovision in Hallo gerelateerd tekstvakken.

7. Toevoegen van Hallo gebruiker tooa **beveiligingsgroep**.

8. Klik op **Opslaan**.

  >[!NOTE]
  >U kunt andere SpringCM gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door SpringCM tooprovision AAD-gebruikersaccounts.  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSpringCM toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSpringCM, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SpringCM**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.
 
Als u op Hallo SpringCM tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SpringCM toepassing.

Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

