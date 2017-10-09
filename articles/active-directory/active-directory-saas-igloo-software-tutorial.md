---
title: 'Zelfstudie: Azure Active Directory-integratie met Igloo Software | Microsoft Docs'
description: Meer informatie over hoe tooconfigure eenmalige aanmelding tussen Azure Active Directory en Igloo Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Zelfstudie: Azure Active Directory-integratie met Igloo Software

In deze zelfstudie leert u hoe toointegrate Igloo Software met Azure Active Directory (Azure AD).

Igloo Software integreren met Azure AD biedt Hallo volgende voordelen:

- U kunt beheren in Azure AD wie toegang tot tooIgloo Software heeft
- U kunt uw gebruikers tooautomatically get aangemelde tooIgloo Software (Single Sign-On) met hun Azure AD-accounts inschakelen
- U kunt uw accounts op één centrale locatie - hello Azure-portal beheren

Als u meer informatie over de integratie met Azure AD SaaS tooknow wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Azure AD-integratie met Igloo Software tooconfigure, moet u Hallo volgende items:

- Een Azure AD-abonnement
- Een Igloo Software eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> tootest hello stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

tootest hello stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Hallo scenario beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Het toevoegen van Igloo Software van Hallo-galerie
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-igloo-software-from-hello-gallery"></a>Het toevoegen van Igloo Software van Hallo-galerie
tooconfigure hello integratie van Igloo Software in Azure AD, moet u tooadd Igloo Software uit Hallo galerie tooyour lijst met beheerde SaaS-apps.

**tooadd Igloo Software uit de galerie hello, Voer Hallo stappen te volgen:**

