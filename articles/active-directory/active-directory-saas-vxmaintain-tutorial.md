---
title: 'Zelfstudie: Azure Active Directory integreren met vxMaintain | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en vxMaintain.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Zelfstudie: Azure Active Directory integreren met vxMaintain

In deze zelfstudie leert u hoe toointegrate vxMaintain met Azure Active Directory (Azure AD).

Deze integratie biedt een aantal belangrijke voordelen. U kunt:

- Besturingselement in Azure AD wie heeft toegang tot toovxMaintain.
- Uw gebruikers tooautomatically aanmelding toovxMaintain met eenmalige aanmelding (SSO) inschakelen met behulp van hun Azure AD-accounts.
- Uw accounts beheren via één centrale locatie: hello Azure-portal.

Zie toolearn meer over de integratie met Azure AD SaaS [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met vxMaintain tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een vxMaintain abonnement SSO-ingeschakeld

> [!NOTE]
> Wanneer u Hallo stappen in deze zelfstudie test, wordt u aangeraden een productie-omgeving niet te gebruiken.

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. 

Hallo-scenario dat geeft een overzicht van deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

* Het toevoegen van vxMaintain van Hallo-galerie
* Configureren en testen van Azure AD eenmalige aanmelding

## <a name="add-vxmaintain-from-hello-gallery"></a>VxMaintain van Hallo galerie toevoegen
tooconfigure hello integratie van vxMaintain met Azure AD, moet u tooadd vxMaintain uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

tooadd vxMaintain via Hallo gallery Hallo te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com), in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop. 

    ![Hello Azure Active Directory-knop][1]

2. Selecteer **bedrijfstoepassingen** > **alle toepassingen**.

    ![Hallo 'Bedrijfstoepassingen' deelvenster][2]
    
3. een toepassing, in Hallo tooadd **alle toepassingen** dialoogvenster, **nieuwe toepassing**.

    !['Nieuwe application' Hallo knop][3]

4. Typ in het zoekvak Hallo **vxMaintain**.

    ![Hallo 'Single Sign-on modus' vervolgkeuzelijst](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Selecteer in de lijst met resultaten Hallo **vxMaintain**, en selecteer vervolgens **toevoegen**.

    ![Hallo vxMaintain koppeling](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie u configureren en testen van Azure AD-SSO met behulp van vxMaintain, op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding toowork moet Azure AD tooknow hello vxMaintain equivalent toohello Azure AD-gebruiker. Dat wil zeggen, moet u een koppeling bestaat tussen hello Azure AD-gebruiker en Hallo bijbehorende vxMaintain gebruiker instellen.

tooestablish hello koppeling relatie toewijzen Hallo vxMaintain **gebruikersnaam** waarde als hello Azure AD **gebruikersnaam** waarde.

tooconfigure en test Azure AD-SSO met behulp van vxMaintain, volledige Hallo bouwstenen te volgen.

### <a name="configure-azure-ad-sso"></a>Azure AD-eenmalige aanmelding configureren

In deze sectie maakt kunt u zowel Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing vxMaintain door Hallo volgende te doen:

1. In de Azure-portal op Hallo Hallo **vxMaintain** toepassing Integratiepagina **eenmalige aanmelding**.

    ![opdracht 'Single sign-on' Hallo][4]

2. tooenable SSO in Hallo **modus voor één aanmelding** vervolgkeuzelijst, selecteer **op basis van SAML aanmelding**.
 
    ![de opdracht 'op basis van SAML aanmelding' Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. Onder **vxMaintain domein en de URL's**, Hallo te volgen:

    ![Hallo vxMaintain sectie domein en URL 's](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. In Hallo **id** vak een URL die is Hallo de volgende syntaxis:`https://<company name>.verisae.com`

    b. In Hallo **antwoord-URL** vak een URL die is Hallo de volgende syntaxis:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Hallo voorgaande waarden zijn niet echt. Deze bijwerken met de werkelijke Hallo-id en antwoord-URL. tooobtain hello waarden, neem contact op met Hallo [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us).
 
4. Onder **SAML-certificaat voor ondertekening van**, selecteer **Metadata XML**, en sla Hallo metagegevens bestand tooyour computer.

    ![de sectie 'SAML handtekeningcertificaat' Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Selecteer **Opslaan**.

    ![de knop Opslaan Hallo](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, verzenden Hallo gedownload **Metadata XML** bestand toohello [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us).

> [!TIP]
> Bij het instellen van de app hello, vindt u een beknopte versie van de voorgaande instructies in Hallo Hallo [Azure-portal](https://portal.azure.com). Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **Single Sign-On** tabblad en toegang Hallo documentatie van Hallo ingesloten **configuratie** sectie. 
>
>toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [het beheren van eenmalige aanmelding voor zakelijke apps](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie kunt u testgebruiker Britta Simon in hello Azure-portal maken door Hallo volgende te doen:

![testgebruiker Hello Azure AD][100]

1. In Hallo **Azure-portal**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.

    ![Hallo 'Azure Active Directory' knop](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. een lijst met gebruikers, toodisplay te gaan**gebruikers en groepen** > **alle gebruikers**.
    
    ![Hallo 'Alle gebruikers' koppelen](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Hallo **alle gebruikers** dialoogvenster wordt geopend. 

3. Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de testgebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en Opmerking Hallo waarde die is gegenereerd in Hallo **wachtwoord** vak.

    d. Selecteer **Maken**.
 
### <a name="create-a-vxmaintain-test-user"></a>Een testgebruiker vxMaintain maken

In deze sectie maakt u testgebruiker Britta Simon in vxMaintain. tooadd gebruikers in Hallo vxMaintain platform, werken met de [vxMaintain ondersteuningsteam](http://www.verisae.com/contact-us). Voordat u eenmalige aanmelding gebruiken, maken en activeren Hallo gebruikers.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u testgebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen toovxMaintain toegang verleent. toodo dus Hallo te volgen:

![Testgebruiker in Hallo weergavenaam lijst][200] 

1. In de Azure-portal Hallo **toepassingen** weergeven, gaat u te**Directory** weergave > **bedrijfstoepassingen** > **alle toepassingen**.

    ![Hallo 'Alle toepassingen' koppelen][201] 

2. In Hallo **toepassingen** selecteert **vxMaintain**.

    ![Hallo vxMaintain koppeling](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Selecteer in het linkerdeelvenster Hallo **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Selecteer **toevoegen** en klikt u op Hallo **toevoegen toewijzing** deelvenster **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][203]

5. In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**, en selecteer vervolgens Hallo **selecteren** knop.

7. In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Test uw Azure AD eenmalige aanmelding

In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.

Selecteren Hallo **vxMaintain** tegel in Hallo Toegangsvenster moet u tooyour vxMaintain toepassing automatisch aanmelden.

Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Volgende stappen

* [Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

