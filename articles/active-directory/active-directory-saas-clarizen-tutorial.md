---
title: 'Zelfstudie: Azure Active Directory-integratie met Clarizen | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Clarizen.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Zelfstudie: Azure Active Directory-integratie met Clarizen

In deze zelfstudie leert u hoe toointegrate Azure Active Directory (Azure AD) met Clarizen. Deze integratie biedt u Hallo volgende voordelen:

- U kunt beheren, in Azure AD, die toegang tooClarizen heeft.
- U kunt uw gebruikers toobe tooClarizen (eenmalige aanmelding) met hun Azure AD-accounts automatisch aangemeld inschakelen.
- U kunt uw accounts op één centrale locatie, hello Azure-portal beheren.

Hallo-scenario in deze zelfstudie bestaat uit twee belangrijke taken:

1. Clarizen uit Hallo galerie toevoegen.
2. Configureren en testen eenmalige aanmelding Azure AD.

Als u meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten
Azure AD-integratie met Clarizen tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Clarizen-abonnement dat ingeschakeld voor eenmalige aanmelding

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Eenmalige aanmelding Azure AD testen in een testomgeving. Gebruik niet uw productieomgeving, tenzij dit noodzakelijk is.
- Als u een Azure AD-testomgeving geen hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Clarizen van Hallo galerie toevoegen
tooconfigure hello integratie van Clarizen in Azure AD Clarizen uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.

1. In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Active Directory** pictogram.

    ![Azure Active Directory-pictogram][1]

2. Klik op **bedrijfstoepassingen**. Klik vervolgens op **alle toepassingen**.

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][2]

3. Klik op Hallo **toevoegen** knop Hallo boven aan het Hallo-dialoogvenster.

    ![de knop "Toevoegen" Hello][3]

