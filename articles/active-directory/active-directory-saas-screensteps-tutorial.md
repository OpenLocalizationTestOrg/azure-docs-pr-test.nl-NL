---
title: 'Zelfstudie: Azure Active Directory-integratie met ScreenSteps | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en ScreenSteps.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Zelfstudie: Azure Active Directory-integratie met ScreenSteps

In deze zelfstudie leert u hoe toointegrate ScreenSteps met Azure Active Directory (Azure AD).

ScreenSteps integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooScreenSteps toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooScreenSteps (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met ScreenSteps tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een ScreenSteps eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van ScreenSteps van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-screensteps-from-hello-gallery"></a>Het toevoegen van ScreenSteps van Hallo-galerie
tooconfigure hello integratie van ScreenSteps in Azure AD, moet u tooadd ScreenSteps uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd ScreenSteps via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **ScreenSteps**, selecteer **ScreenSteps** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![ScreenSteps in de lijst met resultaten Hallo](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met ScreenSteps op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in ScreenSteps is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in ScreenSteps toobe tot stand gebracht.

Wijs in ScreenSteps, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met ScreenSteps, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker ScreenSteps](#create-a-screensteps-test-user)**  -toohave een equivalent van Britta Simon in ScreenSteps die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing ScreenSteps configureren.

**Azure AD tooconfigure eenmalige aanmelding met ScreenSteps, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **ScreenSteps** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. Op Hallo **ScreenSteps domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en ScreenSteps domein eenmalige aanmelding informatie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Deze waarde is geen echte. Deze waarde bijwerken Hello werkelijke aanmeldings-URL, die verderop in deze zelfstudie wordt beschreven. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. Op Hallo **ScreenSteps configuratie** sectie, klikt u op **configureren ScreenSteps** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![ScreenSteps configuratie](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. In een ander browservenster, meld u bij uw bedrijf ScreenSteps site als beheerder.

8. Klik op **Accountinstellingen**.

    ![Accountbeheer](./media/active-directory-saas-screensteps-tutorial/ic778523.png "accountbeheer")

9. Klik op **Single Sign-on**.

    ![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778524.png "externe verificatie")

10. Klik op **Single Sign-on-eindpunt maken**.

    ![Externe verificatie](./media/active-directory-saas-screensteps-tutorial/ic778525.png "externe verificatie")

11. In Hallo **maken één aanmelding eindpunt** sectie, voert u Hallo stappen te volgen:

    ![Maak een verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778526.png "een verificatie-eindpunt maken")
    
    a. In Hallo **titel** textbox, typ een titel.
    
    b. Van Hallo **modus** selecteert **SAML**.
    
    c. Klik op **Create**.

12. **Bewerken** Hallo nieuw eindpunt.

    ![Eindpunt bewerken](./media/active-directory-saas-screensteps-tutorial/ic778528.png "eindpunt bewerken")

13. In Hallo **bewerken één aanmelding eindpunt** sectie, voert u Hallo stappen te volgen:

    ![Externe verificatie-eindpunt](./media/active-directory-saas-screensteps-tutorial/ic778527.png "externe verificatie-eindpunt")

    a. Klik op **nieuwe SAML certificaat uploadbestand**, en vervolgens uploaden Hallo certificaat dat u hebt gedownload vanuit Azure-portal.
    
    b. Plakken **SAML Single Sign-On Service-URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **externe aanmeldings-URL** textbox.
    
    c. Plakken **Sign-Out URL** waarde, die u hebt gekopieerd uit hello Azure-portal in Hallo **afmeldings-URL** textbox.
    
    d. Selecteer een **groep** tooassign gebruikers toowhen deze zijn ingericht.
    
    e. Klik op **Update**.

    f. Kopiëren Hallo **SAML Consumer URL** toohello Klembord en plak in toohello **aanmeldings-URL** textbox in **ScreenSteps domein en de URL's** sectie.
    
    g. Retourneren van toohello **bewerken één aanmelding eindpunt**.
    
    h. Klik op Hallo **voor account instellen als standaardbrowser** knop toouse dit eindpunt voor alle gebruikers die zich bij ScreenSteps aanmelden. U kunt ook klikken op Hallo **toevoegen tooSite** knop toouse dit eindpunt voor specifieke sites in **ScreenSteps**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-screensteps-test-user"></a>Een testgebruiker ScreenSteps maken

In deze sectie kunt u een gebruiker Britta Simon aangeroepen in ScreenSteps maken. Werken met [ScreenSteps Client ondersteuningsteam](https://www.screensteps.com/contact) Hallo gebruikers toevoegen in Hallo ScreenSteps platform. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken. 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooScreenSteps toegang verleent.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooScreenSteps, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **ScreenSteps**.

    ![Hallo ScreenSteps koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo ScreenSteps-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour ScreenSteps toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

