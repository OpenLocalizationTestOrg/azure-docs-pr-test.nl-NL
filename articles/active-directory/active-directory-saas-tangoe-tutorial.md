---
title: 'Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Tangoe opdracht Premium Mobile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Zelfstudie: Azure Active Directory-integratie met Tangoe opdracht Premium Mobile

In deze zelfstudie leert u hoe toointegrate Tangoe opdracht Premium mobiel met Azure Active Directory (Azure AD).

Tangoe opdracht Premium Mobile integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooTangoe opdracht Premium Mobile heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooTangoe opdracht Premium Mobile (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Tangoe opdracht Premium Mobile tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Tangoe opdracht Premium Mobile eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Tangoe opdracht Premium Mobile van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Tangoe opdracht Premium Mobile van Hallo galerie toevoegen
tooconfigure hello integratie van Tangoe opdracht Premium Mobile in Azure AD, moet u tooadd Tangoe opdracht Premium Mobile uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Tangoe opdracht Premium Mobile via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Tangoe opdracht Premium Mobile**, selecteer **Tangoe opdracht Premium Mobile** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Tangoe opdracht Premium Mobile uit de galerie toevoegen ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Tangoe opdracht Premium Mobile is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Tangoe opdracht Premium Mobile toobe tot stand gebracht.

Wijs in Tangoe opdracht Premium Mobile Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Tangoe opdracht Premium Mobile](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave een equivalent van Britta Simon in Tangoe opdracht Premium Mobile gekoppelde toohello Azure AD-weergave van de gebruiker is.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Tangoe opdracht Premium Mobile.

**tooconfigure eenmalige aanmelding Azure AD met Tangoe opdracht Premium Mobile Hallo stappen uitvoeren:**

1. In de Azure-portal op Hallo Hallo **Tangoe opdracht Premium Mobile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. Op Hallo **Tangoe opdracht Premium Mobile domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en mobiele Tangoe opdracht Premium-domein](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met Hallo werkelijke antwoord-URL en de aanmeldings-URL. Neem contact op met [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Klik op **opslaan** knop.

    ![knop Opslaan](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. Op Hallo **Tangoe Premium mobiele configuratie** sectie, klikt u op **configureren Tangoe opdracht Premium Mobile** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Configuratiesectie Tangoe opdracht Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO geconfigureerd voor uw toepassing, neem contact op met uw [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) en biedt de volgende Hallo:

   - Hallo gedownloade metagegevensbestand
   - Hallo **SAML entiteit-ID**
   - Hallo **SAML Single Sign-On Service-URL**
   - Hallo **Sign-Out URL**

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Gebruiker toevoegen](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Maak een testgebruiker Tangoe opdracht Premium Mobile

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Tangoe opdracht Premium Mobile maken. 

Tangoe opdracht Premium mobiele App moet alle Hallo gebruikers toobe ingericht in de toepassing hello voordat u eenmalige aanmelding. Dus neem werk Hello [Tangoe opdracht Premium Mobile Client ondersteuningsteam](https://www.tangoe.com/contact-2/) tooprovision deze gebruikers in de toepassing hello. 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTangoe opdracht Premium Mobile.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooTangoe opdracht Premium Mobile, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Tangoe opdracht Premium Mobile**.

    ![Tangoe opdracht Premium Mobile in lijst met Apps](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD SSO-configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Tangoe opdracht Premium Mobile tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Tangoe opdracht Premium Mobile-applicatie. Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

