---
title: 'Zelfstudie: Azure Active Directory-integratie met Druva | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Druva.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Zelfstudie: Azure Active Directory-integratie met Druva

In deze zelfstudie leert u hoe toointegrate Druva met Azure Active Directory (Azure AD).

Druva integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooDruva toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooDruva (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Druva tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Druva eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Druva van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-druva-from-hello-gallery"></a>Het toevoegen van Druva van Hallo-galerie
tooconfigure hello integratie van Druva in Azure AD, moet u tooadd Druva uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Druva via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Druva**, selecteer **Druva** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Druva in de lijst met resultaten Hallo](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Druva op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Druva is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Druva toobe tot stand gebracht.

Wijs in Druva, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Druva, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Druva](#create-a-druva-test-user)**  -toohave een equivalent van Britta Simon in Druva die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Druva configureren.

**Azure AD tooconfigure eenmalige aanmelding met Druva, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Druva** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. Op Hallo **Druva domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    In Hallo **aanmeldings-URL** textbox type Hallo URL:`https://cloud.druva.com/home`

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. Uw toepassing Druva Hallo SAML asserties verwacht in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour **SAML-Token kenmerken** configuratie. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de voorgaande afbeelding Hallo en uitvoeren van Hallo stappen te volgen:

    | Naam van kenmerk      | De waarde van kenmerk      |
    | ------------------- | -------------------- |
    | synchroon\_auth\_token |Voer Hallo token gegenereerde waarde |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij. Hallo token gegenereerde waarde wordt verderop in de zelfstudie beschreven.
    
    d. Klik op **OK**.    

7. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. Op Hallo **Druva configuratie** sectie, klikt u op **configureren Druva** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. In een ander browservenster, meld u aan tooyour Druva bedrijf site als een beheerder.

10. Ga te**beheren \> instellingen**.

    ![Instellingen](./media/active-directory-saas-druva-tutorial/ic795091.png "instellingen")

11. Voer in het dialoogvenster van de instellingen voor eenmalige aanmelding hello, Hallo stappen te volgen:

    ![Eenmalige aanmelding instellingen](./media/active-directory-saas-druva-tutorial/ic795092.png "eenmalige aanmelding-instellingen")
    
    a. Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **ID-Provider aanmeldings-URL** textbox.
    
    b. Plakken **Sign-Out URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **ID-Provider afmelding URL** textbox.
    
     c. De base-64 gecodeerde certificaat openen in Kladblok, kopieer Hallo inhoud ervan naar het Klembord en plak deze toohello **ID-Provider certificaat** tekstvak
     
     d. Hallo tooopen **instellingen** pagina, klikt u op **opslaan**.

12. Op Hallo **instellingen** pagina, klikt u op **SSO-Token genereren**.

    ![Instellingen](./media/active-directory-saas-druva-tutorial/ic795093.png "instellingen")

13. Op Hallo **Single Sign-on-verificatietoken** dialoogvenster Hallo volgende stappen uit te voeren:

    ![SSO-Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO-Token")
    
    a. Klik op **kopie**, plakken waarde gekopieerd in Hallo **waarde** textbox in Hallo **kenmerk toevoegen** sectie.
    
    b. Klik op **Sluiten**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-druva-test-user"></a>Een testgebruiker Druva maken

In de volgorde tooenable Azure AD gebruikers toolog in tooDruva, moeten ze worden ingericht in Druva. In geval van Druva Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u bij tooyour **Druva** bedrijf site als administrator.

2. Ga te**beheren \> gebruikers**.
   
   ![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795097.png "gebruikers beheren")

3. Klik op **maken van nieuwe**.
   
   ![Gebruikers beheren](./media/active-directory-saas-druva-tutorial/ic795098.png "gebruikers beheren")

4. Voer in het dialoogvenster van de nieuwe gebruiker maken hello, Hallo stappen te volgen:
   
   ![Maken van nieuwegebruiker](./media/active-directory-saas-druva-tutorial/ic795099.png "nieuwegebruiker maken")
   
   a. In Hallo **e-mailadres** textbox Voer Hallo e-mailadres van de gebruiker zoals  **brittasimon@contoso.com** .
   
   b. In Hallo **naam** textbox Voer Hallo-naam van gebruiker zoals **BrittaSimon**.
   
   c. Klik op **gebruiker maken**.

>[!NOTE]
>U kunt andere Druva gebruiker account hulpmiddelen voor het maken of API's die worden geleverd door Druva tooprovision Azure AD-gebruikersaccounts.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooDruva toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooDruva, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Druva**.

    ![Hallo Druva koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Druva tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Druva toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

