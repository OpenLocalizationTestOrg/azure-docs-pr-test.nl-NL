---
title: 'Zelfstudie: Azure Active Directory-integratie met Intacct | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Intacct.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Zelfstudie: Azure Active Directory-integratie met Intacct

In deze zelfstudie leert u hoe toointegrate Intacct met Azure Active Directory (Azure AD).

Intacct integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooIntacct toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooIntacct (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Intacct tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Intacct eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Intacct van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-intacct-from-hello-gallery"></a>Het toevoegen van Intacct van Hallo-galerie
tooconfigure hello integratie van Intacct in Azure AD, moet u tooadd Intacct uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Intacct via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Intacct**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. Selecteer in het deelvenster resultaten hello, **Intacct**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Intacct op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Intacct is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Intacct toobe tot stand gebracht.

Wijs in Intacct, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Intacct, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Intacct](#creating-an-intacct-test-user)**  -toohave een equivalent van Britta Simon in Intacct die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Intacct configureren.

**Azure AD tooconfigure eenmalige aanmelding met Intacct, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Intacct** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. Op Hallo **Intacct domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde met de werkelijke antwoord-URL Hallo bijwerken. Neem contact op met [Intacct ondersteuningsteam](https://us.intacct.com/support) tooget deze waarde.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. Op Hallo **Intacct configuratie** sectie, klikt u op **configureren Intacct** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. Meld u tooyour Intacct bedrijf site als een beheerder in een ander browservenster.

8. Klik op Hallo **bedrijf** tabblad en klik vervolgens op **bedrijfsgegevens**.

    ![Bedrijf](./media/active-directory-saas-intacct-tutorial/ic790037.png "bedrijf")

9. Klik op Hallo **beveiliging** tabblad en klik vervolgens op **bewerken**.

    ![Beveiliging](./media/active-directory-saas-intacct-tutorial/ic790038.png "beveiliging")

10. In Hallo **eenmalige aanmelding (SSO)** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding](./media/active-directory-saas-intacct-tutorial/ic790039.png "eenmalige aanmelding")

    a. Selecteer **eenmalige aanmelding inschakelen op**.

    b. Als **identiteit providertype**, selecteer **SAML 2.0**.

    c. In **URL-verlener** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.
   
    d. In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    e. Open uw **base 64-** gecodeerd certificaat in Kladblok en kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **certificaat** vak.
   
    f. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-intacct-test-user"></a>Een testgebruiker Intacct maken

tooset van Azure AD-gebruikers zodat ze kunnen zich in tooIntacct, deze moeten worden ingericht in Intacct. Voor Intacct is inrichting een handmatige taak.

**tooprovision gebruikersaccounts, Voer Hallo stappen te volgen:**

1. Meld u aan tooyour **Intacct** tenant.

2. Klik op Hallo **bedrijf** tabblad en klik vervolgens op **gebruikers**.

    ![Gebruikers](./media/active-directory-saas-intacct-tutorial/ic790041.png "gebruikers")
3. Klik op Hallo **toevoegen** tabblad.

    ![Voeg](./media/active-directory-saas-intacct-tutorial/ic790042.png "toevoegen")
4. In Hallo **gebruikersgegevens** sectie, voert u Hallo stappen te volgen:

    ![Gebruikersgegevens](./media/active-directory-saas-intacct-tutorial/ic790043.png "gebruikersgegevens")

    a. Voer Hallo **gebruikers-ID**, Hallo **achternaam**, **voornaam**, Hallo **e-mailadres**, Hallo **titel**, en Hallo **Phone** van een Azure AD-account dat u wilt dat tooprovision in Hallo **gebruikersgegevens** sectie.

    b. Selecteer Hallo **beheerdersbevoegdheden** van een Azure AD-account dat u wilt dat tooprovision.
   
    c. Klik op **Opslaan**. Hello Azure AD-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.

>[!NOTE]
>gebruikersaccounts voor tooprovision Azure AD, kunt u andere hulpprogramma's voor Intacct gebruiker-account maken of API's die worden geleverd door Intacct.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooIntacct toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooIntacct, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Intacct**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van Hallo Toegangsvenster.

Wanneer u Hallo Intacct tegel in Hallo toegangsvenster klikt, moet u tooyour Intacct toepassing automatisch worden aangemeld.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

