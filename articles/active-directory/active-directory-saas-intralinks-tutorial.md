---
title: 'Zelfstudie: Azure Active Directory-integratie met Intralinks | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Intralinks.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Zelfstudie: Azure Active Directory-integratie met Intralinks

In deze zelfstudie leert u hoe toointegrate Intralinks met Azure Active Directory (Azure AD).

Intralinks integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooIntralinks toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooIntralinks (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Intralinks tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Intralinks eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Intralinks van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-intralinks-from-hello-gallery"></a>Het toevoegen van Intralinks van Hallo-galerie
tooconfigure hello integratie van Intralinks in Azure AD, moet u tooadd Intralinks uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Intralinks via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Intralinks**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Selecteer in het deelvenster resultaten hello, **Intralinks**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Intralinks op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Intralinks is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Intralinks toobe tot stand gebracht.

Wijs in Intralinks, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Intralinks, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Intralinks](#creating-an-intralinks-test-user)**  -toohave een equivalent van Britta Simon in Intralinks die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Intralinks configureren.

**Azure AD tooconfigure eenmalige aanmelding met Intralinks, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Intralinks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. Op Hallo **Intralinks domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Intralinks Client ondersteuningsteam](https://www.intralinks.com/contact-1) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. tooconfigure eenmalige aanmelding op **Intralinks** zijde, moet u toosend Hallo gedownload **Metadata XML** [Intralinks ondersteuningsteam](https://www.intralinks.com/contact-1). Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-intralinks-test-user"></a>Een testgebruiker Intralinks maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in Intralinks maken. Neem contact op met [Intralinks ondersteuningsteam](https://www.intralinks.com/contact-1) tooadd Hallo gebruikers in Hallo Intralinks platform.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooIntralinks toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooIntralinks, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Intralinks**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.

### <a name="add-intralinks-via-or-elite-application"></a>Intralinks VIA of Elite toepassing toevoegen

Maakt gebruik van Intralinks Hallo dezelfde SSO-identiteitsplatform voor alle andere Intralinks toepassingen met uitzondering van de Deal Nexus toepassing. Dus als u van plan toouse andere Intralinks-toepassing bent hebt eerst u tooconfigure SSO voor één primaire Intralinks toepassing hello procedure die hierboven worden beschreven.

Daarna kunt u volgen Hallo onderstaande procedure tooadd een andere Intralinks toepassing in uw tenant die u van deze primaire toepassing voor eenmalige aanmelding gebruikmaken kunt. 

>[!NOTE]
>Deze functie is beschikbaar alleen tooAzure AD Premium-SKU-klanten en niet beschikbaar voor klanten Free of basis-SKU.

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]


2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Intralinks**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. Op **app Intralinks toevoegen** Hallo volgende stappen uit te voeren:

    ![Intralinks VIA of Elite toepassing toe te voegen](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    a. In **naam** textbox geschikte naam van de toepassing hello bijvoorbeeld Voer **Intralinks Elite**.

    b. Klik op **toevoegen** knop.

6.  In de Azure-portal op Hallo Hallo **Intralinks** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

7. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **gekoppelde aanmelding**.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Ophalen van Hallo Hallo SP gestarte SSO-URL van [Intralinks team](https://www.intralinks.com/contact-1) Hallo voor andere Intralinks-toepassing en voer deze in **configureren aanmeldings-URL** zoals hieronder wordt weergegeven. 
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     Typ in Hallo aanmelding op URL textbox Hallo-URL die wordt gebruikt door uw gebruikers toosign op tooyour Intralinks toepassing met behulp van Hallo patroon volgen:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Hallo toepassing toouser of groepen toewijzen, zoals wordt weergegeven in de sectie Hallo  **[toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Intralinks-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Intralinks toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

