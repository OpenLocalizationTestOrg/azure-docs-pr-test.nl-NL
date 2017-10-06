---
title: 'Zelfstudie: Azure Active Directory-integratie met Optimizely | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Optimizely.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a>Zelfstudie: Azure Active Directory-integratie met Optimizely

In deze zelfstudie leert u hoe toointegrate Optimizely met Azure Active Directory (Azure AD).

Optimizely integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooOptimizely toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooOptimizely (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Optimizely tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Optimizely eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Optimizely van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-optimizely-from-hello-gallery"></a>Het toevoegen van Optimizely van Hallo-galerie
tooconfigure hello integratie van Optimizely in Azure AD, moet u tooadd Optimizely uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Optimizely via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Optimizely**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. Selecteer in het deelvenster resultaten hello, **Optimizely**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Optimizely op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Optimizely is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Optimizely toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Optimizely.

tooconfigure en eenmalige aanmelding Azure AD-test met Optimizely, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Optimizely](#creating-an-optimizely-test-user)**  -toohave een equivalent van Britta Simon in Optimizely die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Optimizely configureren.

**Azure AD tooconfigure eenmalige aanmelding met Optimizely, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Optimizely** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. Op Hallo **Optimizely domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://app.optimizely.net/<instance name>`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`urn:auth0:optimizely:contoso`

    > [!NOTE] 
    > Deze waarden zijn niet Hallo echte. Hallo-waarde wordt bijgewerkt met Hallo werkelijke aanmeldings-URL en de id, die verderop in Hallo zelfstudie wordt uitgelegd. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. Op Hallo **Optimizely configuratie** sectie, klikt u op **configureren Optimizely** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. tooconfigure eenmalige aanmelding op **Optimizely** zijde, neem contact op met uw accountmanager Optimizely en bieden Hallo gedownload **certificaat (Base64)**, en **SAML Single Sign-On Service-URL** . 

8. In het antwoord tooyour e-mail biedt Optimizely u Hallo aanmelding op URL (Serviceprovider geïnitieerde SSO) en Hallo identificatiewaarden (Service Provider entiteit-ID).

    a. Kopiëren Hallo **Serviceprovider geïnitieerde eenmalige aanmelding URL** opgegeven door Optimizely en plakken in Hallo **aanmelding op URL** textbox in **Optimizely domein en de URL's** sectie in Azure portal 

    b. Kopiëren Hallo **Service Provider entiteit-ID** opgegeven door Optimizely en plakken in Hallo **id** textbox in **Optimizely domein en de URL's** sectie in Azure portal 

9. In een ander browservenster, aanmelding tooyour Optimizely toepassing.

10. Klikt u op dat u de accountnaam in de bovenste Hallo rechterbovenhoek en vervolgens **Accountinstellingen**.
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. In het tabblad Account Hallo selectievakje Hallo **eenmalige aanmelding inschakelen** onder eenmalige aanmelding in Hallo **overzicht** sectie.
   
    ![Azure AD voor eenmalige aanmelding](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. Klik op **opslaan**

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van Britta Simon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-optimizely-test-user"></a>Een testgebruiker Optimizely maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Optimizely maken.

1. Selecteer op de startpagina van Hallo **deelnemers** tabblad.

2. tooadd nieuwe medewerker toohello project, klik op **nieuwe medewerker**.
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. Vul Hallo e-mailadres en een rol toewijzen. Klik op **uitnodigen**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. Ze ontvangen een e-uitnodiging. Hallo e-mailadres hebben ze toolog in tooOptimizely.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOptimizely toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooOptimizely, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Optimizely**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Optimizely tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Optimizely toepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

