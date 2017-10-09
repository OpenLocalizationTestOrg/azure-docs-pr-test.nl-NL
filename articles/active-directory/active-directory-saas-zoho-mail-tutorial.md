---
title: 'Zelfstudie: Azure Active Directory-integratie met Zoho | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Zoho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Zelfstudie: Azure Active Directory-integratie met Zoho

In deze zelfstudie leert u hoe toointegrate Zoho met Azure Active Directory (Azure AD).

Zoho integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooZoho toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooZoho (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Zoho tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Zoho eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Zoho van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-zoho-from-hello-gallery"></a>Het toevoegen van Zoho van Hallo-galerie
tooconfigure hello integratie van Zoho in Azure AD, moet u tooadd Zoho uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Zoho via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Zoho**, selecteer **Zoho** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Zoho in de lijst met resultaten Hallo](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Zoho op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Zoho is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Zoho toobe tot stand gebracht.

Wijs in Zoho, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Zoho, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Zoho](#create-a-zoho-test-user)**  -toohave een equivalent van Britta Simon in Zoho die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Zoho configureren.

**Azure AD tooconfigure eenmalige aanmelding met Zoho, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Zoho** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. Op Hallo **Zoho domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Zoho domein eenmalige aanmelding informatie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Zoho Client ondersteuningsteam](https://www.zoho.com/mail/contact.html) tooget deze waarde. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. Op Hallo **Zoho configuratie** sectie, klikt u op **configureren Zoho** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, de URL wachtwoord wijzigen en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Zoho configuratie](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf Zoho Mail site als beheerder.

8. Ga toohello **Configuratiescherm**.
   
    ![Het Configuratiescherm](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Configuratiescherm")

9. Klik op Hallo **SAML-verificatie** tabblad.
   
    ![SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML-verificatie")

10. In Hallo **SAML verificatiegegevens** sectie, voert u Hallo stappen te volgen:
   
    ![Details van SAML-verificatie](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Details van SAML-verificatie")
   
    a. In Hallo **aanmeldings-URL** textbox plakken **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    b. In Hallo **afmelding URL** textbox plakken **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
   
    c. In Hallo **URL van wijzigen wachtwoord** textbox plakken **URL van wijzigen wachtwoord** die u hebt gekopieerd vanuit Azure-portal.
       
    d. Open uw base-64 gecodeerde certificaat gedownload vanuit Azure-portal in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **PublicKey** textbox.
   
    e. Als **algoritme**, selecteer **RSA**.
   
    f. Klik op **OK**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-zoho-test-user"></a>Een testgebruiker Zoho maken

In volgorde tooenable Azure AD gebruikers toolog in Zoho Mail, moeten ze worden ingericht in Zoho Mail. In geval van Zoho E-mail Hallo is inrichting een handmatige taak.

> [!NOTE]
> U kunt andere Zoho afdruk gebruiker account hulpmiddelen voor het maken of API's geleverd door Zoho Mail tooprovision AAD-gebruikersaccounts.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:

1. Meld u bij tooyour **Zoho Mail** bedrijf site als beheerder.

2. Ga te**Configuratiescherm \> e & Docs**.

3. Ga te**Gebruikersdetails \> gebruiker toevoegen**.
   
    ![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "gebruiker toevoegen")

4. Op Hallo **gebruikers toevoegen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Gebruiker toevoegen](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "gebruiker toevoegen")
   
    a. In Hallo **voornaam** textbox type Hallo voornaam van gebruiker zoals **Britta**.

    b. In Hallo **achternaam** textbox type Hallo achternaam van gebruiker zoals **Simon**.

    c. In Hallo **E-mail-ID** textbox type Hallo e-mail-id van gebruiker zoals  **brittasimon@contoso.com** .

    d. In Hallo **wachtwoord** textbox, voer het wachtwoord van gebruiker.
   
    e. Klik op **OK**.  
      
    > [!NOTE]
    > Hello Azure Active Directory-accounthouder ontvangt een e-mail met een account koppelen tooconfirm Hallo voordat deze geactiveerd wordt.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooZoho toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooZoho, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Zoho**.

    ![Hallo Zoho koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Zoho tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Zoho toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

