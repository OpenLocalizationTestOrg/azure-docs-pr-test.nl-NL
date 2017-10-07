---
title: 'Zelfstudie: Azure Active Directory-integratie met Zendesk | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zendesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Zelfstudie: Azure Active Directory-integratie met Zendesk

In deze zelfstudie leert u hoe toointegrate Zendesk met Azure Active Directory (Azure AD).

Zendesk integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooZendesk toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooZendesk (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Zendesk tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Zendesk eenmalige aanmelding ingeschakeld abonnement


> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.


tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Zendesk van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding


## <a name="adding-zendesk-from-hello-gallery"></a>Het toevoegen van Zendesk van Hallo-galerie
tooconfigure hello integratie van Zendesk in Azure AD, moet u tooadd Zendesk uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Zendesk via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure Portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Zendesk**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. Selecteer in het deelvenster resultaten hello, **Zendesk**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Zendesk op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Zendesk is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker in de Zendesk toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Zendesk.

tooconfigure en eenmalige aanmelding Azure AD-test met Zendesk, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Zendesk](#creating-a-zendesk-test-user)**  -toohave een equivalent van Britta Simon in Zendesk die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Zendesk-toepassing.

**Azure AD tooconfigure eenmalige aanmelding met Zendesk, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Zendesk** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. Op Hallo **Zendesk-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.zendesk.com`

    b. In Hallo **id** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en identificatie-URL. Neem contact op met [Zendesk-ondersteuningsteam](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget deze waarden. 

4. Hallo SAML asserties verwacht Zendesk in een specifieke indeling. Er zijn geen verplichte SAML-kenmerken, maar u kunt desgewenst een kenmerk uit toevoegen **gebruikerskenmerken** sectie door de volgende Hallo onderstaande stappen te volgen: 

     ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Klik op Hallo **weergeven en bewerken Hallo andere kenmerken** selectievakje.
     
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Klik op Hallo **kenmerk toevoegen** tooopen **toevoegen kenmerk** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. In Hallo **naam** textbox typenaam van het Hallo-kenmerk (bijvoorbeeld **emailaddress**).
    
    d. Van Hallo **waarde** wilt weergeven, selecteer Hallo kenmerkwaarde (als **user.mail**).
    
    e. Klik op **Ok**
 
    > [!NOTE] 
    > U kenmerken tooadd uitbreidingskenmerken die zich niet in Azure AD standaard gebruiken. Klik op [gebruikerskenmerken die kunnen worden ingesteld in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) kenmerken van een volledige lijst met tooget Hallo van SAML **Zendesk** accepteert. 

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. Op Hallo **Zendesk configuratie** sectie, klikt u op **configureren Zendesk** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Zendesk site als beheerder.

8. Klik op **Admin**.

9. Klik in het Hallo navigatiedeelvenster links op **instellingen**, en klik vervolgens op **beveiliging**.

10. Op Hallo **beveiliging** pagina, voert u Hallo stappen te volgen: 
   
     ![Beveiliging](./media/active-directory-saas-zendesk-tutorial/ic773089.png "beveiliging")

    ![Eenmalige aanmelding](./media/active-directory-saas-zendesk-tutorial/ic773090.png "eenmalige aanmelding")

     a. Klik op Hallo **Admin & Agents** tabblad.

     b. Selecteer **eenmalige aanmelding (SSO) en SAML**, en selecteer vervolgens **SAML**.

     c. In **SAML SSO URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal. 

     d. In **externe URL voor afmelden** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
        
     e. In **vingerafdruk van certificaat** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.
     
     f. Klik op **Opslaan**.

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**. 

### <a name="creating-a-zendesk-test-user"></a>Een testgebruiker Zendesk maken

Azure AD tooenable gebruikers toolog in **Zendesk**, deze moeten worden ingericht in **Zendesk**.  
Afhankelijk van het Hallo-rol is toegewezen in Hallo apps, verwacht dat de Hallo gedrag:

 1. **Eindgebruikers** accounts automatisch worden ingericht als u zich aanmeldt.
 2. **Agent** en **Admin** accounts moeten handmatig worden ingericht in toobe **Zendesk** voordat u zich aanmeldt.
 
**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Zendesk** tenant.

2. Selecteer Hallo **klantenlijst** tabblad.

3. Selecteer Hallo **gebruiker** tabblad en klik op **toevoegen**.
   
    ![Gebruiker toevoegen](./media/active-directory-saas-zendesk-tutorial/ic773632.png "gebruiker toevoegen")
4. Typ de e-mailadres Hallo van een bestaande Azure AD-account dat u wilt tooprovision en klik vervolgens op **opslaan**.
   
    ![Nieuwe gebruiker](./media/active-directory-saas-zendesk-tutorial/ic773633.png "nieuwe gebruiker")

> [!NOTE]
> U kunt andere Zendesk gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Zendesk tooprovision AAD-gebruikersaccounts.


### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooZendesk toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooZendesk, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Zendesk**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Zendesk-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zendesk-toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
