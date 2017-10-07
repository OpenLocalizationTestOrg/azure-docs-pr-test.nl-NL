---
title: 'Zelfstudie: Azure Active Directory-integratie met SD-elementen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SD-elementen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a>Zelfstudie: Azure Active Directory-integratie met SD-elementen

In deze zelfstudie leert u hoe toointegrate SD-elementen met Azure Active Directory (Azure AD).

SD-elementen integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSD elementen heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSD elementen (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met SD-elementen, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SD-elementen eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SD-elementen uit de galerie Hallo
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sd-elements-from-hello-gallery"></a>Het toevoegen van SD-elementen uit de galerie Hallo
tooconfigure hello integratie van SD-elementen in Azure AD, moet u tooadd SD-elementen in Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SD-elementen uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SD-elementen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. Selecteer in het deelvenster resultaten hello, **SD-elementen**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met SD-elementen die op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SD-elementen is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SD-elementen toobe tot stand gebracht.

In de SD-elementen, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met SD-elementen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SD-elementen testgebruiker](#creating-a-sd-elements-test-user)**  -toohave een equivalent van Britta Simon in SD-elementen die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SD-elementen.

**Voer tooconfigure Azure AD eenmalige aanmelding met SD-elementen Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **SD-elementen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. Op Hallo **SD-elementen domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/metadata`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.sdelements.com/sso/saml2/acs/`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) tooget deze waarden.

4. Hallo SAML asserties verwacht toepassing SD-elementen in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Gebruikerskenmerk'** tabblad van de toepassing hello. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen: 

    | Naam van kenmerk | De waarde van kenmerk |
    | --- | --- |
    | E-mail |User.mail |
    | Voornaam |User.givenName |
    | Achternaam |User.surname |

    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.

    d. Klik op **OK**.
 
6. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. Op Hallo **SD-elementen configuratie** sectie, klikt u op **SD-elementen configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. tooget eenmalige aanmelding is ingeschakeld, neem contact op met uw [SD-elementen ondersteuningsteam](mailto:support@sdelements.com) en geeft u het gedownloade bestand Hallo. 

10. In een ander browservenster, aanmelding tooyour SD-elementen tenant als beheerder.

11. Klik in het menu bovenaan Hallo Hallo **System**, en vervolgens **Single Sign-on**. 
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. Op Hallo **instellingen voor eenmalige aanmelding** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    a. Als **SSO Type**, selecteer **SAML**.
   
    b. In Hallo **identiteit Provider entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal. 
   
    c. In Hallo **Provider Single Sign-On Identiteitsservice** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal. 
   
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-sd-elements-test-user"></a>Maken van een testgebruiker SD-elementen

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in SD-elementen van een gebruiker. In geval van SD-elementen Hallo is elementen van de SD-gebruikers te maken een handmatige taak.

**toocreate Britta Simon in SD-elementen, Voer Hallo stappen te volgen:**

1. In een browservenster, aanmelding tooyour SD-elementen bedrijf site als beheerder.

2. Klik in het menu bovenaan Hallo Hallo **Gebruikersbeheer**, en vervolgens **gebruikers**.
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. Klik op **nieuwe gebruiker toevoegen**.
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. Op Hallo **nieuwe gebruiker toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Maken van een testgebruiker SD-elementen](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    a. In Hallo **e** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .
   
    b. In Hallo **voornaam** textbox Voer Hallo voornaam van de gebruiker zoals **Britta**.
   
    c. In Hallo **achternaam** textbox Voer Hallo achternaam van de gebruiker zoals **Simon**.
   
    d. Als **rol**, selecteer **gebruiker**. 
   
    e. Klik op **gebruiker maken**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSD elementen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSD elementen, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SD-elementen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.
  
Wanneer u Hallo SD-elementen in het deelvenster toegang Hallo tegel klikt, krijgt u automatisch aangemelde tooyour elementen van de SD-toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

