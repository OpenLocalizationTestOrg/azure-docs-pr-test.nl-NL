---
title: 'Zelfstudie: Azure Active Directory-integratie met Boomi | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Boomi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Zelfstudie: Azure Active Directory-integratie met Boomi

In deze zelfstudie leert u hoe toointegrate Boomi met Azure Active Directory (Azure AD).

Boomi integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooBoomi toegang heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooBoomi (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Boomi tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Boomi eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Boomi van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-boomi-from-hello-gallery"></a>Het toevoegen van Boomi van Hallo-galerie
tooconfigure hello integratie van Boomi in Azure AD, moet u tooadd Boomi uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Boomi via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Boomi**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. Selecteer in het deelvenster resultaten hello, **Boomi**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Boomi op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Boomi is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Boomi toobe tot stand gebracht.

Wijs in Boomi, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Boomi, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Boomi](#creating-a-boomi-test-user)**  -toohave een equivalent van Britta Simon in Boomi die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Boomi configureren.

**Azure AD tooconfigure eenmalige aanmelding met Boomi, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Boomi** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Op Hallo **Boomi domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [Boomi ondersteuningsteam](https://boomi.com/company/contact/) tooget deze waarden.

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Hallo SAML asserties verwacht Boomi toepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. Hallo volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster uitvoeren Hallo volgende stappen uit voor elke rij in Hallo tabel hieronder weergegeven:

    | Naam van kenmerk | De waarde van kenmerk |
    | -------------- | --------------- |
    | FEDERATION_ID | User.mail |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.
    
    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.
    
    d. Klik op **OK**.

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. Op Hallo **Boomi configuratie** sectie, klikt u op **configureren Boomi** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. In een ander browservenster, meld u bij uw bedrijf Boomi site als beheerder. 

9. Navigeer te**bedrijfsnaam** en ga te**instellen**.

10. Klik op Hallo **SSO opties** tabblad en Voer onderstaande stappen te volgen.

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Controleer **inschakelen SAML Single Sign-On** selectievakje.

    b. Klik op **importeren** tooupload Hallo certificaat gedownload vanuit Azure AD te**Provider identiteitscertificaat**.
    
    c. In Hallo **identiteit Provider aanmeldings-URL** textbox Hallo-waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.

    d. Als **Federation Id locatie**, selecteer **Federation-Id wordt FEDERATION_ID kenmerk element** keuzerondje. 

    e. Klik op **opslaan** knop.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-boomi-test-user"></a>Een testgebruiker Boomi maken

In de volgorde tooenable Azure AD gebruikers toolog in tooBoomi, moeten ze worden ingericht in Boomi. In geval van Boomi Hallo is inrichting een handmatige taak.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:

1. Aanmelden tooyour Boomi bedrijf site als beheerder.

2. Na het aanmelden, te navigeren**Gebruikersbeheer** en ga te**gebruikers**.

    ![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "gebruikers")

3. Klik op  **+**  pictogram en Hallo **toevoegen/onderhouden gebruikersrollen** dialoogvenster wordt geopend.

    ![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "gebruikers")

    ![Gebruikers](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "gebruikers")

    a. In Hallo **e-mailadres gebruiker** textbox type Hallo e-mailadres van de gebruiker, zoals BrittaSimon@contoso.com.
    
    b. In Hallo **voornaam** textbox type Hallo voornaam van gebruiker zoals Britta.

    c. In Hallo **achternaam** textbox type Hallo achternaam van gebruiker zoals Simon.
    
    d. Voer van Hallo gebruiker **Federatie-ID**. Elke gebruiker moet een Federation-ID die een unieke identificatie van Hallo gebruiker binnen Hallo-account hebben.
    
    e. Hallo toewijzen **standaardgebruiker** rol toohello gebruiker. Geen toewijzen Hallo beheerdersrol omdat die hem normale lucht toegang als één aanmelding toegang wilt geven.
    
    f. Klik op **OK**.
    
    > [!NOTE]
    > Hallo-gebruiker ontvangt een e-mailmelding Welkom met een wachtwoord dat gebruikt toolog in toohello AtomSphere account worden kan omdat het wachtwoord wordt beheerd via Hallo id-provider niet. U kunt andere Boomi gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Boomi tooprovision AAD-gebruikersaccounts. 

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooBoomi toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooBoomi, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Boomi**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Boomi tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Boomi toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

