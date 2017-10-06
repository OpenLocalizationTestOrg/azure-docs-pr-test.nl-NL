---
title: 'Zelfstudie: Azure Active Directory-integratie met Rally Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Rally Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Zelfstudie: Azure Active Directory-integratie met Rally Software

In deze zelfstudie leert u hoe toointegrate Rally Software met Azure Active Directory (Azure AD).

Software Rally integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooRally Software heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooRally Software (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Software Rally tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Software Rally eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Software Rally van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-rally-software-from-hello-gallery"></a>Het toevoegen van Software Rally van Hallo-galerie
tooconfigure hello integratie van Software Rally in Azure AD, moet u tooadd Rally Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Rally Software uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Rally Software**, selecteer **Rally Software** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Software in de lijst met resultaten Hallo Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Rally Software op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Software Rally is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in Software Rally toobe tot stand gebracht.

In Software Rally Hallo waarde Hallo toewijzen **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Rally Software, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Rally Software](#create-a-rally-software-test-user)**  -toohave een equivalent van Britta Simon in Rally Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Rally configureren.

**Voer tooconfigure Azure AD eenmalige aanmelding met Rally Software Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Rally Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. Op Hallo **Rally Software domein en URL's** sectie, voert u Hallo stappen te volgen:

    ![Software-domein en de URL's eenmalige aanmelding informatie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.rally.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Rally Software Client ondersteuningsteam](https://help.rallydev.com/) tooget deze waarden. 
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. Op Hallo **softwareconfiguratie Rally** sectie, klikt u op **Rally Software configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL en de entiteit-ID SAML** van Hallo **Naslaggids punt.**

    ![De softwareconfiguratie Rally](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. Meld u bij tooyour **Rally Software** tenant.

8. Klik in de werkbalk bovenaan Hallo Hallo op **Setup**, en selecteer vervolgens **abonnement**.
   
    ![Abonnement](./media/active-directory-saas-rally-software-tutorial/ic769531.png "abonnement")

9. Klik op Hallo **actie** knop. Selecteer **abonnement bewerken** op Hallo rechtsboven Hallo-werkbalk.

10. Op Hallo **abonnement** dialoogvenster pagina Hallo volgende stappen uit te voeren en klik vervolgens op **opslaan en sluiten**:
   
    ![Verificatie](./media/active-directory-saas-rally-software-tutorial/ic769542.png "verificatie")
   
    a. Selecteer **Rally of eenmalige aanmelding verificatie** uit de vervolgkeuzelijst verificatie.

    b. In Hallo **identiteit provider URL** textbox plakken Hallo-waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal. 

    c. In Hallo **eenmalige aanmelding, afmelding** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-rally-software-test-user"></a>Een testgebruiker Rally Software maken

Voor Azure AD gebruikers toobe kunnen toosign in, moeten ze ingerichte toohello Rally softwaretoepassing met behulp van de namen van de Azure Active Directory-gebruiker zijn.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u bij tooyour Rally Software tenant.

2. Ga te**Setup \> gebruikers**, en klik vervolgens op **+ nieuw toevoegen**.
   
    ![Gebruikers](./media/active-directory-saas-rally-software-tutorial/ic781039.png "gebruikers")

3. Hallo typenaam in een tekstvak voor de nieuwe gebruiker Hallo en klik vervolgens op **toevoegen met Details**.

4. In Hallo **gebruiker maken** sectie, voert u Hallo stappen te volgen:
   
    ![Gebruiker maken](./media/active-directory-saas-rally-software-tutorial/ic781040.png "gebruiker maken")

    a. In Hallo **gebruikersnaam** textbox Hallo-typenaam van de gebruiker zoals **Brittsimon**.
   
    b. In **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .

    c. In **voornaam** tekst hello eerste naam van gebruiker zoals **Britta**.

    d. In **achternaam** tekst hello laatste naam van gebruiker zoals **Simon**.

    e. Klik op **opslaan en sluiten**.

   >[!NOTE]
   >U kunt andere Software Rally gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Software Rally tooprovision Azure AD-gebruikersaccounts.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooRally Software.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooRally Software, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Rally Software**.

    ![Hallo Rally Software koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.

Als u op Hallo Rally Software tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Rally softwaretoepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

