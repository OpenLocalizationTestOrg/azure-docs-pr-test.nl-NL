---
title: 'Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor FishEye/filterkroes | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kantega SSO voor FishEye/filterkroes.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: fdd68b5e90c3e2893887650735429a33e21ffa68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a>Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor FishEye/filterkroes

In deze zelfstudie leert u hoe toointegrate Kantega SSO voor FishEye/filterkroes met Azure Active Directory (Azure AD).

Kantega SSO voor FishEye/filterkroes integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tooKantega eenmalige aanmelding voor FishEye/filterkroes heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooKantega eenmalige aanmelding inschakelen voor FishEye/filterkroes (Single Sign-On) met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Kantega SSO voor FishEye/filterkroes tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Kantega SSO voor eenmalige aanmelding FishEye/filterkroes abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Kantega SSO voor FishEye/filterkroes van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-kantega-sso-for-fisheyecrucible-from-hello-gallery"></a>Het toevoegen van Kantega SSO voor FishEye/filterkroes van Hallo-galerie
tooconfigure hello integratie van Kantega SSO voor FishEye/filterkroes in Azure AD, moet u tooadd Kantega SSO van hello galerie tooyour lijst met beheerde SaaS-apps voor FishEye/filterkroes.

**tooadd Kantega SSO voor FishEye/filterkroes via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Kantega SSO voor FishEye/filterkroes**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. Selecteer in het deelvenster resultaten hello, **Kantega SSO voor FishEye/filterkroes**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Kantega SSO voor FishEye/filterkroes op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kantega SSO voor FishEye/filterkroes is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Kantega SSO voor FishEye/filterkroes toobe tot stand gebracht.

Wijs in Kantega SSO voor FishEye/filterkroes, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Kantega SSO voor FishEye/filterkroes, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SSO Kantega voor FishEye/filterkroes testgebruiker](#creating-a-kantega-sso-for-fisheyecrucible-test-user)**  -toohave een equivalent van Britta Simon in Kantega SSO voor FishEye/filterkroes die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw Kantega SSO voor FishEye/filterkroes toepassing configureren.

**tooconfigure eenmalige aanmelding Azure AD met Kantega SSO voor FishEye/filterkroes uitvoeren Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Kantega SSO voor FishEye/filterkroes** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. In **IDP** modus op Hallo geïnitieerd **Kantega SSO voor FishEye/filterkroes domein en URL's** sectie Hallo stap uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. In **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en Hallo stap uit te voeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Deze waarden worden ontvangen tijdens de configuratie van Hallo van FishEye/filterkroes invoegtoepassing die later in Hallo zelfstudie wordt beschreven.

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. Meld u in een ander browservenster in tooyour FishEye/filterkroes op de lokale server als beheerder.

8. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. Klik bij systeeminstellingen op **vinden van nieuwe invoegtoepassingen**. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. Search **Kantega SSO voor filterkroes** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. Hallo-invoegtoepassing installatie wordt gestart. 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. Zodra het Hallo-installatie is voltooid. Klik op **Sluiten**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. Klik op **Beheren**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. In Hallo **SAML** sectie. Selecteer **Azure Active Directory (Azure AD)** van Hallo **toevoegen identiteitsprovider** vervolgkeuzelijst.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. Abonnement als selecteren **Basic**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. Op Hallo **App-eigenschappen** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    a. Kopiëren Hallo **App ID URI** waarde en deze gebruiken als **id, de antwoord-URL en de aanmeldings-URL** op Hallo **Kantega SSO voor FishEye/filterkroes domein en URL's** sectie in Azure-portal.

    b. Klik op **Volgende**.

18. Op Hallo **metagegevens importeren** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    a. Selecteer **metagegevensbestand op mijn computer**, en de metagegevens-uploadbestand, die u hebt gedownload vanuit Azure-portal.

    b. Klik op **Volgende**.

19. Op Hallo **en SSO** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    a. Naam van de identiteitsprovider Hallo toevoegen in **identiteit providernaam** textbox (bijvoorbeeld Azure AD).

    b. Klik op **Volgende**.

20. Hallo-handtekeningcertificaat en klik op **volgende**.    

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. Op Hallo **vissenoog gebruikersaccounts** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    a. Selecteer **gebruikers in de FishEye interne Directory maken, indien nodig** en Voer Hallo juiste naam van groep Hallo voor gebruikers (kan meerdere Nee. van groepen van elkaar gescheiden door komma's).

    b. Klik op **Volgende**.

22. Klik op **Voltooien**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. Op Hallo **bekend domeinen voor Azure AD** sectie, voert u de volgende stappen:   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    a. Selecteer **domeinen bekend** van Hallo linkerpaneel van Hallo pagina.

    b. Voer in Hallo domeinnaam **domeinen bekend** textbox.

    c. Klik op **Opslaan**.  

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a>Maken van een SSO Kantega voor FishEye/filterkroes testgebruiker

Azure AD tooenable gebruikers toolog tooFishEye/filterkroes, ze in FishEye/filterkroes moeten worden ingericht. In Kantega SSO voor FishEye/filterkroes is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Tooyour filterkroes op de lokale server aanmelden als beheerder.

2. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **gebruikers**.

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. Onder **gebruikers** tabblad gedeelte, klikt u op **gebruiker toevoegen**.

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. Op Hallo **nieuwe gebruiker toevoegen** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    a. In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.
    
    b. In Hallo **weergavenaam** textbox weergavenaam van de gebruiker Hallo zoals Britta Simon.
    
    c. In Hallo **e-mailadres** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.

    d. In Hallo **wachtwoord** textbox type Hallo wachtwoord van gebruiker.  

    e. In Hallo **wachtwoord bevestigen** textbox Hallo Bevestig het wachtwoord van gebruiker.

    f. Klik op **Add**.   

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooKantega eenmalige aanmelding voor FishEye/filterkroes.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooKantega SSO voor FishEye/filterkroes Hallo stappen uitvoeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Kantega SSO voor FishEye/filterkroes**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Kantega SSO FishEye/filterkroes tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Kantega SSO voor FishEye/filterkroes toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

