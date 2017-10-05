---
title: 'Zelfstudie: Azure Active Directory-integratie met Help Scout | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Scout Help.
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
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Zelfstudie: Azure Active Directory-integratie met Scout Help

In deze zelfstudie leert u hoe Scout te integreren met Azure Active Directory (Azure AD).

Bij het ophalen van de volgende voordelen van Scout te integreren met Azure AD:

- In Azure AD kunt u bepalen wie toegang heeft tot Scout Help.
- U kunt uw gebruikers helpen Scout automatisch aanmelden met behulp van eenmalige aanmelding en Azure AD-account van een gebruiker.
- U kunt uw accounts op één centrale locatie, de Azure-portal beheren.

Zie voor meer informatie over software als een dienst (SaaS)-app-integratie met Azure AD, [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Als u Azure AD-integratie met Help Scout instelt, moet u de volgende items:

- Een Azure AD-abonnement
- Een abonnement te Scout met eenmalige aanmelding ingeschakeld 

> [!NOTE]
> Als u de stappen in deze zelfstudie hebt getest, wordt u aangeraden dat u deze niet in een productieomgeving testen.

Aanbevelingen voor het testen van de stappen in deze zelfstudie:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. 

Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Help Scout uit de galerie toevoegen.
2. Instellen en testen van eenmalige aanmelding Azure AD.

## <a name="add-help-scout-from-the-gallery"></a>Help Scout uit de galerie toevoegen
Om in te stellen de integratie van Help Scout met Azure AD in de galerie toevoegen Scout helpen aan de lijst met beheerde SaaS-apps.

Help Scout uit de galerie toevoegen:

1. In de [Azure-portal](https://portal.azure.com), selecteer in het menu links **Azure Active Directory**. 

    ![De Azure Active Directory-knop][1]

2. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![De pagina met Enterprise-toepassingen][2]
    
3. Selecteer om een nieuwe toepassing toe **nieuwe toepassing**.

    ![De knop Nieuw toepassing][3]

4. Voer in het zoekvak **helpen Scout**. Selecteer in de lijst met zoekresultaten **helpen Scout**, en selecteer vervolgens **toevoegen**.

    ![Help Scout in de lijst met resultaten](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Instellen en testen eenmalige aanmelding Azure AD

In deze sectie kunt u instellen en eenmalige aanmelding Azure AD-test met Scout Help op basis van een testgebruiker met de naam *Britta Simon*.

Voor eenmalige aanmelding werkt, moet Azure AD de equivalente Azure AD-gebruiker in de Help Scout bekend. Een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Help Scout moet worden ingesteld.

Om te bepalen van de relatie koppeling in de Help Scout voor **gebruikersnaam**, wijs de waarde van de **gebruikersnaam** in Azure AD.

Als u wilt configureren en Azure AD eenmalige aanmelding met Scout te testen, moet u de volgende taken uitvoeren:

1. [Instellen van eenmalige aanmelding Azure AD](#set-up-azure-ad-single-sign-on). Hiermee stelt u een gebruiker deze functie wilt gebruiken.
2. [Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user). Azure AD tests eenmalige aanmelding met de gebruiker Britta Simon.
3. [Maak een testgebruiker Scout Help](#create-a-help-scout-test-user). Maakt een equivalent van Britta Simon in Help Scout, dat is gekoppeld aan de Azure AD-weergave van de gebruiker.
4. [Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user). Ingesteld Britta Simon naar Azure AD gebruikt eenmalige aanmelding.
5. [Test eenmalige aanmelding](#test-single-sign-on). Verifieert dat de configuratie werkt.

### <a name="set-up-azure-ad-single-sign-on"></a>Instellen van eenmalige aanmelding Azure AD

In deze sectie kunt instellen u Azure AD eenmalige aanmelding in de Azure portal. Vervolgens instellen u eenmalige aanmelding in uw toepassing Scout Help.

Voor het instellen van Azure AD eenmalige aanmelding met Scout helpen:

1. In de Azure-portal op de **helpen Scout** toepassing Integratiepagina **eenmalige aanmelding**.
 
    ![Koppeling voor eenmalige aanmelding instellen][4]

2. Op de **eenmalige aanmelding** pagina voor **modus**, selecteer **op basis van SAML aanmelding**.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Onder **helpen Scout domein en URL's**, als u wilt dat voor het instellen van de toepassing in de IDP geïnitieerde modus voltooid de volgende stappen uit:

    1. In de **id** Voer een URL die het volgende patroon volgen is:`urn:auth0:helpscout:<instancename>`

    2. In de **antwoord-URL** Voer een URL die het volgende patroon volgen is:`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Als u wilt dat de toepassing in de modus Serviceprovider geïnitieerde ingesteld, selecteert u de **weergeven geavanceerde instellingen voor URL** uit en doe vervolgens het volgende:

    * In de **aanmelden URL** Voer een URL die de volgende indeling heeft:`https://secure.helpscout.net/members/login/`

    ![Help-URL's en Scout domein één aanmelding informatie](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > De waarden in deze URL's zijn voor de demonstratie alleen. Werk de waarden op met de werkelijke identificatie-URL en de antwoord-URL. Als u deze waarden, neem contact op met [helpen Scout ondersteuningsteam](mailto:help@helpscout.com). 

5. Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Selecteer **Opslaan**.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. Als u eenmalige aanmelding aan de kant van de Help Scout instelt, verzendt het gedownloade metagegevens-XML-bestand naar de [helpen Scout ondersteuningsteam](mailto:help@helpscout.com). Het ondersteuningsteam Scout Help is deze instelling zodat de SAML eenmalige aanmelding verbinding juist is ingesteld op beide zijden van toepassing.

> [!TIP]
> Vindt u een beknopte versie van deze instructies in de [Azure-portal](https://portal.azure.com), terwijl u uw app instelt. Nadat u de app door te selecteren toevoegen **Active Directory** > **bedrijfstoepassingen**, selecteer de **Single Sign-On** tabblad. U hebt toegang tot het embedded-documentatie in de **configuratie** sectie aan de onderkant van de pagina. Zie voor meer informatie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

In deze sectie in de Azure portal maakt u een testgebruiker Britta Simon met de naam.

![Een Azure AD-testgebruiker maken][100]

Een testgebruiker maken in Azure AD:

1. Selecteer in de Azure-portal in het menu links **Azure Active Directory**.

    ![De Azure Active Directory-knop](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.

    ![Gebruikers en groepen selecteren en selecteer alle gebruikers](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster aan de bovenkant van de **alle gebruikers** pagina **toevoegen**.

    ![De knop toevoegen](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster Vervolledig de volgende stappen uit:

    1. In de **naam** Voer **BrittaSimon**.

    2. In de **gebruikersnaam** Voer het e-mailadres van gebruiker Britta Simon.

    3. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    4. Selecteer **Maken**.

        ![Het dialoogvenster gebruiker](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Een testgebruiker Scout te maken

Het object van deze sectie is het maken van een gebruiker met de naam Britta Simon in Scout Help. Help Scout ondersteunt just in time (Just in time) inrichting, die standaard is ingeschakeld.

In deze sectie vindt er geen actie of de taak is voltooid. Als een gebruiker niet al in de Help Scout bestaat, wordt een nieuw wordt gemaakt wanneer u probeert te openen Scout Help.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie kunt u de gebruiker Britta Simon Azure AD eenmalige aanmelding gebruiken door de gebruikerstoegang verlenen aan Help Scout toestaan.

![Toewijzen van de gebruikersrol][200] 

Britta Simon toewijzen aan Scout helpen:

1. Open de toepassingen in de Azure portal en gaat u naar de directoryweergave. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **helpen Scout**.

    ![De Scout Help-koppeling in de lijst met toepassingen](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Selecteer in het menu links **gebruikers en groepen**.

    ![De koppeling gebruikers en groepen][202]

4. Selecteer **Toevoegen**. Klik op de **toevoegen toewijzing** pagina **gebruikers en groepen**.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op de **gebruikers en groepen** pagina in de lijst met gebruikers, selecteer **Britta Simon**.

6. Op de **gebruikers en groepen** pagina **Selecteer**.

7. Op de **toevoegen toewijzing** pagina **toewijzen**.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van het toegangsvenster.

Wanneer u de tegel Help Scout in het deelvenster toegang selecteert, moet u worden automatisch aangemeld bij uw toepassing Scout Help.

Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
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

