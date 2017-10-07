---
title: "Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en IBM Kenexa enquête Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise

In deze zelfstudie leert u hoe toointegrate IBM Kenexa enquête Enterprise met Azure Active Directory (Azure AD).

IBM Kenexa enquête Enterprise integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooIBM Kenexa enquête onderneming heeft.
- U kunt uw gebruikers tooautomatically aanmelding tooIBM Kenexa enquête Enterprise inschakelen met behulp van eenmalige aanmelding (SSO) met hun Azure AD-accounts.
- U kunt uw accounts op één locatie beheren: hello Azure-portal.

Als u tooknow meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met IBM Kenexa enquête Enterprise tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een abonnement IBM Kenexa enquête Enterprise SSO-ingeschakeld

> [!NOTE]
> Wanneer u Hallo stappen in deze zelfstudie test, wordt u aangeraden een productie-omgeving niet te gebruiken.

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving. Hallo scenario beschreven in de zelfstudie Hallo bestaat uit twee belangrijkste bouwstenen:

* IBM Kenexa enquête Enterprise uit Hallo galerie toe te voegen.
* Configureren en testen van Azure AD-SSO

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>IBM Kenexa enquête Enterprise van Hallo galerie toevoegen
IBM Kenexa enquête Enterprise tooconfigure Hallo integratie van IBM Kenexa enquête onderneming in Azure AD toevoegen via Hallo galerie tooyour lijst met beheerde SaaS-apps.

IBM Kenexa enquête Enterprise via Hallo gallery tooadd Hallo te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, klik op Hallo **Azure Active Directory** knop. 

    ![Hello Azure Active Directory-knop][1]

2. Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. tooadd een toepassing, klikt u op Hallo **nieuwe toepassing** knop.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **IBM Kenexa enquête Enterprise**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Selecteer in de lijst met resultaten Hallo **IBM Kenexa enquête Enterprise**, en klik vervolgens op Hallo **toevoegen** knop tooadd Hallo-toepassing.

    ![IBM Kenexa enquête Enterprise in de lijst met resultaten Hallo](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen van Azure AD-SSO met IBM Kenexa enquête Enterprise op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding toowork moet Azure AD tooidentify Hallo IBM Kenexa enquête Enterprise gebruiker equivalent in Azure AD. Azure AD moet met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en een bijbehorende gebruiker maken in IBM Kenexa enquête onderneming.

Hallo-waarde toewijzen Hallo-tooestablish Hallo koppeling relatie **gebruikersnaam** in IBM Kenexa enquête Enterprise als de waarde Hallo Hallo **gebruikersnaam** in Azure AD.

Hallo bouwstenen in de volgende twee secties Hallo tooconfigure en test Azure AD-SSO met IBM Kenexa enquête Enterprise, voltooid.

### <a name="configure-azure-ad-sso"></a>Azure AD-eenmalige aanmelding configureren

In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing IBM Kenexa enquête Enterprise door Hallo volgende te doen:

1. In de Azure-portal op Hallo Hallo **IBM Kenexa enquête Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![IBM Kenexa enquête Enterprise configureren één aanmelding koppeling][4]

2. In Hallo **eenmalige aanmelding** dialoogvenster in Hallo **modus** de optie **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. In Hallo **IBM Kenexa enquête Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![IBM Kenexa enquête Enterprise domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. In Hallo **id** textbox type een URL met Hallo patroon volgen:`https://surveys.kenexa.com/<companycode>`

    b. In Hallo **antwoord-URL** textbox type een URL met Hallo patroon volgen:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Hallo voorgaande waarden zijn niet echt. Deze bijwerken met de werkelijke Hallo-id en antwoord-URL. tooobtain Werkelijke waarden, neem contact op met Hallo Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).

4. Onder **SAML-certificaat voor ondertekening van**, klikt u op **certificaat (Base64)**, en sla Hallo certificaat bestand tooyour computer.

    ![Hallo downloadkoppeling voor het certificaat (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Hallo IBM Kenexa enquête bedrijfstoepassing verwacht tooreceive Hallo Security Asserties Markup Language (SAML) asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen toohello configuratie van de kenmerken van SAML-token. Hallo waarde van Hallo gebruiker-id claim Hallo antwoord moet overeenkomen met Hallo SSO-ID die geconfigureerd in Hallo Kenexa systeem. toomap Hallo juiste gebruikers-id in uw organisatie als SSO Internet Datagram Protocol (IDP), werken met Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw). 

    Azure AD wordt standaard Hallo gebruikers-id als Hallo gebruiker UPN (User Principal Name)-waarde ingesteld. U kunt deze waarde op Hallo wijzigen **kenmerk** tabblad, zoals wordt weergegeven in de volgende schermafbeelding Hallo. Hallo-integratie werkt alleen nadat u de toewijzing correct Hallo hebt voltooid.
    
    ![Hallo gebruikerskenmerken dialoogvenster](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Klik op **Opslaan**.

    ![Hallo configureren eenmalige aanmelding knop Opslaan](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. Hallo tooopen **eenmalige aanmelding configureren** venster onder **IBM Kenexa enquête Enterprise Configuration**, klikt u op **configureren IBM Kenexa enquête Enterprise**. 
 
    ![Hallo configureren IBM Kenexa enquête Enterprise-koppeling](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Kopiëren Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML één Service-URL aanmelding** waarden uit Hallo **Naslaggids** sectie.

8. In Hallo **eenmalige aanmelding configureren** venster onder **Naslaggids**, kopie Hallo **Sign-Out URL**, **SAML entiteit-ID**, en  **SAML één Service-URL aanmelding** waarden.

9. tooconfigure SSO op Hallo **IBM Kenexa enquête Enterprise** zijde, Hallo gedownload verzenden **certificaat (Base64)**, **Sign-Out URL**, **SAML entiteit-ID**, en **SAML één Service-URL aanmelding** waarden toohello [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> U kunt verwijzen tooa beknopte versie van deze instructies in Hallo [Azure-portal](https://portal.azure.com) terwijl u Hallo-app instelt. Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, klikt u op Hallo **eenmalige aanmelding** tabblad en vervolgens toegang Hallo ingesloten documentatie via Hallo **configuratie** sectie aan Hallo einde. toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [documentatie van Azure AD ingesloten](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie kunt u testgebruiker Britta Simon in hello Azure-portal maken door Hallo volgende te doen:

![Een Azure AD-testgebruiker maken][100]

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Een IBM Kenexa enquête Enterprise testgebruiker maken

In deze sectie kunt u een gebruiker met de naam van Britta Simon in IBM Kenexa enquête onderneming maken. 

toocreate gebruikers in Hallo IBM Kenexa enquête bedrijfssysteem en kaart Hallo SSO-ID voor deze, kunt u samenwerken met Hallo [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw). Deze waarde SSO-ID moet ook toegewezen toohello gebruiker id-waarde van Azure AD. U kunt deze standaardinstelling op Hallo wijzigen **kenmerk** tabblad.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u gebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooIBM Kenexa enquête Enterprise.

![Hallo-gebruikersrollen toewijzen][200] 

tooassign gebruiker Britta Simon tooIBM Kenexa enquête Enterprise, Hallo te volgen:

1. Open in hello Azure-portal, Hallo **toepassingen** weergeven, gaat u toohello **Directory** weergave, selecteer **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen**.

    ![Hallo 'bedrijfstoepassingen' en 'Alle toepassingen' koppelingen][201] 

2. In Hallo **toepassingen** selecteert **IBM Kenexa enquête Enterprise**.

    ![Hallo IBM Kenexa enquête Enterprise koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Klik in het linkerdeelvenster Hallo **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op Hallo **toevoegen** knop en klik vervolgens op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.

6. In Hallo **gebruikers en groepen** dialoogvenster vak, klikt u op Hallo **Selecteer** knop.

7. In Hallo **toevoegen toewijzing** dialoogvenster vak, klikt u op Hallo **toewijzen** knop.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.

Wanneer u klikt op Hallo **IBM Kenexa enquête Enterprise** tegel in Hallo Toegangsvenster, u moet automatisch aangemeld tooyour IBM Kenexa enquête bedrijfstoepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
