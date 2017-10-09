---
title: 'Zelfstudie: Azure Active Directory-integratie met HR2day door Merces | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en HR2day door Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Zelfstudie: Azure Active Directory-integratie met HR2day door Merces

In deze zelfstudie leert u hoe toointegrate HR2day door Merces met Azure Active Directory (Azure AD).

HR2day door Merces integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die tooHR2day door Merces toegang heeft.
- U kunt uw gebruikers tooautomatically ophalen aangemeld tooHR2day door Merces met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie--hello Azure-portal beheren.

Zie voor meer informatie over de integratie met Azure AD SaaS [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met HR2day door Merces tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement.
- Een HR2day door eenmalige aanmelding Merces abonnement ingeschakeld.

> [!NOTE]
> Met behulp van een productie-omgeving tootest Hallo stappen in deze zelfstudie aanbevolen niet.

tootest hello stappen in deze zelfstudie volgt u deze aanbevelingen:

- Gebruik uw productieomgeving geen tenzij dit noodzakelijk is.
- Ophalen van een [één maand gratis proefversie van Azure AD](https://azure.microsoft.com/pricing/free-trial/) als u nog geen hebt.  

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo-scenario dat hier wordt beschreven, bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van HR2day door Merces van Hallo-galerie.
2. Configureren en testen van Azure AD eenmalige aanmelding.

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>HR2day door Merces van Hallo galerie toevoegen
tooconfigure hello integratie van HR2day door Merces in Azure AD HR2day door Merces uit Hallo galerie tooyour lijst met beheerde SaaS-apps toevoegen.

**tooadd HR2day door Merces via Hallo gallery nemen Hallo stappen te volgen:**

1. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Ga te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. tooadd een nieuwe toepassing selecteert Hallo **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **HR2day door Merces**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Selecteer in het deelvenster resultaten hello, **HR2day door Merces**, en selecteer vervolgens Hallo **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met HR2day door Merces op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow die Hallo equivalent in HR2day door Merces tooa gebruiker in Azure AD is. Met andere woorden, moet u een koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in HR2day door Merces tooestablish.

Wijs in HR2day door Merces hello **gebruikersnaam** in Azure AD te **gebruikersnaam** tooestablish Hallo relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met HR2day door Merces, moet u toocomplete Hallo bouwstenen te volgen:

1. [Eenmalige aanmelding Azure AD configureren](#configuring-azure-ad-single-sign-on): uw toouse gebruikers deze functie inschakelt.
2. [Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user): Azure AD Test eenmalige aanmelding met Britta Simon.
3. [Maken van een HR2day door Merces testgebruiker](#creating-an-hr2day-by-merces-test-user): maken van een exemplaar van Britta Simon in HR2day door Merces die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. [Toewijzen van de testgebruiker hello Azure AD](#assigning-the-azure-ad-test-user): inschakelen Britta Simon toouse eenmalige aanmelding Azure AD.
5. [Test eenmalige aanmelding](#testing-single-sign-on): controleren of Hallo configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw HR2day door Merces toepassing.

**Azure AD tooconfigure eenmalige aanmelding met HR2day door Merces, nemen Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **HR2day door Merces** toepassing Integratiepagina **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. tooenable eenmalige aanmelding, in Hallo **eenmalige aanmelding** dialoogvenster, **modus** als **op basis van SAML aanmelding**.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. In Hallo **HR2day Merces domein en URL's** sectie kan nemen Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. In Hallo **aanmeldings-URL** vak een URL met behulp van Hallo patroon volgen: `https://<tenantname>.force.com/<instancename>`.

    b. In Hallo **id** vak een URL met behulp van Hallo patroon volgen: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met Hallo werkelijke aanmeldings-URL en -id. Neem contact op met Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl) tooget deze waarden. 
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie **Certificate(Base64)**, en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Deze sectie wordt beschreven hoe tooenable gebruikers tooauthenticate tooHR2day door Merces aan hun account in Azure AD. Ze doen dit met behulp van de federatieserver die gebaseerd op Hallo SAML-protocol.

    Uw HR2day door Merces toepassing verwacht Hallo SAML asserties in een specifieke indeling waarvoor u tooadd aangepast kenmerk toewijzingen tooyour SAML-token. Hallo volgende Schermafbeelding toont een voorbeeld hiervan. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Voordat u de SAML-verklaring Hallo configureren kunt, moet u contact opneemt Hallo [HR2day door Merces Client ondersteuningsteam](mailto:servicedesk@merces.nl) en het Hallo-waarde van de unieke id-kenmerk Hallo aanvraag voor uw tenant. U moet deze waarde toocomplete Hallo stappen in de volgende sectie Hallo. 

6. In Hallo **eenmalige aanmelding** dialoogvenster in Hallo **gebruikerskenmerken** sectie, Hallo SAML-token kenmerk configureren zoals wordt weergegeven in Hallo installatiekopie te volgen. Los Hallo stappen te volgen.
    
      | Naam van kenmerk    |   De waarde van kenmerk |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join ([e] '102938475Z' ' @ ' |
    
      a. Hallo tooopen **kenmerk toevoegen** dialoogvenster Selecteer **toevoegen kenmerk**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. In Hallo **naam** in het vak **ATTR_LOGINCLAIM**.

    c. Van Hallo **waarde** selecteert **Join()**.

    d. Van Hallo **tekenreeks1** selecteert **user.mail**.

    e. Voor **tekenreeks2**, typ Hallo unieke id die wordt geleverd door uw team HR2day.

    f. In Hallo **scheidingsteken** in het vak  **@** .
    
    g. Selecteer **Ok**.

7. Selecteer Hallo **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. In Hallo **HR2day door Merces configuratie** sectie **HR2day configureren door Merces** tooopen hello **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** van Hallo **Naslaggids** sectie.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure eenmalige aanmelding voor uw toepassing, neem contact op met de Hallo [HR2day door Merces client ondersteuningsteam](mailTo:servicedesk@merces.nl). Hallo gedownload koppelen **Certificate(Base64)** tooyour e-bestand. Bieden ook Hallo **Sign-Out URL**, **SAML entiteit-ID**, en **SAML Single Sign-On Service-URL** zodat ze kunnen worden geconfigureerd voor eenmalige aanmelding-integratie.

    > [!NOTE]
    >Vermeld toohello Merces team dat deze integratie moet entiteit-ID toobe ingesteld met Hallo patroon Hallo **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Nadat u deze app van Hallo toevoegen **Active Directory** > **bedrijfstoepassingen** sectie, selecteer Hallo **Single Sign-On** tabblad. Vervolgens toegang Hallo documentatie via Hallo ingesloten **configuratie** sectie Hallo onder aan. Meer informatie over Hallo embedded-documentatie-functie in Hallo [documentatie van Azure AD ingesloten]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate nemen Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, selecteert u Hallo **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en selecteer vervolgens **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello **gebruiker** dialoogvenster, **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. In Hallo **gebruiker** in het dialoogvenster nemen Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** vak, type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven**, en schrijf Hallo wachtwoord.

    d. Selecteer **Maken**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Een HR2day door Merces testgebruiker maken

Hallo-doel van deze sectie is toocreate Britta Simon in HR2day aangeroepen door Merces van een gebruiker. tooadd Hallo Hallo HR2day-account, het werken met Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Als u handmatig een gebruiker toocreate nodig, neem dan contact op met de Hallo [HR2day door Merces client ondersteuningsteam](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door haar tooHR2day toegang door Merces verlenen.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooHR2day door Merces, nemen Hallo stappen te volgen:**

1. In hello Azure portal, open Hallo toepassingen bekijken, gaat toohello directory weergeven, en ga vervolgens te**bedrijfstoepassingen**. Selecteer vervolgens **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **HR2day door Merces**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Selecteer in het menu aan de linkerkant Hallo Hallo **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Selecteer Hallo **toevoegen** knop. Klik op Hallo **toevoegen toewijzing** dialoogvenster, **gebruikers en groepen**.

    ![Gebruiker toewijzen][203]

5. In Hallo **gebruikers en groepen** dialoogvenster in Hallo **gebruikers** selecteert **Britta Simon**.

6. Klik op Hallo **Selecteer** knop.

7. In Hallo **toevoegen toewijzing** dialoogvenster, **toewijzen**.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

Hallo doel van deze sectie is tootest uw configuratie Azure AD eenmalige aanmelding via Hallo Toegangsvenster.  

Wanneer u Hallo HR2day door Merces-tegel in Hallo Toegangsvenster selecteert, ophalen u automatisch aangemeld tooyour HR2day door Merces toepassing.

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

