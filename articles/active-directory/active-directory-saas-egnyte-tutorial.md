---
title: 'Zelfstudie: Azure Active Directory-integratie met Egnyte | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Egnyte.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Zelfstudie: Azure Active Directory-integratie met Egnyte

In deze zelfstudie leert u hoe toointegrate Egnyte met Azure Active Directory (Azure AD).

Egnyte integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooEgnyte toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooEgnyte (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Egnyte tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Egnyte eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Egnyte van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-egnyte-from-hello-gallery"></a>Het toevoegen van Egnyte van Hallo-galerie
tooconfigure hello integratie van Egnyte in Azure AD, moet u tooadd Egnyte uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Egnyte via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Egnyte**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. Selecteer in het deelvenster resultaten hello, **Egnyte**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Egnyte op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Egnyte is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Egnyte toobe tot stand gebracht.

Wijs in Egnyte, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Egnyte, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Egnyte](#creating-an-egnyte-test-user)**  -toohave een equivalent van Britta Simon in Egnyte die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Egnyte configureren.

**Azure AD tooconfigure eenmalige aanmelding met Egnyte, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Egnyte** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. Op Hallo **Egnyte domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Egnyte Client ondersteuningsteam](https://www.egnyte.com/corp/contact_egnyte.html) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. Op Hallo **Egnyte configuratie** sectie, klikt u op **configureren Egnyte** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. In een ander browservenster, meld u aan tooyour Egnyte bedrijf site als een beheerder.

8. Klik op **instellingen**.
   
   ![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787819.png "instellingen")

9. Hallo-menu en klik op **instellingen**.

   ![Instellingen](./media/active-directory-saas-egnyte-tutorial/ic787820.png "instellingen")

10. Klik op Hallo **configuratie** tabblad en klik vervolgens op **beveiliging**.

    ![Beveiliging](./media/active-directory-saas-egnyte-tutorial/ic787821.png "beveiliging")

11. In Hallo **eenmalige aanmelding verificatie** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige verificatie](./media/active-directory-saas-egnyte-tutorial/ic787822.png "eenmalige-verificatie")   
    
    a. Als **eenmalige aanmelding verificatie**, selecteer **SAML 2.0**.
   
    b. Als **identiteitsprovider**, selecteer **AzureAD**.
   
    c. Plakken **SAML Single Sign-On Service-URL** gekopieerd vanuit Azure-portal naar Hallo **identiteit provider aanmeldings-URL** textbox.
   
    d. Plakken **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal in Hallo **identiteit provider entiteit-ID** textbox.
      
    e. De base-64 gecodeerde certificaat openen in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **provider identiteitscertificaat** textbox.
   
    f. Als **standaard Gebruikerskoppeling**, selecteer **e-mailadres**.
   
    g. Als **domeinspecifieke verlener waarde**, selecteer **uitgeschakeld**.
   
    h. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-egnyte-test-user"></a>Een testgebruiker Egnyte maken

Azure AD tooenable gebruikers toolog in tooEgnyte, ze in Egnyte moeten worden ingericht. In geval van Egnyte Hallo is inrichting een handmatige taak.

**tooprovision een gebruikersaccounts uitvoeren Hallo volgende stappen:**

1. Meld u bij tooyour **Egnyte** bedrijf site als administrator.

2. Ga te**instellingen \> gebruikers en groepen**.

3. Klik op **nieuwe gebruiker toevoegen**, en selecteer vervolgens Hallo-type van de gebruiker gewenste tooadd.
   
   ![Gebruikers](./media/active-directory-saas-egnyte-tutorial/ic787824.png "gebruikers")

4. In Hallo **nieuwe standaardgebruiker** sectie, voert u Hallo stappen te volgen:
   
   ![Nieuwe standaardgebruiker](./media/active-directory-saas-egnyte-tutorial/ic787825.png "nieuwe standaardgebruiker")   

   a. Type Hallo **e**, **gebruikersnaam**, en andere details van een geldige Azure Active Directory-account dat u wilt dat tooprovision.
   
   b. Klik op **Opslaan**.
    
    >[!NOTE]
    >Hello Azure Active Directory-accounthouder ontvangt een melding per e-mail.
    >

>[!NOTE]
>U kunt andere Egnyte gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Egnyte tooprovision AAD-gebruikersaccounts.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooEgnyte toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooEgnyte, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Egnyte**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Egnyte tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Egnyte toepassing.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

