---
title: 'Zelfstudie: Azure Active Directory-integratie met Help Scout | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Scout Help.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Zelfstudie: Azure Active Directory-integratie met Scout Help

In deze zelfstudie leert u hoe toointegrate helpen gids met Azure Active Directory (Azure AD).

U de volgende voordelen van Scout te integreren met Azure AD Hallo krijgen:

- In Azure AD, kunt u bepalen wie toegang tooHelp Scout heeft.
- U kunt uw gebruikers tooHelp Scout automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.
- U kunt uw accounts op één centrale locatie hello Azure-portal beheren.

Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooset van Azure AD-integratie met Help Scout, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een abonnement te Scout met eenmalige aanmelding ingeschakeld 

> [!NOTE]
> Als u Hallo stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.

Aanbevelingen voor het testen van Hallo stappen in deze zelfstudie:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. 

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Help Scout uit Hallo galerie toevoegen.
2. Instellen en testen van eenmalige aanmelding Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Help Scout van Hallo galerie toevoegen
tooset van integratie van Help Scout met Azure AD in de galerie Hallo Hallo Scout Help tooyour lijst met beheerde SaaS-apps toevoegen.

tooadd Scout uit de galerie Hallo helpen:

1. In Hallo [Azure-portal](https://portal.azure.com), Hallo linkermenu in, selecteer **Azure Active Directory**. 

    ![Hello Azure Active Directory-knop][1]

2. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![pagina met toepassingen Hallo Enterprise][2]
    
3. Selecteer een nieuwe toepassing tooadd **nieuwe toepassing**.

    ![knop voor nieuwe toepassing Hello][3]

4. Voer in het zoekvak Hallo **helpen Scout**. Selecteer in de zoekresultaten hello, **helpen Scout**, en selecteer vervolgens **toevoegen**.

    ![Scout Help in de lijst met resultaten Hallo](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Instellen en testen eenmalige aanmelding Azure AD

In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met Scout Help op basis van een testgebruiker met de naam *Britta Simon*.

Voor één aanmelding toowork moet Azure AD tooknow hello Azure AD-equivalent gebruiker in Scout Help. Een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Help Scout moet worden ingesteld.

Hallo tooestablish relatie in Scout te koppelen voor **gebruikersnaam**, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD.

tooconfigure en eenmalige aanmelding Azure AD-test met Help Scout, volledige Hallo taken te volgen:

1. [Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on). Een gebruiker toouse ingesteld met deze functie.
2. [Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user). Azure AD tests eenmalige aanmelding met Hallo gebruiker Britta Simon.
3. [Maak een testgebruiker Scout Help](#create-a-help-scout-test-user). Een exemplaar van Britta Simon in Help Scout gekoppelde toohello Azure AD-weergave van Hallo gebruiker is gemaakt.
4. [Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user). Stelt Britta Simon toouse eenmalige aanmelding Azure AD.
5. [Test eenmalige aanmelding](#test-single-sign-on). Controleert of dat die Hallo configuratie werkt.

### <a name="set-up-azure-ad-single-sign-on"></a>Instellen van eenmalige aanmelding Azure AD

In deze sectie kunt instellen u Azure AD eenmalige aanmelding in hello Azure-portal. Vervolgens instellen u eenmalige aanmelding in uw toepassing Scout Help.

tooset van Azure AD eenmalige aanmelding met Scout helpen:

1. In de Azure-portal op Hallo Hallo **helpen Scout** toepassing Integratiepagina **eenmalige aanmelding**.
 
    ![Koppeling voor eenmalige aanmelding instellen][4]

2. Op Hallo **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Onder **helpen Scout domein en URL's**, als u wilt dat tooset Hallo-toepassing in de IDP geïnitieerde modus volledige Hallo stappen te volgen:

    1. In Hallo **id** Voer een URL Hallo patroon volgen:`urn:auth0:helpscout:<instancename>`

    2. In Hallo **antwoord-URL** Voer een URL Hallo patroon volgen:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Als u in de modus Serviceprovider geïnitieerde tooset toepassing hello, selecteert u Hallo **weergeven geavanceerde instellingen voor URL** selectievakje en vervolgens Hallo te volgen:

    * In Hallo **aanmelden URL** Voer een URL Hallo volgende indeling:`https://secure.helpscout.net/members/login/`

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > Hallo-waarden in deze URL's zijn voor alleen demonstratie. Hallo-waarden bijwerken met Hallo werkelijke identificatie-URL en de antwoord-URL. Neem contact op met tooget deze waarden [helpen Scout ondersteuningsteam](mailto:help@helpscout.com). 

5. Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Selecteer **Opslaan**.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset van één aanmelding Hallo Scout Help-zijde, verzenden Hallo gedownload metagegevens XML-bestand toohello [helpen Scout ondersteuningsteam](mailto:help@helpscout.com). Deze instelling is van toepassing Hello Help Scout ondersteuningsteam zodat Hallo SAML één aanmelding verbinding juist is ingesteld op beide zijden.

> [!TIP]
> U kunt een beknopte versie van deze instructies in Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u uw app instelt! Nadat u Hallo app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer Hallo **Single Sign-On** tabblad. U hebt toegang tot documentatie in Hallo Hallo ingesloten **configuratie** sectie Hallo Hallo pagina onderaan in. Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

In deze sectie in hello Azure-portal, maakt u een testgebruiker Britta Simon met de naam.

![Een Azure AD-testgebruiker maken][100]

toocreate een testgebruiker in Azure AD:

1. Selecteer in de Azure-portal in het linkermenu Hallo Hallo **Azure Active Directory**.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.

    ![Gebruikers en groepen selecteren en selecteer alle gebruikers](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Hallo tooopen **gebruiker** in het dialoogvenster bovenaan Hallo Hallo **alle gebruikers** pagina **toevoegen**.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster, volledige Hallo stappen te volgen:

    1. In Hallo **naam** Voer **BrittaSimon**.

    2. In Hallo **gebruikersnaam** Voer Hallo e-mailadres van de gebruiker Britta Simon.

    3. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    4. Selecteer **Maken**.

        ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Een testgebruiker Scout te maken

Hallo-doel van deze sectie is toocreate Britta Simon in Scout helpen met de naam van een gebruiker. Help Scout ondersteunt just in time (Just in time) inrichting, die standaard is ingeschakeld.

In deze sectie is er geen actie of een taak toocomplete. Als een gebruiker nog niet in de Help Scout bestaat, wordt een nieuwe gemaakt wanneer u tooaccess Scout Help probeert.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie maakt toestaan u Hallo gebruiker Britta Simon eenmalige aanmelding toouse Azure AD Hallo gebruiker account toegang tooHelp Scout verleent.

![Hallo-gebruikersrollen toewijzen][200] 

tooassign Britta Simon tooHelp Scout:

1. Hallo toepassingen weergave opent in hello Azure-portal, en gaat u toohello directory weergeven. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **helpen Scout**.

    ![Hallo Scout Help-koppeling in lijst met toepassingen Hallo](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Selecteer in het linkermenu Hallo **gebruikers en groepen**.

    ![Hallo gebruikers en groepen koppelen][202]

4. Selecteer **Toevoegen**. Klik vervolgens op Hallo **toevoegen toewijzing** pagina **gebruikers en groepen**.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op Hallo **gebruikers en groepen** pagina in de lijst Hallo van gebruikers, selecteer **Britta Simon**.

6. Op Hallo **gebruikers en groepen** pagina **Selecteer**.

7. Op Hallo **toevoegen toewijzing** pagina **toewijzen**.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw configuratie Azure AD eenmalige aanmelding met behulp van het toegangsvenster Hallo testen.

Wanneer u Hallo Scout Help-tegel in het toegangsvenster Hallo selecteert, moet u tooyour Scout Help-toepassing automatisch worden aangemeld.

Zie voor meer informatie over het toegangsvenster [inleiding toohello toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

