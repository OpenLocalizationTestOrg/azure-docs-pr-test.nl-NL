---
title: 'Zelfstudie: Azure Active Directory-integratie met Onit | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Onit.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a>Zelfstudie: Azure Active Directory-integratie met Onit

In deze zelfstudie leert u hoe toointegrate Onit met Azure Active Directory (Azure AD).

Onit integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooOnit toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooOnit (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Onit tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Onit eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving

In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Onit van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-onit-from-hello-gallery"></a>Het toevoegen van Onit van Hallo-galerie
tooconfigure hello integratie van Onit in Azure AD, moet u tooadd Onit uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Onit via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Onit**, selecteer **Onit** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Onit in de lijst met resultaten Hallo](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Onit op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Onit is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Onit toobe tot stand gebracht.

Wijs in Onit, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met Onit, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Onit](#create-an-onit-test-user)**  -toohave een equivalent van Britta Simon in Onit die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing Onit configureren.

**Azure AD tooconfigure eenmalige aanmelding met Onit, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Onit** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. Op Hallo **Onit domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Onit domein eenmalige aanmelding informatie](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<sub-domain>.onit.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<sub-domain>.onit.com`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [Onit Client ondersteuningsteam](https://www.onit.com/support) tooget deze waarden. 
 
4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, kopie Hallo **VINGERAFDRUK** waarde van het certificaat.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. Hallo SAML asserties verwacht Onit toepassing in een specifieke indeling. Configureer Hallo claims voor deze toepassing te volgen. U kunt waarden van deze kenmerken Hallo beheren vanuit Hallo **'Atrribute'** tabblad van de toepassing hello. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals in afbeelding Hallo en uitvoeren van Hallo stappen te volgen:
    
    | Naam van kenmerk | De waarde van kenmerk |
    | ------------------- | -------------------- |
    | E-mail | User.mail |
    
    a. Klik op **toevoegen kenmerk** tooopen hello **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    b. In Hallo **naam** textbox Hallo kenmerknaam wordt weergegeven voor die rij.

    c. Van Hallo **waarde** lijst, type Hallo-kenmerkwaarde wordt weergegeven voor die rij.

    d. Hallo laat **Namespace** leeg.
    
    e. Klik op **OK**.

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. Op Hallo **Onit configuratie** sectie, klikt u op **configureren Onit** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Onit configuratie](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. In een ander browservenster, meld u bij uw bedrijf Onit site als beheerder.

10. Klik in het menu bovenaan Hallo Hallo **beheer**.
   
   ![Beheer](./media/active-directory-saas-onit-tutorial/IC791174.png "beheer")
11. Klik op **bewerken Corporation**.
   
   ![Bewerken Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Corporation bewerken")
   
12. Klik op Hallo **beveiliging** tabblad.
    
    ![Bedrijfsgegevens bewerken](./media/active-directory-saas-onit-tutorial/IC791176.png "bedrijfsgegevens bewerken")

13. Op Hallo **beveiliging** tabblad, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding](./media/active-directory-saas-onit-tutorial/IC791177.png "eenmalige aanmelding")

    a. Als **Verificatiestrategie**, selecteer **eenmalige aanmelding en het wachtwoord**.
    
    b. In **Idp doel-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.

    c. In **Idp afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL**, die u hebt gekopieerd vanuit Azure-portal.

    d. In **Idp Cert vingerafdruk (SHA1)** textbox plakken Hallo **vingerafdruk** waarde van het certificaat dat u hebt gekopieerd vanuit Azure-portal.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-an-onit-test-user"></a>Een testgebruiker Onit maken

In de volgorde tooenable Azure AD gebruikers toolog in Onit, moeten ze worden ingericht in Onit.  

In geval van Onit Hallo is inrichting een handmatige taak.

**tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:**

1. Meld u aan bij tooyour **Onit** bedrijf site als beheerder.
2. Klik op **gebruiker toevoegen**.
   
   ![Beheer](./media/active-directory-saas-onit-tutorial/IC791180.png "beheer")
3. Op Hallo **gebruiker toevoegen** dialoogvenster pagina, voert u Hallo stappen te volgen:
   
   ![Gebruiker toevoegen](./media/active-directory-saas-onit-tutorial/IC791181.png "gebruiker toevoegen")
   
  1. Type Hallo **naam** en Hallo **e-mailadres** van een geldig Azure tekstvakken met betrekking tot AD-account u wilt dat tooprovision in Hallo.
  2. Klik op **Create**.    
   
 > [!NOTE]
 > Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooOnit toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooOnit, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Onit**.

    ![Hallo Onit koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Onit tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Onit toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

