---
title: 'Zelfstudie: Azure Active Directory-integratie met Aha! | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Aha!.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a>Zelfstudie: Azure Active Directory-integratie met Aha!

In deze zelfstudie leert u hoe toointegrate Aha! met Azure Active Directory (Azure AD).

Integratie van Aha! met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooAha heeft!
- U kunt uw gebruikers tooautomatically get aangemelde tooAha inschakelen! (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Aha tooconfigure!, moet u de volgende items Hallo:

- Een Azure AD-abonnement
- Een Aha! eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Toe te voegen Aha! uit de galerie Hallo
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-aha-from-hello-gallery"></a>Toe te voegen Aha! uit de galerie Hallo
tooconfigure hello integratie van Aha! met Azure AD moet u tooadd Aha! van Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Aha! uitvoeren vanuit Hallo-galerie Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Aha!**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. Selecteer in het deelvenster resultaten hello, **Aha!**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Aha! op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker van het bijbehorende equivalent Hallo in Aha! is tooa gebruiker in Azure AD. Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Aha! moet toobe tot stand gebracht.

In Aha!, waarde Hallo Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en Azure AD test eenmalige aanmelding met Aha!, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een Aha! testgebruiker](#creating-an-aha-test-user)**  -toohave een equivalent van Britta Simon in Aha! dat is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Aha! de toepassing.

**tooconfigure eenmalige aanmelding Azure AD met Aha!, Hallo volgende stappen uit te voeren:**

1. In de Azure-portal op Hallo Hallo **Aha!** pagina van de integratie van toepassing, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. Op Hallo **Aha! Domein- en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.aha.io/session/new`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.aha.io`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Aha! Client-ondersteuningsteam](https://www.aha.io/company/contact) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. Aanmelden in een ander browservenster tooyour Aha! bedrijf-site als beheerder.

7. Klik in het menu bovenaan Hallo Hallo **instellingen**.

    ![Instellingen](./media/active-directory-saas-aha-tutorial/IC798950.png "instellingen")

8. Klik op **Account**.
   
    ![Profiel](./media/active-directory-saas-aha-tutorial/IC798951.png "profiel")

9. Klik op **beveiligings- en eenmalige aanmelding**.
   
    ![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798952.png "beveiligings- en eenmalige aanmelding")

10. In **Single Sign-On** sectie als **identiteitsprovider**, selecteer **SAML2.0**.
   
    ![Beveiliging en eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798953.png "beveiligings- en eenmalige aanmelding")

11. Op Hallo **Single Sign-On** configuratie pagina, voert u Hallo stappen te volgen:
    
    ![Eenmalige aanmelding](./media/active-directory-saas-aha-tutorial/IC798954.png "eenmalige aanmelding")
    
       a. In Hallo **naam** textbox, typ een naam voor uw configuratie.

       b. Voor **configureren met behulp van**, selecteer **metagegevensbestand**.
   
       c. tooupload uw gedownloade metagegevensbestand, klikt u op **Bladeren**.
   
       d. Klik op **Update**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-aha-test-user"></a>Maken van een Aha! testgebruiker

Azure AD tooenable gebruikers toolog in tooAha!, deze moeten worden ingericht in Aha!.  

In geval van Aha Hallo!, wordt een geautomatiseerde taak ingericht. Er is geen actie-item voor u.

Gebruikers worden automatisch gemaakt indien nodig tijdens Hallo eerste eenmalige aanmelding poging.

>[!NOTE]
>U kunt andere Aha! hulpmiddelen voor het maken van account of API's die worden geleverd door Aha! tooprovision AAD-gebruikersaccounts.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooAha!.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooAha!, Hallo volgende stappen uit te voeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Aha!**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u uw instellingen voor eenmalige aanmelding tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

