---
title: 'Zelfstudie: Azure Active Directory-integratie met Freshservice | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Zelfstudie: Azure Active Directory-integratie met Freshservice

In deze zelfstudie leert u hoe toointegrate Freshservice met Azure Active Directory (Azure AD).

Freshservice integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooFreshservice toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooFreshservice (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Freshservice tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Freshservice eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Freshservice van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-freshservice-from-hello-gallery"></a>Het toevoegen van Freshservice van Hallo-galerie
tooconfigure hello integratie van Freshservice in Azure AD, moet u tooadd Freshservice uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Freshservice via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Freshservice**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. Selecteer in het deelvenster resultaten hello, **Freshservice**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Freshservice op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Freshservice is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Freshservice toobe tot stand gebracht.

Wijs in Freshservice, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Freshservice, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Freshservice](#creating-a-freshservice-test-user)**  -toohave een equivalent van Britta Simon in Freshservice die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Freshservice configureren.

**Azure AD tooconfigure eenmalige aanmelding met Freshservice, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Freshservice** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. Op Hallo **Freshservice domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<democompany>.freshservice.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Freshservice Client ondersteuningsteam](https://support.freshservice.com/) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, Kopieer **VINGERAFDRUK** waarde van het certificaat.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. Op Hallo **Freshservice configuratie** sectie, klikt u op **configureren Freshservice** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. In een ander browservenster, meld u aan tooyour Freshservice bedrijf site als een beheerder.

8. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
    ![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")

9. In Hallo **Customer Portal**, klikt u op **beveiliging**.
   
    ![Beveiliging](./media/active-directory-saas-freshservice-tutorial/ic790815.png "beveiliging")

10. In Hallo **beveiliging** sectie, voert u Hallo stappen te volgen:
   
    ![Eenmalige aanmelding](./media/active-directory-saas-freshservice-tutorial/ic790816.png "eenmalige aanmelding")
   
    a. Switch **eenmalige aanmelding**.

    b. Selecteer **SAML SSO**.

    c. In Hallo **aanmeldings-URL van SAML** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    d. In Hallo **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

    e. In **beveiliging certificaat vingerafdruk** textbox plakken Hallo **VINGERAFDRUK** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.

    f. Klik op **opslaan**
   
> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-freshservice-test-user"></a>Een testgebruiker Freshservice maken

Azure AD tooenable gebruikers toolog in tooFreshService, ze in FreshService moeten worden ingericht. In geval van FreshService Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **FreshService** bedrijf site als beheerder.

2. Klik in het menu bovenaan Hallo Hallo **Admin**.
   
    ![Beheerder](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")

3. In Hallo **Gebruikersbeheer** sectie, klikt u op **aanvragers**.
   
    ![Aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790818.png "aanvragers")

4. Klik op **nieuwe aanvrager**.
   
    ![Nieuwe aanvragers](./media/active-directory-saas-freshservice-tutorial/ic790819.png "nieuwe aanvragers")

5. In Hallo **nieuwe aanvrager** sectie, voert u Hallo stappen te volgen:
   
    ![Nieuwe aanvrager](./media/active-directory-saas-freshservice-tutorial/ic790820.png "nieuwe aanvrager")   

    a. Voer Hallo **voornaam** en **e** kenmerken van een geldige Azure Active Directory-account dat u wilt dat tooprovision in Hallo gerelateerde tekstvakken.

    b. Klik op **Opslaan**.
   
    >[!NOTE]
    >Hello Azure Active Directory-accounthouder opgehaald een e-mailbericht met inbegrip van een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt
    >  

>[!NOTE]
>U kunt andere FreshService gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door FreshService tooprovision AAD-gebruikersaccounts.
>  

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooFreshservice, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Freshservice**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Freshservice tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Freshservice toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

