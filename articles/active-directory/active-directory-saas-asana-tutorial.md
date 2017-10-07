---
title: 'Zelfstudie: Azure Active Directory-integratie met Asana | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Asana.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Zelfstudie: Azure Active Directory-integratie met Asana

In deze zelfstudie leert u hoe toointegrate Asana met Azure Active Directory (Azure AD).

Asana integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooAsana toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooAsana (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Asana tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Asana eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Asana van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-asana-from-hello-gallery"></a>Het toevoegen van Asana van Hallo-galerie
tooconfigure hello integratie van Asana in Azure AD, moet u tooadd Asana uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Asana via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Asana**, selecteer **Asana** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Asana op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Asana is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Asana toobe tot stand gebracht.

Wijs in Asana, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Asana, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Asana](#create-an-asana-test-user)**  -toohave een equivalent van Britta Simon in Asana die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Asana configureren.

**Azure AD tooconfigure eenmalige aanmelding met Asana, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Asana** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Op Hallo **Asana domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Asana domein eenmalige aanmelding informatie](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ de URL:`https://app.asana.com/`

    b. In Hallo **id** textbox typewaarde:`https://app.asana.com/`
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Op Hallo **Asana configuratie** sectie, klikt u op **configureren Asana** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Asana configuratie](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. In een ander browservenster, aanmelding tooyour Asana toepassing. tooconfigure SSO in Asana, toegang Hallo werkruimte-instellingen door te klikken op Hallo de naam van de werkruimte op Hallo rechtsboven welkomstscherm. Klik vervolgens op  **\<naam van uw werkruimte\> instellingen**. 
   
    ![Asana SSO-instellingen](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Op Hallo **organisatie-instellingen** venster, klikt u op **beheer**. Klik vervolgens op **leden moeten zich aanmelden via SAML** tooenable Hallo SSO-configuratie. Hallo Hallo stappen uitvoeren:
   
    ![Eenmalige aanmelding, organisatie-instellingen configureren](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. In Hallo **aanmelden pagina-URL** textbox plakken Hallo **SAML Single Sign-On Service-URL**.

     b. Klik met de rechtermuisknop op Hallo-certificaat gedownload vanuit Azure-portal, open vervolgens Hallo certificaatbestand in Kladblok of uw voorkeur teksteditor. Kopiëren Hallo inhoud tussen Hallo beginnen en end certificaattitel Hallo en plak deze in Hallo **X.509-certificaat** textbox.

9. Klik op **Opslaan**. Ga te[Asana-handleiding voor het instellen van eenmalige aanmelding](https://asana.com/guide/help/premium/authentication#gl-saml) als u meer hulp nodig hebt.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-an-asana-test-user"></a>Een testgebruiker Asana maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Asana maken.

1. Op **Asana**, gaat u toohello **Teams** sectie in het linkerdeelvenster Hallo. Klik op Hallo plus knop aanmelden. 
   
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Typ Hallo e britta.simon@contoso.com in het tekstvak Hallo en selecteer vervolgens **uitnodigen**.

3. Klik op **uitnodiging verzenden**. Hallo nieuwe gebruiker ontvangt een e-mailbericht in haar e-mailaccount. Ze toocreate nodig hebt en Hallo account valideren.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooAsana toegang verleent.

![Hallo-gebruikersrollen toewijzen][200]

**tooassign Britta Simon tooAsana, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Asana**.

    ![Hallo Asana koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD eenmalige aanmelding.

Ga tooAsana aanmeldingspagina. Invoegen in Hallo e-mailadres tekstvak Hallo e-mailadres britta.simon@contoso.com. Hallo wachtwoordtekstvak laat in leeg en klik vervolgens op **aanmelden**. U zult omgeleid tooAzure AD-aanmeldingspagina. Voer uw Azure AD-referenties. U bent nu aangemeld op Asana.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
