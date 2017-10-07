---
title: 'Zelfstudie: Azure Active Directory-integratie met Kintone | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Zelfstudie: Azure Active Directory-integratie met Kintone

In deze zelfstudie leert u hoe toointegrate Kintone met Azure Active Directory (Azure AD).

Kintone integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooKintone toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooKintone (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Kintone tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Kintone eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Kintone van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-kintone-from-hello-gallery"></a>Het toevoegen van Kintone van Hallo-galerie
tooconfigure hello integratie van Kintone in Azure AD, moet u tooadd Kintone uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Kintone via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Kintone**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. Selecteer in het deelvenster resultaten hello, **Kintone**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Kintone op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kintone is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kintone toobe tot stand gebracht.

Wijs in Kintone, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Kintone, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Kintone](#creating-a-kintone-test-user)**  -toohave een equivalent van Britta Simon in Kintone die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Kintone configureren.

**Azure AD tooconfigure eenmalige aanmelding met Kintone, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Kintone** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. Op Hallo **Kintone domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.kintone.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Kintone Client ondersteuningsteam](https://www.kintone.com/contact/) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. Op Hallo **Kintone configuratie** sectie, klikt u op **configureren Kintone** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's, en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. In een ander browservenster, meld u aan bij uw **Kintone** bedrijf site als beheerder.

8. Klik op **instellingen**.
   
    ![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")

9. Klik op **gebruikers & Systeembeheer**.
   
    ![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruikers & Systeembeheer")

10. Onder **Systeembeheer \> beveiliging** klikt u op **aanmelding**.
   
    ![Aanmelding](./media/active-directory-saas-kintone-tutorial/ic785881.png "aanmelding")

11. Klik op **inschakelen SAML-verificatie**.
   
    ![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML-verificatie")

12. Voer in Hallo sectie SAML-verificatie, Hallo stappen te volgen:
    
    ![SAML-verificatie](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML-verificatie")
    
    a. In Hallo **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    b. In Hallo **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
    
    c. Klik op **Bladeren** tooupload uw gedownloade certificaat.
    
    d. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-kintone-test-user"></a>Een testgebruiker Kintone maken

Azure AD tooenable gebruikers toolog in tooKintone, ze in Kintone moeten worden ingericht.  
In geval van Kintone Hallo is inrichting een handmatige taak.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:

1. Meld u bij tooyour **Kintone** bedrijf site als beheerder.

2. Klik op **instelling**.
   
    ![Instellingen](./media/active-directory-saas-kintone-tutorial/ic785879.png "instellingen")

3. Klik op **gebruikers & Systeembeheer**.
   
    ![Gebruikers & Systeembeheer](./media/active-directory-saas-kintone-tutorial/ic785880.png "gebruiker & Systeembeheer")

4. Onder **Gebruikersbeheer**, klikt u op **afdelingen gebr & uikers**.
   
    ![Afdeling gebr & uikers](./media/active-directory-saas-kintone-tutorial/ic785888.png "afdeling gebr & uikers")

5. Klik op **nieuwe gebruiker**.
   
    ![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785889.png "nieuwe gebruikers")

6. In Hallo **nieuwe gebruiker** sectie, voert u Hallo stappen te volgen:
   
    ![Nieuwe gebruikers](./media/active-directory-saas-kintone-tutorial/ic785890.png "nieuwe gebruikers")
   
    a. Typ een **weergavenaam**, **aanmeldingsnaam**, **nieuw wachtwoord**, **wachtwoord bevestigen**, **e-mailadres**, en andere details van een geldige AAD-account dat u wilt dat tooprovision in Hallo bijbehorende tekstvakken.
 
    b. Klik op **Opslaan**.

> [!NOTE]
> U kunt andere Kintone gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Kintone tooprovision AAD-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooKintone toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooKintone, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Kintone**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Kintone tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Kintone toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

