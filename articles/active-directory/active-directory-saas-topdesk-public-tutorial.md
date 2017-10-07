---
title: 'Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en TOPdesk - openbaar.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Zelfstudie: Azure Active Directory-integratie met TOPdesk - openbare

In deze zelfstudie leert u hoe toointegrate TOPdesk - openbare met Azure Active Directory (Azure AD).

Integratie van TOPdesk - openbare met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD die toegang tooTOPdesk - openbaar is.
- U kunt uw gebruikers tooautomatically get aangemelde tooTOPdesk - openbare (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren.

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met TOPdesk - tooconfigure openbaar, moet u de volgende items Hallo:

- Een Azure AD-abonnement
- Een TOPdesk - openbare eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. TOPdesk - openbare uit Hallo galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-topdesk---public-from-hello-gallery"></a>TOPdesk - openbare uit Hallo galerie toevoegen
tooconfigure hello integratie van TOPdesk - openbare in Azure AD, moet u tooadd TOPdesk - openbare uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd TOPdesk - openbare via Hallo gallery Hallo stappen uitvoeren:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Hello Azure Active Directory-knop][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Hallo Enterprise toepassingen blade][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![knop voor nieuwe toepassing Hello][3]

4. Typ in het zoekvak Hallo **TOPdesk - openbare**, selecteer **TOPdesk - openbare** van resultaat deelvenster klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Lijst met zoekresultaten TOPdesk - openbare in Hallo](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met TOPdesk - openbare op basis van een testgebruiker 'Britta Simon' genoemd.

Azure AD moet tooknow welke gebruiker van het bijbehorende equivalent Hallo in TOPdesk voor eenmalige aanmelding toowork - openbaar is tooa gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker Hallo in TOPdesk - moet openbaar toobe tot stand gebracht.

In TOPdesk - Public worden toegekend aanwijzen Hallo waarde Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en Azure AD eenmalige aanmelding met TOPdesk - openbare testen, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een TOPdesk - openbare testgebruiker](#create-a-topdesk---public-test-user)**  - toohave een equivalent van Britta Simon in TOPdesk - openbare die gekoppelde toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen van de testgebruiker hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding in uw TOPdesk - openbare toepassing configureren.

**tooconfigure eenmalige aanmelding Azure AD met TOPdesk - openbaar, Hallo volgende stappen uit te voeren:**

1. In de Azure-portal op Hallo Hallo **TOPdesk - openbare** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Op Hallo **TOPdesk - URL's en openbare domein** sectie, voert u Hallo stappen te volgen:

    ![TOPdesk - URL's en openbare domein eenmalige aanmelding informatie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net`
    
    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Antwoord-URL is explaned verderop in de zelfstudie. Neem contact op met [TOPdesk - ondersteuningsteam openbare Client](https://help.topdesk.com/saas/enterprise/user/) tooget deze waarden.  

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens Hallo op uw computer.

    ![Hallo certificaat downloadkoppeling](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Op Hallo **TOPdesk - configuratie van openbare** sectie, klikt u op **configureren TOPdesk - openbare** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van Hallo **Naslaggids punt.**

    ![TOPdesk - openbare configuratie](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Meld u aan bij tooyour **TOPdesk - openbare** bedrijf site als beheerder.

8. In Hallo **TOPdesk** menu, klikt u op **instellingen**.
   
    ![Instellingen](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "instellingen")

9. Klik op **aanmeldingsinstellingen**.
   
    ![Instellingen voor aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "aanmeldingsinstellingen")

10. Vouw Hallo **aanmeldingsinstellingen** menu en klik vervolgens op **algemene**.
   
    ![Algemene](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "algemeen")

11. In Hallo **openbare** sectie Hallo **SAML aanmelding** configuratie sectie, voert u Hallo stappen te volgen:
   
    ![Instellingen voor technische](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "technische instellingen")
   
    a. Klik op **downloaden** toodownload openbare metagegevensbestand Hallo en lokaal opslaan op uw computer.
   
    b. Open het metagegevensbestand Hallo gedownload, en Ga naar Hallo **AssertionConsumerService** knooppunt.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Kopiëren Hallo **AssertionConsumerService** waarde, plakt u deze waarde in Hallo **antwoord-URL** textbox in **TOPdesk - URL's en openbare domein** sectie.      
   
12. een certificaatbestand toocreate uitvoeren Hallo stappen te volgen:
    
    ![Certificaat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "certificaat")
    
    a. Open Hallo gedownload bestand met metagegevens vanuit Azure-portal.
    
    b. Vouw Hallo **RoleDescriptor** knooppunt met een **xsi: type** van **ingevoerd: ApplicationServiceType**.
    
    c. Kopieer de waarde Hallo Hallo **X509Certificate** knooppunt.
    
    d. Opslaan Hallo gekopieerd **X509Certificate** waarde lokaal op uw computer in een bestand.

13. In Hallo **openbare** sectie, klikt u op **toevoegen**.
    
    ![SAML-aanmelding](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML-aanmelding")

14. Op Hallo **SAML-configuratie-assistent** dialoogvenster pagina, voert u Hallo stappen te volgen:
    
    ![SAML-configuratie-assistent](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "assistent voor SAML-configuratie")
    
    a. tooupload de metagegevens van het gedownloade bestand vanuit Azure-portal onder **Federatiemetagegevens**, klikt u op **Bladeren**.

    b. uw certificaat bestand onder tooupload **certificaat (RSA)**, klikt u op **Bladeren**.

    c. tooupload Hallo logo-bestand die u hebt gekregen Hallo TOPdesk ondersteuningsteam, onder **Logo pictogram**, klikt u op **Bladeren**.

    d. In Hallo **naam gebruikerskenmerk** textbox type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. In Hallo **weergavenaam** textbox, typ een naam voor uw configuratie.

    f. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. Klik in Azure-portal in het linkerdeelvenster Hallo Hallo op Hallo **Azure Active Directory** knop.

    ![Hello Azure Active Directory-knop](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    ![Hallo 'Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. tooopen hello **gebruiker** in het dialoogvenster, klikt u op **toevoegen** Hallo boven aan het Hallo **alle gebruikers** in het dialoogvenster.

    ![knop voor Hallo toevoegen](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. In Hallo **gebruiker** dialoogvenster Voer Hallo stappen te volgen:

    ![het dialoogvenster Hallo-gebruiker](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. In Hallo **naam** in het vak **BrittaSimon**.

    b. In Hallo **gebruikersnaam** type Hallo e-mailadres van de gebruiker Britta Simon vak.

    c. Selecteer Hallo **wachtwoord weergeven** selectievakje en schrijf Hallo-waarde die wordt weergegeven in Hallo **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-topdesk---public-test-user"></a>Een TOPdesk - openbare testgebruiker maken

In de volgorde tooenable Azure AD-gebruikers toolog in TOPdesk - openbaar, ze in TOPdesk - openbare moeten worden ingericht.  
In geval van TOPdesk - Hallo openbare inrichting is een handmatige taak.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure gebruikers inrichten, Voer Hallo stappen te volgen:
1. Meld u aan bij tooyour **TOPdesk - openbare** bedrijf site als administrator.

2. Klik in het menu bovenaan Hallo Hallo **TOPdesk \> nieuw \> ondersteuningsbestanden \> persoon**.
   
    ![Persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "persoon")

3. Voer in het dialoogvenster van de nieuwe persoon Hallo, Hallo stappen te volgen:
   
    ![Nieuwe persoon](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "nieuwe persoon")
   
    a. Klik op tabblad Algemeen van Hallo.

    b. In Hallo **achternaam** textbox, typ de achternaam van de gebruiker Hallo zoals Simon
 
    c. Selecteer een **Site** voor Hallo-account.
 
    d. Klik op **Opslaan**.

> [!NOTE]
> U kunt geen andere TOPdesk - hulpmiddelen voor het maken van account openbaar gebruiker of geleverd door TOPdesk - gebruikersaccounts openbare tooprovision Azure AD-API's gebruiken.

### <a name="assign-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooTOPdesk - openbaar.

![Hallo-gebruikersrollen toewijzen][200] 

**tooassign Britta Simon tooTOPdesk - openbaar, Hallo volgende stappen uit te voeren:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **TOPdesk - openbare**.

    ![Hallo TOPdesk - openbare koppelen in de lijst met Hallo-toepassingen](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![de koppeling 'Gebruikers en groepen' Hallo][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Hallo toevoegen toewijzing deelvenster][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Wanneer u klikt op Hallo TOPdesk - openbare-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour TOPdesk - openbare toepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

