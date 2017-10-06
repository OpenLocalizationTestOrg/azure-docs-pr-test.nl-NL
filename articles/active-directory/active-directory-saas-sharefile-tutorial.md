---
title: 'Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Citrix ShareFile.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: d7eaf140e56c40f9f621062849dd8558588ffd1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a>Zelfstudie: Azure Active Directory-integratie met Citrix ShareFile

In deze zelfstudie leert u hoe toointegrate Citrix ShareFile met Azure Active Directory (Azure AD).

Citrix ShareFile integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooCitrix ShareFile heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooCitrix ShareFile (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Citrix ShareFile tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Citrix ShareFile eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Citrix ShareFile van Hallo galerie toevoegen
2. Configureren en testen eenmalige aanmelding Azure AD

## <a name="add-citrix-sharefile-from-hello-gallery"></a>Citrix ShareFile van Hallo galerie toevoegen
tooconfigure hello integratie van Citrix ShareFile in Azure AD, moet u Citrix ShareFile tooadd uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Citrix ShareFile via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Citrix ShareFile**, selecteer **Citrix ShareFile** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Lijst met zoekresultaten Citrix ShareFile in Hallo](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie maakt u configureert en test eenmalige aanmelding Azure AD met Citrix ShareFile op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Citrix ShareFile is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Citrix ShareFile toobe tot stand gebracht.

In Citrix ShareFile, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Citrix ShareFile, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Citrix ShareFile](#create-a-citrix-sharefile-test-user)**  -toohave een equivalent van Britta Simon in Citrix ShareFile die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Citrix ShareFile configureren.

**Azure AD tooconfigure eenmalige aanmelding met Citrix ShareFile, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Citrix ShareFile** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. Op Hallo **Citrix ShareFile domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Citrix ShareFile domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenant-name>.sharefile.com/saml/login`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL. Neem contact op met [Citrix ShareFile Client ondersteuningsteam](https://www.citrix.co.in/products/sharefile/support.html) tooget deze waarde. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. Op Hallo **Citrix-configuratie voor ShareFile** sectie, klikt u op **configureren Citrix ShareFile** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Citrix ShareFile-configuratie](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. In een ander browservenster, meld u aan bij uw **Citrix ShareFile** bedrijf site als beheerder.

8. Klik in de werkbalk bovenaan Hallo Hallo op **Admin**.

9. Selecteer in de Hallo navigatiedeelvenster links **configureren Single Sign-On**.
   
    ![Beheer account](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account beheer")

10. Op Hallo **Single Sign-On / SAML 2.0-configuratie** dialoogvenster pagina onder **basisinstellingen**, Hallo volgende stappen uit te voeren:
   
    ![Eenmalige aanmelding](./media/active-directory-saas-sharefile-tutorial/ic773628.png "eenmalige aanmelding")
   
    a. Klik op **SAML inschakelen**.
    
    b. In **uw IDP verlener / entiteit-ID** textbox plakken Hallo-waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.

    c. Klik op **wijziging** volgende toohello **X.509-certificaat** veld en klikt u vervolgens uploaden Hallo certificaat u hebt gedownload van hello Azure-portal.
    
    d. In **aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
    
    e. In **afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.

11. Klik op **opslaan** op Hallo Citrix ShareFile-beheerportal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-citrix-sharefile-test-user"></a>Een testgebruiker Citrix ShareFile maken

In de volgorde tooenable Azure AD gebruikers toolog in Citrix ShareFile, moeten ze worden ingericht in Citrix ShareFile. In geval van Citrix ShareFile Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Meld u bij tooyour **Citrix ShareFile** tenant.

2. Klik op **gebruikers beheren \> beheren van gebruikers Home \> + werknemer**.
   
   ![Maken van de werknemer](./media/active-directory-saas-sharefile-tutorial/IC781050.png "werknemer maken")

3. Op Hallo **basisinformatie** sectie, voert u onderstaande stappen te volgen:
   
   ![Algemene informatie](./media/active-directory-saas-sharefile-tutorial/IC799951.png "basisinformatie")
   
   a. In Hallo **e-mailadres** textbox type Hallo e-mailadres van Britta Simon als  **brittasimon@contoso.com** .
   
   b. In Hallo **voornaam** textbox type **voornaam** van gebruiker als **Britta**.
   
   c. In Hallo **achternaam** textbox type **achternaam** van gebruiker als **Simon**.

4. Klik op **gebruiker toevoegen**.
  
   >[!NOTE]
   >Hello Azure AD-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt. U kunt andere Citrix ShareFile gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Citrix ShareFile tooprovision Azure AD-gebruikersaccounts.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooCitrix ShareFile.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooCitrix ShareFile, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Citrix ShareFile**.

    ![Hallo Citrix ShareFile koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Citrix ShareFile-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Citrix ShareFile-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

