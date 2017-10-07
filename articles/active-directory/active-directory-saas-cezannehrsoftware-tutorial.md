---
title: 'Zelfstudie: Azure Active Directory-integratie met Cezanne HR software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Cezanne HR-software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Zelfstudie: Azure Active Directory integreren met Cezanne HR-software

In deze zelfstudie leert u hoe toointegrate Cezanne HR-software met Azure Active Directory (Azure AD).

Cezanne HR software integreren met Azure AD biedt u Hallo volgende voordelen. U kunt:

- Beheren in Azure AD die toegang tooCezanne heeft HR-software.
- Schakel uw gebruikers tooautomatically aanmelding tooCezanne HR-software met eenmalige aanmelding (SSO) met hun Azure AD-accounts.
- Uw accounts beheren via één centrale locatie: hello Azure-portal.

Zie toolearn meer informatie over de software als een dienst (SaaS)-app-integratie met Azure AD [wat is er toegang tot toepassingen en SSO met Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met Cezanne HR-software, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Cezanne HR software abonnement SSO-ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, het is raadzaam dat u niet een productieomgeving gebruikt.

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving. 

Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

* Het toevoegen van Cezanne HR-software van Hallo-galerie
* Configureren en testen van Azure AD-SSO

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Cezanne HR software uit de galerie Hallo toevoegen
tooconfigure hello integratie van Cezanne HR-software in Azure AD Cezanne HR software uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.

tooadd Cezanne HR software uit de galerie hello, Hallo te volgen:

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop. 

    ![Hallo 'Azure Active Directory' knop][1]

2. Selecteer **bedrijfstoepassingen** > **alle toepassingen**.

    ![Hallo 'Alle toepassingen' koppelen][2]
    
3. een nieuwe toepassing hello boven aan het Hallo tooadd **alle toepassingen** dialoogvenster, **nieuwe toepassing**.

    !['Nieuwe application' Hallo knop][3]

4. Typ in het zoekvak Hallo **Cezanne HR Software**.

    ![Hallo zoekvak](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Selecteer in de lijst met resultaten Hallo **Cezanne HR Software** en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.

    ![lijst met resultaten Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie maakt u configureren en testen van Azure AD-SSO met Cezanne HR-software op basis van een testgebruiker genaamd "Britta Simon."

Voor eenmalige aanmelding toowork moet Azure AD tooknow hello Cezanne HR software equivalent toohello Azure AD-gebruiker. Met andere woorden, moet u een koppeling relatie tussen een Azure AD-gebruiker en de verwante Hallo-gebruiker maken in Hallo Cezanne HR-software.

tooestablish hello koppeling relatie toewijzen Hallo Cezanne HR software **gebruikersnaam** waarde als hello Azure AD **gebruikersnaam** waarde.

tooconfigure en test Azure AD-SSO met behulp van Cezanne HR-software, volledige Hallo bouwstenen te volgen.

### <a name="configure-azure-ad-sso"></a>Azure AD-eenmalige aanmelding configureren

In deze sectie kunt u Azure AD-eenmalige aanmelding inschakelen in hello Azure-portal en configureren van eenmalige aanmelding in uw toepassing Cezanne HR door Hallo volgende te doen:

1. In de Azure-portal op Hallo Hallo **Cezanne HR Software** toepassing Integratiepagina **eenmalige aanmelding**.

    ![opdracht 'Single sign-on' Hallo][4]

2. tooenable SSO in Hallo **eenmalige aanmelding** dialoogvenster, selecteer Hallo **modus** als **op basis van SAML aanmelding**.
 
    ![Hallo 'Modus' vak](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. Onder **Cezanne HR Software domein en de URL's**, Hallo te volgen:

    ![de sectie 'Cezanne HR Software domein en URL's ' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. In Hallo **aanmeldings-URL** vak een URL die is Hallo de volgende syntaxis:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. In Hallo **antwoord-URL** vak een URL die is Hallo de volgende syntaxis:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Hallo voorgaande waarden zijn niet echt. Deze bijwerken met Hallo werkelijke antwoord-URL en Hallo aanmeldings-URL. tooobtain hello waarden, neem contact op met Hallo [Cezanne HR software client ondersteuningsteam](mailto:info@cezannehr.com).

4. Onder **SAML-certificaat voor ondertekening van**, selecteer **certificaat (Base64)**, en sla het Hallo-certificaatbestand op uw computer.

    ![de sectie 'SAML handtekeningcertificaat' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Selecteer **Opslaan**.

    ![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. Onder **Cezanne HR-softwareconfiguratie**, selecteer **Cezanne HR-Software configureren** tooopen hello **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID** en **SAML Single Sign-On-Service** URL uit Hallo **Naslaggids** sectie.

    ![de sectie 'Cezanne HR softwareconfiguratie' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. Een ander browservenster, meld u aan bij tooyour Cezanne HR software tenant als beheerder.

8. Selecteer in het linkerdeelvenster Hallo **Setup van System**. Selecteer **beveiligingsinstellingen** > **eenmalige aanmelding configuratie**.

    ![Hallo 'Single Sign-On-configuratie' koppeling](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. In Hallo **toestaan dat gebruikers toolog aan Hallo eenmalige aanmelding (SSO)-services te volgen met** deelvenster, selecteer Hallo **SAML 2.0** selectievakje in en selecteer Hallo **geavanceerde configuratie** optie.

    ![Eenmalige aanmelding opties voor services](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Selecteer **nieuwe toevoegen**.

    ![Hallo "toevoegen" om](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. Onder **SAML 2.0 identiteitsproviders**, Hallo te volgen:

    ![de sectie 'SAML 2.0 identiteitsproviders' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. In Hallo **weergavenaam** Hallo- naam van de id-provider.

    b. In Hallo **entiteits-id** vak, plak Hallo **SAML entiteit-ID** die u hebt gekopieerd uit hello Azure-portal. 

    c. In Hallo **SAML Binding** keuzelijst met invoervak, selecteer **POST**.

    d. In Hallo **Security Token Service-eindpunt** vak, plak Hallo **SAML Single Sign-On-Service** URL die u hebt gekopieerd uit hello Azure-portal. 
    
    e. In Hallo **gebruikersnaam van het ID-kenmerk** Voer `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. Hallo tooupload certificaat gedownload vanuit Azure AD, selecteer Hallo **uploaden** knop.
    
    g. Selecteer **OK**. 

12. Selecteer **Opslaan**.

    ![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Bij het instellen van de app hello, vindt u een beknopte versie van de voorgaande instructies in Hallo Hallo [Azure-portal](https://portal.azure.com). Nadat u Hallo app toegevoegd uit Hallo **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **eenmalige aanmelding** tabblad. Vervolgens toegang Hallo documentatie van Hallo ingesloten **configuratie** sectie. 

toolearn meer informatie over de functie voor Hallo embedded-documentatie, Zie [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
In deze sectie maakt u testgebruiker Britta Simon in hello Azure-portal.

![Hallo testgebruiker Britta Simon][100]

een testgebruiker in Azure AD toocreate Hallo te volgen:

1. In Hallo **Azure-portal**, in linkerdeelvenster hello, selecteert u Hallo **Azure Active Directory** knop.

    ![Hallo 'Azure Active Directory' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers, selecteer **gebruikers en groepen** > **alle gebruikers**.
    
    ![Hallo 'Alle gebruikers' koppelen](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Hallo **alle gebruikers** dialoogvenster wordt geopend.

3. Hallo tooopen **gebruiker** dialoogvenster, **toevoegen**.
 
    ![de knop "Toevoegen" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** dialoogvenster vak, Hallo te volgen:
 
    ![Hallo 'Gebruiker' dialoogvenster](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** vak gebruiker Britta Simon **e-mailadres**.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en Opmerking Hallo waarde die is gegenereerd in Hallo **wachtwoord** vak.

    d. Selecteer **Maken**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Maak een testgebruiker Cezanne HR-software

Azure AD tooenable gebruikers toosign in tooCezanne HR-software, ze in Cezanne HR software moeten worden ingericht. In geval van Cezanne HR software Hallo is inrichting een handmatige taak.

Een gebruikersaccount inrichten door Hallo volgende te doen:

1.  Meld u tooyour Cezanne HR software bedrijf site als beheerder.

2.  Selecteer in het linkerdeelvenster Hallo **Setup van System** > **gebruikers beheren** > **nieuwe gebruiker toevoegen**.

    ![Hallo 'Nieuwe gebruiker toevoegen' koppeling](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nieuwe gebruiker")

3.  Onder **persoon Details**, Hallo te volgen:

    ![in de sectie 'Persoon Details' Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nieuwe gebruiker")
    
    a. Stel **interne gebruiker** als **OFF**.
    
    b. In Hallo **voornaam** vak, type Hallo voornaam van gebruiker, bijvoorbeeld **Britta**.  
 
    c. In Hallo **achternaam** vak, type Hallo gebruiker achternaam op, bijvoorbeeld **Simon**.
    
    d. In Hallo **e** e-mailadres van de gebruiker hello, bijvoorbeeld: Typ Brittasimon@contoso.com.

4.  Onder **accountgegevens**, Hallo te volgen:

    ![sectie "Gegevens" Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nieuwe gebruiker")
    
    a. In Hallo **gebruikersnaam** e-mailadres van de gebruiker hello, bijvoorbeeld: Typ Brittasimon@contoso.com.
    
    b. In Hallo **wachtwoord** typt u het wachtwoord van gebruiker Hallo.
    
    c. In Hallo **beveiligingsrol** de optie **HR Professional**.
    
    d. Selecteer **OK**.

5. Op Hallo **eenmalige aanmelding** tabblad in Hallo **SAML 2.0-id's** sectie **nieuwe toevoegen**.

    ![Hallo "toevoegen" om](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "gebruiker")

6. In Hallo **identiteitsprovider** keuzelijst, selecteert u de id-provider. In Hallo **gebruikers-id** Voer Hallo e-mailadres voor test gebruiker Britta Simon van account.

    ![vakken 'Identiteitsprovider' en 'Gebruikers-id' Hallo](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "gebruiker")
    
7. Selecteer **Opslaan**.

    ![Hallo 'Opslaan' knop](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "gebruiker")

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u testgebruiker Britta Simon toouse Azure eenmalige aanmelding inschakelen tooCezanne HR-software toegang verleent.

![Toegang van gebruikers testen][200] 

1. In hello Azure-portal, opent u Hallo toepassingen weergeven en gaat toohello directory weergeven. Selecteer **bedrijfstoepassingen** > **alle toepassingen**.

    ![Hallo 'Alle toepassingen' koppelen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Cezanne HR Software**.

    ![lijst met Hallo 'Toepassingen'](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Selecteer **Toevoegen**. Klik dan in Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][203]

5. In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.

6. In Hallo **gebruikers en groepen** dialoogvenster, **Selecteer**.

7. In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.
    
### <a name="test-sso"></a>Test eenmalige aanmelding

In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van Hallo Toegangsvenster.

Wanneer u Hallo Cezanne HR software tegel in het deelvenster toegang Hallo selecteert, u zich aanmelden automatisch tooyour Cezanne HR softwaretoepassing.

## <a name="next-steps"></a>Volgende stappen

* [Lijst met zelfstudies over het toointegrate SaaS-apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en SSO met Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

