---
title: 'Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bamboe | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Kantega SSO voor Bamboe.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 8bf637ff440e8e3948db882861bee6e73f8aa879
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a>Zelfstudie: Azure Active Directory-integratie met Kantega SSO voor Bamboe

In deze zelfstudie leert u hoe toointegrate Kantega SSO voor Bamboe met Azure Active Directory (Azure AD).

Kantega SSO voor Bamboe integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooKantega SSO voor Bamboe heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooKantega SSO voor Bamboe (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Kantega SSO voor Bamboe tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Kantega SSO voor eenmalige aanmelding Bamboe abonnement ingeschakeld

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Kantega SSO voor Bamboe van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-kantega-sso-for-bamboo-from-hello-gallery"></a>Het toevoegen van Kantega SSO voor Bamboe van Hallo-galerie
tooconfigure hello integratie van Kantega SSO voor Bamboe in Azure AD, moet u tooadd Kantega SSO van hello galerie tooyour lijst met beheerde SaaS-apps voor Bamboe.

**tooadd Kantega SSO voor Bamboe via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Kantega SSO voor Bamboe**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. Selecteer in het deelvenster resultaten hello, **Kantega SSO voor Bamboe**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met Kantega SSO voor Bamboe op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Kantega SSO voor Bamboe is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in Kantega SSO voor Bamboe toobe tot stand gebracht.

Wijs in Kantega SSO voor Bamboe, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als Hallo-waarde van Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Kantega SSO voor Bamboe, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SSO Kantega voor de testgebruiker Bamboe](#creating-a-kantega-sso-for-bamboo-test-user)**  -toohave een equivalent van Britta Simon in Kantega SSO voor Bamboe die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw Kantega SSO voor Bamboe toepassing configureren.

**tooconfigure eenmalige aanmelding Azure AD met Kantega SSO voor Bamboe, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Kantega SSO voor Bamboe** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. In **IDP** modus op Hallo geïnitieerd **Kantega SSO voor Bamboe domein en URL's** sectie Hallo stap uitvoeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    a. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. In **SP** geïnitieerd modus selectievakje **weergeven geavanceerde instellingen voor URL** en Hallo stap uit te voeren:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Deze waarden worden ontvangen tijdens de configuratie van Hallo van bamboe invoegtoepassing die later in Hallo zelfstudie wordt beschreven.

5. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. Meld u in een ander browservenster in tooyour Bamboe op de lokale server als beheerder.

8. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. Klik onder sectie tabblad invoegtoepassingen op **vinden van nieuwe invoegtoepassingen**. Search **Kantega SSO voor Bamboe (SAML & Kerberos)** en klik op **installeren** knop tooinstall Hallo nieuwe SAML-invoegtoepassing.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. Hallo-invoegtoepassing installatie wordt gestart.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. Zodra het Hallo-installatie is voltooid. Klik op **Sluiten**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. Klik op **Beheren**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.  

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. In Hallo **SAML** sectie. Selecteer **Azure Active Directory (Azure AD)** van Hallo **toevoegen identiteitsprovider** vervolgkeuzelijst.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. Abonnement als selecteren **Basic**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. Op Hallo **App-eigenschappen** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    a. Kopiëren Hallo **App ID URI** waarde en deze gebruiken als **id, de antwoord-URL en de aanmeldings-URL** op Hallo **Kantega SSO voor Bamboe domein en URL's** sectie in Azure-portal.

    b. Klik op **Volgende**.

17. Op Hallo **metagegevens importeren** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    a. Selecteer **metagegevensbestand op mijn computer**, en de metagegevens-uploadbestand, die u hebt gedownload vanuit Azure-portal.

    b. Klik op **Volgende**.

18. Op Hallo **en SSO** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    a. Naam van de identiteitsprovider Hallo toevoegen in **identiteit providernaam** textbox (bijvoorbeeld Azure AD).

    b. Klik op **Volgende**.

19. Hallo-handtekeningcertificaat en klik op **volgende**.    

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. Op Hallo **Bamboe gebruikersaccounts** sectie, voert u de volgende stappen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    a. Selecteer **gebruikers in de Bamboe interne Directory maken, indien nodig** en Voer Hallo juiste naam van groep Hallo voor gebruikers (kan meerdere Nee. van groepen van elkaar gescheiden door komma's).

    b. Klik op **Volgende**.

21. Klik op **Voltooien**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. Op Hallo **bekend domeinen voor Azure AD** sectie, voert u de volgende stappen:   

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

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

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a>Maken van een SSO Kantega voor Bamboe testgebruiker

Azure AD tooenable gebruikers toolog in tooBamboo, ze in Bamboe moeten worden ingericht. In Kantega SSO voor Bamboe is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Tooyour Bamboe op de lokale server aanmelden als beheerder.

2. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. Klik op **gebruikers**. Onder Hallo **gebruiker toevoegen** sectie, dit stappen uitvoeren:

    ![Werknemer toevoegen](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    a. In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.
    
    b. In Hallo **wachtwoord** textbox type Hallo wachtwoord van gebruiker.

    c. In Hallo **wachtwoord bevestigen** textbox Hallo Bevestig het wachtwoord van gebruiker.
    
    d. In Hallo **volledige naam** textbox, volledige naam van de gebruiker Hallo zoals Britta Simon type.
    
    e. In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.
    
    f. Klik op **Opslaan**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooKantega SSO voor Bamboe.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooKantega SSO voor Bamboe, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Kantega SSO voor Bamboe**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Kantega SSO Bamboe tegel in Hallo toegangsvenster klikt, krijgt u automatisch aangemelde tooyour Kantega SSO voor Bamboe toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

