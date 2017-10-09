---
title: 'Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Salesforce Sandbox.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Zelfstudie: Azure Active Directory-integratie met Salesforce Sandbox

In deze zelfstudie leert u hoe toointegrate Salesforce Sandbox met Azure Active Directory (Azure AD).

Salesforce Sandbox integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSalesforce Sandbox heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSalesforce Sandbox (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Salesforce Sandbox tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Salesforce Sandbox eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Salesforce Sandbox van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Het toevoegen van Salesforce Sandbox van Hallo-galerie
tooconfigure hello integratie van Salesforce Sandbox in Azure AD, moet u tooadd Salesforce Sandbox uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Salesforce Sandbox via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. Klik op **nieuwe toepassing** knop op Hallo Hallo dialoogvenster bovenaan.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Salesforce Sandbox**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. Selecteer in het deelvenster resultaten hello, **Salesforce Sandbox**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en test eenmalige aanmelding Azure AD met Salesforce-Sandbox op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Salesforce Sandbox is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Salesforce Sandbox toobe tot stand gebracht.

Deze relatie koppeling wordt vastgesteld door het toewijzen van de waarde van Hallo Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** in Salesforce Sandbox.

tooconfigure en eenmalige aanmelding Azure AD-test met Salesforce Sandbox, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Salesforce Sandbox](#creating-a-salesforce-sandbox-test-user)**  -toohave een equivalent van Britta Simon in Salesforce Sandbox die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw Salesforce-Sandbox-toepassing.

**Voer tooconfigure Azure AD eenmalige aanmelding met Salesforce-Sandbox Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **Salesforce Sandbox** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. Op Hallo **Salesforce sandbox-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     In Hallo **aanmeldings-URL** textbox Hallo typewaarde met Hallo patroon volgen:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Deze waarde is geen echte Hallo. Deze waarde bijwerken met Hallo werkelijke aanmeldings-URL. Neem contact op met [Salesforce Sandbox Client ondersteuningsteam](https://help.salesforce.com/support) tooget deze waarde.


4. Als u al eenmalige aanmelding voor een ander exemplaar van Salesforce Sandbox hebt geconfigureerd in uw directory, dan moet u ook Hallo configureren **id** toohave dezelfde waarde als Hallo Hallo **aanmelden URL**. 
    
    >[!Note]
    >Hallo **id** veld kan worden gevonden door te controleren Hallo **weergeven geavanceerde instellingen** selectievakje op Hallo **App-URL configureren** van Hallo menu 


5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. Op Hallo **Salesforce Sandbox configuratie** sectie, klikt u op **Salesforce Sandbox configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Een nieuw tabblad openen in uw browser en meld u bij tooyour Salesforce Sandbox administrator-account.

9. Klik in het menu bovenaan Hallo Hallo **Setup**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Klik in het navigatievenster aan de linkerkant Hallo Hallo op **beveiligingsmechanismen**, en klik vervolgens op **instellingen voor eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. Voer op Hallo sectie instellingen voor eenmalige aanmelding, Hallo stappen te volgen: ![configureren eenmalige aanmelding](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  Selecteer **SAML ingeschakeld**. 

     b.  Klik op **Nieuw**.

12. Op Hallo SAML Single Sign-On zoekinstellingen, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.In hello naam textbox, Hallo typenaam van Hallo-configuratie (bijvoorbeeld: *SPSSOWAAD\_Test*). 

    b. Plakken **SMAL entiteit-ID** waarde in Hallo **verlener** textbox.

    c. In Hallo **entiteit-Id** textbox type **https://test.salesforce.com** als het eerste exemplaar van Salesforce Sandbox toe te voegen tooyour directory Hallo. Als u al een exemplaar van Salesforce Sandbox, moet u voor Hallo hebt toegevoegd **entiteit-ID** type in Hallo **aanmelding op URL**, die moet worden in deze indeling:`http://company.my.salesforce.com`  
 
    d. Klik op **Bladeren** tooupload Hallo certificaat gedownload.  

    e. Als **SAML identiteitstype**, selecteer **Assertion bevat Hallo Federatie-ID van het gebruikersobject Hallo**.
 
    f. Als **SAML identiteit locatie**, selecteer **identiteit is in Hallo NameIdentifier element van Hallo onderwerp instructie**.

    g. Plakken **Single Sign-On Service-URL** in Hallo **identiteit Provider aanmeldings-URL** textbox. 

    h. SFDC biedt geen ondersteuning voor SAML-afmelden.  Als een tijdelijke oplossing 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' te plakken in Hallo **identiteit Provider afmelding URL** textbox.

    ik. Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP POST**. 

    j. Klik op **Opslaan**.

### <a name="enable-your-domain"></a>Uw domein inschakelen
Deze sectie wordt ervan uitgegaan dat u al hebt gemaakt een domein.  Zie voor meer informatie [definiëren van uw domeinnaam](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable uw domein Hallo volgende stappen uit te voeren:**

1. Klik in het Hallo navigatiedeelvenster links op **domeinbeheer**, en klik vervolgens op **mijn domein.**
   
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Zorg dat uw domein correct is geconfigureerd. 

2. In Hallo **aanmelding paginainstellingen** sectie, klikt u op **bewerken**, naarmate **verificatieservice**, selecteer Hallo-naam van Hallo SAML Single Sign-On-instelling van de vorige Hallo sectie en ten slotte op **opslaan**.
   
   ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Als u een domein geconfigureerd hebt, moeten uw gebruikers Hallo domein URL toologin toohello Salesforce sandbox gebruiken.  

tooget Hallo waarde van de URL van de hello, klikt u op Hallo SSO profiel die u hebt gemaakt in de vorige sectie Hallo.    

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. Bovenaan Hallo Hallo dialoogvenster, klikt u op **toevoegen** tooopen hello **gebruiker** dialoogvenster.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Maken van een testgebruiker Salesforce Sandbox

In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Salesforce Sandbox. SalesForce Sandbox ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.
Er is geen actie-item voor u in deze sectie. Als een gebruiker in Salesforce Sandbox nog niet bestaat, wordt een nieuw gemaakt wanneer u tooaccess Salesforce Sandbox probeert.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSalesforce Sandbox.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSalesforce Sandbox, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Salesforce Sandbox**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Als u uw instellingen SSO tootest wilt, open Hallo Toegangsvenster. Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Gebruikers inrichten configureren](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

