---
title: 'Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en afbeelding Relay.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: baf39e4437b85c2de5b524984ad5ca39badbab63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a>Zelfstudie: Azure Active Directory-integratie met installatiekopie Relay

In deze zelfstudie leert u hoe toointegrate installatiekopie Relay met Azure Active Directory (Azure AD).

Afbeelding Relay integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooImage Relay heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooImage Relay (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met installatiekopie Relay tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een installatiekopie Relay eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van afbeelding Relay van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-image-relay-from-hello-gallery"></a>Het toevoegen van afbeelding Relay van Hallo-galerie
tooconfigure hello integratie van afbeelding Relay in Azure AD, moet u tooadd installatiekopie Relay uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd installatiekopie Relay via Hallo gallery uitvoeren Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **installatiekopie Relay**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. Selecteer in het deelvenster resultaten hello, **installatiekopie Relay**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met installatiekopie Relay op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in afbeelding Relay is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante gebruiker Hallo in afbeelding Relay toobe tot stand gebracht.

In afbeelding Relay, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en eenmalige aanmelding Azure AD-test met installatiekopie Relay, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een installatiekopie Relay testgebruiker](#creating-an-image-relay-test-user)**  -toohave een equivalent van Britta Simon in afbeelding Relay dat is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw installatiekopie Relay-toepassing.

**Voer tooconfigure Azure AD eenmalige aanmelding met installatiekopie Relay, Hallo stappen te volgen:**

1. In Azure-portal op Hallo Hallo **installatiekopie Relay** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. Op Hallo **installatiekopie Relay domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.imagerelay.com/`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<companyname>.imagerelay.com/sso/metadata`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke aanmeldings-URL en -id. Neem contact op met [installatiekopie Relay Client ondersteuningsteam](http://support.imagerelay.com/) tooget deze waarden. 
 


4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. Op Hallo **Image Relay-configuratie** sectie, klikt u op **installatiekopie Relay configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out Service URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. Meld u tooyour installatiekopie Relay bedrijf site als een beheerder in een ander browservenster.

8. Klik in de werkbalk van de Hallo Hallo bovenaan, op Hallo **gebruikers en machtigingen** werkbelasting.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. Klik op **maken van nieuwe machtiging**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. In Hallo **eenmalige aanmelding op instellingen** werkbelasting, selecteer Hallo **deze groep kan alleen aanmelden via eenmalige aanmelding** selectievakje en klik vervolgens op **opslaan**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. Ga te**Accountinstellingen**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. Ga toohello **eenmalige aanmelding op instellingen** werkbelasting.
    
     ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. Op Hallo **SAML instellingen** dialoogvenster Hallo volgende stappen uit te voeren:
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    a. In **aanmeldings-URL** textbox plakken Hallo-waarde van **Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.

    b. In **afmelding URL** textbox plakken Hallo-waarde van **Service-URL met eenmalige Sign-Out** die u hebt gekopieerd vanuit Azure-portal.

    c. Als **indeling naam-Id**, selecteer **urn: oasis: namen: tc: SAML:1.1:nameid-indeling: emailAddress**.

    d. Als **Binding opties voor het aanvragen van Hallo serviceprovider (installatiekopie-Relay)**, selecteer **POST Binding**.

    e. Onder **x.509-certificaat**, klikt u op **certificaat bijwerken**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    f. Hallo gedownload certificaat openen in Kladblok en plak deze in Hallo x.509-certificaat textbox Hallo inhoud kopiëren.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    g. In **compileerprogramma gebruikersaanvragen** sectie, selecteer Hallo **compileerprogramma gebruikersaanvragen inschakelen**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    h. Selecteer Hallo machtigingsgroep (bijvoorbeeld **SSO Basic**) dat is toegestaan toosign in alleen via eenmalige aanmelding.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    ik. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-image-relay-test-user"></a>Maken van een installatiekopie Relay testgebruiker

Hallo-doel van deze sectie is toocreate Britta Simon aangeroepen in Relay installatiekopie van een gebruiker.

**toocreate een gebruiker Britta Simon aangeroepen in de installatiekopie Relay, Voer Hallo stappen te volgen:**

1. Eenmalige aanmelding tooyour installatiekopie Relay bedrijf site als beheerder.

2. Ga te**gebruikers en machtigingen** en selecteer **SSO-gebruiker maken**.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. Voer Hallo **e**, **voornaam**, **achternaam**, en **bedrijf** van Hallo gebruiker gewenste tooprovision en selecteer Hallo machtigingsgroep (bijvoorbeeld: Basic SSO) die is Hallo-groep die alleen via eenmalige aanmelding kunt aanmelden.
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. Klik op **Create**.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooImage Relay.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooImage Relay, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **installatiekopie Relay**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

Hallo-doel van deze sectie is tootest uw Azure AD-configuratie voor één aanmelding via Hallo Toegangsvenster.    

Als u op Hallo installatiekopie Relay-tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour installatiekopie Relay-toepassing.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

