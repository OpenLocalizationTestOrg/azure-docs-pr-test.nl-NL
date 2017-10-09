---
title: 'Zelfstudie: Azure Active Directory-integratie met SAML SSO voor Jira door resolutie GmbH | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAML SSO voor Jira door resolutie GmbH.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Zelfstudie: Azure Active Directory-integratie met SAML SSO voor Jira door resolutie GmbH

In deze zelfstudie leert u hoe toointegrate SAML SSO voor Jira door resolutie GmbH met Azure Active Directory (Azure AD).

Integratie van SAML SSO voor Jira door resolutie GmbH met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tooSAML eenmalige aanmelding voor Jira door resolutie GmbH heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSAML eenmalige aanmelding inschakelen voor Jira door resolutie GmbH (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SAML SSO voor Jira door resolutie GmbH tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SAML SSO voor Jira door resolutie GmbH eenmalige aanmelding voor ingeschakelde abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SAML SSO voor Jira door resolutie GmbH van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>Het toevoegen van SAML SSO voor Jira door resolutie GmbH van Hallo-galerie
tooconfigure hello integratie van SAML SSO voor Jira door resolutie GmbH in Azure AD, moet u tooadd SAML SSO door resolutie GmbH uit Hallo galerie tooyour lijst met beheerde SaaS-apps voor Jira.

**tooadd SAML SSO voor Jira door resolutie GmbH via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **SAML SSO voor Jira door resolutie GmbH**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. Selecteer in het deelvenster resultaten hello, **SAML SSO voor Jira door resolutie GmbH**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met SAML SSO voor Jira door resolutie die GmbH op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke gebruiker Hallo equivalent in SAML SSO voor Jira door resolutie GmbH is tooa gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in SAML SSO voor Jira door de resolutie moet GmbH toobe tot stand gebracht.

Wijs in SAML SSO voor Jira door resolutie GmbH, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met SAML SSO voor Jira door resolutie GmbH, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SAML SSO voor Jira door resolutie GmbH testgebruiker](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave een equivalent van Britta Simon in SAML SSO voor Jira door resolutie GmbH die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw SAML SSO voor Jira configureren door de resolutie GmbH toepassing.

**tooconfigure eenmalige aanmelding Azure AD met SAML SSO voor Jira door resolutie GmbH, Voer Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **SAML SSO voor Jira door resolutie GmbH** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. Op Hallo **SAML SSO voor Jira door resolutie GmbH domein en URL's** sectie, indien gewenst tooconfigure Hallo toepassing in **IDP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`

4. Controleer **weergeven geavanceerde instellingen voor URL**. U kunt eventueel tooconfigure Hallo toepassing in **SP** modus gestart:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Neem contact op met [SAML SSO voor Jira door resolutie GmbH Client ondersteuningsteam](https://www.resolution.de/go/support) tooget deze waarden. 

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. Aanmelden in een ander browservenster tooyour **SAML SSO voor Jira door resolutie GmbH beheerportal** als beheerder.

8. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. U bent omgeleide tooAdministrator Access-pagina. Voer Hallo **wachtwoord** en klik op **bevestigen** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. Klik onder sectie tabblad invoegtoepassingen op **vinden van nieuwe invoegtoepassingen**. Search **SAML eenmalige aanmelding op (SSO) voor JIRA** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. Hallo-invoegtoepassing installatie wordt gestart. Klik op **Sluiten**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Klik op **Beheren**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. Op **SAML-configuratie voor invoegtoepassing van SingleSignOn** pagina, klikt u op **toevoegen van extra identiteitsprovider** knop tooconfigure Hallo-instellingen van de id-Provider.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Voer de volgende stappen uit op deze pagina:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Voeg **naam** Hallo identiteitsprovider (bijvoorbeeld Azure AD).
    
    b. Voeg **beschrijving** Hallo identiteitsprovider (bijvoorbeeld Azure AD).

    c. Klik op **XML** en selecteer Hallo **metagegevens** bestand, dat u hebt gedownload vanuit Azure-portal.

    d. Klik op **Load** knop.

    e. Hallo IdP metagegevens worden gelezen en wordt ingevuld in velden als gemarkeerd in de schermafbeelding Hallo Hallo.   

16. Klik op **instellingen opslaan** knop toosave Hallo instellingen.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Maken van een SAML SSO voor Jira door resolutie GmbH testgebruiker

Azure AD tooenable gebruikers toolog in tooSAML SSO voor Jira door resolutie GmbH deze moeten worden ingericht in SAML SSO voor Jira door resolutie GmbH.  
In SAML SSO voor Jira door resolutie GmbH is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Tooyour SAML SSO voor Jira door resolutie GmbH bedrijf site als een beheerder zich aanmelden.

2. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. U staat op het omgeleide tooAdministrator toegang pagina tooenter **wachtwoord** en klik op **bevestigen** knop.

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. Onder **Gebruikersbeheer** tabblad gedeelte, klikt u op **gebruiker maken**.

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. Op Hallo **'Een nieuwe gebruiker maken'** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Werknemer toevoegen](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. In Hallo **e-mailadres** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.

    b. In Hallo **volledige naam** textbox, volledige naam van de gebruiker Hallo zoals Britta Simon type.

    c. In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.

    d. In Hallo **wachtwoord** textbox type Hallo wachtwoord van gebruiker.

    e. Klik op **gebruiker maken**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAML eenmalige aanmelding voor Jira door resolutie GmbH.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooSAML SSO voor Jira door resolutie GmbH, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SAML SSO voor Jira door resolutie GmbH**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo SAML SSO voor Jira door resolutie GmbH tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAML SSO voor Jira door resolutie GmbH toepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

