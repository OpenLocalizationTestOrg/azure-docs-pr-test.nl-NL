---
title: 'Zelfstudie: Azure Active Directory-integratie met de Planning van Predictix assortiment | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Predictix assortiment plannen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1294b712caf12fdafaf65d70a02ee9fbdc3e84a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a>Zelfstudie: Azure Active Directory-integratie met Predictix assortiment plannen

In deze zelfstudie leert u hoe toointegrate Predictix assortiment plannen met Azure Active Directory (Azure AD).

Predictix assortimentplanning integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooPredictix assortiment plannen heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooPredictix assortiment plannen (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met de Planning van Predictix assortiment tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Predictix assortimentplanning eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Predictix assortiment plannen van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-predictix-assortment-planning-from-hello-gallery"></a>Het toevoegen van Predictix assortiment plannen van Hallo-galerie
tooconfigure hello integratie van de Planning van Predictix assortiment in Azure AD, moet u tooadd Predictix assortiment plannen uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Predictix assortimentplanning via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Predictix assortiment plannen**, selecteer **Predictix assortimentplanning** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo toepassing.

    ![Predictix assortiment plannen in de lijst met resultaten Hallo](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Predictix assortiment plannen op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in de Planning van Predictix assortiment is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker bij het plannen van Predictix assortiment Hallo toobe tot stand gebracht.

Bij het plannen van Predictix assortiment, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Predictix assortimentplanning, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Predictix assortimentplanning](#create-a-predictix-assortment-planning-test-user)**  -toohave een equivalent van Britta Simon Predictix assortiment plannen die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Predictix assortiment plannen.

**tooconfigure Azure AD eenmalige aanmelding met de Predictix assortimentplanning, Voer Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **Predictix assortimentplanning** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. Op Hallo **Predictix assortiment Planning domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Predictix assortiment Planning domein eenmalige aanmelding informatie](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Predictix assortiment Planning Client ondersteuningsteam](http://www.infor.com/support) tooget deze waarden. 
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. Op Hallo **Predictix assortiment Planning configuratie** sectie, klikt u op **configureren Predictix assortimentplanning** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Predictix assortiment Planning configuratie](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. tooconfigure eenmalige aanmelding op **Predictix assortimentplanning** zijde, moet u toosend Hallo gedownload **Certificate(Base64)**, **SAML entiteit-ID**,  **SAML Single Sign-On Service-URL**, en **Sign-Out URL** te[ondersteuningsteam Predictix assortimentplanning](http://www.infor.com/support). Ze deze instelling toohave Hallo SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-predictix-assortment-planning-test-user"></a>Maak een testgebruiker Predictix assortiment plannen

In deze sectie maakt u Britta Simon aangeroepen bij het plannen van Predictix assortiment van een gebruiker. Neem contact op met [ondersteuningsteam Predictix assortimentplanning](http://www.infor.com/contact/) tooadd Hallo gebruikers in Hallo Predictix assortimentplanning platform.
 > [!NOTE]
 > Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooPredictix assortiment plannen.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooPredictix assortimentplanning, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Predictix assortimentplanning**.

    ![Hallo Predictix assortiment plannen koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Predictix assortimentplanning tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour toepassing Predictix assortiment plannen.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

