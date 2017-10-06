---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Zelfstudie: Azure Active Directory-integratie met Salesforce

In deze zelfstudie leert u hoe toointegrate Salesforce met Azure Active Directory (Azure AD).

Salesforce integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooSalesforce toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSalesforce (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Salesforce tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Salesforce eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Salesforce van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-salesforce-from-hello-gallery"></a>Het toevoegen van Salesforce van Hallo-galerie
tooconfigure hello integratie van Salesforce in Azure AD, moet u tooadd Salesforce uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Salesforce via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Salesforce**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. Selecteer in het deelvenster resultaten hello, **Salesforce**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Salesforce op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Salesforce is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Salesforce toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Salesforce.

tooconfigure en eenmalige aanmelding Azure AD-test met Salesforce, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Salesforce](#creating-a-salesforce-test-user)**  -toohave een equivalent van Britta Simon in Salesforce die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Salesforce-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met Salesforce, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Salesforce** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. Op Hallo **Salesforce-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen: 
   * Account voor de onderneming:`https://<subdomain>.my.salesforce.com`
   * Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Werk deze waarden met Hallo werkelijke aanmeldings-URL. Neem contact op met [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. Op Hallo **Salesforce configuratie** sectie, klikt u op **configureren Salesforce** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.** 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Een nieuw tabblad openen in uw browser en meld u bij tooyour Salesforce administrator-account.

8.  Onder Hallo **beheerder** navigatiedeelvenster, klikt u op **beveiligingsmechanismen** tooexpand Hallo gerelateerde sectie. Klik vervolgens op **instellingen voor eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  Op Hallo **instellingen voor eenmalige aanmelding** pagina, klikt u op Hallo **bewerken** knop.
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Als u instellingen voor eenmalige aanmelding niet kan tooenable voor uw Salesforce-account zijn, moet u mogelijk toocontact [Salesforce Client ondersteuningsteam](https://help.salesforce.com/support). 

10. Selecteer **SAML ingeschakeld**, en klik vervolgens op **opslaan**.

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure uw SAML eenmalige aanmelding-instellingen, klikt u op **nieuw**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. Op Hallo **SAML Single Sign-On instelling bewerken** maken Hallo volgende configuraties:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    a. Voor Hallo **naam** veld, typ een beschrijvende naam voor deze configuratie. Om een waarde voor **naam** automatisch invullen Hallo **API-naam** textbox.

    b. Plakken **SMAL entiteit-ID** waarde in Hallo **verlener** veld in Salesforce.

    c. In Hallo **tekstvak voor de entiteit-Id**, typ de naam van uw Salesforce-domein met Hallo patroon volgen:
      
      * Account voor de onderneming:`https://<subdomain>.my.salesforce.com`
      * Developer-account:`https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Klik op **Bladeren** of **bestand kiezen** tooopen hello **bestand kiezen tooUpload** dialoogvenster uw Salesforce-certificaat selecteren en klik vervolgens op **Openen**tooupload Hallo certificaat.

    e. Voor **SAML identiteitstype**, selecteer **verklaring van de gebruiker salesforce.com gebruikersnaam bevat**.

    f. Voor **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**

    g. Plakken **Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** veld in Salesforce.
    
    h. Voor **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP-omleiding**.
    
    ik. Tot slot op **opslaan** tooapply uw SAML eenmalige aanmelding-instellingen.

13. Klik op Hallo navigatiedeelvenster links in Salesforce **domeinbeheer** tooexpand Hallo bijbehorende sectie en klik vervolgens op **mijn domein**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Schuif omlaag toohello **verificatieconfiguratie** sectie en op Hallo **bewerken** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. In Hallo **verificatieservice** sectie, beschrijvende naam van uw configuratie SAML SSO Hallo selecteren en klik op **opslaan**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Als meer dan één authentication-service is ingeschakeld, kunnen gebruikers zich na vragen aan gebruiker tooselect welke verificatieservice die ze willen toosign met tijdens de initialisatie van eenmalige aanmelding tooyour Salesforce-omgeving. Als u niet dat deze toohappen wilt, dan u moet **laat alle andere verificatieservices uitgeschakeld**.
<CE>    
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Op Hallo linkernavigatiedeelvenster in Hallo **Azure-portal**, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-salesforce-test-user"></a>Een testgebruiker Salesforce maken

In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce. SalesForce ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.
Er is geen actie-item voor u in deze sectie. Als een gebruiker in Salesforce nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Salesforce probeert.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooSalesforce toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSalesforce, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Salesforce**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

tootest uw eenmalige aanmelding-instellingen, open Hallo Toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meldt u zich bij Hallo test-account en klikt u op **Salesforce**.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

