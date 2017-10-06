---
title: 'Zelfstudie: Azure Active Directory-integratie met SAP HANA | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en SAP HANA.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Zelfstudie: Azure Active Directory-integratie met SAP HANA

In deze zelfstudie leert u hoe toointegrate SAP HANA met Azure Active Directory (Azure AD).

SAP HANA integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooSAP HANA heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooSAP HANA (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met SAP HANA tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een SAP HANA eenmalige aanmelding ingeschakeld abonnement
- Een actieve HANA exemplaar op een openbare IaaS, on-premises virtuele Azure-machines of grote SAP-exemplaren in Azure
- Hallo XSA beheer Web Interface evenals HANA Studio is geïnstalleerd op Hallo HANA exemplaar.

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving van SAP HANA. Hallo-integratie eerst testen in ontwikkeling of staging-omgeving van toepassing hello en vervolgens gebruik Hallo productie-omgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van SAP HANA van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-sap-hana-from-hello-gallery"></a>Het toevoegen van SAP HANA van Hallo-galerie
tooconfigure hello integratie van SAP HANA in Azure AD, moet u tooadd SAP HANA uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd SAP HANA via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **SAP HANA**, selecteer **SAP HANA** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing. 

    ![Hallo nieuwe toepassing](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met SAP HANA op basis van een testgebruiker genaamd "Britta Simon."

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in SAP HANA is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in SAP HANA toobe tot stand gebracht.

Wijs in SAP HANA Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met SAP HANA, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SAP HANA-testgebruiker](#creating-a-sap-hana-test-user)**  -toohave een equivalent van Britta Simon in SAP HANA die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing SAP HANA.

**Voer tooconfigure Azure AD eenmalige aanmelding met SAP HANA Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **SAP HANA** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. Op Hallo **SAP HANA-domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Domein- en URL's van eenmalige aanmelding informatie](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    a. In Hallo **id** textbox type als:`HA100` 

    b. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Werk deze waarden met Hallo werkelijke id en de antwoord-URL. Neem contact op met [SAP HANA Client ondersteuningsteam](https://cloudplatform.sap.com/contact.html) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Als het certificaat is niet actief vervolgens deze actief maken door te klikken op Hallo selectievakje 'Maken nieuw certificaat active' in hello Azure AD. 

5. SAP HANA-toepassing verwacht Hallo SAML asserties in een specifieke indeling. Hallo volgende Schermafbeelding toont een voorbeeld voor deze. Hier wordt de Hallo hebt toegewezen **gebruikers-id** met **ExtractMailPrefix()** functie van **user.mail**. Dit geeft voorvoegsel op Hallo van e-mailadres van Hallo-gebruiker die is Hallo unieke gebruikersnaam. Dit wordt toohello SAP HANA-toepassing in elke geslaagde reactie verzonden.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. In Hallo **gebruikerskenmerken** sectie op Hallo **eenmalige aanmelding** dialoogvenster:

    a. In Hallo **gebruikers-id** vervolgkeuzelijst, selecteer **ExtractMailPrefix**.
    
    b. In Hallo **Mail** vervolgkeuzelijst, selecteer **user.mail**.

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure eenmalige aanmelding op **SAP HANA** side, aanmelding tooyour **HANA XSA webconsole** door te bladeren toohello respectieve HTTPS-eindpunt.

    > [!Note]
    > In de standaardconfiguratie Hallo leidt Hallo URL Hallo aanvraag tooa aanmeldingsscherm, waarvoor Hallo referenties van een geverifieerde SAP HANA-database toocomplete Hallo aanmeldingsproces. Hallo-gebruiker die zich aanmeldt hebben Hallo bevoegdheden vereist tooperform SAML-beheertaken.

9. Hallo XSA Web Interface, navigeert u in te**SAML-identiteitsprovider** en klik op Hallo van daaruit **'+'** -knop op Hallo Hallo scherm toodisplay Hallo toevoegen identiteit Provider Informatiedeelvenster onderaan en uit te voeren Hallo stappen te volgen:

    ![ID-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap1.png)

    a. In Hallo **toevoegen identiteit Provider Info** deelvenster plakken Hallo inhoud Hallo Metadata XML, die u hebt gedownload vanuit Azure-portal naar Hallo **metagegevens** textbox.

    ![Instellingen voor de id-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Als de inhoud van XML-document Hallo Hallo geldig zijn, Hallo bij het parseren van proces Hallo vereiste informatie op tooinsert haalt in Hallo **onderwerp, de entiteit-ID en de verlener** velden in algemene gegevens Hallo scherm en URL velden in Hallo Hallo Scherm doelgebied, bijvoorbeeld  **basis-URL en SingleSignOn (*)**.

    ![Instellingen voor de id-Provider toevoegen](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. In het naamvak Hallo Hallo algemene gegevens scherm, voer een naam voor de nieuwe SSO SAML-identiteitsprovider Hallo.

    > [!Note]
    > de naam Hallo Hallo SAML IDP is verplicht en moet uniek zijn. deze weergegeven in Hallo lijst met beschikbare SAML IDPs die wordt weergegeven als u SAML als Hallo verificatiemethode voor SAP HANA XS toepassingen toouse, bijvoorbeeld bij Hallo verificatie scherm van Hallo XS artefact beheerprogramma voor websites selecteert.

10. Hallo-details van nieuwe SAML-identiteitsprovider Hallo opslaan. Kies **opslaan** toosave details van SAML-identiteitsprovider Hallo Hallo en Hallo nieuwe SAML IDP toohello lijst met bekende SAML IDPs toe te voegen.

    ![knop Opslaan](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. In de Studio HANA binnen Systeemeigenschappen Hallo Hallo **configuratie** tabblad, alleen instellingen door te filteren **saml** en pas Hallo **assertion_timeout** van **10 sec** te**120 sec**.

    ![assertion_timeout instelling](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![knop voor Hallo toevoegen](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-sap-hana-test-user"></a>De gebruiker van een SAP HANA-test maken

Azure AD tooenable gebruikers toolog in tooSAP HANA, moeten ze worden ingericht in SAP HANA.
SAP HANA ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.

Als u handmatig een gebruiker toocreate moet, voert u Hallo stappen te volgen:

>[!Note]
>Hallo externe verificatie door de gebruiker Hallo gebruikt, kunt u wijzigen.
Externe gebruikers worden geverifieerd met behulp van een extern systeem, bijvoorbeeld een Kerberos-systeem. Voor gedetailleerde informatie over externe identiteiten contact op met uw [domeinbeheerder](https://cloudplatform.sap.com/contact.html).

1. Open Hallo [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) als administrator en inschakelen Hallo DB-gebruiker voor SAML-SSO.

    ![Gebruiker maken](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Maatstreepjes Hallo onzichtbaar selectievakje toohello links van de **SAML** en volg de koppeling van Hallo configureren.

3. Klik op **toevoegen** tooadd Hallo SAML IDP, en klik op **OK** juiste SAML IDP selecteren Hallo.

4. Hallo toevoegen **externe identiteit** (ex. Hier BrittaSimon) of kies **''** en klik op **OK**.

    >[!Note]
    >Als 'Elke' selectievakje niet is ingeschakeld, wordt de Hallo-gebruikersnaam in HANA tooexactly overeen Hallo-naam van de gebruiker Hallo in Hallo UPN voordat het domeinachtervoegsel hello moet (dat wil zeggen BrittaSimon@contoso.com zou worden BrittaSimon in HANA).

5. Voor testdoeleinden alle toewijzen **'XS'** rollen toohello gebruiker.

    ![rollen toewijzen](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > U moet deze geschikt is voor uw gebruiksvoorbeelden alleen machtigingen op te geven.

6. Hallo gebruiker opslaan.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooSAP HANA.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooSAP HANA, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **SAP HANA**.

    ![Gebruiker toewijzen](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo SAP HANA-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour SAP HANA-toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