1. In Hallo  **[Azure-portal](https://portal.azure.com)**, Hallo linkernavigatievenster op, klik op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

2. Navigeer te**bedrijfstoepassingen**. Ga te**alle toepassingen**.

    ![Toepassingen][2]
    
3. de nieuwe toepassing tooadd, klikt u op **nieuwe toepassing** knop bovenaan Hallo van dialoogvenster.

    ![Toepassingen][3]

4. Typ in het zoekvak Hallo **Igloo Software**.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. Selecteer in het deelvenster resultaten hello, **Igloo Software**, en klik vervolgens op **toevoegen** knop tooadd Hallo-toepassing.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert en test eenmalige aanmelding Azure AD met Igloo Software op basis van een testgebruiker 'Britta Simon' genoemd.

Voor één aanmelding toowork moet Azure AD tooknow welke Hallo equivalent in Igloo Software is tooa gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en het Hallo gerelateerde gebruiker in Software Igloo toobe tot stand gebracht.

In Igloo Software, wijs Hallo-waarde van Hallo **gebruikersnaam** in Azure AD als waarde Hallo Hallo **gebruikersnaam** tooestablish Hallo koppeling relatie.

tooconfigure en test eenmalige aanmelding Azure AD met Igloo Software, moet u toocomplete Hallo bouwstenen te volgen:

1. **[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable uw toouse gebruikers deze functie.
2. **[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  -tootest Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maken van een testgebruiker Igloo Software](#creating-an-igloo-software-test-user)**  -toohave een equivalent van Britta Simon in Igloo-Software die is gekoppeld toohello Azure AD-weergave van de gebruiker.
4. **[Toewijzen hello Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD eenmalige aanmelding.
5. **[Testen van eenmalige aanmelding](#testing-single-sign-on)**  -tooverify Hallo of configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in hello Azure-portal en eenmalige aanmelding configureren in uw toepassing Igloo Software.

**Voer tooconfigure Azure AD eenmalige aanmelding met Igloo Software Hallo stappen te volgen:**

1. In de Azure-portal op Hallo Hallo **Igloo Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

2. Op Hallo **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** tooenable eenmalige aanmelding.
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. Op Hallo **Igloo Software domein en de URL's** sectie, voert u Hallo stappen te volgen:

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. In Hallo **aanmeldings-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com`

    b. In Hallo **id** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`

    c. In Hallo **antwoord-URL** textbox, typ een URL met Hallo patroon volgen:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Deze waarden zijn niet echt. Bijwerken van deze waarden Hello werkelijke id, de antwoord-URL en de aanmeldings-URL. Neem contact op met [Igloo Software Client ondersteuningsteam](https://www.igloosoftware.com/services/support) tooget deze waarden. 

4. Op Hallo **SAML-certificaat voor ondertekening van** sectie, klikt u op **Certificate(Base64)** en sla het Hallo-certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. Op Hallo **Igloo softwareconfiguratie** sectie, klikt u op **Igloo Software configureren** tooopen **eenmalige aanmelding configureren** venster. Kopiëren Hallo **Sign-Out URL's en SAML Single Sign-On Service** van Hallo **Naslaggids punt.**

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. In een ander browservenster, meld u aan tooyour Igloo Software bedrijf site als een beheerder.

8. Ga toohello **Configuratiescherm**.
   
     ![Het Configuratiescherm](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Configuratiescherm")

9. In Hallo **lidmaatschap** tabblad **aanmelding In instellingen**.
   
    ![Meld u aan instellingen](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "instellingen aanmelden")

10. Klik in de configuratiesectie SAML hello, op **SAML-verificatie configureren**.
   
    ![De SAML-configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML-configuratie")
   
11. In Hallo **algemene configuratie** sectie, voert u Hallo stappen te volgen:
   
    ![Algemene configuratie](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "algemene configuratie")

    a. In Hallo **verbindingsnaam** textbox, typ een naam voor uw configuratie.
   
    b. In Hallo **IdP aanmeldings-URL** textbox plakken Hallo-waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.
   
    c. In Hallo **IdP afmelding URL** textbox plakken Hallo-waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.
    
    d. Selecteer **afmelding antwoord en Type van de HTTP-aanvraag** als **POST**.
   
    e. Open uw **base 64-** gecodeerd certificaat in Kladblok gedownload vanuit Azure-portal kopie Hallo inhoud ervan naar het Klembord en plak deze toohello **openbaar certificaat** textbox.
    
12. In Hallo **respons en de configuratie van verificatie**, Hallo volgende stappen uit te voeren:
    
    ![Respons en de configuratie van verificatie](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "respons en de configuratie van verificatie")
  
      a. Als **identiteitsprovider**, selecteer **Microsoft ADFS**.
      
      b. Als **id van het Type**, selecteer **e-mailadres**. 

      c. In Hallo **e kenmerk** textbox type **emailaddress**.

      d. In Hallo **voornaam kenmerk** textbox type **givenname**.

      e. In Hallo **laatste naamkenmerk** textbox type **achternaam**.

13. Hallo te volgen stappen toocomplete Hallo configuratie uitvoeren:
    
    ![Het maken van de gebruiker op aanmelden](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "aanmaken op aanmelding gebruiker") 

     a. Als **aanmaken op aanmelding gebruiker**, selecteer **Maak een nieuwe gebruiker in uw site wanneer ze zich aanmelden**.

     b. Als **aanmelden instellingen**, selecteer **gebruik SAML-knop op het scherm 'Aanmelden'**.

     c. Klik op **Opslaan**.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen Hallo lezen [Azure-portal](https://portal.azure.com), terwijl u Hallo-app instelt.  Na het toevoegen van deze app van Hallo **Active Directory > bedrijfstoepassingen** sectie, klikt u op Hallo **Single Sign-On** tabblad en toegang Hallo ingesloten documentatie via Hallo  **Configuratie** sectie Hallo onder aan. U kunt meer lezen over Hallo embedded-documentatie-functie hier: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken
Hallo-doel van deze sectie is toocreate een testgebruiker in hello Azure-portal Britta Simon aangeroepen.

![Azure AD-gebruiker maken][100]

**een testgebruiker in Azure AD toocreate uitvoeren Hallo stappen te volgen:**

1. In Hallo **Azure-portal**, op Hallo navigatiedeelvenster links, klikt u op **Azure Active Directory** pictogram.

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. toodisplay hello lijst met gebruikers door te gaan**gebruikers en groepen** en klik op **alle gebruikers**.
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. Hallo tooopen **gebruiker** dialoogvenster, klikt u op **toevoegen** op Hallo Hallo dialoogvenster bovenaan.
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. Op Hallo **gebruiker** dialoogvenster pagina, voert u Hallo stappen te volgen:
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. In Hallo **naam** textbox type **BrittaSimon**.

    b. In Hallo **gebruikersnaam** textbox type Hallo **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en schrijf Hallo-waarde van Hallo **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-an-igloo-software-test-user"></a>Een testgebruiker Igloo Software maken

Er is geen actie-item voor u tooconfigure gebruikers inrichten tooIgloo Software.  

Wanneer een toegewezen gebruiker probeert toolog in tooIgloo Hallo-paneel voor apptoegang, Igloo Software met Software controleert of de gebruiker Hallo bestaat.  Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Igloo Software.

### <a name="assigning-hello-azure-ad-test-user"></a>Toewijzen van de testgebruiker hello Azure AD

In deze sectie kunt u Britta Simon toouse Azure eenmalige aanmelding inschakelen door het verlenen van toegang tooIgloo Software.

![Gebruiker toewijzen][200] 

**tooassign Britta Simon tooIgloo Software, Voer Hallo stappen te volgen:**

1. In hello Azure-portal, Hallo toepassingen weergeven, openen en vervolgens toohello directoryweergave navigeren en ga te**bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met de toepassingen van Hallo **Igloo Software**.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. Klik in het menu aan de linkerkant Hallo Hallo op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers Hallo.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Testen van eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van Hallo Toegangsvenster testen.

Als u op Hallo Igloo Software tegel in Hallo Toegangsvenster, krijgt u automatisch aangemelde tooyour Igloo softwaretoepassing.
Zie voor meer informatie over het toegangsvenster [inleiding toohello Toegangspaneel](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende bronnen

* [Lijst met zelfstudies over het tooIntegrate SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

