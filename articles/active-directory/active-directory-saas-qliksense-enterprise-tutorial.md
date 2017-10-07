---
title: 'Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Qlik zin Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Zelfstudie: Azure Active Directory-integratie met Qlik zin Enterprise

In deze zelfstudie leert u hoe toointegrate Qlik zin Enterprise met Azure Active Directory (Azure AD).

Qlik zin Enterprise integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooQlik Enterprise zin heeft.
- U kunt uw gebruikers tooautomatically get aangemelde tooQlik zin Enterprise (Single Sign-On) inschakelen met hun Azure AD-accounts.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Qlik zin Enterprise tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Qlik zin Enterprise eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Qlik zin Enterprise van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Het toevoegen van Qlik zin Enterprise van Hallo-galerie
tooconfigure hello integratie van Qlik zin Enterprise in Azure AD, moet u tooadd Qlik zin Enterprise uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Qlik zin Enterprise via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **Qlik zin Enterprise**, selecteer **Qlik zin Enterprise** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Qlik zin Enterprise in de lijst met resultaten Hallo](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie configureert en test eenmalige aanmelding Azure AD met Qlik zin Enterprise op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Qlik zin onderneming is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in Qlik zin onderneming toobe tot stand gebracht.

Wijs in Qlik zin Enterprise, Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Qlik zin voor ondernemingen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een testgebruiker Qlik zin Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave een equivalent van Britta Simon in Qlik zin onderneming die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Qlik zin Enterprise.

**tooconfigure eenmalige aanmelding Azure AD bij Qlik zin Enterprise, Voer Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Qlik zin Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. Op Hallo **Qlik zin Enterprise domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![URL's en Qlik zin Enterprise domein eenmalige aanmelding informatie](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Houd er rekening mee hallo afsluitende slash aan Hallo einde van deze URI. Dit is vereist.
    
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden met Hallo werkelijke aanmeldings-URL en id, die worden beschreven verderop in deze zelfstudie of neem contact op met update [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Voorbereiden Hallo federatieve metagegevens-XML-bestand, zodat u die tooQlik zin-server uploaden kunt.
   
    > [!NOTE]
    > Voordat u uploadt Hallo IdP metagegevens toohello Qlik zin server, moet de Hallo bestand bewerkt toobe tooremove informatie tooensure werking tussen Azure AD en Qlik zin-server.
    
    ![QlikSense][qs24]
   
    a. Hallo FederationMetaData.xml bestand, dat u hebt gedownload vanuit Azure-portal in een teksteditor openen.
   
    b. Zoeken naar Hallo waarde **RoleDescriptor**.  Er zijn vier gegevens (twee paren openen en sluiten elementlabels).
   
    c. Hallo RoleDescriptor tags en alle informatie daartussen in Hallo bestand verwijderen.
   
    d. Hallo-bestand opslaan en deze in de buurt te houden voor gebruik verderop in dit document.

7. Navigeer toohello Qlik zin Qlik Management Console (QMC) als een gebruiker die virtuele proxyconfiguraties kunt maken.

8. Hallo QMC, klik op Hallo **virtuele proxy's** menu-item.
   
    ![QlikSense][qs6] 

9. Klik onder Hallo van welkomstscherm op Hallo **nieuw** knop.
   
    ![QlikSense][qs7]

10. welkomstscherm virtuele proxy bewerken wordt weergegeven.  Op Hallo is rechts van welkomstscherm een menu voor het zichtbaar maken van configuratie-opties.
   
    ![QlikSense][qs9]

11. Hallo identificatie menu-optie is ingeschakeld, Voer Hallo identificatiegegevens voor hello Azure virtuele proxyconfiguratie.
    
    ![QlikSense][qs8]  
    
    a. Hallo **beschrijving** veld is een beschrijvende naam voor de virtuele proxyconfiguratie Hallo.  Voer een waarde voor een beschrijving.
    
    b. Hallo **voorvoegsel** veld identificeert Hallo virtuele proxy eindpunt voor het verbinden van tooQlik zin met Azure AD eenmalige aanmelding.  Voer een naam uniek voorvoegsel voor deze virtuele proxy.
    
    c. **Time-out voor inactiviteit sessie (minuten)** Hallo time-out voor verbindingen via deze virtuele proxy is.
    
    d. Hallo **cookie-kop sessienaam** is Hallo cookie naam opslaan Hallo sessie-id voor Hallo Qlik zin sessie een gebruiker na een geslaagde authenticatie ontvangt.  Deze naam moet uniek zijn.

12. Klik op Hallo verificatie menu optie toomake zichtbaar.  Hallo verificatie scherm wordt weergegeven.
    
    ![QlikSense][qs10]
    
    a. Hallo **anonieme toegangsmodus** vervolgkeuzelijst bepaalt als anonieme gebruikers toegang Qlik zin via virtuele Hallo-proxy tot mogelijk.  Hallo standaardoptie is geen anonieme gebruiker.
    
    b. Hallo **verificatiemethode** vervolgkeuzelijst bepaalt Hallo verificatie schema Hallo virtuele proxy wordt gebruikt.  Selecteer SAML in de vervolgkeuzelijst Hallo.  Meer opties als gevolg hiervan worden weergegeven.
    
    c. In Hallo **SAML host URI veld**, invoer Hallo hostnaam gebruikers invoeren tooaccess Qlik zin via deze virtuele SAML-proxy.  Hallo-hostnaam is Hallo-uri van Hallo Qlik zin-server.
    
    d. In Hallo **SAML entiteit-ID**, Voer Hallo dezelfde waarde die is opgegeven voor veld URI Hallo SAML-host.
    
    e. Hallo **SAML IdP metagegevens** Hallo bestand bewerkt eerder in Hallo **Federatiemetagegevens van Azure AD-configuratie bewerken** sectie.  **Voordat u uploadt Hallo IdP metagegevens, Hallo bestand bewerkt toobe moet** tooensure goede werking van tooremove informatie tussen Azure AD en Qlik zin-server.  **Raadpleeg de bovenstaande instructies voor toohello als Hallo bestand heeft nog toobe bewerkt.**  Als Hallo-bestand is bewerkt klikt u op de knop Bladeren Hallo en selecteer Hallo bewerkte metagegevens bestand tooupload het toohello virtuele proxyconfiguratie.
    
    f. Hallo naam of het schema kenmerkverwijzing voor Hallo SAML-kenmerk dat vertegenwoordigt Hallo invoeren **UserID** Azure AD toohello Qlik zin server verzendt.  Schema referentie-informatie is beschikbaar in hello Azure app schermen post-configuratie.  toouse hello naamkenmerk, voer `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    g. Voer Hallo-waarde voor Hallo **gebruikerslijst** die zijn aangesloten toousers tijdens de verificatie tooQlik zin server via Azure AD.  Hardcoded waarden moeten worden omgeven door **vierkante haakjes []**.  een kenmerk in hello Azure AD SAML-verklaring verzonden toouse Geef Hallo-naam van Hallo kenmerk in dit tekstvak **zonder** vierkante haken.
    
    h. Hallo **SAML-ondertekeningsalgoritme** sets Hallo serviceprovider (in dit geval Qlik zin server) voor Certificaatondertekening voor Hallo virtuele proxyconfiguratie.  Als Qlik zin server gebruikmaakt van een vertrouwd certificaat gegenereerd met behulp van de Microsoft Enhanced RSA and AES Cryptographic Provider, Hallo SAML-ondertekeningsalgoritme ook wijzigen**SHA-256**.
    
    ik. Hallo SAML kenmerk toewijzing sectie kunt u extra kenmerken zoals groepen toobe verzonden tooQlik zin voor gebruik in regels.

13. Klik op Hallo **LOAD BALANCING** menu optie toomake deze zichtbaar.  Hallo Load Balancing scherm wordt weergegeven.
    
    ![QlikSense][qs11]

14. Klik op Hallo **toevoegen nieuwe serverknooppunt** knop, selecteer engine knooppunt of knooppunten Qlik zin wordt sessies toofor taakverdeling doeleinden verzenden en klikt u op Hallo **toevoegen** knop.
    
    ![QlikSense][qs12]

15. Klik op Hallo menu Geavanceerd optie toomake zichtbaar. Hallo geavanceerde scherm wordt weergegeven.
    
    ![QlikSense][qs13]
    
    Hallo Host witte lijst identificeert hostnamen die worden geaccepteerd wanneer toohello Qlik zin server verbinding te maken.  **Voer Hallo-hostnaam gebruikers opgeven wanneer tooQlik zin server verbinding kunnen maken.** Hallo-hostnaam is Hallo dezelfde waarde als Hallo SAML host uri zonder Hallo https://.

16. Klik op Hallo **toepassen** knop.
    
    ![QlikSense][qs14]

17. Klik op OK tooaccept Hallo waarschuwingsbericht weergegeven waarin wordt vermeld proxy's gekoppelde toohello virtuele proxy wordt opnieuw gestart.
    
    ![QlikSense][qs15]

18. Aan de rechterkant Hallo van welkomstscherm, Hallo gekoppelde items menu wordt weergegeven.  Klik op Hallo **proxy's** menuoptie.
    
    ![QlikSense][qs16]

19. Hallo proxy scherm wordt weergegeven.  Klik op Hallo **koppeling** knop Hallo onder toolink proxy toohello virtuele proxy.
    
    ![QlikSense][qs17]

20. Selecteer Hallo proxyknooppunt dat ondersteuning biedt voor deze virtuele proxyverbinding en klikt u op Hallo **koppeling** knop.  Na het koppelen, wordt Hallo proxy vermeld onder de bijbehorende proxy's.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. Nadat het over vijf tooten seconden Hallo vernieuwen QMC bericht wordt weergegeven.  Klik op Hallo **QMC vernieuwen** knop.
    
    ![QlikSense][qs20]

22. Wanneer Hallo QMC is vernieuwd, klikt u op Hallo **virtuele proxy's** menu-item. Hallo nieuwe SAML virtuele proxy vermelding wordt vermeld in de tabel Hallo op het welkomstscherm.  Één klik op Hallo virtuele proxy vermelding.
    
    ![QlikSense][qs51]

23. Hallo onderaan welkomstscherm in wordt Hallo downloaden SP metagegevens knop geactiveerd.  Klik op Hallo **downloaden SP metagegevens** knop toosave hello tooa bestand met metagegevens.
    
    ![QlikSense][qs52]

24. Open Hallo sp metagegevensbestand.  Houd rekening met Hallo **id van de entiteit** post en Hallo **AssertionConsumerService** vermelding.  Deze waarden zijn equivalent toohello **id** en Hallo **aanmelden URL** in de configuratie van de toepassing hello Azure AD. Plak deze waarden in Hallo **Qlik zin Enterprise domein en de URL's** sectie in de toepassingsconfiguratie hello Azure AD als ze niet overeen komen en vervolgens moet u ze in Azure AD-App-configuratiewizard Hallo vervangen.
    
    ![QlikSense][qs53]

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

   ![Hello Azure Active Directory-knop](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

   ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

   ![knop voor Hallo toevoegen](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

   ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   a. In Hallo **naam** in het vak **BrittaSimon**.

   b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

   c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

   d. Klik op **Create**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Maak een testgebruiker Qlik zin Enterprise

In deze sectie kunt u een gebruiker met de naam van Britta Simon in Qlik zin onderneming maken. Werken met [Qlik zin Enterprise Client ondersteuningsteam](https://www.qlik.com/us/services/support) Hallo gebruikers toevoegen in Hallo Qlik zin Enterprise-platform. Gebruikers moeten worden gemaakt en worden geactiveerd voordat u eenmalige aanmelding gebruiken. 

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooQlik zin Enterprise.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooQlik zin Enterprise, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Qlik zin Enterprise**.

    ![Hallo Qlik zin Enterprise koppeling in de lijst met Hallo-toepassingen](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Qlik zin Enterprise-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Qlik zin bedrijfstoepassing. 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

