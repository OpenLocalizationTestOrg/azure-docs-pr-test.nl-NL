---
title: 'Zelfstudie: Azure Active Directory-integratie met RFPIO | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Zelfstudie: Azure Active Directory-integratie met RFPIO

In deze zelfstudie leert u hoe toointegrate RFPIO met Azure Active Directory (Azure AD).

RFPIO integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt bepalen wie in Azure AD die tooRFPIO toegang heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooRFPIO (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie--hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met RFPIO tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement.
- Een RFPIO eenmalige aanmelding op ingeschakeld abonnement.

> [!NOTE]
> Niet aanbevolen dat u een productie-omgeving tootest Hallo stappen in deze zelfstudie.

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik uw productieomgeving tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo-scenario dat wordt beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van RFPIO van Hallo-galerie.
2. Configureren en testen van Azure AD eenmalige aanmelding.

## <a name="add-rfpio-from-hello-gallery"></a>RFPIO van Hallo galerie toevoegen
tooconfigure hello integratie van RFPIO in Azure AD, moet u tooadd RFPIO uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO uit Hallo-galerie

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Toepassingen][2]
    
3. tooadd een nieuwe toepassing selecteert Hallo **nieuwe toepassing** knop op Hallo bovenaan in het dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **RFPIO**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Selecteer in het deelvenster resultaten hello, **RFPIO**, en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie configureert en test eenmalige aanmelding Azure AD met RFPIO op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo-relatie is tussen de gebruiker die equivalent in RFPIO en een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in RFPIO toobe tot stand gebracht.

Wijs in RFPIO, Hallo-waarde van **gebruikersnaam** in Azure AD als Hallo-waarde van **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met RFPIO, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configuring-azure-ad-single-sign-on)**--tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**--tootest eenmalige aanmelding Azure AD met Britta Simon.
3. **[Maak een testgebruiker RFPIO](#creating-a-rfpio-test-user)**  --toohave een equivalent van Britta Simon in RFPIO die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assigning-the-azure-ad-test-user)**--tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#testing-single-sign-on)**  --tooverify als Hallo configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw toepassing RFPIO configureren.

**Azure AD tooconfigure eenmalige aanmelding met RFPIO, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **RFPIO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Op Hallo **RFPIO domein en de URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. In Hallo **id** textbox type Hallo URL:`https://www.rfpio.com`

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Controleer **weergeven geavanceerde instellingen voor URL**.

    c. In Hallo **Relay status** textbox een tekenreekswaarde invoeren. Neem contact op met [RFPIO ondersteuningsteam](https://www.rfpio.com/contact/) tooget deze waarde. 

4. Controleer **weergeven geavanceerde instellingen voor URL**. U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    In Hallo **aanmelden URL** textbox type Hallo URL:`https://www.app.rfpio.com`

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. In een andere web-browservenster aanmelding toohello **RFPIO** website als beheerder.

8. Klik op Hallo onder linkerhoek vervolgkeuzelijst.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Klik op Hallo **organisatie-instellingen**. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Klik op Hallo **functies & integratie**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. In Hallo **SAML-configuratie van SSO** klikt u op **bewerken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. In deze sectie voert u volgende acties:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Hallo inhoud Hallo kopiëren **gedownload van metagegevens-XML** en plak deze in Hallo **identiteit configuratie** veld.

    > [!NOTE]
    >toocopy Hallo van inhoud gedownload **Metadata XML** gebruik **Kladblok ++** of de juiste **XML-Editor**. 

    b. Klik op **valideren**.

    c. Na klikken **valideren**, spiegelen **SAML(Enabled)** tooon.

    d. Klik op **indienen**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="create-a-rfpio-test-user"></a>Een testgebruiker RFPIO maken

Azure AD tooenable gebruikers toolog in tooRFPIO, ze in RFPIO moeten worden ingericht.  
In geval van RFPIO Hallo is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Aanmelden tooyour RFPIO bedrijf site als beheerder.

2. Klik op Hallo onder linkerhoek vervolgkeuzelijst.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Klik op Hallo **organisatie-instellingen**. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Klik op **TEAMLEDEN**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Klik op **leden toevoegen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. In Hallo **nieuwe leden toevoegen** sectie. Voer de volgende acties:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Voer **e-mailadres** in Hallo **Voer één e-mailadres per regel** veld.

    b. Selecteer Plese **rol** volgens uw vereisten.

    c. Klik op **leden toevoegen**.
        
    > [!NOTE]
    > Hello Azure Active Directory-accounthouder ontvangt een e-mailbericht en een koppeling tooconfirm volgt hun account voordat deze geactiveerd wordt.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen tooRFPIO toegang verleent.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooRFPIO, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **RFPIO**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van Hallo Toegangsvenster.

Als u op Hallo RFPIO-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour RFPIO toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het toointegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

