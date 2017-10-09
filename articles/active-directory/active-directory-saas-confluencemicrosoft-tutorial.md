---
title: 'Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en samenloop SAML SSO door Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Zelfstudie: Azure Active Directory-integratie met samenloop SAML SSO door Microsoft

In deze zelfstudie leert u hoe toointegrate samenloop SAML SSO door Microsoft met Azure Active Directory (Azure AD).

Samenloop SAML SSO door Microsoft integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooConfluence SAML SSO door Microsoft heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooConfluence SAML SSO door Microsoft (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

tooconfigure Azure AD-integratie met samenloop SAML SSO door Microsoft, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Samenloop servertoepassing is geïnstalleerd op een Windows 64-bits-server (on-premises of cloud Hallo IaaS infrastructuur)
- Samenloop server is een HTTPS-functionaliteit
- Opmerking Hallo ondersteund versies voor samenloop invoegtoepassing worden vermeld in onderstaande sectie.
- Samenloop server bereikbaar is op internet is met name tooAzure AD aanmelding pagina voor verificatie en moet kunnen tooreceive Hallo-token van Azure AD
- Beheerdersreferenties worden ingesteld in samenloop
- WebSudo is uitgeschakeld in samenloop
- Testgebruiker gemaakt in Hallo samenloop servertoepassing

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving van samenloop. Hallo-integratie eerst testen in ontwikkeling of staging-omgeving van toepassing hello en vervolgens gebruik Hallo productie-omgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-confluence"></a>Ondersteunde versies van samenloop 

Vanaf nu de volgende versies van samenloop worden ondersteund:

- Samenloop: 5.0 too5.10

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van samenloop SAML SSO door Microsoft van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a>Het toevoegen van samenloop SAML SSO door Microsoft van Hallo-galerie
tooconfigure hello integratie van samenloop SAML SSO door Microsoft in Azure AD, moet u tooadd samenloop SAML SSO door Microsoft in Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd samenloop SAML SSO door Microsoft via Hallo gallery Hallo stappen uitvoeren:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **samenloop SAML SSO door Microsoft**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. Selecteer in het deelvenster resultaten hello, **samenloop SAML SSO door Microsoft**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met samenloop SAML SSO door Microsoft op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in samenloop SAML SSO door Microsoft is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in samenloop SAML SSO door Microsoft toobe tot stand gebracht.

In samenloop SAML SSO door Microsoft, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met samenloop SAML SSO door Microsoft, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een SSO samenloop SAML door Microsoft testgebruiker](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave een equivalent van Britta Simon in samenloop SAML SSO door Microsoft die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw samenloop SAML eenmalige aanmelding configureren door toepassing van Microsoft.

**tooconfigure eenmalige aanmelding Azure AD met samenloop SAML SSO door Microsoft, voert u Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **samenloop SAML SSO door Microsoft** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. Op Hallo **samenloop SAML SSO door Microsoft-Domain en URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/plugins/servlet/saml/auth`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Poort is optioneel, mocht dat een benoemde URL. Deze waarden worden ontvangen tijdens de configuratie van Hallo van samenloop-invoegtoepassing wordt verderop in de zelfstudie Hallo besproken.
 

4. Hallo toogenerate **metagegevens** -url, Hallo volgende stappen uit te voeren:

    a. Klik op **App registraties**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    b. Klik op **eindpunten** tooopen **eindpunten** in het dialoogvenster.  
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    c. Klik op Hallo kopie knop toocopy **DOCUMENT met federatieve metagegevens** url en plak deze in Kladblok.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    d. Ga nu toohello eigenschappenpagina van **samenloop SAML SSO door Microsoft** en kopiëren Hallo **toepassings-Id** met **kopie** knop en plak deze in Kladblok.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    e. Hallo genereren **metagegevens-URL** met Hallo patroon volgen: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` en kopieer deze waarde in Kladblok, zoals het later voor de configuratie van Hallo van Hallo-invoegtoepassing gebruikt wordt.

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. Neem contact op met [Microsoft](mailto:waadpartners@microsoft.com) met de volgende informatie voor Hallo samenloop invoegtoepassing Hallo.
    
    *   Naam van de klant:
    *   De naam van de primaire domeincontroller:
    *   Azure AD Premium: Ja/Nee (invoegtoepassing zijn beschikbaar tooall Hallo klant vrije-, Basic- en Premium-SKU gebruikt)
    *   Het aantal gebruikers met behulp van deze integratie:
    *   Samenloop versie:
    *   Opmerkingen:

7. Meld u in een ander browservenster in tooyour samenloop exemplaar als beheerder.

8. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **invoegtoepassingen**.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. Klik onder sectie tabblad invoegtoepassingen op **invoegtoepassingen beheren**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. Handmatig uploaden Hallo invoegtoepassing geleverd door Microsoft. Zodra het Hallo-invoegtoepassing is geïnstalleerd, wordt deze weergegeven **gebruiker geïnstalleerd** invoegtoepassingen sectie van **beheren invoegtoepassing** sectie.

11. Klik op **configureren** tooconfigure Hallo nieuwe invoegtoepassing.

12. Voer de volgende stappen uit op de configuratiepagina:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    a. In **metagegevens-URL** Hallo plakken **metagegevens-URL** gegenereerd op basis van Azure AD en klikt u op Hallo **oplossen** knop. Hallo IdP metagegevens-URL worden gelezen en alle informatie van Hallo velden gevuld.

    > [!Note]
    > Gebruikers-ID van SAML-standaardlocatie is naam-id. U kunt deze optie tooan-kenmerk wijzigen en Hallo relevante kenmerknaam invoeren.

    > [!TIP]
    > Zorg ervoor dat er slechts één certificaat toegewezen tegen Hallo app zodat er geen fout is bij het oplossen van Hallo metagegevens. Als er meerdere certificaten, bij het omzetten van metagegevens hello, haalt de beheerder een fout opgetreden.
    
    b. Kopiëren Hallo **id, de antwoord-URL en de URL met eenmalige** waarden en plak ze in **id, de antwoord-URL en de URL met eenmalige** respectievelijk in tekstvakken **samenloop SAML SSO door Microsoft-Domain en URL's**  sectie op Azure-portal.

    c. In **aanmeldingsnaam van de knop** Hallo-typenaam van knop voor uw organisatie wil dat Hallo gebruikers toosee op het aanmeldingsscherm.

    d. In **SAML-ID gebruikerslocaties** Selecteer **gebruikersnaam wordt Hallo NameIdentifier element Hallo onderwerp instructie** of **gebruikers-ID is in een kenmerkelement**.  Deze ID heeft toobe Hallo samenloop gebruikers-id. Als het Hallo-gebruikersnaam niet overeenkomt, kan vervolgens niet worden gebruikers toolog in. 
    
    e. Als u selecteert **gebruikers-ID is in een kenmerkelement** optie, klik dan in **kenmerknaam** textbox typenaam Hallo van Hallo kenmerk waar gebruikers-Id wordt verwacht. 

    f. Als u federatieve domein hello (zoals ADFS enz.) met Azure AD gebruikt, klikt u op Hallo **inschakelen Thuisrealmdetectie** optie en configureer Hallo **domeinnaam**.
    
    g. In **domeinnaam** type Hallo domeinnaam hier in geval van een Hallo op basis van AD FS-aanmelding.

    h. Controleer **eenmalige aanmelding inschakelen uit** desgewenst toolog uit vanuit Azure AD wanneer een gebruiker zich afmeldt van samenloop. 

    ik. Klik op **opslaan** knop toosave Hallo instellingen.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a>Maken van een SSO samenloop SAML door Microsoft testgebruiker

Azure AD tooenable gebruikers toolog in tooConfluence op de lokale server ze moeten worden ingericht in samenloop SAML SSO door Microsoft. Voor samenloop SAML SSO door Microsoft is inrichting een handmatige taak.

**een gebruikersaccount tooprovision uitvoeren Hallo stappen te volgen:**

1. Tooyour samenloop op de lokale server aanmelden als beheerder.

2. Beweeg de muisaanwijzer op het tandwiel en klikt u op Hallo **Gebruikersbeheer**.

    ![Werknemer toevoegen](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. Klik onder de sectie gebruikers op **gebruikers toevoegen** tabblad. Op Hallo **'Gebruiker toevoegen'** dialoogvenster pagina, voert u Hallo stappen te volgen:

    ![Werknemer toevoegen](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    a. In Hallo **gebruikersnaam** textbox type Hallo e-mailadres van de gebruiker zoals Britta Simon.

    b. In Hallo **volledige naam** textbox type Hallo volledige naam van gebruiker zoals Britta Simon.

    c. In Hallo **e** textbox type Hallo e-mailadres van de gebruiker, zoals Brittasimon@contoso.com.

    d. In Hallo **wachtwoord** textbox Hallo een wachtwoord op voor Britta Simon.

    e. Klik op **wachtwoord bevestigen** Hallo wachtwoord opnieuw invoeren.
    
    f. Klik op **toevoegen** knop.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooConfluence SAML SSO door Microsoft.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooConfluence SAML SSO door Microsoft, voert u Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **samenloop SAML SSO door Microsoft**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo samenloop SAML SSO door Microsoft-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour samenloop SAML SSO door toepassing van Microsoft.
Zie voor meer informatie over Hallo Toegangspaneel [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