4. Typ in het zoekvak Hallo **Clarizen**.

    !['Clarizen' hello zoekvak te typen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Selecteer in het deelvenster met resultaten Hallo **Clarizen**, en klik vervolgens op **toevoegen** tooadd Hallo-toepassing.

    ![Clarizen selecteren in het resultatenvenster Hallo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In de Hallo uit te voeren, configureren en testen eenmalige aanmelding Azure AD met Clarizen op basis van de testgebruiker Hallo Britta Simon.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Clarizen is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Clarizen toobe tot stand gebracht. U de relatie van deze koppeling tot stand brengen door toe te wijzen Hallo-waarde van **gebruikersnaam** in Azure AD als Hallo-waarde van **gebruikersnaam** in Clarizen.

tooconfigure en eenmalige aanmelding Azure AD-test met Clarizen, volledige Hallo bouwstenen te volgen:

1. **[Eenmalige aanmelding Azure AD configureren](#configure-azure-ad-single-sign-on)**  tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  tootest eenmalige aanmelding Azure AD met Britta Simon.
3. **[Maak een testgebruiker Clarizen](#create-a-clarizen-test-user)**  toohave een equivalent van Britta Simon in Clarizen die is gekoppeld toohello Azure AD-weergave van haar.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren
Schakel Azure AD eenmalige aanmelding in hello Azure-portal en configureer eenmalige aanmelding in uw toepassing Clarizen.

1. In de Azure-portal op Hallo Hallo **Clarizen** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Te klikken op "Single sign-on"][4]

2. In Hallo **eenmalige aanmelding** in het dialoogvenster voor **modus**, selecteer **op basis van SAML aanmelding** tooenable eenmalige aanmelding.

    !['Op basis van SAML aanmelding' selecteren](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. In Hallo **Clarizen domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Dialoogvensters voor id en de antwoord-URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. In Hallo **id** vak Hallo typewaarde als: **Clarizen**

    b. In Hallo **antwoord-URL** typt u een URL met behulp van Hallo patroon volgen: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Deze zijn niet Hallo echte waarden. U hebt toouse Hallo werkelijke id en antwoord-URL. Hier is het raadzaam Hallo unieke waarde van een tekenreeks te gebruiken, zoals id Hallo. tooget Werkelijke waarden, neem contact op met Hallo Hallo [Clarizen ondersteuningsteam](https://success.clarizen.com/hc/en-us/requests/new).

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.

    ![Te klikken op 'Nieuw certificaat maken'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. In Hallo **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram Kalender Hallo en kiest u een vervaldatum. Klik vervolgens op **Opslaan**.

    ![Selecteren en een vervaldatum opslaan](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. In Hallo **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren**, en klik vervolgens op **opslaan**.

    ![Als u het selectievakje Hallo voor het nieuwe certificaat Hallo actief maken](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. In Hallo **rollovercertificaat** in het dialoogvenster, klikt u op **OK**.

    ![Te klikken op 'OK' tooconfirm die u toomake Hallo certificaat active wilt](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. In Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het Hallo-certificaatbestand op uw computer.

    !['Certificaat (Base64)' toostart Hallo downloaden te klikken op](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. In Hallo **Clarizen configuratie** sectie, klikt u op **configureren Clarizen** tooopen hello **eenmalige aanmelding configureren** venster.

    ![Te klikken op 'Clarizen configureren'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    !['Configureren aanmelding' venster, inclusief URL's en bestanden](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. Meld u tooyour Clarizen bedrijf site als een beheerder in een ander browservenster.

11. Klik op uw gebruikersnaam en klik vervolgens op **instellingen**.

    ![Te klikken op 'Instellingen' onder uw gebruikersnaam](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "instellingen")

12. Klik op Hallo **globale instellingen** tabblad. Vervolgens volgende te**Federated Authentication**, klikt u op **bewerken**.

    ![Tabblad 'Globale instellingen'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "globale instellingen")

13. In Hallo **Federated Authentication** dialoogvenster Voer Hallo stappen te volgen:

    ![In het dialoogvenster 'Federated Authentication'](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")

    a. Selecteer **inschakelen voor federatieve verificatie**.

    b. Klik op **uploaden** tooupload uw gedownloade certificaat.

    c. In Hallo **aanmelden URL** Voer Hallo-waarde van **SAML Single Sign-On Service-URL** van venster hello Azure AD-toepassing-configuratie.

    d. In Hallo **Sign-out URL** Voer Hallo-waarde van **Sign-Out URL** van venster hello Azure AD-toepassing-configuratie.

    e. Selecteer **POST gebruiken**.

    f. Klik op **Opslaan**.

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In hello Azure-portal, maakt u een testgebruiker Britta Simon aangeroepen.

![Naam en e-mailadres van de testgebruiker hello Azure AD][100]

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** pictogram.

    ![Azure Active Directory-pictogram](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Klik op **gebruikers en groepen**, en klik vervolgens op **alle gebruikers** toodisplay Hallo lijst met gebruikers.

    ![Te klikken op 'Gebruikers en groepen' en 'Alle gebruikers'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. Klik boven Hallo van dialoogvenster Hallo op **toevoegen** tooopen hello **gebruiker** in het dialoogvenster.

    ![de knop "Toevoegen" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![In het dialoogvenster met de naam, e-mailadres en wachtwoord 'Gebruiker' ingevuld](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** vak type Hallo e-mailadres van Hallo Britta Simon account.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde Hallo van **wachtwoord**.

    d. Klik op **Create**.

### <a name="create-a-clarizen-test-user"></a>Een testgebruiker Clarizen maken
Azure AD gebruikers toosign tooenable in tooClarizen, moet u gebruikersaccounts inrichten. In geval van Clarizen Hallo is inrichting een handmatige taak.

1. Meld u tooyour Clarizen bedrijf site als beheerder.

2. Klik op **mensen**.

    ![Te klikken op 'Mensen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "personen")

3. Klik op **gebruiker uitnodigen**.

    ![Knop 'Gebruiker uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "gebruikers uitnodigen")

4. In Hallo **personen uitnodigen** dialoogvenster Voer Hallo stappen te volgen:

    ![Dialoogvenster 'Personen uitnodigen'](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "personen uitnodigen")

    a. In Hallo **e** vak type Hallo e-mailadres van Hallo Britta Simon account.

    b. Klik op **uitnodigen**.

    > [!NOTE]
    > Hello Azure Active Directory-accounthouder wordt een e-mailbericht ontvangen en volg een koppeling tooconfirm hun account maken voordat deze geactiveerd wordt.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD
Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooClarizen toegang verlenen.

![Toegewezen testgebruiker][200]

1. In hello Azure-portal, Hallo toepassingen weergave opent, blader toohello directory weergeven, klikt u op **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen**.

    ![Te klikken op 'Bedrijfstoepassingen' en 'Alle toepassingen'][201]

2. Selecteer in de lijst met de toepassingen van Hallo **Clarizen**.

    ![Clarizen selecteren in lijst Hallo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Klik in het linkerdeelvenster Hallo **gebruikers en groepen**.

    ![Te klikken op 'Gebruikers en groepen'][202]

4. Klik op Hallo **toevoegen** knop. Klik op Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.

    ![Hallo "Toevoegen" knop en Hallo 'Toewijzing toevoegen' dialoogvenster][203]

5. In Hallo **gebruikers en groepen** dialoogvenster, **Britta Simon** in Hallo lijst met gebruikers.

6. In Hallo **gebruikers en groepen** dialoogvenster vak, klikt u op Hallo **Selecteer** knop.

7. In Hallo **toevoegen toewijzing** dialoogvenster vak, klikt u op Hallo **toewijzen** knop.

### <a name="test-single-sign-on"></a>Test eenmalige aanmelding
Test uw configuratie Azure AD eenmalige aanmelding met Hallo Toegangsvenster.

Wanneer u Hallo Clarizen tegel in Hallo toegangsvenster klikt, moet u tooyour Clarizen toepassing automatisch worden aangemeld.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
